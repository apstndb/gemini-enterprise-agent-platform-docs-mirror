---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections
title: Collections
description: Learn about Collections in Vector Search 2.0 and how to use them.
data_source: docs.cloud.google.com
---

In Vector Search 2.0, *Collections* are used to store related Data Objects. They provide a source of truth that you can query to determine the exact state of the Data Objects they contain.

## Collection Schema

When you create a Collection, you must provide the following [JSON schemas](https://json-schema.org/) :

  - A data schema, which provides the user-defined structure of your data.

  - A vector schema that defines and configures the vector fields for your Data Objects.

Together, these are referred to as the *Collection Schema* .

> **Note:** Schemas must follow the JSON Schema draft-07 specification.  
>   
> To help ensure data integrity and high-speed performance, the system enforces a strict schema validation policy. When you define a JSON schema for your Collection, the `additionalProperties` keyword is always treated as `false` regardless of how it is defined in your schema.

## Creating a Collection

The following example demonstrates how to create a Collection with the ID `  COLLECTION_ID  ` , specifying both a data schema and a vector schema.

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections?collection_id=COLLECTION_ID

Request JSON body:

    {
      "data_schema": {
        "type": "object",
        "properties": {
          "year": {
            "type": "number"
          },
          "genre": {
            "type": "string"
          },
          "director": {
            "type": "string"
          },
          "title": {
            "type": "string"
          }
        }
      },
      "vector_schema": {
        "plot_embedding": {
          "dense_vector": {
            "dimensions": 3
          }
        },
        "soundtrack_embedding": {
          "dense_vector": {
            "dimensions": 5
          }
        },
        "genre_embedding": {
          "dense_vector": {
            "dimensions": 4
          }
        },
        "sparse_embedding": {
          "sparse_vector": {}
        }
      },
      "labels": {
        "fookey": "barvalue"
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
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections?collection_id=COLLECTION_ID"

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
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections?collection_id=COLLECTION_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.vectorsearch.v1beta.OperationMetadata",
        "createTime": "2026-01-23T17:17:29.687753204Z",
        "target": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        "verb": "create",
        "requestedCancellation": false,
        "apiVersion": "v1beta"
      },
      "done": false
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - DATA\_SCHEMA\_FILE : The local path to the JSON schema file for the data part of the data objects.
    
    Example file content:
    
        {
          "type": "object",
          "properties": {
            "year": { "type": "number" },
            "genre": { "type": "string" },
            "director": { "type": "string" },
            "title": { "type": "string" }
          }
        }

  - VECTOR\_SCHEMA\_FILE : The local path to the JSON schema file for the vector fields.
    
    Example file content:
    
        {
          "plot_embedding": {
            "denseVector": { "dimensions": 3 }
          },
          "soundtrack_embedding": {
            "denseVector": { "dimensions": 5 }
          },
          "genre_embedding": {
            "denseVector": { "dimensions": 4 }
          },
          "sparse_embedding": {
            "sparseVector": {}
          }
        }

  - COLLECTION\_ID : The ID of the collection.

  - LOCATION : The region where you are using Agent Platform.

  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud beta vector-search collections create COLLECTION_ID \
      --data-schema=DATA_SCHEMA_FILE \
      --vector-schema=VECTOR_SCHEMA_FILE \
      --labels=fookey=barvalue \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud beta vector-search collections create COLLECTION_ID `
      --data-schema=DATA_SCHEMA_FILE `
      --vector-schema=VECTOR_SCHEMA_FILE `
      --labels=fookey=barvalue `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud beta vector-search collections create COLLECTION_ID ^
      --data-schema=DATA_SCHEMA_FILE ^
      --vector-schema=VECTOR_SCHEMA_FILE ^
      --labels=fookey=barvalue ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    Created collection [COLLECTION_ID].

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    vector_search_service_client = vectorsearch_v1beta.VectorSearchServiceClient()
    
    # The JSON schema for the data
    data_schema = {
        "type": "object",
        "properties": {
            "year": {"type": "number"},
            "genre": {"type": "string"},
            "director": {"type": "string"},
            "title": {"type": "string"},
        },
    }
    
    # The JSON schema for the vector
    vector_schema = {
        "plot_embedding": {"dense_vector": {"dimensions": 3}},
        "soundtrack_embedding": {"dense_vector": {"dimensions": 5}},
        "genre_embedding": {"dense_vector": {"dimensions": 4}},
        "sparse_embedding": {"sparse_vector": {}},
    }
    
    collection = vectorsearch_v1beta.Collection(
        data_schema=data_schema,
        vector_schema=vector_schema,
    )
    request = vectorsearch_v1beta.CreateCollectionRequest(
        parent="projects/PROJECT_ID/locations/LOCATION",
        collection_id="COLLECTION_ID",
        collection=collection,
    )
    
    # Create the collection
    operation = vector_search_service_client.create_collection(request=request)
    operation.result()

In the example, a request is made with `collection_id` set to `  COLLECTION_ID  ` and the following as part of the request body:

1.  `data_schema` - Specifies the Data Object structure.

2.  `vector_schema` - Configures and defines the vector fields.

All fields within the schemas must be explicitly defined. The JSON schema option `additionalProperties` isn't supported.

> **Note:** During Preview, when you use auto-embeddings, you are charged for calls to the Gemini Enterprise Agent Platform embedding service.

## Getting a Collection

The following example demonstrates how to get a reference to an existing Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    GET https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID

Request JSON body:

    {
      "data_schema": {
        "type": "object",
        "properties": {
          "year": {
            "type": "number"
          },
          "genre": {
            "type": "string"
          },
          "director": {
            "type": "string"
          },
          "title": {
            "type": "string"
          }
        }
      },
      "vector_schema": {
        "plot_embedding": {
          "dense_vector": {
            "dimensions": 3
          }
        },
        "soundtrack_embedding": {
          "dense_vector": {
            "dimensions": 5
          }
        },
        "genre_embedding": {
          "dense_vector": {
            "dimensions": 4
          }
        },
        "sparse_embedding": {
          "sparse_vector": {}
        }
      },
      "labels": {
        "fookey": "barvalue"
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
      "createTime": "2026-01-23T17:17:29.681218929Z",
      "updateTime": "2026-01-23T17:17:30.402200642Z",
      "labels": {
        "fookey": "barvalue"
      },
      "vectorSchema": {
        "genre_embedding": {
          "denseVector": {
            "dimensions": 4
          }
        },
        "sparse_embedding": {
          "sparseVector": {}
        },
        "plot_embedding": {
          "denseVector": {
            "dimensions": 3
          }
        },
        "soundtrack_embedding": {
          "denseVector": {
            "dimensions": 5
          }
        }
      },
      "dataSchema": {
        "type": "object",
        "properties": {
          "title": {
            "type": "string"
          },
          "year": {
            "type": "number"
          },
          "genre": {
            "type": "string"
          },
          "director": {
            "type": "string"
          }
        }
      }
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud  beta vector-search collections describe COLLECTION_ID \
    --location=LOCATION \
    --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud  beta vector-search collections describe COLLECTION_ID `
    --location=LOCATION `
    --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud  beta vector-search collections describe COLLECTION_ID ^
    --location=LOCATION ^
    --project=PROJECT_ID

You should receive a response similar to the following:

    createTime: '2026-01-23T17:17:29.681218929Z'
    dataSchema:
      properties:
        director:
          type: string
        genre:
          type: string
        title:
          type: string
        year:
          type: number
      type: object
    labels:
      fookey: barvalue
    name: projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID
    updateTime: '2026-01-23T17:17:30.402200642Z'
    vectorSchema:
      genre_embedding:
        denseVector:
          dimensions: 4
      plot_embedding:
        denseVector:
          dimensions: 3
      soundtrack_embedding:
        denseVector:
          dimensions: 5
      sparse_embedding:
        sparseVector: {}

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    vector_search_service_client = vectorsearch_v1beta.VectorSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1beta.GetCollectionRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
    )
    
    # Make the request
    response = vector_search_service_client.get_collection(request=request)
    
    # Handle the response
    print(response)

## Listing Collections

The following example demonstrates how to retrieve a list of existing Collections.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    GET https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "collections": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
          "createTime": "2026-01-23T17:17:29.681218929Z",
          "updateTime": "2026-01-23T17:17:30.402200642Z",
          "labels": {
            "fookey": "barvalue"
          },
          "vectorSchema": {
            "genre_embedding": {
              "denseVector": {
                "dimensions": 4
              }
            },
            "sparse_embedding": {
              "sparseVector": {}
            },
            "plot_embedding": {
              "denseVector": {
                "dimensions": 3
              }
            },
            "soundtrack_embedding": {
              "denseVector": {
                "dimensions": 5
              }
            }
          },
          "dataSchema": {
            "type": "object",
            "properties": {
              "year": {
                "type": "number"
              },
              "genre": {
                "type": "string"
              },
              "director": {
                "type": "string"
              },
              "title": {
                "type": "string"
              }
            }
          }
        }
      ]
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud beta vector-search collections list \
    --location=LOCATION \
    --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud beta vector-search collections list `
    --location=LOCATION `
    --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud beta vector-search collections list ^
    --location=LOCATION ^
    --project=PROJECT_ID

You should receive a response similar to the following:

    ---
    createTime: '2026-01-23T17:17:29.681218929Z'
    dataSchema:
      properties:
        director:
          type: string
        genre:
          type: string
        title:
          type: string
        year:
          type: number
      type: object
    labels:
      fookey: barvalue
    name: projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID
    updateTime: '2026-01-23T17:17:30.402200642Z'
    vectorSchema:
      genre_embedding:
        denseVector:
          dimensions: 4
      plot_embedding:
        denseVector:
          dimensions: 3
      soundtrack_embedding:
        denseVector:
          dimensions: 5
      sparse_embedding:
        sparseVector: {}

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    vector_search_service_client = vectorsearch_v1beta.VectorSearchServiceClient()
    
    # Initialize request argument
    request = vectorsearch_v1beta.ListCollectionsRequest(
        parent="projects/PROJECT_ID/locations/LOCATION",
    )
    
    # Make the request
    page_result = vector_search_service_client.list_collections(request=request)
    
    # Handle the response
    for response in page_result:
        print(response)

## Updating a Collection

The `UpdateCollection` method lets you modify an existing Collection resource. You can control which fields are updated through `update_mask` . If you don't provide an update mask, any fields present in your update request overwrites the corresponding fields in the Collection.

Fields specified in the update mask are relative to the Collection resource. To completely replace the entire Collection resource with the one provided in the request, use `*` as the update mask.

You can update the following fields:

  - `display_name`
  - `description`
  - `labels`
  - `data_schema`
  - `vector_schema`

You can make the following updates for `data_schema` and `vector_schema` :

  - Add fields.

  - Remove the `vertex_embedding_config` field from `vector_schema` elements. All other fields can't be removed.

  - Specify a sub-field path in `update__mask` to update nested members within `data_schema` and `vector_schema` . For example:
    
      - `data_schema.properties.new_field`
      - `vector_schema.my_vector_field`

## Deleting a Collection

The following example demonstrates how to delete an existing Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    DELETE https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/operations/operation-1769280311389-64926ac77ed08-661d4521-c7d3036c",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.vectorsearch.v1beta.OperationMetadata",
        "createTime": "2026-01-24T18:45:11.402619681Z",
        "target": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        "verb": "delete",
        "requestedCancellation": false,
        "apiVersion": "v1beta"
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

    gcloud beta vector-search collections delete COLLECTION_ID \
    --location=LOCATION \
    --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud beta vector-search collections delete COLLECTION_ID `
    --location=LOCATION `
    --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud beta vector-search collections delete COLLECTION_ID ^
    --location=LOCATION ^
    --project=PROJECT_ID

You should receive a response similar to the following:

    Deleted collection [COLLECTION_ID].

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    vector_search_service_client = vectorsearch_v1beta.VectorSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1beta.DeleteCollectionRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
    )
    
    # Make the request
    operation = vector_search_service_client.delete_collection(request=request)
    operation.result()

## What's next?

  - Learn how to [create Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects#creating_a_data_object) to add to a Collection, or [import the data from Cloud Storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/migration-from-vs-1_0) .

  - See how to [query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query) and [search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search) for Data Objects.
