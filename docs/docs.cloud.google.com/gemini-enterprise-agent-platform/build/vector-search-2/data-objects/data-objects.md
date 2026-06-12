---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects
title: Data Objects
description: Learn about Data Objects in Agent Retrieval (formerly Vector Search 2.0).
data_source: docs.cloud.google.com
---

In Agent Retrieval (formerly Vector Search 2.0), Collections store data as individual JSON objects called Data Objects. This page describes the validation rules a Data Object must satisfy, and how to create, read, update, import, export, and delete Data Objects either individually or in batch.

## Data validation

Every Data Object that Agent Retrieval ingests is checked against a fixed set of rules. If any rule fails for a record, that record is rejected and emitted to the error sink with `code = INVALID_ARGUMENT` ; later checks do *not* run for that record. To avoid the "fix one error, re-ingest, hit the next error" loop, validate your dataset against **all** of the data validation rules before kicking off an ingestion or index build.

The pipeline applies the validations in this order:

| Stage                            | What it checks                                                                                                                       |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| 1\. Parsing                      | JSON is well-formed; required top-level fields exist; field types are correct                                                        |
| 2\. ID validations               | The `id` field is present and matches the documented ID format                                                                       |
| 3\. Data field schema            | The `data` payload conforms to the JSON Schema declared in the Collection's `CollectionConfig`                                       |
| 4\. Embedding validations        | Each dense/sparse vector matches the Collection's vector schema (name, type, dimension, finite values, sparse parity and uniqueness) |
| 5\. Searchable-fields population | Fields marked searchable in the schema can be successfully extracted from `data`                                                     |

### 1\. Parsing validations

Parsing validations run first, while turning each input line into an internal Data Object. They apply to both supported JSON shapes, the **default** format (with a top-level `vectors` / `data` object) and the **v1** format (with `embedding` , `sparse_embedding` , `restricts` , or `numeric_restricts` ). The format is auto-detected per record.

  - **JSON must be parseable.** Each line must parse as a JSON object. A line whose top-level keys match neither the default nor v1 format is rejected with `Unknown JSON format for string: <line>` .
  - **`id` is required.** Every record must contain a non-null `id` . Otherwise: `'id' field is missing or null` .
  - **Embeddings must be present (v1 format only).** A v1-format record must contain at least one of `embedding` or `sparse_embedding` . Otherwise: `'embedding' or 'sparse_embedding' fields are missing` .
  - **Dense embedding type checks.** The dense embedding field ( `embedding` in v1, or any array value under `vectors` in the default format) must be a JSON array of numbers. A value that cannot be coerced to a `float` is rejected with `'<field>' field contains non-float values` .
  - **Sparse embedding structure checks.** For every sparse vector:
      - Must be a JSON object.
      - Must contain both arrays: `values` (floats) and `indices` (longs); in v1 these are `values` and `dimensions` .
      - `values` must not be empty.
      - Indexes must be non-negative.
      - `values.length` must equal `indices.length` (or v1 `dimensions.length` ).
  - **`data` field type.** If present, `data` must be a JSON object, not an array, string, or scalar. Otherwise: `'data' field is not a JSON object` .
  - **`numeric_restricts` shape (v1 format).** `numeric_restricts` must be a JSON array of objects. Each entry must have a string `namespace` and must set **exactly one** of `value_int` , `value_float` , or `value_double` .

Most "first failure" issues come from this stage. Common errors include a stringified number in an embedding array, a missing `id` , or `values` / `indices` of different lengths.

### 2\. ID validations

