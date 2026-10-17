---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-rag-managed-vertex-ai-vector-search
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-rag-managed-vertex-ai-vector-search
title: Use Vector Search 2.0 with RAG
description: Use Rag Managed Gemini Enterprise Agent Platform Vector Search as vector database.
data_source: docs.cloud.google.com
---

> **Preview**
>
> Some of the RAG features are Preview offerings, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as-is" and may have limited support, and changes to Pre-GA products and features may not be compatible with other Pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) . By using the Gemini API on Gemini Enterprise Agent Platform, you agree to the Generative AI Preview [terms and conditions](https://cloud.google.com/trustedtester/aitos) (Preview Terms).

> The [VPC-SC security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) and CMEK are supported by Agent Platform RAG Engine. Data residency and AXT security controls aren't supported.

> RAG Engine corpora that are backed by Vector Search 2.0 are available only in `us-central1` .

This page shows you how RAG Engine on Gemini Enterprise Agent Platform uses [Gemini Enterprise Agent Platform Vector Search 2.0](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/overview) , which is a Google Cloud product that serves as a comprehensive storage and retrieval system to store and manage vector representations of your documents. The Gemini Enterprise Agent Platform Vector Search 2.0 is then used to retrieve relevant documents based on the document's semantic similarity to a given query.

RAG will manage the Vector Search 2.0 collections for you and you will have full access to the Vector Search 2.0 collections in your project.

## Choosing a RAG backend

When using RAG Engine on Gemini Enterprise Agent Platform, you can choose between different backend storage options for your RAG corpora. The following table summarizes the key differences:

| Backend Option                 | Underlying Technology                              | Management by RAG Engine                                                         | Data Visibility in Project           | CMEK Support |
|--------------------------------|----------------------------------------------------|----------------------------------------------------------------------------------|--------------------------------------|--------------|
| `RagManagedVertexVectorSearch` | Gemini Enterprise Agent Platform Vector Search 2.0 | Fully managed by Google.                                                         | Visible in your Google Cloud project | No           |
| `VertexVectorSearch`           | Gemini Enterprise Agent Platform Vector Search 1.0 | User is expected to set up, manage, and clean up the Vector Search 1.0 instance. | Visible in your Google Cloud project | No           |
| `RagManagedDb`                 | Spanner                                            | Fully managed by Google.                                                         | Not directly visible in your project | Yes          |

Choose `RagManagedVertexVectorSearch` for the latest features, automated management, and transparency into your Vector Search 2.0 data. If CMEK support is a strict requirement, consider `RagManagedDb` , keeping in mind the lack of direct visibility into the backend database.

## Enable Vector Search API

