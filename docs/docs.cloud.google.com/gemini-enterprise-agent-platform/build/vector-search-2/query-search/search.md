---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search
title: Searching for Data Objects
description: Learn about the different ways to search for Data Objects in Agent Retrieval (formerly Vector Search 2.0).
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

    POST https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:search

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
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:search"

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
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/dataObjects:search" | Select-Object -Expand Content

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

    gcloud vector-search collections data-objects search \
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

    gcloud vector-search collections data-objects search `
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

    gcloud vector-search collections data-objects search ^
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

    from google.cloud import vectorsearch_v1
    
    # Create the client
    data_object_search_service_client = vectorsearch_v1.DataObjectSearchServiceClient()
    
    # Initialize request
    vector_search = vectorsearch_v1.VectorSearch(
        search_field="plot_embedding",
        vector={"values": [0.1, 0.2, 0.3]},
        filter={"genre": {"$eq": "Thriller"}},
        top_k=5,
    )
    request = vectorsearch_v1.SearchDataObjectsRequest(
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

## Advanced text search

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Agent Retrieval text search API lets you express text searches through *structured queries* containing one or more *subqueries* , allowing you to:

  - Match against specific [Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects) fields.

  - Specify the [type](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#match_type) of match to perform:
    
      - Per *term* , case-insensitive
    
      - Exactly, case-sensitive

  - Include per-language [enhancements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#enhancement) to match on term stems, synonyms, misspellings, and stop words (such as "a", "an", and "the").

  - Use [`AND`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#and) , [`OR`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#or) , and [`NOT`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#not) boolean operators to combine subqueries.

  - Control evaluation order by [grouping](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#grouping) subqueries together.

  - [Boost](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#boosts) score contributions to influence rankings.

> **Warning:** Don't use structured queries with the `search_text` and `data_field_name` fields, otherwise the error `INVALID_ARGUMENT` will be returned.

There are three types of subqueries:

  - [**Text**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#text) : Provides the search text and one or more fields to match against.

  - [**Unary**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#unary) : Applies a [**NOT**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#not) operation on a single subquery.

  - [**Combined**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#combined) : Applies the [`AND`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#and) or [`OR`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#or) operator to combine subqueries, and can be used to [group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search#grouping) other combined subqueries to control evaluation order.

> **Note:** Structured queries can contain a maximum of 1024 subqueries and a nesting depth of 2.

The examples on this page use the [Collection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections) demonstrated in the following table. It contains six Data Objects and defines the following fields in its data schema: the strings `ID` , `Title` , `Description` , and the string array `Keywords` .

| ID | Title                  | Description                                              | Keywords                                                   |
| :- | :--------------------- | :------------------------------------------------------- | :--------------------------------------------------------- |
| 1  | The Quick Brown Fox    | A quick brown fox easily jumps over the lazy dog.        | wild, forest, mammal, orange, agility, predator            |
| 2  | Lazy Dog Days          | The brown dog sleeps.                                    | domestic, pet, house, canine, calm, lazy, obedient         |
| 3  | Fox vs Dog             | The quick fox outsmarts the dog.                         | wild, domestic, conflict, caniformia, mammals, interaction |
| 4  | Brown Bears            | Quick movements in the forest.                           | wild, forest, ursine, apex predator, hibernation, giant    |
| 5  | A foxy story           | The dog jumps high.                                      | cunning, jumps                                             |
| 6  | My Lazy Days of Summer | A short story about relaxing during the summer vacation. | summer, relax, vacation, sun                               |

### Text subqueries

Text queries match against one or more fields in a Data Object. All structured queries must contain at least one text query.

The following example defines a basic text query:

    "text_search": {
      "structured_query": {
        "text": {
          "text": "fox vs dog"
        }
      }
    }

By default, the text is split into individual terms, and each term is searched for in the fields specified. In the preceding example, the terms "fox", "vs", and "dog" are searched for in the `Title` field.

Text queries have the following optional parameters:

  - `fields` : An array of fields to match against. If not specified, the default is to match against all fields. Fields are matched with an implicit `OR` operator.

  - `match_type` : The type of match to perform. The match type can be `EXACT` , which specifies the field must match the search text exactly. If the field is a string array, a match is performed against any element in the array.

  - `enhancement` : Specifies `enabled` and a `languageCode` , allowing matches to be performed against synonyms, stems, misspellings, and stop words in the language specified for `languageCode` (for example, `en-US` ). The default is no enhancement.

  - `boost` : Optional. A multiplier to apply to the score of the query. The default is `1.0` .

### Match type

The `match_type` parameter specifies how search text matches a field's value.

The parameter's value can be:

  - `EXACT` : The field must match the query term exactly. If the field is a string array, a match is performed against any element in the array.

The following example specifies the `EXACT` match type:

    "text_search": {
      "structured_query": {
        "text": {
          "text": "Fox vs Dog",
          "fields": [ "Title" ],
          "match_type": "EXACT"
        }
      }
    }

### Match type for string arrays

The results of the query are shown in the following table:

| Score  | ID | Title      | Description                      | Keywords                                                   |
| :----- | :- | :--------- | :------------------------------- | :--------------------------------------------------------- |
| 1.0000 | 3  | Fox vs Dog | The quick fox outsmarts the dog. | wild, domestic, conflict, caniformia, mammals, interaction |

When the field is a string array, the search text is matched against any array element.

The following example shows how to search for the exact text `wild` in the `Keywords` string array:

    "text_search": {
      "structured_query": {
        "text": {
          "text": "wild",
          "fields": [ "Keywords" ],
          "match_type": "EXACT"
        }
      }
    }

The results of the query are shown in the following table:

| Score  | ID | Title               | Description                                       | Keywords                                                   |
| :----- | :- | :------------------ | :------------------------------------------------ | :--------------------------------------------------------- |
| 1.0000 | 3  | Fox vs Dog          | The quick fox outsmarts the dog.                  | wild, domestic, conflict, caniformia, mammals, interaction |
| 1.0000 | 4  | Brown Bears         | Quick movements in the forest.                    | wild, forest, ursine, apex predator, hibernation, giant    |
| 1.0000 | 1  | The Quick Brown Fox | A quick brown fox easily jumps over the lazy dog. | wild, forest, mammal, orange, agility, predator            |

### Query enhancements

Search queries can include an optional `queryEnhancement` parameter to specify language-specific enhancements. This includes matching against synonyms, stems (for example, the "jump" stem "jumping"), incorrect spellings, and stop words (such as "a", "an", and "the").

> **Note:** Query enhancements can incur a small decrease in performance

The parameter is an object with the following properties:

  - `enabled` : A boolean that specifies whether to enable enhancements.

  - `languageCode` : A string that specifies the language for the enhancements (for example, `en-US` ).

The following example enables enhancements for the `en-US` language:

    "text_search": {
      "structured_query": {
        "text": {
          "text": {
            "text": "jump",
            "fields": [ "Description" ],
            "queryEnhancement": {
              "enabled": true,
              "languageCode": "en-US"
            }
          }
        }
      }
    }

The results of the query are shown in the following table:

| Score  | ID | Title               | Description                                       | Keywords                                        |
| :----- | :- | :------------------ | :------------------------------------------------ | :---------------------------------------------- |
| 0.3419 | 1  | The Quick Brown Fox | A quick brown fox easily jumps over the lazy dog. | wild, forest, mammal, orange, agility, predator |
| 0.3419 | 5  | A foxy story        | The dog jumps high.                               | cunning, jumps                                  |

If `queryEnhancement` was not specified or `enabled` was `false` , no match would be made.

### Combined subqueries

Combined queries apply a boolean operation to two or more subqueries. The supported operations are `AND` and `OR` .

Combined queries have the following properties:

  - `op` : The boolean operator to apply to the subqueries. The value can be `AND` or `OR` .

  - `subQueries` : An array of subqueries to combine. These can be any of the supported subquery types, including other combined queries. There is a maximum nesting depth of 2.
    
      - `boost` : Optional. A multiplier to apply to the score of the query. The default is `1.0` .

### Conjunction ( `AND` )

The `AND` operator matches Data Objects that contain the terms of all subqueries.

The following example demonstrates how to combine three text queries using the `AND` operator:

    "text_search": {
      "structured_query": {
        "combine": {
          "op": "AND",
          "subQueries": [
            {
              "text": {
                "text": "Brown",
                "fields": [ "Title" ]
              }
            },
            {
              "text": {
                "text": "quick",
                "fields": [ "Description" ]
              }
            },
            {
              "text": {
                "text": "forest predator",
                "fields": [ "Keywords" ]
              }
            }
          ]
        }
      }
    }

In the example, matches are only made if all three subqueries match.

The results of the query are shown in the following table:

| Score  | ID | Title               | Description                                       | Keywords                                                |
| :----- | :- | :------------------ | :------------------------------------------------ | :------------------------------------------------------ |
| 5.0587 | 4  | Brown Bears         | Quick movements in the forest.                    | wild, forest, ursine, apex predator, hibernation, giant |
| 5.0587 | 1  | The Quick Brown Fox | A quick brown fox easily jumps over the lazy dog. | wild, forest, mammal, orange, agility, predator         |

When a text subquery has multiple fields to match on, an implicit `OR` is applied, as shown in the following example:

    "text_search": {
      "structured_query": {
        "combine": {
          "op": "AND",
          "subQueries": [
            {
              "text": {
                "text": "Brown",
                "fields": [ "Title", "Description" ]
              }
            },
            {
              "text": {
                "text": "quick",
                "fields": [ "Description" ]
              }
            },
            {
              "text": {
                "text": "forest predator",
                "fields": [ "Keywords" ]
              }
            }
          ]
        }
      }
    }

In the preceding example:

  - The first subquery matches the case-insensitive term `Brown` in either the `Title` or `Description` field.

  - The second subquery matches the case-insensitive term `quick` in the `Description` field.

  - The third subquery matches the case-insensitive terms `forest` and `predator` in any of the values in the `Keywords` string array field.

  - If all three subqueries match, a match is made on the combined query.

The results of the query are shown in the following table:

| Score  | ID | Title               | Description                                       | Keywords                                                |
| :----- | :- | :------------------ | :------------------------------------------------ | :------------------------------------------------------ |
| 6.3176 | 1  | The Quick Brown Fox | A quick brown fox easily jumps over the lazy dog. | wild, forest, mammal, orange, agility, predator         |
| 5.0587 | 4  | Brown Bears         | Quick movements in the forest.                    | wild, forest, ursine, apex predator, hibernation, giant |

### Disjunction ( `OR` )

The `OR` operator matches Data Objects that contain the terms of at least one of the subqueries.

The following example demonstrates how to combine three text queries using the `OR` operator:

    "text_search": {
      "structured_query": {
        "combine": {
          "op": "OR",
          "subQueries": [
            {
              "text": {
                "text": "Brown",
                "fields": [ "Title", "Description" ]
              }
            },
            {
              "text": {
                "text": "quick",
                "fields": [ "Description" ]
              }
            },
            {
              "text": {
                "text": "forest predator",
                "fields": [ "Keywords" ]
              }
            }
          ]
        }
      }
    }

In the example, a match is made if any of the three subqueries match.

The results of the query are shown in the following table:

| Score  | ID | Title               | Description                                       | Keywords                                                |
| :----- | :- | :------------------ | :------------------------------------------------ | :------------------------------------------------------ |
| 6.3176 | 1  | The Quick Brown Fox | A quick brown fox easily jumps over the lazy dog. | wild, forest, mammal, orange, agility, predator         |
| 5.0587 | 4  | Brown Bears         | Quick movements in the forest.                    | wild, forest, ursine, apex predator, hibernation, giant |

### Grouping

Combined subqueries can be nested within other combined subqueries in order to control the evaluation order.

> **Note:** The maximum nesting depth is 2.

The following example demonstrates how to group subqueries:

    "text_search": {
      "structured_query": {
        "combine": {
          "op": "AND",
          "subQueries": [
            {
              "combine": {
                "op": "OR",
                "subQueries": [
                  {
                    "text": {
                      "text": "Fox",
                      "fields": [ "Title" ]
                    }
                  },
                  {
                    "text": {
                      "text": "jumps",
                      "fields": [ "Description" ]
                    }
                  }
                ]
              }
            },
            {
              "unary": {
                "op": "NOT",
                "subQuery": {
                  "text": {
                    "text": "domestic",
                    "fields": [ "Keywords" ]
                  }
                }
              }
            }
          ]
        }
      }
    }

The preceding example is equivalent to the following: (Case-insensitive `Fox` in `Title` **OR** case-insensitive `jumps` in `Description` ) **AND NOT** case-insensitive `domestic` in any of the `Keywords` elements.

The following table shows the results of the query:

| Score  | ID | Title               | Description                                       | Keywords                                        |
| :----- | :- | :------------------ | :------------------------------------------------ | :---------------------------------------------- |
| 3.5178 | 1  | The Quick Brown Fox | A quick brown fox easily jumps over the lazy dog. | wild, forest, mammal, orange, agility, predator |
| 2.2589 | 5  | A foxy story        | The dog jumps high.                               | cunning, jumps                                  |

### Unary subqueries

Unary subqueries apply a boolean operation to a single subquery in a structured query. The `NOT` operator is the only supported unary operation.

Unary queries have the following properties:

  - `op` : The boolean operator to apply to the subquery. The value can be `NOT` .

  - `subQuery` : The subquery to apply the unary operation to.
    
      - `boost` : Optional. A multiplier to apply to the score of the query. The default is `1.0` .

> **Note:** Unary queries can contain only a single subquery.

### Negation ( `NOT` )

The `NOT` operator matches Data Objects that don't contain the terms of the subquery.

The following example demonstrates how to use the `NOT` operator:

    "text_search": {
      "structured_query": {
        "unary": {
          "op": "NOT",
          "subQuery": {
            "text": {
              "text": "dog",
              "fields": [ "Description" ]
            }
          }
        }
      }
    }

The results of the query are shown in the following table:

| Score | ID | Title                  | Description                                              | Keywords                                                |
| :---- | :- | :--------------------- | :------------------------------------------------------- | :------------------------------------------------------ |
| 1.000 | 4  | Brown Bears            | Quick movements in the forest.                           | wild, forest, ursine, apex predator, hibernation, giant |
| 1.000 | 6  | My Lazy Days of Summer | A short story about relaxing during the summer vacation. | summer, relax, vacation, sun                            |

When applied to a string array, the `NOT` operator matches a Data Object if the term is not contained in any of the array's elements.

In the example, a match is made if the case-insensitive term `orange` is not contained in any element of the `Keywords` string array.

    "text_search": {
      "structured_query": {
        "combine": {
          "op": "AND",
          "subQueries": [
            {
              "text": {
                "text": "Brown",
                "fields": [ "Title" ]
              }
            },
            {
              "text": {
                "text": "quick",
                "fields": [ "Description" ]
              }
            },
            {
              "text": {
                "text": "forest predator",
                "fields": [ "Keywords" ]
              }
            },
            {
              "unary": {
                "op": "NOT",
                "subQuery": {
                  "text": {
                    "text": "orange",
                    "fields": [ "Keywords" ]
                  }
                }
              }
            }
          ]
        }
      }
    }

The results of the query are shown in the following table:

| Score  | ID | Title       | Description                    | Keywords                                                |
| :----- | :- | :---------- | :----------------------------- | :------------------------------------------------------ |
| 6.0587 | 4  | Brown Bears | Quick movements in the forest. | wild, forest, ursine, apex predator, hibernation, giant |

### Boosting

Any subquery can have a `boost` parameter to apply a multiplier to the score of the subquery. By default, all subqueries have a `boost` of `1.0` .

The following example demonstrates how to boost a subquery:

    "text_search": {
      "structured_query": {
        "combine": {
          "op": "OR",
          "subQueries": [
            {
              "text": {
                "text": "fox",
                "fields": [ "Title" ]
              },
              "boost": 1.0
            },
            {
              "text": {
                "text": "jumps",
                "fields": [ "Description" ]
              },
              "boost": 1.0
            },
            {
              "text": {
                "text": "interaction",
                "fields": [ "Keywords" ]
              },
              "boost": 5.0
            }
          ]
        }
      }
    }

The results of the query are shown in the following table:

| Score  | ID | Title               | Description                                       | Keywords                                                   |
| :----- | :- | :------------------ | :------------------------------------------------ | :--------------------------------------------------------- |
| 7.5534 | 3  | Fox vs Dog          | The quick fox outsmarts the dog.                  | wild, domestic, conflict, caniformia, mammals, interaction |
| 2.5178 | 1  | The Quick Brown Fox | A quick brown fox easily jumps over the lazy dog. | wild, forest, mammal, orange, agility, predator            |
| 1.2589 | 5  | A foxy story        | The dog jumps high.                               | cunning, jumps                                             |

## Semantic search

This search converts your text query into embeddings to find results based on semantic meaning. It uses the `embedding-config` defined in your schema to generate the query embedding. If multiple `vector_search` fields are provided, results are combined using equal weights.

> **Note:** Only vector fields that are managed by an auto-embedding specification can be used in a semantic search.

## Searching using hybrid search

Use `batch_search_data_objects` to execute multiple searches in parallel (vector search, text search, and semantic search). The results can optionally be combined and ranked using the **`ReciprocalRankFusion`** Ranker, which merges result sets using the Reciprocal Rank Fusion (RFF) algorithm.