Data Object IDs must comply with [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . In practice this means:

  - **1-63 characters long.**
  - **Lowercase letters, digits, and hyphens ( `-` ) only.** No uppercase, no underscores, no spaces, no symbols, no Unicode.
  - **Must start with a lowercase letter** ( `a-z` ).
  - **Must end with a lowercase letter or a digit** (no trailing `-` ).

Regular expression: `[a-z]([-a-z0-9]{0,61}[a-z0-9])?`

The following table shows common examples:

| ID               | Valid? | Why                                                                       |
| ---------------- | ------ | ------------------------------------------------------------------------- |
| `doc-123`        | Yes    | Starts with a letter, only lowercase + digits + hyphen, ends with a digit |
| `a`              | Yes    | A single lowercase letter is the minimum                                  |
| `product-sku-42` | Yes    | All rules satisfied                                                       |
| `Doc-123`        | No     | Uppercase `D` not allowed                                                 |
| `123-doc`        | No     | Must start with a **letter** , not a digit                                |
| `doc_123`        | No     | Underscore not allowed                                                    |
| `doc-123-`       | No     | Cannot end with a hyphen                                                  |
| `my doc`         | No     | Spaces not allowed                                                        |
| 64+ characters   | No     | Maximum length is 63                                                      |

This shape is the DNS label rule (the part between dots in a hostname like `my-service.example.com` ). It is reused here so that IDs round-trip safely through URLs, filenames, logs, and CLIs without escaping.

### 3\. Data field validations (JSON Schema)

The data field validation stage runs only if the Collection has a `dataSchema` declared in its `CollectionConfig` . If no schema is configured, this stage is skipped.

  - **Schema compliance.** The Data Object's `data` payload is serialized to JSON and validated against the configured JSON Schema (Draft 7). The validator reports **one error per schema violation** , so a record with three bad fields produces three error messages.
      - Message: `DataObject with id <id> failed schema validation: <error>` .
  - **Schema processing errors.** If the schema validator itself throws (for example, unsupported draft features), the record is rejected with `DataObject with id <id> failed schema validation processing: <exception>` .

### 4\. Embedding field validations

The embedding field validation stage iterates first over dense vectors and then sparse vectors. A single shared set of seen vector names spans **both** lists, so a name cannot be used twice -- even across the dense and sparse boundary.

#### Shared rules (apply to both dense and sparse)

| Rule                                                                           | Why it matters                                                                                                        | Error message                                                                                                           |
| ------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| **No duplicate vector names** across dense and sparse for the same Data Object | Two entries with the same vector name would target the same storage key, producing undefined last-write-wins behavior | `... has duplicate embedding field '<name>' across its dense/sparse vectors; each vector name must appear at most once` |
| **Vector name must be declared** in the `CollectionConfig` vector schema       | An unknown vector name cannot be routed to a column                                                                   | `... has dense/sparse embedding field '<name>' but this field is not defined in CollectionConfig vector schema`         |

#### Dense-vector-only rules

| Rule                                                                                                                              | Error message                                                                                                          |
| --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| The field must be configured as **dense** in the Collection schema.                                                               | `... has dense embedding field '<name>' but CollectionConfig defines it as non-dense`                                  |
| **Dimension must match** the configured dimension.                                                                                | `... field '<name>': expected dense embedding dimension <expected>, but got <actual>`                                  |
| **All values must be finite** -- no `NaN` , `+Infinity` , or `-Infinity` . Non-finite values would corrupt distance computations. | `... field '<name>': dense embedding contains non-finite value <v> at index <i> (NaN/Infinity values are not allowed)` |

#### Sparse-vector-only rules

| Rule                                                                 | Error message                                                                                                              |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| The field must be configured as **sparse** in the Collection schema. | `... has sparse embedding field '<name>' but CollectionConfig defines it as non-sparse`                                    |
| **Indices/values length parity** : `indicesCount == valuesCount` .   | `... field '<name>': sparse embedding has <n> indices but <m> values; indices and values must have the same length`        |
| **Non-negative indices** : every index \>= 0.                        | `... field '<name>': sparse embedding contains negative index <i> at position <p> (indices must be non-negative)`          |
| **Unique indices** within the same sparse vector.                    | `... field '<name>': sparse embedding contains duplicate index <i> (each index must appear at most once)`                  |
| **All values must be finite.**                                       | `... field '<name>': sparse embedding contains non-finite value <v> at position <p> (NaN/Infinity values are not allowed)` |

### 5\. Searchable-fields population

After embedding validation succeeds, the pipeline walks the `data` payload using the Collection's `dataSchema` and copies fields that the schema declares (string, integer/number, boolean, array of string, and nested objects) into a searchable-fields index. Two failure modes here will also reject a record:

  - A path that should be a struct contains a scalar (for example, the schema says `author.name` is a string but `author` is itself a string in the document).
  - An array-of-strings field contains a non-string element.

These typically indicate that the document's shape has drifted from the declared schema and are not always caught at the JSON Schema stage.

### Pre-flight checklist

Before kicking off an ingestion or index build, validate the entire dataset against the following rules. This is the same set of checks the pipeline applies, ordered so a single client-side pass surfaces every issue:

1.  **Format** -- every line parses as JSON and matches either the default or v1 shape.
2.  **IDs** -- match the RFC 1035 regular expression `[a-z]([-a-z0-9]{0,61}[a-z0-9])?` and are unique across the dataset.
3.  **Embeddings present** -- at least one vector per record; vector names are listed in your `CollectionConfig` vector schema with the correct dense or sparse type.
4.  **Dense vectors** -- correct dimension; no `NaN` , `+Inf` , or `-Inf` values.
5.  **Sparse vectors** -- `values.length == indices.length` ; all indexes greater or equal to 0 and unique. Non-finite values are not allowed.
6.  **No duplicate vector names** within a record across dense and sparse.
7.  **Data schema** -- if a `dataSchema` is configured, your `data` payload validates against it (Draft 7), and every field's actual JSON type matches the declared type (especially for nested objects and arrays of strings).
8.  **v1 `numeric_restricts`** -- every entry has a string `namespace` and exactly one of `value_int` / `value_float` / `value_double` .

## Create a Data Object

The following example demonstrates adding a single Data Object to a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects?dataObjectId=DATA_OBJECT_ID

Request JSON body:

    {
      "data": {
        "director": "Frank Darabont",
        "genre": "Drama",
        "title": "The Shawshank Redemption",
        "year": 1994
      },
      "vectors":{
        "genre_embedding": {
          "dense": {
            "values": [ 0.38638010860523064, 0.739343471733759, 0.16189056837017107, 0.5271366865924485 ]
          }
        },
        "plot_embedding": {
          "dense": {
            "values": [ 0.4752082440607731, 0.09026746166854707, 0.8752307753619009 ]
          }
        },
        "soundtrack_embedding": {
          "dense": {
            "values": [ 0.5920451749052875, 0.08301644173787519, 0.1264733498775969, 0.6196429624200321, 0.4925828581737443 ]
          }
        },
        "sparse_embedding": {
          "sparse": {
            "indices": [ 4065, 13326, 17377, 25918, 28105, 32683, 42998 ],
            "values": [ 1, 6, 3, 2, 8, 5, 2 ]
          }
        }
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects?dataObjectId=DATA_OBJECT_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects?dataObjectId=DATA_OBJECT_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID",
      "data": {
        "director": "Frank Darabont",
        "title": "The Shawshank Redemption",
        "year": 1994,
        "genre": "Drama"
      },
      "vectors": {
        "genre_embedding": {
          "dense": {
            "values": [
              0.3863801,
              0.73934346,
              0.16189057,
              0.5271367
            ]
          }
        },
        "plot_embedding": {
          "dense": {
            "values": [
              0.47520825,
              0.090267465,
              0.8752308
            ]
          }
        },
        "soundtrack_embedding": {
          "dense": {
            "values": [
              0.5920452,
              0.08301644,
              0.12647335,
              0.619643,
              0.49258286
            ]
          }
        },
        "sparse_embedding": {
          "sparse": {
            "values": [
              1,
              6,
              3,
              2,
              8,
              5,
              2
            ],
            "indices": [
              4065,
              13326,
              17377,
              25918,
              28105,
              32683,
              42998
            ]
          }
        }
      }
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - DATA\_FILE : The local path to a JSON file containing the data part of the data object.
    
    Example file content:
    
        {
          "director": "Frank Darabont",
          "genre": "Drama",
          "title": "The Shawshank Redemption",
          "year": 1994
        }

  - VECTORS\_FILE : The local path to a JSON file containing the vectors part of the data object.
    
    Example file content:
    
        {
          "genre_embedding": {
            "dense": {
              "values": [ 0.38638010860523064, 0.739343471733759, 0.16189056837017107, 0.5271366865924485 ]
            }
          },
          "plot_embedding": {
            "dense": {
              "values": [ 0.4752082440607731, 0.09026746166854707, 0.8752307753619009 ]
            }
          },
          "soundtrack_embedding": {
            "dense": {
              "values": [ 0.5920451749052875, 0.08301644173787519, 0.1264733498775969, 0.6196429624200321, 0.4925828581737443 ]
            }
          },
          "sparse_embedding": {
            "sparse": {
              "indices": [ 4065, 13326, 17377, 25918, 28105, 32683, 42998 ],
              "values": [ 1, 6, 3, 2, 8, 5, 2 ]
            }
          }
        }

  - DATA\_OBJECT\_ID : The ID of the data object.

  - COLLECTION\_ID : The ID of the collection.

  - LOCATION : The region where you are using Agent Platform.

  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections data-objects create DATA_OBJECT_ID \
      --data=DATA_FILE \
      --vectors=VECTORS_FILE \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud vector-search collections data-objects create DATA_OBJECT_ID `
      --data=DATA_FILE `
      --vectors=VECTORS_FILE `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud vector-search collections data-objects create DATA_OBJECT_ID ^
      --data=DATA_FILE ^
      --vectors=VECTORS_FILE ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    Created dataObject [DATA_OBJECT_ID].

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    data_object_service_client = vectorsearch_v1.DataObjectServiceClient()
    
    # Initialize request
    data_object = vectorsearch_v1.DataObject(
        data={
            "title": "The Shawshank Redemption",
            "genre": "Drama",
            "year": 1994,
            "director": "Frank Darabont",
        },
        vectors={
            "plot_embedding": {
                "dense": {"values": [0.1, 0.2, 0.3]}
            },
            "genre_embedding": {
                "dense": {"values": [0.4, 0.5, 0.6, 0.7]}
            },
            "soundtrack_embedding": {
                "dense": {"values": [0.8, 0.9, 1.0, 1.1, 1.2]}
            },
            "sparse_embedding": {
                "sparse": {"values": [1.0, 2.0], "indices": [10, 20]}
            },
        },
    )
    request = vectorsearch_v1.CreateDataObjectRequest(
        parent="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        data_object_id="DATA_OBJECT_ID",
        data_object=data_object,
    )
    
    # Make the request
    response = data_object_service_client.create_data_object(request=request)
    
    # Handle the response
    print(response)

Embedding fields that have an auto-embedding specified in the Collection Schema are automatically populated. You can also bring your own embeddings (BYOE) to set vector field values that are not automatically populated.

> **Note:** Creating a Data Object is an atomic operation. The Data Object is created or, if there is an error, the entire request fails.

## Batch create Data Objects

For efficient bulk ingestion of small numbers of records (up to **1000 Data Objects per request** ), use `batchCreate` . The whole batch is atomic: either all Data Objects are created, or the entire request fails. For larger datasets, prefer [importing Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects#import) from Cloud Storage.

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:batchCreate

Request JSON body:

    {
      "requests": [
        {
          "parent": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
          "dataObjectId": "movie-1",
          "dataObject": {
            "data": {
              "title": "The Shawshank Redemption",
              "year": 1994
            },
            "vectors": {
              "plot_embedding": {
                "dense": { "values": [0.47, 0.09, 0.87] }
              }
            }
          }
        },
        {
          "parent": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
          "dataObjectId": "movie-2",
          "dataObject": {
            "data": {
              "title": "The Godfather",
              "year": 1972
            },
            "vectors": {
              "plot_embedding": {
                "dense": { "values": [0.12, 0.55, 0.31] }
              }
            }
          }
        }
      ]
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:batchCreate"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:batchCreate" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "dataObjects": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-1",
          "data": {
            "title": "The Shawshank Redemption",
            "year": 1994
          },
          "vectors": {
            "plot_embedding": {
              "dense": { "values": [0.47, 0.09, 0.87] }
            }
          }
        },
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-2",
          "data": {
            "title": "The Godfather",
            "year": 1972
          },
          "vectors": {
            "plot_embedding": {
              "dense": { "values": [0.12, 0.55, 0.31] }
            }
          }
        }
      ]
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections data-objects batch-create \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID \
      --requests='[
        {
          "parent":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
          "dataObjectId":"movie-1",
          "dataObject":{"data":{"title":"The Shawshank Redemption","year":1994},"vectors":{"plot_embedding":{"dense":{"values":[0.47,0.09,0.87]}}}}
        },
        {
          "parent":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
          "dataObjectId":"movie-2",
          "dataObject":{"data":{"title":"The Godfather","year":1972},"vectors":{"plot_embedding":{"dense":{"values":[0.12,0.55,0.31]}}}}
        }
      ]'

#### Windows (PowerShell)

    gcloud vector-search collections data-objects batch-create `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID `
      --requests='[
        {
          "parent":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
          "dataObjectId":"movie-1",
          "dataObject":{"data":{"title":"The Shawshank Redemption","year":1994},"vectors":{"plot_embedding":{"dense":{"values":[0.47,0.09,0.87]}}}}
        },
        {
          "parent":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
          "dataObjectId":"movie-2",
          "dataObject":{"data":{"title":"The Godfather","year":1972},"vectors":{"plot_embedding":{"dense":{"values":[0.12,0.55,0.31]}}}}
        }
      ]'

#### Windows (cmd.exe)

> **Note:** If this command uses `'` for quoting content, replace these single quotes with double quotes. If quoting is nested, use `\"` to escape the inner quotes.

    gcloud vector-search collections data-objects batch-create ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID ^
      --requests='[
        {
          "parent":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
          "dataObjectId":"movie-1",
          "dataObject":{"data":{"title":"The Shawshank Redemption","year":1994},"vectors":{"plot_embedding":{"dense":{"values":[0.47,0.09,0.87]}}}}
        },
        {
          "parent":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
          "dataObjectId":"movie-2",
          "dataObject":{"data":{"title":"The Godfather","year":1972},"vectors":{"plot_embedding":{"dense":{"values":[0.12,0.55,0.31]}}}}
        }
      ]'

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    data_object_service_client = vectorsearch_v1.DataObjectServiceClient()
    
    parent = "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID"
    
    # Build per-DataObject create requests.
    requests = [
        vectorsearch_v1.CreateDataObjectRequest(
            parent=parent,
            data_object_id="movie-1",
            data_object=vectorsearch_v1.DataObject(
                data={"title": "The Shawshank Redemption", "year": 1994},
                vectors={
                    "plot_embedding": {"dense": {"values": [0.47, 0.09, 0.87]}},
                },
            ),
        ),
        vectorsearch_v1.CreateDataObjectRequest(
            parent=parent,
            data_object_id="movie-2",
            data_object=vectorsearch_v1.DataObject(
                data={"title": "The Godfather", "year": 1972},
                vectors={
                    "plot_embedding": {"dense": {"values": [0.12, 0.55, 0.31]}},
                },
            ),
        ),
    ]
    
    request = vectorsearch_v1.BatchCreateDataObjectsRequest(
        parent=parent,
        requests=requests,
    )
    
    # Make the request
    response = data_object_service_client.batch_create_data_objects(request=request)
    
    # Handle the response
    for data_object in response.data_objects:
        print(data_object.name)

## Get a Data Object

The following example demonstrates how to get a Data Object with the ID `  DATA_OBJECT_ID  ` from a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    GET https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID",
      "createTime": "2026-01-31T20:05:06Z",
      "updateTime": "2026-01-31T20:05:06Z",
      "data": {
        "title": "The Shawshank Redemption",
        "director": "Frank Darabont",
        "year": 1994,
        "genre": "Drama"
      },
      "vectors": {
        "sparse_embedding": {
          "sparse": {
            "values": [
              1,
              6,
              3,
              2,
              8,
              5,
              2
            ],
            "indices": [
              4065,
              13326,
              17377,
              25918,
              28105,
              32683,
              42998
            ]
          }
        },
        "genre_embedding": {
          "dense": {
            "values": [
              0.3863801,
              0.73934346,
              0.16189057,
              0.5271367
            ]
          }
        },
        "plot_embedding": {
          "dense": {
            "values": [
              0.47520825,
              0.090267465,
              0.8752308
            ]
          }
        },
        "soundtrack_embedding": {
          "dense": {
            "values": [
              0.5920452,
              0.08301644,
              0.12647335,
              0.619643,
              0.49258286
            ]
          }
        }
      }
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections data-objects describe DATA_OBJECT_ID \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud vector-search collections data-objects describe DATA_OBJECT_ID `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud vector-search collections data-objects describe DATA_OBJECT_ID ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    name: projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID
    data:
      director: Frank Darabont
      genre: Drama
      title: The Shawshank Redemption
      year: 1994
    vectors:
      genre_embedding:
        dense:
          values:
          - 0.3863801
          - 0.73934346
          - 0.16189057
          - 0.5271367
      plot_embedding:
        dense:
          values:
          - 0.47520825
          - 0.090267465
          - 0.8752308
      soundtrack_embedding:
        dense:
          values:
          - 0.5920452
          - 0.08301644
          - 0.12647335
          - 0.619643
          - 0.49258286
      sparse_embedding:
        sparse:
          indices:
          - 4065
          - 13326
          - 17377
          - 25918
          - 28105
          - 32683
          - 42998
          values:
          - 1.0
          - 6.0
          - 3.0
          - 2.0
          - 8.0
          - 5.0
          - 2.0

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    data_object_service_client = vectorsearch_v1.DataObjectServiceClient()
    
    # Initialize request
    request = vectorsearch_v1.GetDataObjectRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID",
    )
    
    # Make the request
    response = data_object_service_client.get_data_object(request=request)
    
    # Handle the response
    print(response)

## Update a Data Object

The following example demonstrates how to update the `title` data field and `plot_embedding` vector values in the Data Object with the ID `  DATA_OBJECT_ID  ` in a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    PATCH https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID

Request JSON body:

    {
      "data": {
        "title": "The Shawshank Redemption (updated)"
      },
      "vectors": {
        "plot_embedding": {
          "dense": {
            "values": [
              1.0,
              1.0,
              1.0
            ]
          }
        }
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X PATCH \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method PATCH `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID",
      "data": {
        "title": "The Shawshank Redemption (updated)"
      },
      "vectors": {
        "plot_embedding": {
          "dense": {
            "values": [
              1,
              1,
              1
            ]
          }
        }
      }
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections data-objects update DATA_OBJECT_ID \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID \
      --data='{"title": "The Shawshank Redemption (updated)"}' \
      --update-vectors='{"plot_embedding": {"dense": {"values": [1.0, 1.0, 1.0]}}}'

#### Windows (PowerShell)

    gcloud vector-search collections data-objects update DATA_OBJECT_ID `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID `
      --data='{"title": "The Shawshank Redemption (updated)"}' `
      --update-vectors='{"plot_embedding": {"dense": {"values": [1.0, 1.0, 1.0]}}}'

#### Windows (cmd.exe)

> **Note:** If this command uses `'` for quoting content, replace these single quotes with double quotes. If quoting is nested, use `\"` to escape the inner quotes.

    gcloud vector-search collections data-objects update DATA_OBJECT_ID ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID ^
      --data='{"title": "The Shawshank Redemption (updated)"}' ^
      --update-vectors='{"plot_embedding": {"dense": {"values": [1.0, 1.0, 1.0]}}}'

You should receive a response similar to the following:

    Updated dataObject [DATA_OBJECT_ID].

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    data_object_service_client = vectorsearch_v1.DataObjectServiceClient()
    
    # Initialize request
    data_object = vectorsearch_v1.DataObject(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID",
        data={"title": "The Shawshank Redemption (updated)"},
        vectors={
            "plot_embedding": {
                "dense": {"values": [1., 1., 1.]}
            },
        },
    )
    request = vectorsearch_v1.UpdateDataObjectRequest(
        data_object=data_object,
    )
    
    # Make the request
    response = data_object_service_client.update_data_object(request=request)
    
    # Handle the response
    print(response)

## Batch update Data Objects

To update many Data Objects at once, use `batchUpdate` . A maximum of **1000 Data Objects** can be updated in a single batch. Each per-record request specifies the `dataObject` (which must include its full resource `name` plus the fields you want to change) and an `updateMask` listing which fields to overwrite. Fields not listed in the mask are left unchanged.

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:batchUpdate

Request JSON body:

    {
      "requests": [
        {
          "dataObject": {
            "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-1",
            "data": { "genre": "Thriller" }
          },
          "updateMask": "data.genre"
        },
        {
          "dataObject": {
            "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-2",
            "vectors": {
              "plot_embedding": {
                "dense": { "values": [0.21, 0.34, 0.55] }
              }
            }
          },
          "updateMask": "vectors.plot_embedding"
        }
      ]
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:batchUpdate"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:batchUpdate" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

``` 
{}
```

### gcloud

Before using any of the command data below, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections data-objects batch-update \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID \
      --requests='[
        {
          "dataObject":{"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-1","data":{"genre":"Thriller"}},
          "updateMask":"data.genre"
        },
        {
          "dataObject":{"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-2","vectors":{"plot_embedding":{"dense":{"values":[0.21,0.34,0.55]}}}},
          "updateMask":"vectors.plot_embedding"
        }
      ]'

#### Windows (PowerShell)

    gcloud vector-search collections data-objects batch-update `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID `
      --requests='[
        {
          "dataObject":{"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-1","data":{"genre":"Thriller"}},
          "updateMask":"data.genre"
        },
        {
          "dataObject":{"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-2","vectors":{"plot_embedding":{"dense":{"values":[0.21,0.34,0.55]}}}},
          "updateMask":"vectors.plot_embedding"
        }
      ]'

#### Windows (cmd.exe)

> **Note:** If this command uses `'` for quoting content, replace these single quotes with double quotes. If quoting is nested, use `\"` to escape the inner quotes.

    gcloud vector-search collections data-objects batch-update ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID ^
      --requests='[
        {
          "dataObject":{"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-1","data":{"genre":"Thriller"}},
          "updateMask":"data.genre"
        },
        {
          "dataObject":{"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-2","vectors":{"plot_embedding":{"dense":{"values":[0.21,0.34,0.55]}}}},
          "updateMask":"vectors.plot_embedding"
        }
      ]'