To use RAG Managed Gemini Enterprise Agent Platform Vector Search, you need to first enable the [Vector Search API](https://console.developers.google.com/apis/api/vectorsearch.googleapis.com/) .

### Create a RAG corpus with `RagManagedVertexVectorSearch`

This code samples demonstrates how to create a RAG corpus using `RagManagedVertexVectorSearch` .

### Python

```
from vertexai.preview import rag
import vertexai

PROJECT_ID = YOUR_PROJECT_ID
LOCATION = YOUR_RAG_ENGINE_LOCATION
DISPLAY_NAME = YOUR_RAG_CORPUS_DISPLAY_NAME

# Initialize Agent Platform API once per session
vertexai.init(project=PROJECT_ID, location=LOCATION)

vector_db = rag.RagManagedVertexVectorSearch()
rag_corpus = rag.create_corpus(
    display_name=DISPLAY_NAME, backend_config=rag.RagVectorDbConfig(vector_db=vector_db))
```

### REST

Replace the following variables:

- **` PROJECT_ID `** : Your project ID.
- **` LOCATION `** : The region to process the request.
- **` CORPUS_DISPLAY_NAME `** : The display name of the RAG corpus.

```
PROJECT_ID=PROJECT_ID
LOCATION=LOCATION
CORPUS_DISPLAY_NAME=CORPUS_DISPLAY_NAME

curl -X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora \
-d '{
      "display_name" : '\""${CORPUS_DISPLAY_NAME}"\"',
      "vector_db_config": {
        "rag_managed_vertex_vector_search": {}
      }
    }'
```

### Importing your data into `RagManagedVertexVectorSearch`

You can use either the `ImportRagFiles` API or the `UploadRagFile` API to import your data into the `RagManagedVertexVectorSearch` .

To upload your local file into your RAG corpus, see [Upload a RAG file](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/media/upload) . To import data into your RAG corpus, see the following code sample that demonstrates how to import from Cloud Storage. To learn about the supported data sources, see [Data sources supported for RAG](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-data-ingestion#supported-data-sources) .

### Python

```
from vertexai.preview import rag
import vertexai

PROJECT_ID = YOUR_PROJECT_ID
LOCATION = YOUR_RAG_ENGINE_LOCATION
CORPUS_ID = YOUR_CORPUS_ID
PATHS = ["gs://my_bucket/my_files_dir"]

# Initialize Agent Platform API once per session
vertexai.init(project=PROJECT_ID, location=LOCATION)

corpus_name = f"projects/{PROJECT_ID}/locations/{LOCATION}/ragCorpora/{CORPUS_ID}"
# This is a non blocking call.
response = await rag.import_files_async(
    corpus_name=corpus_name,
    paths=PATHS,
)

# Wait for the import to complete.
await response.result()
```

### REST

```
GCS_URI=GCS_URI

curl -X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora/${CORPUS_ID}/ragFiles:import \
-d '{
  "import_rag_files_config": {
    "gcs_source": {
      "uris": '\""${GCS_URI}"\"',
      },
  }
}'
```

## Create an Index for your corpus

RAG Engine creates a Vector Search 2.0 Collection for each corpus, but it doesn't create an [Index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes) on that Collection. Until you create one, every retrieval is a brute-force KNN scan.

A brute-force scan is slower than an indexed search, and [KNN runs only on Collections of up to 100,000 Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query) . RAG Engine stores one chunk per Data Object, so once a corpus passes that limit, retrieval fails until an Index exists.

Don't index every corpus. An Index runs on its own serving infrastructure and is billed for as long as it exists, whether or not it is queried. To decide which corpora need one, see [Decide which corpora to index](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-rag-managed-vertex-ai-vector-search#when-to-index) .

Once an Index exists, retrieval uses it automatically. The corpus doesn't change and your data doesn't need to be imported again.

If you are indexing several corpora, script the loop: there is no bulk creation path. Concurrent index operations are quota-limited, so create the Indexes serially or in small batches. For more information, see [Quotas](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/quotas) .

### Before you begin

Creating an Index requires the `vectorsearch.indexes.create` permission on the Collection, and counting its Data Objects requires `vectorsearch.dataObjects.query` . Both permissions are included in the Vector Search Admin ( `roles/vectorsearch.admin` ) role; Vector Search Index Writer ( `roles/vectorsearch.indexWriter` ) grants the first. The [Vector Search API](https://console.developers.google.com/apis/api/vectorsearch.googleapis.com/) must also be enabled on the project.

### Find your corpus IDs

In your project, each corpus has exactly one Collection, named `vertex-rag- `` RAG_CORPUS_ID` . List your corpora to get their IDs.

Replace **` PROJECT_ID `** with your project ID:

```
PROJECT_ID=PROJECT_ID
LOCATION=us-central1

curl -X GET \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
"https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora?pageSize=100"
```

The numeric portion at the end of each corpus `name` is the ` RAG_CORPUS_ID ` . Each corpus also reports the full Collection resource name in `vectorDbConfig.ragManagedVertexVectorSearch.collectionName` .

The response lists at most 100 corpora, and at most 25 if you omit `pageSize` . If the response includes a `nextPageToken` , pass that value as `pageToken` to fetch the next page.

If you already know the ` RAG_CORPUS_ID ` you want to index, fetch that one corpus instead. The response carries the same `collectionName` :

```
curl -X GET \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
"https://${LOCATION}-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/${LOCATION}/ragCorpora/RAG_CORPUS_ID"
```

### Decide which corpora to index

For each corpus, count the Data Objects in its Collection. Pass an empty `filter` to count the whole Collection:

```
COLLECTION_ID=vertex-rag-RAG_CORPUS_ID

curl -X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
"https://vectorsearch.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/collections/${COLLECTION_ID}/dataObjects:aggregate" \
-d '{"aggregate": "COUNT", "filter": {}}'
```

The count comes back in `aggregateResults` :

```
{
  "aggregateResults": [
    {
      "count": 95217
    }
  ]
}
```

Create an Index for that corpus when either of the following is true:

- **The count is near or above 100,000.** The limit counts Data Objects, not files, so a corpus holding a small number of large files can still be well over it.
- **Retrieval is too slow at your query rate.** An indexed search is faster than a brute-force scan, and the gap widens as the Collection grows.

Otherwise leave the corpus unindexed and avoid the serving cost. You can add an Index later if it grows.

> **Note:** `dataObjects:aggregate` only supports `COUNT` , and the call is billed as a scan of the Collection.

### Review the Collection schema

RAG Engine creates each Collection with the following schema. Use these names when you specify the index field and filter fields.

| Field               | Kind         | Description                                                                                                    |
|---------------------|--------------|----------------------------------------------------------------------------------------------------------------|
| `text_embedding`    | Dense vector | The chunk embedding. This is the field you index. The number of dimensions matches the corpus embedding model. |
| `corpus_id`         | String       | The ID of the RAG corpus.                                                                                      |
| `file_id`           | String       | The ID of the RAG file the chunk came from.                                                                    |
| `chunk_id`          | String       | The ID of the chunk.                                                                                           |
| `chunk_data`        | String       | The chunk text.                                                                                                |
| `chunk_data_type`   | String       | The type of the chunk data.                                                                                    |
| `file_original_uri` | String       | The original URI of the source file.                                                                           |
| `rag_metadata`      | String       | User-supplied metadata for the chunk.                                                                          |

> **Note:** The Collection has no sparse vector field, so hybrid search isn't available on RAG Engine corpora.

### Choose the Index settings

> **Important:** The `index_field` , `distance_metric` , `filter_fields` , `store_fields` , and infrastructure mode settings are permanent.

`UpdateIndex` changes only the display name, description, labels, and replica counts, so to change any of the settings in this section, you must delete the Index and create a new one.

**Index field:** Set it to `text_embedding` , the only vector field in the Collection schema.

**Distance metric:** Set it to cosine. RAG Engine always sends `COSINE_DISTANCE` on its retrieval requests, and Vector Search 2.0 rejects a retrieval request whose metric doesn't match the Index. The metric defaults to `DOT_PRODUCT` when you omit it, so an Index created without it breaks retrieval for that corpus. RAG Engine reports the failure as `FAILED_PRECONDITION` with the message `Failed to process Rag Managed Vertex Vector Search response.` , which doesn't identify the metric as the cause. The spelling differs by surface: the REST body takes `COSINE_DISTANCE` , and the gcloud CLI flag takes `cosine-distance` .

**Infrastructure:** Leave the Index on the default performance-optimized infrastructure, because cosine distance isn't supported on storage-optimized infrastructure. An Index runs on dedicated serving infrastructure and is billed for as long as it exists. On `v1` , `min_replica_count` and `max_replica_count` both default to `2` , so by default the Index is served by two replicas and doesn't autoscale. For more information, see [Collection Indexes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes) .

**Filter fields:** Set `filter_fields` to `file_id` only. It is the only field RAG Engine filters on at retrieval time, and it does so only when a retrieval request restricts the search to specific files. In particular, `corpus_id` holds the same value for every Data Object in a given Collection, so filtering on it provides no benefit.

Metadata filtering also needs no additional filter fields. When a retrieval request sets `ragRetrievalConfig.filter.metadataFilter` , RAG Engine resolves the filter against your file metadata first, converts the result into the set of matching RAG file IDs, and sends that set to Vector Search as the same `file_id` filter. Adding `rag_metadata` to `filter_fields` increases the Index size without changing retrieval.

**Store fields:** Leave `store_fields` unset. RAG Engine requests all data fields on every retrieval, which never qualifies for inline serving, so the chunk data is read from the backing database regardless. Fields listed in `store_fields` are pushed into the Index and count toward its size, so setting them adds cost without changing retrieval.

### Create the Index

### Python

Replace the following variables:

- **` PROJECT_ID `** : Your project ID.
- **` RAG_CORPUS_ID `** : The ID of the RAG corpus to index.

```
from google.cloud import vectorsearch_v1

client = vectorsearch_v1.VectorSearchServiceClient()

index = vectorsearch_v1.Index(
    index_field="text_embedding",
    distance_metric=vectorsearch_v1.DistanceMetric.COSINE_DISTANCE,
    filter_fields=["file_id"],
)
request = vectorsearch_v1.CreateIndexRequest(
    parent="projects/PROJECT_ID/locations/us-central1/collections/vertex-rag-RAG_CORPUS_ID",
    index_id="vertex-rag-RAG_CORPUS_ID-index",
    index=index,
)

operation = client.create_index(request=request)

# Wait for the result (note this may take up to several minutes).
operation.result()
```

### REST

Replace the following variables:

- **` PROJECT_ID `** : Your project ID.
- **` RAG_CORPUS_ID `** : The ID of the RAG corpus to index.

```
PROJECT_ID=PROJECT_ID
RAG_CORPUS_ID=RAG_CORPUS_ID
LOCATION=us-central1
COLLECTION_ID=vertex-rag-${RAG_CORPUS_ID}
INDEX_ID=${COLLECTION_ID}-index

curl -X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
"https://vectorsearch.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/collections/${COLLECTION_ID}/indexes?indexId=${INDEX_ID}" \
-d '{
      "index_field": "text_embedding",
      "distance_metric": "COSINE_DISTANCE",
      "filter_fields": ["file_id"]
    }'
```

### gcloud

Replace the following variables:

- **` PROJECT_ID `** : Your project ID.
- **` RAG_CORPUS_ID `** : The ID of the RAG corpus to index.

```
gcloud vector-search collections indexes create vertex-rag-RAG_CORPUS_ID-index \
  --collection=vertex-rag-RAG_CORPUS_ID \
  --index-field=text_embedding \
  --distance-metric=cosine-distance \
  --filter-fields=file_id \
  --location=us-central1 \
  --project=PROJECT_ID
```

The command blocks until the operation finishes unless you pass `--async` .

### Poll for completion

Creating an Index returns a long-running operation:

```
{
  "name": "projects/PROJECT_ID/locations/us-central1/operations/operation-1770302393524-64a14a54fa197-0dea326c-5a90efda",
  "metadata": {
    "@type": "type.googleapis.com/google.cloud.vectorsearch.v1.OperationMetadata",
    "createTime": "2026-02-05T14:39:53.558308609Z",
    "target": "projects/PROJECT_ID/locations/us-central1/collections/vertex-rag-RAG_CORPUS_ID/indexes/vertex-rag-RAG_CORPUS_ID-index",
    "verb": "create",
    "apiVersion": "v1"
  },
  "done": false
}
```

Poll the operation using the name from that response:

```
OPERATION_NAME=OPERATION_NAME

curl -X GET \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
"https://vectorsearch.googleapis.com/v1/${OPERATION_NAME}"
```

When `done` is `true` , a `response` field means the Index built successfully, and an `error` field gives the reason it failed. Building an Index takes several minutes, and longer for a large corpus.

To list the operations in the project and location, run the following:

```
curl -X GET \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
"https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/us-central1/operations"
```

To inspect an existing Index, run the following:

```
gcloud vector-search collections indexes describe vertex-rag-RAG_CORPUS_ID-index \
  --collection=vertex-rag-RAG_CORPUS_ID \
  --location=us-central1 \
  --project=PROJECT_ID
```

To delete an Index, which you must do to change any of its permanent settings, run the following. Retrieval falls back to a brute-force KNN scan until the replacement Index is built, and fails entirely if the corpus exceeds 100,000 chunks.

```
gcloud vector-search collections indexes delete vertex-rag-RAG_CORPUS_ID-index \
  --collection=vertex-rag-RAG_CORPUS_ID \
  --location=us-central1 \
  --project=PROJECT_ID
```

## What's next

- To import files and folders from Google Drive or Cloud Storage, see [Import RAG files example](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles/import) .

- To list RAG files, see [List RAG files example](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles/list) .

- To use a reranker for retrieval, see [Reranking for Gemini Enterprise Agent Platform RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/retrieval-and-ranking)

- To tune Index infrastructure, distance metrics, and ScaNN parameters, see [Collection Indexes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes) .
