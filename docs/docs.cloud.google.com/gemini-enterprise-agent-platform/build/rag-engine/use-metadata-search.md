---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-metadata-search
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-metadata-search
title: Filter with metadata search
description: Use metadata search to filter contexts during retrieval in RAG Engine on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> Some of the RAG features are Preview offerings, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as-is" and may have limited support, and changes to Pre-GA products and features may not be compatible with other Pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) . By using the Gemini API on Gemini Enterprise Agent Platform, you agree to the Generative AI Preview [terms and conditions](https://cloud.google.com/trustedtester/aitos) (Preview Terms).

> The [VPC-SC security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) and CMEK are supported by Agent Platform RAG Engine. Data residency and AXT security controls aren't supported.

> **VPC Service Controls:** The metadata search feature is unavailable for projects that had VPC Service Controls enabled before metadata search was released to Preview. If you enable VPC Service Controls after the Preview release, metadata search is available to use.

This page shows how to use the schema-based metadata search feature in RAG Engine on Gemini Enterprise Agent Platform. You can define a metadata schema for a corpus, attach metadata to files within that corpus, and use this metadata to filter contexts during retrieval.

> **Note:** Metadata search is available only in the `v1beta1` API. It isn't supported in serverless mode.

## Before you begin

To use metadata search, you must have an existing RAG corpus and RAG files. To learn how to create a corpus and upload files, see [Manage your RAG knowledge base](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/manage-your-rag-corpus) .

When you create a corpus or upload a file, the API returns a numeric `RAG_CORPUS_ID` and `RAG_FILE_ID` (for example, `123456789` ). You must have these IDs on hand to manage your metadata resources.

## Metadata resources

The metadata search feature uses the following resource hierarchy:

  - **RagCorpus:** The top-level resource that contains your RAG files and their configurations.
    
      - **RagDataSchema:** A child resource of `RagCorpus` . It defines the structure for a single metadata field used within the corpus. Each schema specifies a key (for example, `year` ) and a data type ( `INTEGER` , `FLOAT` , `STRING` , `DATETIME` , `BOOLEAN` , or `LIST` ). You must define a `RagDataSchema` for each metadata key that you intend to use for filtering.
    
      - **RagFile:** A child resource of `RagCorpus` representing a single ingested document.
        
          - **RagMetadata:** A child resource of `RagFile` . It represents a single key-value metadata pair attached to that specific file (for example, `year=2024` ). The key used in a `RagMetadata` resource must correspond to a key defined in a `RagDataSchema` for the parent corpus. Multiple `RagMetadata` resources can be attached to a single file.

## Manage metadata schemas

After you create a RAG corpus, define the metadata structure using the `RagDataSchema` resource at the corpus level. You can also view and delete the schemas you define.

### Define metadata schemas

When defining a schema, you specify a key and a data type. The valid types a key can be are:

  - `INTEGER` : Passed in metadata values as an `int_value` .
  - `FLOAT` : Passed in metadata values as a `float_value` .
  - `STRING` : Passed in metadata values as a `str_value` .
  - `DATETIME` : Passed in metadata values as a `datetime_value` (RFC 3339 formatted string, for example, "2024-01-01T00:00:00Z").
  - `BOOLEAN` : Passed in metadata values as a `bool_value` .
  - `LIST` : Passed in metadata values as a `list_value` . The following REST sample shows how to batch create metadata schemas that define the `year` , and `month` fields for a corpus.

### REST

Replace the following variables:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the RAG corpus.

<!-- end list -->

    PROJECT_ID=PROJECT_ID
    LOCATION=LOCATION
    RAG_CORPUS_ID=RAG_CORPUS_ID
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora/${RAG_CORPUS_ID}/ragDataSchemas:batchCreate \
    -d '{
      "parent": "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'",
      "requests": [
        {
          "parent": "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'",
          "rag_data_schema": {
            "key": "year",
            "schema_details": {"type": "INTEGER"}
          }
        },
        {
          "parent": "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'",
          "rag_data_schema": {
            "key": "month",
            "schema_details": {"type": "STRING"}
          }
        }
      ]
    }'

### List metadata schemas

The following REST sample shows how to list the metadata schemas defined for a corpus.

### REST

Replace the following variables:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the RAG corpus.

<!-- end list -->

    PROJECT_ID=PROJECT_ID
    LOCATION=LOCATION
    RAG_CORPUS_ID=RAG_CORPUS_ID
    curl -X GET \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora/${RAG_CORPUS_ID}/ragDataSchemas

### Delete metadata schemas

The following REST sample shows how to batch delete metadata schemas from a corpus.

### REST

Replace the following variables:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the RAG corpus.
  - **RAG\_DATA\_SCHEMA\_KEY\_1** : The key name of the first metadata schema to delete.
  - **RAG\_DATA\_SCHEMA\_KEY\_2** : The key name of the second metadata schema to delete.

<!-- end list -->

    PROJECT_ID=PROJECT_ID
    LOCATION=LOCATION
    RAG_CORPUS_ID=RAG_CORPUS_ID
    RAG_DATA_SCHEMA_KEY_1=RAG_DATA_SCHEMA_KEY_1
    RAG_DATA_SCHEMA_KEY_2=RAG_DATA_SCHEMA_KEY_2
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora/${RAG_CORPUS_ID}/ragDataSchemas:batchDelete \
    -d '{
      "names": [
        "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'/ragDataSchemas/'"${RAG_DATA_SCHEMA_KEY_1}"'",
        "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'/ragDataSchemas/'"${RAG_DATA_SCHEMA_KEY_2}"'"
      ]
    }'

## Manage file metadata