### Python

    from google.cloud import vectorsearch_v1
    from google.protobuf import field_mask_pb2
    
    # Create the client
    data_object_service_client = vectorsearch_v1.DataObjectServiceClient()
    
    parent = "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID"
    
    # Each entry specifies the DataObject to update (with its full resource
    # name) and an update_mask listing the fields to overwrite. Fields not
    # listed in the mask are left unchanged.
    requests = [
        vectorsearch_v1.UpdateDataObjectRequest(
            data_object=vectorsearch_v1.DataObject(
                name=f"{parent}/dataObjects/movie-1",
                data={"genre": "Thriller"},
            ),
            update_mask=field_mask_pb2.FieldMask(paths=["data.genre"]),
        ),
        vectorsearch_v1.UpdateDataObjectRequest(
            data_object=vectorsearch_v1.DataObject(
                name=f"{parent}/dataObjects/movie-2",
                vectors={
                    "plot_embedding": {"dense": {"values": [0.21, 0.34, 0.55]}},
                },
            ),
            update_mask=field_mask_pb2.FieldMask(paths=["vectors.plot_embedding"]),
        ),
    ]
    
    request = vectorsearch_v1.BatchUpdateDataObjectsRequest(
        parent=parent,
        requests=requests,
    )
    
    # Make the request
    data_object_service_client.batch_update_data_objects(request=request)

