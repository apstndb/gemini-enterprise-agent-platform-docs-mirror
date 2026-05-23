---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/migration-from-vs-1_0
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/migration-from-vs-1_0
title: Migrate from Vector Search 1.0
description: Migrate from Vector Search 1.0
data_source: docs.cloud.google.com
---

To streamline the transition from Vector Search 1.0, a new feature has been introduced to the `ImportDataObjects` API.

The migration process involves three key steps:

1.  **Create a Collection with a matching schema.** Before importing, you must create a Collection. Its data schema must be structured to accommodate the transformed Vector Search 1.0 data.

2.  **Initiate the import process.** Call the `ImportDataObjects` API, specifying the Cloud Storage location of your Vector Search 1.0 data and enabling the conversion flag `detect_and_convert_vs1_json` .

3.  **Understand data transformation.** Familiarize yourself with how your Vector Search 1.0 data fields are mapped to the new Data Object structure.

## Create a Collection

First, create a Collection with a data schema that mirrors the structure of your Vector Search 1.0 data.

### REST

    curl -X POST \
      'https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections?collection_id=COLLECTION_ID' \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H 'Content-Type: application/json' \
      -d '{
        "data_schema": {
          "type": "object",
          "properties": {
            "restricts": {
              "type": "object",
              "properties": {
                "genres": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                },
                "director": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            },
            "restricts_deny": {
              "type": "object",
              "properties": {
                "genres": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            },
            "numeric_restricts": {
              "type": "object",
              "properties": {
                "year": {
                  "type": "integer"
                },
                "imdb_rating": {
                  "type": "number",
                  "format": "float"
                }
              }
            },
            "embedding_metadata": {
              "type": "object",
              "properties": {
                "plot": {
                  "type": "string"
                },
                "customers_review_summary": {
                  "type": "string"
                },
                "critics_review_summary": {
                  "type": "string"
                }
              },
            }
          }
        },
        "vector_schema": {
          "embedding": {
            "dense_vector": {
              "dimensions": 768
            }
          },
          "sparse_embedding": {
            "sparse_vector": {}
          }
        }
      }'

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    vector_search_service_client = vectorsearch_v1beta.VectorSearchServiceClient()
    
    # The JSON schema for the data
    data_schema = {
        "type": "object",
        "properties": {
            "restricts": {
                "type": "object",
                "properties": {
                    "genres": {"type": "array", "items": {"type": "string"}},
                    "director": {"type": "array", "items": {"type": "string"}},
                },
            },
            "restricts_deny": {
                "type": "object",
                "properties": {
                    "genres": {"type": "array", "items": {"type": "string"}}
                },
            },
            "numeric_restricts": {
                "type": "object",
                "properties": {
                    "year": {"type": "integer"},
                    "imdb_rating": {"type": "number", "format": "float"},
                },
            },
            "embedding_metadata": {
                "type": "object",
                "properties": {
                    "plot": {"type": "string"},
                    "customers_review_summary": {"type": "string"},
                    "critics_review_summary": {"type": "string"},
                },
            },
        },
    }
    
    # The JSON schema for the vector
    vector_schema = {
        "embedding": {"dense_vector": {"dimensions": 768}},
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

## Import your Vector Search 1.0 data

Next, use the `ImportDataObjects` API on your newly created collection. Point it to the Cloud Storage bucket containing your Vector Search 1.0 data.

### REST

    curl -X POST \
    "https://vectorsearch.googleapis.com/v1beta/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID:importDataObjects" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      -d '{
        "gcs_import": {
          "contents_uri": "gs://your-bucket/path/to/your-data.jsonl",
          "error_uri": "gs://your-bucket/path/to/import-errors/"
        }
      }'

### Python

    from google.cloud import vectorsearch_v1beta
    
    # Create the client
    vector_search_service_client = vectorsearch_v1beta.VectorSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1beta.ImportDataObjectsRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        gcs_import={
          "contents_uri": "gs://your-bucket/path/to/your-data.jsonl",
          "error_uri": "gs://your-bucket/path/to/import-errors/",
        },
    )
    
    # Make the request
    operation = vector_search_service_client.import_data_objects(request=request)
    
    # Wait for the result (note this may take up to several minutes)
    operation.result()

## Data transformation

During the import process, your Vector Search 1.0 data will be transformed into Vector Search 2.0 Data Objects. The following examples illustrate how the fields are mapped.

**Vector Search 1.0 Cloud Storage file format**

    {
        "id": "movie-789",
        "embedding": [-0.23, 0.88, 0.11, ...],
        "sparse_embedding": {"values": [0.1, 0.2], "dimensions": [1, 4]},
        "restricts": [
            {"namespace": "genres", "allow": ["science-fiction", "action"], "deny": ["horror"]},
            {"namespace": "director", "allow": ["Christopher Nolan"]}
        ],
        "numeric_restricts": [
            {"namespace": "year", "value_int": 2010},
            {"namespace": "imdb_rating", "value_float": 8.8}
        ],
        "embedding_metadata": {
            "plot": "...",
            "customers_review_summary": "...",
            "critics_review_summary": "..."
        }
    }

**Transformed Vector Search 2.0 Data Object**

    DataObject(
        name="/.../movie-789",
        data={
            "restricts": {
                "genres": ["science-fiction", "action"],
                "director": ["Christopher Nolan"],
            },
            "restricts_deny": {
                "genres": ["horror"]
            },
            "numeric_restricts": {
                "year": 2010,
                "imdb_rating": 8.8,
            },
            "embedding_metadata": {
                "plot": "...",
                "customers_review_summary": "...",
                "critics_review_summary": "...",
            }
        },
        vectors={
            "embedding": {"dense_vector": {"values": [-0.23, 0.88, 0.11, ...]}},
            "sparse_embedding": {"sparse_vector": {"values": [0.1, 0.2], "indices": [1, 4]}},
        }
    )