After you upload or import files to your corpus, you can attach, update, view, and delete metadata associated with those files.

### Attach metadata to a file

The attached metadata must conform to the schema defined for the corpus. The following REST sample shows how to attach multiple metadata values to a file.

### REST

Replace the following variables:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the RAG corpus.
  - **RAG\_FILE\_ID** : The ID of the RAG file.

<!-- end list -->

    PROJECT_ID=PROJECT_ID
    LOCATION=LOCATION
    RAG_CORPUS_ID=RAG_CORPUS_ID
    RAG_FILE_ID=RAG_FILE_ID
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora/${RAG_CORPUS_ID}/ragFiles/${RAG_FILE_ID}/ragMetadata:batchCreate \
    -d '{
      "parent": "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'/ragFiles/'"${RAG_FILE_ID}"'",
      "requests": [
        {
          "parent": "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'/ragFiles/'"${RAG_FILE_ID}"'",
          "rag_metadata": {
            "user_specified_metadata": { "key": "year", "value": { "int_value": 2024 } }
          }
        },
        {
          "parent": "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'/ragFiles/'"${RAG_FILE_ID}"'",
          "rag_metadata": {
            "user_specified_metadata": { "key": "month", "value": { "str_value": "May" } }
          }
        }
      ]
    }'

### List metadata for a file

The following REST sample shows how to list the metadata attached to a specific file.

### REST

Replace the following variables:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the RAG corpus.
  - **RAG\_FILE\_ID** : The ID of the RAG file.

<!-- end list -->

    PROJECT_ID=PROJECT_ID
    LOCATION=LOCATION
    RAG_CORPUS_ID=RAG_CORPUS_ID
    RAG_FILE_ID=RAG_FILE_ID
    curl -X GET \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora/${RAG_CORPUS_ID}/ragFiles/${RAG_FILE_ID}/ragMetadata

### Update metadata

You can update the metadata values attached to a file. The following REST sample shows how to update the metadata value associated with the `year` key. The `RAG_METADATA_KEY` is the string used when you created the metadata.

### REST

Replace the following variables:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the RAG corpus.
  - **RAG\_FILE\_ID** : The ID of the RAG file.
  - **RAG\_METADATA\_KEY** : The key name of the metadata to update.

<!-- end list -->

    PROJECT_ID=PROJECT_ID
    LOCATION=LOCATION
    RAG_CORPUS_ID=RAG_CORPUS_ID
    RAG_FILE_ID=RAG_FILE_ID
    RAG_METADATA_KEY=RAG_METADATA_KEY
    curl -X PATCH \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora/${RAG_CORPUS_ID}/ragFiles/${RAG_FILE_ID}/ragMetadata/${RAG_METADATA_KEY} \
    -d '{
      "user_specified_metadata": { "key": "'"${RAG_METADATA_KEY}"'", "value": { "int_value": 2025 } }
    }'

### Delete metadata from a file

The following REST sample shows how to batch delete metadata values from a file.

### REST

Replace the following variables:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the RAG corpus.
  - **RAG\_FILE\_ID** : The ID of the RAG file.
  - **RAG\_METADATA\_KEY\_1** : The key name of the first metadata value to delete.
  - **RAG\_METADATA\_KEY\_2** : The key name of the second metadata value to delete.

<!-- end list -->

    PROJECT_ID=PROJECT_ID
    LOCATION=LOCATION
    RAG_CORPUS_ID=RAG_CORPUS_ID
    RAG_FILE_ID=RAG_FILE_ID
    RAG_METADATA_KEY_1=RAG_METADATA_KEY_1
    RAG_METADATA_KEY_2=RAG_METADATA_KEY_2
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora/${RAG_CORPUS_ID}/ragFiles/${RAG_FILE_ID}/ragMetadata:batchDelete \
    -d '{
      "names": [
        "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'/ragFiles/'"${RAG_FILE_ID}"'/ragMetadata/'"${RAG_METADATA_KEY_1}"'",
        "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'/ragFiles/'"${RAG_FILE_ID}"'/ragMetadata/'"${RAG_METADATA_KEY_2}"'"
      ]
    }'

## Filter contexts with metadata

To improve the relevance of your results, use file metadata to narrow down the search space during context retrieval. Add a `metadata_filter` expression to your `RetrieveContexts` request using [CEL (Common Expression Language)](https://github.com/google/cel-spec) (for example, `year == 2024 && month == "May"` ). Only files with metadata that matches the filter expression are considered for retrieval.

The following REST sample shows how to retrieve contexts using a metadata filter.

### REST

Replace the following variables:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the RAG corpus.

<!-- end list -->

    PROJECT_ID=PROJECT_ID
    LOCATION=LOCATION
    RAG_CORPUS_ID=RAG_CORPUS_ID
    QUERY="except share amounts"
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}:retrieveContexts -d '{
        "vertex_rag_store": {
           "rag_resources": [
             {
               "rag_corpus": "projects/'"${PROJECT_ID}"'/locations/'"${LOCATION}"'/ragCorpora/'"${RAG_CORPUS_ID}"'"
             }
           ]
        },    
        "query": {
          "text": "'"${QUERY}"'", 
          "rag_retrieval_config": {
             "top_k": 10,
             "filter": {
                "vector_distance_threshold": 0.5,
                "metadata_filter": "year == 2024 && month == \"May\""
             }
          }
        }
    }'

## What's next

  - To learn more about uploading and managing files, see [Manage your RAG knowledge base](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/manage-your-rag-corpus) .
  - To learn more about standard vector search in RAG, see [Use Vector Search with RAG](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-vertexai-vector-search) .