## Import Data Objects

The following example demonstrates how to import Data Objects from Cloud Storage into a Collection with the ID `  COLLECTION_ID  ` . Use import for large datasets; for smaller bulk ingests (up to 1000 records) consider [creating Data Objects in batch](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects#batch-create) .

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID:importDataObjects

Request JSON body:

    {
      "gcsImport": {
        "contentsUri": "gs://your-bucket/path/to/your-data.json",
        "errorUri": "gs://your-bucket/path/to/import-errors/",
        "outputUri": "gs://your-bucket/path/to/import-output/"
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID:importDataObjects"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID:importDataObjects" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/operations/operation-1770039043815-649d75471f76e-08de3049-276a02be",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.vectorsearch.v1.ImportDataObjectsMetadata",
        "createTime": "2026-02-02T13:30:43.874527852Z"
      },
      "done": false
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections import-data-objects COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID \
      --gcs-import-contents-uri="gs://your-bucket/path/to/your-data.json" \
      --gcs-import-error-uri="gs://your-bucket/path/to/import-errors/" \
      --gcs-import-output-uri="gs://your-bucket/path/to/import-output/" \
      --async

#### Windows (PowerShell)

    gcloud vector-search collections import-data-objects COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID `
      --gcs-import-contents-uri="gs://your-bucket/path/to/your-data.json" `
      --gcs-import-error-uri="gs://your-bucket/path/to/import-errors/" `
      --gcs-import-output-uri="gs://your-bucket/path/to/import-output/" `
      --async

#### Windows (cmd.exe)

    gcloud vector-search collections import-data-objects COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID ^
      --gcs-import-contents-uri="gs://your-bucket/path/to/your-data.json" ^
      --gcs-import-error-uri="gs://your-bucket/path/to/import-errors/" ^
      --gcs-import-output-uri="gs://your-bucket/path/to/import-output/" ^
      --async

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    vector_search_service_client = vectorsearch_v1.VectorSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1.ImportDataObjectsRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        gcs_import={
          "contents_uri": "gs://your-bucket/path/to/your-data/",
          "error_uri": "gs://your-bucket/path/to/import-errors/",
        },
    )
    
    # Make the request
    operation = vector_search_service_client.import_data_objects(request=request)
    
    # Wait for the result (note this may take up to several minutes)
    operation.result()

Folder `gs://your-bucket/path/to/your-data/` can contain one or more files each containing multiple Data Objects. Use this structure for large datasets that are spread across multiple files. The following file formats are supported in Agent Retrieval:

  - JSONL, where each line is a JSON object having three top level properties: `id` , `data` , and `vectors` . Use this format for new Agent Retrieval datasets when you want human-readable input for inspecting and editing by hand.
  - AVRO: Use this format for new Agent Retrieval datasets when you need a compact, schema-validated binary format -- typically for large datasets produced by data-pipeline tools such as Dataflow, Beam, or Spark.
  - Vector Search JSON: Use this format only when you are migrating an existing Vector Search (Vector Search 1.0) JSON dataset and want to reuse it as-is.
  - Vector Search AVRO: Use this format only when you are migrating an existing Vector Search (Vector Search 1.0) AVRO dataset and want to reuse it as-is.

The following provides an example of the JSONL with the required properties.

    {
      "id": "movie-789",
      "data": {
        "title":"The Shawshank Redemption",
        "plot": "...",
        "year":1994,
        "avg_rating": 8.5,
        "movie_runtime_info": {
            "hours": 2,
            "minutes": 5
        },
      },
      "vectors": {
        "title_embedding": [-0.23, 0.88, 0.11, ...],
        "sparse_embedding": {
          "values": [0.01, -0.93, 0.27, ...],
          "indices": [23, 83, 131, ...]
        }
      }
    }

### AVRO

For AVRO files, each record must conform to the `DataObject` Avro schema shown. The fields mirror the JSONL format:

  - `id` (required `string` ).
  - `vectors` ( `map` , default `{}` ). Each entry is keyed by the vector name and its value is either an `array` of `float` (dense vector) or a `SparseVector` record with `values` (array of `float` ) and `indices` (array of `long` ).
  - `data` (nullable `map` , default `null` ). Keys are data field names. Each value is a `DataValue` record whose `value` field is a union over the supported primitive types ( `boolean` , `int` , `long` , `float` , `double` , `string` ) plus `array` of `DataValue` and `map` of `string` to `DataValue` for nested structures.
  - `etag` (nullable `string` , default `null` ).

<!-- end list -->

    {
      "namespace": "com.google.cloud.ai.vectorsearch",
      "type": "record",
      "name": "DataObject",
      "fields": [
        {
          "name": "id",
          "type": "string"
        },
        {
          "name": "vectors",
          "type": {
            "type": "map",
            "values": [
              {
                "type": "array",
                "items": "float"
              },
              {
                "type": "record",
                "name": "SparseVector",
                "fields": [
                  {
                    "name": "values",
                    "type": { "type": "array", "items": "float" }
                  },
                  {
                    "name": "indices",
                    "type": { "type": "array", "items": "long" }
                  }
                ]
              }
            ]
          },
          "default": {}
        },
        {
          "name": "data",
          "type": [
            "null",
            {
              "type": "map",
              "values": {
                "type": "record",
                "name": "DataValue",
                "fields": [
                  {
                    "name": "value",
                    "type": [
                      "boolean",
                      "int",
                      "long",
                      "float",
                      "double",
                      "string",
                      {
                        "type": "array",
                        "items": "DataValue"
                      },
                      {
                        "type": "map",
                        "values": "DataValue"
                      }
                    ]
                  }
                ]
              }
            }
          ],
          "default": null
        },
        {
          "name": "etag",
          "type": [
            "null",
            "string"
          ],
          "default": null
        }
      ]
    }

The following snippet shows the conceptual contents of a single AVRO record that matches the preceding JSONL example. Note that under this schema each entry in `data` is wrapped in a `DataValue` record (with a single `value` field), which is how AVRO represents the heterogeneous types in `data` :

    {
      "id": "movie-789",
      "vectors": {
        "title_embedding": [-0.23, 0.88, 0.11],
        "sparse_embedding": {
          "values": [0.01, -0.93, 0.27],
          "indices": [23, 83, 131]
        }
      },
      "data": {
        "title": { "value": "The Shawshank Redemption" },
        "plot": { "value": "..." },
        "year": { "value": 1994 },
        "avg_rating": { "value": 8.5 },
        "movie_runtime_info": {
          "value": {
            "hours":   { "value": 2 },
            "minutes": { "value": 5 }
          }
        }
      }
    }

> **Note:** `plot_embedding` is automatically populated and shouldn't be specified in the JSONL or AVRO file.

## Export Data Objects

The following example demonstrates how to export every Data Object in a Collection to Cloud Storage in JSONL format. The destination bucket must be in the same region as the Collection. Export is a long-running operation.

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID:exportDataObjects

Request JSON body:

    {
      "gcsDestination": {
        "exportUri": "gs://your-bucket/path/to/export-dir/",
        "format": "JSONL"
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID:exportDataObjects"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID:exportDataObjects" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/operations/operation-1770039043815-649d75471f76e-08de3049-276a02be",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.vectorsearch.v1.ExportDataObjectsMetadata",
        "createTime": "2026-02-02T13:30:43.874527852Z"
      },
      "done": false
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections export-data-objects COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID \
      --gcs-destination-export-uri="gs://your-bucket/path/to/export-dir/" \
      --gcs-destination-format="jsonl" \
      --async

#### Windows (PowerShell)

    gcloud vector-search collections export-data-objects COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID `
      --gcs-destination-export-uri="gs://your-bucket/path/to/export-dir/" `
      --gcs-destination-format="jsonl" `
      --async

#### Windows (cmd.exe)

    gcloud vector-search collections export-data-objects COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID ^
      --gcs-destination-export-uri="gs://your-bucket/path/to/export-dir/" ^
      --gcs-destination-format="jsonl" ^
      --async

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    vector_search_service_client = vectorsearch_v1.VectorSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1.ExportDataObjectsRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        gcs_destination={
            "export_uri": "gs://your-bucket/path/to/export-dir/",
            "format": vectorsearch_v1.ExportDataObjectsRequest.GcsExportDestination.Format.JSONL,
        },
    )
    
    # Make the request
    operation = vector_search_service_client.export_data_objects(request=request)
    
    # Wait for the result (note this may take up to several minutes)
    operation.result()

## Delete a Data Object

The following example shows how to delete a single Data Object `  DATA_OBJECT_ID  ` from a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    DELETE https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/operations/operation-1770039043815-649d75471f76e-08de3049-276a02be",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.vectorsearch.v1.ExportDataObjectsMetadata",
        "createTime": "2026-02-02T13:30:43.874527852Z"
      },
      "done": false
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections data-objects delete DATA_OBJECT_ID \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud vector-search collections data-objects delete DATA_OBJECT_ID `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud vector-search collections data-objects delete DATA_OBJECT_ID ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    Deleted dataObject [DATA_OBJECT_ID].

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    data_object_service_client = vectorsearch_v1.DataObjectServiceClient()
    
    # Initialize request
    request = vectorsearch_v1.DeleteDataObjectRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID",
    )
    
    # Make the request
    data_object_service_client.delete_data_object(request=request)

## Batch delete Data Objects

To delete many Data Objects at once, use `batchDelete` with a list of fully-qualified Data Object resource names. A maximum of **1000 Data Objects** can be deleted in a single batch.

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:batchDelete

Request JSON body:

    {
      "requests": [
        { "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-1" },
        { "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-2" }
      ]
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:batchDelete"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:batchDelete" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

``` 
{}
```

### gcloud

Before using any of the command data below, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections data-objects batch-delete \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID \
      --requests='[
        {"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-1"},
        {"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-2"}
      ]'

#### Windows (PowerShell)

    gcloud vector-search collections data-objects batch-delete `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID `
      --requests='[
        {"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-1"},
        {"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-2"}
      ]'

