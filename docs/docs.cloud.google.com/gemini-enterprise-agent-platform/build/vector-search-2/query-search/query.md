---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query
title: Querying Collections for Data Objects
description: Learn how to query collections for data objects in Agent Retrieval (formerly Vector Search 2.0).
data_source: docs.cloud.google.com
---

The purpose of the Query API is to retrieve Data Objects from a Collection using a filter. This is similar to querying a database table and using a SQL `WHERE` clause. You can also use aggregation to get a count of Data Objects matching a filter.

> **Note:** KNN queries can be sent to Collections containing a maximum of 100,000 Data Objects.

## Filter expression language

In addition to KNN/ANN search functionality, Agent Retrieval provides versatile query capabilities using a custom query language. The query language is explained in the following table.

| Filter   | Description                                                                                     | Supported Types         | Example                                                             |
| :------- | :---------------------------------------------------------------------------------------------- | :---------------------- | :------------------------------------------------------------------ |
| **$eq**  | Matches Data Objects with field values that are **equal** to a specified value.                 | Number, string, boolean | `{"genre": {"$eq": "documentary"}}`                                 |
| **$ne**  | Matches Data Objects with field values that are **not equal** to a specified value.             | Number, string, boolean | `{"genre": {"$ne": "drama"}}`                                       |
| **$gt**  | Matches Data Objects with field values that are **greater than** a specified value.             | Number                  | `{"year": {"$gt": 2019}}`                                           |
| **$gte** | Matches Data Objects with field values that are **greater than or equal** to a specified value. | Number                  | `{"year": {"$gte": 2020}}`                                          |
| **$lt**  | Matches Data Objects with field values that are **less than** a specified value.                | Number                  | `{"year": {"$lt": 2020}}`                                           |
| **$lte** | Matches Data Objects with field values that are **less than or equal** to a specified value.    | Number                  | `{"year": {"$lte": 2020}}`                                          |
| **$in**  | Matches Data Objects with field values that are **in** a specified array.                       | String                  | `{"genre": {"$in": ["comedy", "documentary"]}}`                     |
| **$nin** | Matches Data Objects with field values that are **not in** a specified array.                   | String                  | `{"genre": {"$nin": ["comedy", "documentary"]}}`                    |
| **$and** | Joins query clauses with a logical **AND.**                                                     | \-                      | `{"$and": [{"genre": {"$eq": "drama"}}, {"year": {"$gte": 2020}}]}` |
| **$or**  | Joins query clauses with a logical **OR.**                                                      | \-                      | `{"$or": [{"genre": {"$eq": "drama"}}, {"year": {"$gte": 2020}}]}`  |
| **$all** | Selects the documents where the array value of a field contains all specified values.           | \-                      | `{"colors": {"$all": ["red", "blue"]}}`                             |

> **Note:** Filter expressions cannot be nested deeper than two levels.

## Querying Collections

The following example demonstrates how to use a filter to query for Data Objects in a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:query

