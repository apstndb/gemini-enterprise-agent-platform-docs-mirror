---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search
title: Searching for Data Objects
description: Learn about the different ways to search for Data Objects in Vector Search 2.0.
data_source: docs.cloud.google.com
---

The purpose of the Search API is to find Data Objects that are similar to a given query and return a list of ranked results (ranked by similarity). The Search API also supports filtering.

The Search API offers a variety of ways to search for Data Objects: vector search, full text search, and semantic search. Additionally, multiple searches of any type can be combined together to achieve hybrid search.

## Vector search

Vector search lets you provide your own query vector. This is the required method for searching embedding fields that don't have an `embedding-config` . If multiple `vector_search` fields are provided, results are combined using equal weights.

The following example demonstrates how to perform a vector search on a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:search

Request JSON body:

    {
      "vector_search": {
        "search_field": "plot_embedding",
        "vector": {
          "values": [
            0.42426406871192845,
            0.565685424949238,
            0.7071067811865475
          ]
        },
        "filter": {
          "genre": {
            "$eq": "Thriller"
          }
        },
        "top_k": 5,
        "output_fields": {
          "data_fields": "*",
          "vector_fields": "*",
          "metadata_fields": "*"
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
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:search"

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
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:search" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "results": [
        {
          "dataObject": {
            "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/1",
            "createTime": "2026-01-31T20:05:06Z",
            "updateTime": "2026-02-02T13:59:24Z",
            "data": {
              "year": 1991,
              "title": "The Silence of the Lambs",
              "director": "Jonathan Demme",
              "genre": "Thriller"
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
          },
          "distance": 1.697
        },
        {
          "dataObject": {
            "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/2",
            "createTime": "2026-02-04T14:35:29Z",
            "updateTime": "2026-02-04T14:37:29Z",
            "data": {
              "year": 1995,
              "title": "Se7en",
              "director": "David Fincher",
              "genre": "Thriller"
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
                    1,
                    1,
                    1
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
          },
          "distance": 1.75
        }
      ]
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - SEARCH\_VECTOR\_FILE : The local path to a JSON file containing the dense or sparse vector to search with.
    
    Example file content for a dense vector:
    
        {
          "dense": {
            "values": [
              0.42426406871192845,
              0.565685424949238,
              0.7071067811865475
            ]
          }
        }
    
    Example file content for a sparse vector:
    
        {
          "sparse": {
            "indices": [1, 5, 10],
            "values": [0.1, 0.5, 0.21]
          }
        }

  - COLLECTION\_ID : The ID of the collection.

  - LOCATION : The region where you are using Agent Platform.

  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud beta vector-search collections data-objects search \
      --vector-search-field="plot_embedding" \
      --vector-from-file=SEARCH_VECTOR_FILE \
      --json-filter='{"genre": {"$eq": "Thriller"}}' \
      --top-k=5 \
      --output-data-fields='*' \
      --output-vector-fields='*' \
      --output-metadata-fields='*' \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud beta vector-search collections data-objects search `
      --vector-search-field="plot_embedding" `
      --vector-from-file=SEARCH_VECTOR_FILE `
      --json-filter='{"genre": {"$eq": "Thriller"}}' `
      --top-k=5 `
      --output-data-fields='*' `
      --output-vector-fields='*' `
      --output-metadata-fields='*' `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

> **Note:** If this command uses `'` for quoting content, replace these single quotes with double quotes. If quoting is nested, use `\"` to escape the inner quotes.

    gcloud beta vector-search collections data-objects search ^
      --vector-search-field="plot_embedding" ^
      --vector-from-file=SEARCH_VECTOR_FILE ^
      --json-filter='{"genre": {"$eq": "Thriller"}}' ^
      --top-k=5 ^
      --output-data-fields='*' ^
      --output-vector-fields='*' ^
      --output-metadata-fields='*' ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    ---
    dataObject:
      createTime: '2026-01-31T20:05:06Z'
      data:
        director: Jonathan Demme
        genre: Thriller
        title: The Silence of the Lambs
        year: 1991
      name: projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/1
      updateTime: '2026-02-02T13:59:24Z'
      vectors:
        genre_embedding:
          dense:
            values:
            - 0.38638
            - 0.739343
            - 0.161891
            - 0.527137
        plot_embedding:
          dense:
            values:
            - 1.0
            - 1.0
            - 1.0
        soundtrack_embedding:
          dense:
            values:
            - 0.592045
            - 0.0830164
            - 0.126473
            - 0.619643
            - 0.492583
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
    distance: 1.697
    ---
    dataObject:
      createTime: '2026-02-04T14:35:29Z'
      data:
        director: David Fincher
        genre: Thriller
        title: Se7en
        year: 1995
      name: projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/2
      updateTime: '2026-02-04T14:37:29Z'
      vectors:
        genre_embedding:
          dense:
            values:
            - 0.38638
            - 0.739343
            - 0.161891
            - 0.527137
        plot_embedding:
          dense:
            values:
            - 1.0
            - 1.0
            - 1.0
        soundtrack_embedding:
          dense:
            values:
            - 0.592045
            - 0.0830164
            - 0.126473
            - 0.619643
            - 0.492583
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
    distance: 1.75

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    data_object_search_service_client = vectorsearch_v1beta.DataObjectSearchServiceClient()
    
    # Initialize request
    vector_search = vectorsearch_v1beta.VectorSearch(
        search_field="plot_embedding",
        vector={"values": [0.1, 0.2, 0.3]},
        filter={"genre": {"$eq": "Thriller"}},
        top_k=5,
    )
    request = vectorsearch_v1beta.SearchDataObjectsRequest(
        parent="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        vector_search=vector_search,
    )
    
    # Make the request
    response = data_object_search_service_client.search_data_objects(request=request)
    
    # Handle the response
    print(response)

## Text search

This performs full-text search without sparse vectors. The default "word" query dialect treats the entire input as individual search terms with an implicit `AND` operator. You can set `enhanced_query` to `true` to expand search terms, handle stemming, stop word removal, and allow for additional search operators:

  - `OR` : A case-sensitive disjunction operator that matches documents containing at least one of the specified terms. It only applies to the two adjacent terms.

  - `"` : (double quotes) for phrase search.

  - `-` : The negation operator. It excludes documents containing any terms it is placed before.

## Semantic search

This search converts your text query into embeddings to find results based on semantic meaning. It uses the `embedding-config` defined in your schema to generate the query embedding. If multiple `vector_search` fields are provided, results are combined using equal weights.

> **Note:** Only vector fields that are managed by an auto-embedding specification can be used in a semantic search.

## Searching using hybrid search

Use `batch_search_data_objects` to execute multiple searches in parallel (vector search, text search, and semantic search). The results can optionally be combined and ranked using the **`ReciprocalRankFusion`** Ranker, which merges result sets using the Reciprocal Rank Fusion (RFF) algorithm.
