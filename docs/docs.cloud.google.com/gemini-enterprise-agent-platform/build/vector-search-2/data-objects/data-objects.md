---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects
title: Data Objects
description: Learn about Data Objects in Vector Search 2.0.
data_source: docs.cloud.google.com
---

In Vector Search 2.0, Collections store data as individual JSON objects called Data Objects. This page provides information on how to create Data Objects or import them from Cloud Storage buckets, and how to update and delete them.

## Creating a Data Object

The following example demonstrates adding a Data Object to a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects?dataObjectId=DATA_OBJECT_ID

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
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects?dataObjectId=DATA_OBJECT_ID"

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
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects?dataObjectId=DATA_OBJECT_ID" | Select-Object -Expand Content

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

    gcloud beta vector-search collections data-objects create DATA_OBJECT_ID \
      --data=DATA_FILE \
      --vectors=VECTORS_FILE \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud beta vector-search collections data-objects create DATA_OBJECT_ID `
      --data=DATA_FILE `
      --vectors=VECTORS_FILE `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud beta vector-search collections data-objects create DATA_OBJECT_ID ^
      --data=DATA_FILE ^
      --vectors=VECTORS_FILE ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    Created dataObject [DATA_OBJECT_ID].

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    data_object_service_client = vectorsearch_v1beta.DataObjectServiceClient()
    
    # Initialize request
    data_object = vectorsearch_v1beta.DataObject(
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
    request = vectorsearch_v1beta.CreateDataObjectRequest(
        parent="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        data_object_id="DATA_OBJECT_ID",
        data_object=data_object,
    )
    
    # Make the request
    response = data_object_service_client.create_data_object(request=request)
    
    # Handle the response
    print(response)

Embedding fields that have an auto-embedding specified in the Collection Schema are automatically populated. You can also bring your own embeddings (BYOE) to set vector field values that are not automatically populated.

> **Note:** Creating Data Objects is an atomic operation. All Data Objects are created, or the entire request fails, if there is an error.

## Importing Data Objects

The following example demonstrates how to import Data Objects from Cloud Storage into a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID:importDataObjects

Request JSON body:

    {
      "gcs_import": {
        "contents_uri": "gs://your-bucket/path/to/your-data/",
        "error_uri": "gs://your-bucket/path/to/import-errors/"
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
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID:importDataObjects"

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
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID:importDataObjects" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/operations/operation-1770039043815-649d75471f76e-08de3049-276a02be",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.vectorsearch.v1beta.ImportDataObjectsMetadata",
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

    gcloud beta vector-search collections import-data-objects COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID \
      --gcs-import-contents-uri="gs://your-bucket/path/to/your-data/" \
      --gcs-import-error-uri="gs://your-bucket/path/to/import-errors/" \
      --async

#### Windows (PowerShell)

    gcloud beta vector-search collections import-data-objects COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID `
      --gcs-import-contents-uri="gs://your-bucket/path/to/your-data/" `
      --gcs-import-error-uri="gs://your-bucket/path/to/import-errors/" `
      --async

#### Windows (cmd.exe)

    gcloud beta vector-search collections import-data-objects COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID ^
      --gcs-import-contents-uri="gs://your-bucket/path/to/your-data/" ^
      --gcs-import-error-uri="gs://your-bucket/path/to/import-errors/" ^
      --async

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    vector_search_service_client = vectorsearch_v1beta.VectorSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1beta.ImportDataObjectsRequest(
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

Folder `gs://your-bucket/path/to/your-data/` can contain one or more files each containing multiple Data Objects. Use this structure for large datasets that are spread across multiple files. The following file formats are supported in Vector Search 2.0:

  - JSONL, where each line is a JSON object having three top level properties: `id` , `data` , and `vectors`
  - AVRO
  - Vector Search JSON
  - Vector Search AVRO

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

> **Note:** "plot\_embedding" is automatically populated and shouldn't be specified in the JSONL file.

## Get a Data Object

The following example demonstrates how to get a Data Object with the ID `  DATA_OBJECT_ID  ` from a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    GET https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID" | Select-Object -Expand Content

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

    gcloud beta vector-search collections data-objects describe DATA_OBJECT_ID \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud beta vector-search collections data-objects describe DATA_OBJECT_ID `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud beta vector-search collections data-objects describe DATA_OBJECT_ID ^
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

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    data_object_service_client = vectorsearch_v1beta.DataObjectServiceClient()
    
    # Initialize request
    request = vectorsearch_v1beta.GetDataObjectRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID",
    )
    
    # Make the request
    response = data_object_service_client.get_data_object(request=request)
    
    # Handle the response
    print(response)

## Updating a Data Object

The following example demonstrates how to update the `title` data field and `plot_embedding` vector values in the Data Object with the ID `  DATA_OBJECT_ID  ` in a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    PATCH https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID

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
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID"

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
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID" | Select-Object -Expand Content

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

    gcloud beta vector-search collections data-objects update DATA_OBJECT_ID \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID \
      --data='{"title": "The Shawshank Redemption (updated)"}' \
      --update-vectors='{"plot_embedding": {"dense": {"values": [1.0, 1.0, 1.0]}}}'

#### Windows (PowerShell)

    gcloud beta vector-search collections data-objects update DATA_OBJECT_ID `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID `
      --data='{"title": "The Shawshank Redemption (updated)"}' `
      --update-vectors='{"plot_embedding": {"dense": {"values": [1.0, 1.0, 1.0]}}}'

#### Windows (cmd.exe)

> **Note:** If this command uses `'` for quoting content, replace these single quotes with double quotes. If quoting is nested, use `\"` to escape the inner quotes.

    gcloud beta vector-search collections data-objects update DATA_OBJECT_ID ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID ^
      --data='{"title": "The Shawshank Redemption (updated)"}' ^
      --update-vectors='{"plot_embedding": {"dense": {"values": [1.0, 1.0, 1.0]}}}'

You should receive a response similar to the following:

    Updated dataObject [DATA_OBJECT_ID].

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    data_object_service_client = vectorsearch_v1beta.DataObjectServiceClient()
    
    # Initialize request
    data_object = vectorsearch_v1beta.DataObject(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID",
        data={"title": "The Shawshank Redemption (updated)"},
        vectors={
            "plot_embedding": {
                "dense": {"values": [1., 1., 1.]}
            },
        },
    )
    request = vectorsearch_v1beta.UpdateDataObjectRequest(
        data_object=data_object,
    )
    
    # Make the request
    response = data_object_service_client.update_data_object(request=request)
    
    # Handle the response
    print(response)

## Delete Data Objects

You can delete individual Data Objects by name or batch delete Data Objects.

The following shows how to delete the Data Object `  DATA_OBJECT_ID  ` from a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - DATA\_OBJECT\_ID : The ID of the data object.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    DELETE https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID" | Select-Object -Expand Content

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

    gcloud beta vector-search collections data-objects delete DATA_OBJECT_ID \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud beta vector-search collections data-objects delete DATA_OBJECT_ID `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud beta vector-search collections data-objects delete DATA_OBJECT_ID ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    Deleted dataObject [DATA_OBJECT_ID].

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    data_object_service_client = vectorsearch_v1beta.DataObjectServiceClient()
    
    # Initialize request
    request = vectorsearch_v1beta.DeleteDataObjectRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/DATA_OBJECT_ID",
    )
    
    # Make the request
    data_object_service_client.delete_data_object(request=request)

## What's next?

  - Discover how to [use ETags for Data Object concurrency control](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/using-etags-for-concurrency-control) .
  - Learn about [Collection Indexes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes) .
  - See how to [query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query) and [search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search) for Data Objects.