Request JSON body:

    {
      "page_size": 10,
      "page_token": "",
      "filter": {
        "$or": [
          {
            "director": {
              "$eq": "Akira Kurosawa"
            }
          },
          {
            "$and": [
              {
                "director": {
                  "$eq": "David Fincher"
                }
              },
              {
                "genre": {
                  "$ne": "Thriller"
                }
              }
            ]
          }
        ]
      },
      "output_fields": {
        "data_fields": "*",
        "vector_fields": "*",
        "metadata_fields": "*"
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
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:query"

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
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:query" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "dataObjects": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/1",
          "createTime": "2026-02-04T14:35:29Z",
          "updateTime": "2026-02-04T14:37:29Z",
          "data": {
            "title": "Seven Samurai",
            "director": "Akira Kurosawa",
            "genre": "Action",
            "year": 1954
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
            "plot_embedding": {
              "dense": {
                "values": [
                  1,
                  1,
                  1
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
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/2",
          "createTime": "2026-02-04T15:35:29Z",
          "updateTime": "2026-02-04T15:37:29Z",
          "data": {
            "title": "The Social Network",
            "director": "David Fincher",
            "genre": "Drama",
            "year": 2010
          },
          "vectors": {
            "genre_embedding": {
              "dense": {
                "values": [
                  0.1,
                  0.2,
                  0.3,
                  0.4
                ]
              }
            },
            "sparse_embedding": {
              "sparse": {
                "values": [
                  1
                ],
                "indices": [
                  1000
                ]
              }
            },
            "plot_embedding": {
              "dense": {
                "values": [
                  0.1,
                  0.1,
                  0.1
                ]
              }
            },
            "soundtrack_embedding": {
              "dense": {
                "values": [
                  0.1,
                  0.2,
                  0.3,
                  0.4,
                  0.5
                ]
              }
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

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud beta vector-search collections data-objects query \
      --json-filter='{"$or": [{"director": {"$eq": "Akira Kurosawa"}},{"$and": [{"director": {"$eq": "David Fincher"}},{"genre": {"$ne": "Thriller"}}]}]}' \
      --output-data-fields='*' \
      --output-vector-fields='*' \
      --output-metadata-fields='*' \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud beta vector-search collections data-objects query `
      --json-filter='{"$or": [{"director": {"$eq": "Akira Kurosawa"}},{"$and": [{"director": {"$eq": "David Fincher"}},{"genre": {"$ne": "Thriller"}}]}]}' `
      --output-data-fields='*' `
      --output-vector-fields='*' `
      --output-metadata-fields='*' `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

> **Note:** If this command uses `'` for quoting content, replace these single quotes with double quotes. If quoting is nested, use `\"` to escape the inner quotes.

    gcloud beta vector-search collections data-objects query ^
      --json-filter='{"$or": [{"director": {"$eq": "Akira Kurosawa"}},{"$and": [{"director": {"$eq": "David Fincher"}},{"genre": {"$ne": "Thriller"}}]}]}' ^
      --output-data-fields='*' ^
      --output-vector-fields='*' ^
      --output-metadata-fields='*' ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    ---
    createTime: '2026-02-04T14:35:29Z'
    data:
      director: Akira Kurosawa
      genre: Action
      title: Seven Samurai
      year: 1954
    name: projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/1
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
    ---
    createTime: '2026-02-04T15:35:29Z'
    data:
      director: David Fincher
      genre: Drama
      title: The Social Network
      year: 2010
    name: projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects/2
    updateTime: '2026-02-04T15:37:29Z'
    vectors:
      genre_embedding:
        dense:
          values:
          - 0.1
          - 0.2
          - 0.3
          - 0.4
      plot_embedding:
        dense:
          values:
          - 0.1
          - 0.1
          - 0.1
      soundtrack_embedding:
        dense:
          values:
          - 0.1
          - 0.2
          - 0.3
          - 0.4
          - 0.5
      sparse_embedding:
        sparse:
          indices:
          - 1000
          values:
          - 1.0

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    data_object_search_service_client = vectorsearch_v1beta.DataObjectSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1beta.QueryDataObjectsRequest(
        parent="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        filter={
            "$or": [
                {"director": {"$eq": "Akira Kurosawa"}},
                {
                    "$and": [
                        {"director": {"$eq": "David Fincher"}},
                        {"genre": {"$ne": "Thriller"}},
                    ]
                },
            ]
        },
    )
    
    # Make the request
    page_result = data_object_search_service_client.query_data_objects(request=request)
    
    # Handle the response
    for response in page_result:
        print(response)

To perform an aggregation, you use the `aggregate` endpoint and specify the type of aggregation in the request body.

The following example demonstrates how to count all Data Objects in a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:aggregate

Request JSON body:

    {
      "aggregate": "count"
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:aggregate"

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
        -Uri "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:aggregate" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "aggregateResults": [
        {
          "count": 1000
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

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud beta vector-search collections data-objects aggregate \
      --aggregation-method=count \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud beta vector-search collections data-objects aggregate `
      --aggregation-method=count `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud beta vector-search collections data-objects aggregate ^
      --aggregation-method=count ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    aggregateResults:
    - count: 1000

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    data_object_search_service_client = vectorsearch_v1beta.DataObjectSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1beta.AggregateDataObjectsRequest(
        parent="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        aggregate="COUNT",
    )
    
    # Make the request
    response = data_object_search_service_client.aggregate_data_objects(request=request)
    
    # Handle the response
    print(response)

## What's next?

  - Learn how to [search for Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search) .