#### Windows (cmd.exe)

> **Note:** If this command uses `'` for quoting content, replace these single quotes with double quotes. If quoting is nested, use `\"` to escape the inner quotes.

    gcloud vector-search collections data-objects batch-delete ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID ^
      --requests='[
        {"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-1"},
        {"name":"projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/movie-2"}
      ]'

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    data_object_service_client = vectorsearch_v1.DataObjectServiceClient()
    
    parent = "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID"
    
    requests = [
        vectorsearch_v1.DeleteDataObjectRequest(
            name=f"{parent}/dataObjects/movie-1",
        ),
        vectorsearch_v1.DeleteDataObjectRequest(
            name=f"{parent}/dataObjects/movie-2",
        ),
    ]
    
    request = vectorsearch_v1.BatchDeleteDataObjectsRequest(
        parent=parent,
        requests=requests,
    )
    
    # Make the request
    data_object_service_client.batch_delete_data_objects(request=request)

## Count Data Objects

To count how many Data Objects a Collection contains, use the `aggregate` operation with the `COUNT` aggregation method. The same call accepts an optional JSON filter expression so you can count only the Data Objects that match a predicate (for example, `genre == "sci-fi"` ).

To count **every** Data Object in the Collection, omit the filter.

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:aggregate

Request JSON body:

    {
      "aggregate": "COUNT",
      "filter": { "genre": { "$eq": "sci-fi" } }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:aggregate"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:aggregate" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "aggregateResults": [
        { "count": "42" }
      ]
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections data-objects aggregate \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID \
      --aggregation-method=count \
      --json-filter='{"genre": {"$eq": "sci-fi"}}'

#### Windows (PowerShell)

    gcloud vector-search collections data-objects aggregate `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID `
      --aggregation-method=count `
      --json-filter='{"genre": {"$eq": "sci-fi"}}'

#### Windows (cmd.exe)

> **Note:** If this command uses `'` for quoting content, replace these single quotes with double quotes. If quoting is nested, use `\"` to escape the inner quotes.

    gcloud vector-search collections data-objects aggregate ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID ^
      --aggregation-method=count ^
      --json-filter='{"genre": {"$eq": "sci-fi"}}'

### Python

    from google.cloud import vectorsearch_v1
    from google.protobuf import struct_pb2
    from google.protobuf import json_format
    
    # Create the client
    search_client = vectorsearch_v1.DataObjectSearchServiceClient()
    
    parent = "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID"
    
    # Optional: build a JSON filter. Omit `filter=` to count everything.
    filter_struct = json_format.ParseDict(
        {"genre": {"$eq": "sci-fi"}}, struct_pb2.Struct()
    )
    
    request = vectorsearch_v1.AggregateDataObjectsRequest(
        parent=parent,
        aggregate=vectorsearch_v1.AggregationMethod.COUNT,
        filter=filter_struct,
    )
    
    # Make the request
    response = search_client.aggregate_data_objects(request=request)
    
    # The count value is returned in aggregate_results[0].
    for result in response.aggregate_results:
        print(result)

## What's next?

  - Discover how to [use ETags for Data Object concurrency control](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/using-etags-for-concurrency-control) .
  - Learn about [Collection Indexes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes) .
  - See how to [query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query) and [search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search) for Data Objects.
