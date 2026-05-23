---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-feature-store-with-rag
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-feature-store-with-rag
title: Use Vertex AI Feature Store in Gemini Enterprise Agent Platform RAG Engine
description: Learn how to use Vertex AI Feature Store as the vector database for Gemini Enterprise Agent Platform RAG Engine to handle large data volumes and improve performance.
data_source: docs.cloud.google.com
---

> The [VPC-SC security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) and CMEK are supported by Agent Platform RAG Engine. Data residency and AXT security controls aren't supported.

> **Preview**
> 
> Some of the RAG features are Preview offerings, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as-is" and may have limited support, and changes to Pre-GA products and features may not be compatible with other Pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) . By using the Gemini API on Gemini Enterprise Agent Platform, you agree to the Generative AI Preview [terms and conditions](https://cloud.google.com/trustedtester/aitos) (Preview Terms).

> To see an example of using RAG Engine with Feature Store, run the "Agent Platform RAG Engine with Agent Platform Feature Store" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/rag-engine/rag_engine_feature_store.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Frag-engine%2Frag_engine_feature_store.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Frag-engine%2Frag_engine_feature_store.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/rag-engine/rag_engine_feature_store.ipynb)

This page shows you how to set up [Vertex AI Feature Store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning//featurestore/latest/overview) as the vector database to use with RAG Engine.

You can also follow along using the [RAG Engine with Vertex AI Feature Store](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/rag-engine/rag_engine_feature_store.ipynb) notebook.

By integrating Vertex AI Feature Store as an additional vector database, RAG Engine can use Vertex AI Feature Store to handle large data volumes with low latency, which helps to improve the performance and scalability of your RAG applications.

## Set up a Vertex AI Feature Store

Vertex AI Feature Store, a managed cloud-native service, is an essential component of Gemini Enterprise Agent Platform. It simplifies machine learning (ML) feature management and online serving by letting you manage feature data within a BigQuery table or view. This enables low-latency online feature serving.

For `FeatureOnlineStore` instances created with optimized online serving, you can take advantage of a vector similarity search to retrieve a list of semantically similar or related entities, which are known as *approximate nearest neighbors* .

The following sections show you how to set up a Vertex AI Feature Store instance for your RAG application.

### Create a BigQuery table schema

Use Google Cloud console to create a BigQuery table schema. It must contain the following fields to serve as the data source.

| Field name          | Data type | Status   |
| ------------------- | --------- | -------- |
| `corpus_id`         | `String`  | Required |
| `file_id`           | `String`  | Required |
| `chunk_id`          | `String`  | Required |
| `chunk_data_type`   | `String`  | Nullable |
| `chunk_data`        | `String`  | Nullable |
| `file_original_uri` | `String`  | Nullable |
| `embeddings`        | `Float`   | Repeated |

This code sample demonstrates how to define your BigQuery table schema.

### SQL

``` 
  CREATE TABLE `PROJECT_ID.input_us_central1.rag_source_new` (
    `corpus_id` STRING NOT NULL,
    `file_id` STRING NOT NULL,
    `chunk_id` STRING NOT NULL,
    `chunk_data_type` STRING,
    `chunk_data` STRING,
    `embeddings` ARRAY<FLOAT64>,
    `file_original_uri` STRING
  );
```

### Provision a `FeatureOnlineStore` instance

To enable online serving of features, use the Vertex AI Feature Store `CreateFeatureOnlineStore` API to set up a `FeatureOnlineStore` instance. If you are provisioning a `FeatureOnlineStore` for the first time, the operation might take approximately five minutes to complete.

### REST

To create an online store instance, send a `POST` request by using the [`featureOnlineStores.create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the `FeatureOnlineStore` instance, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the new `FeatureOnlineStore` instance.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME

Request JSON body:

    {
      "optimized": {}
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureOnlineStoreOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-18T17:49:23.847496Z",
          "updateTime": "2023-09-18T17:49:23.847496Z"
        }
      }
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    
    def create_optimized_public_feature_online_store_sample(
        project: str,
        location: str,
        feature_online_store_id: str,
    ):
        aiplatform.init(project=project, location=location)
        fos = feature_store.FeatureOnlineStore.create_optimized_store(
            feature_online_store_id
        )
        return fos

  - `project` : Your project ID.
  - `location` : Region where you want to create the `FeatureOnlineStore` instance, such as `us-central1` .
  - `feature_online_store_id` : The name of the new `FeatureOnlineStore` instance.

### Create a `FeatureView` resource

To connect the BigQuery table, which stores the feature data source, to the `FeatureOnlineStore` instance, call the `CreateFeatureView` API to create a `FeatureView` resource. When you create a `FeatureView` resource, choose the default distance metric `DOT_PRODUCT_DISTANCE` , which is defined as the negative of the dot product (smaller `DOT_PRODUCT_DISTANCE` indicates higher similarity).

This code sample demonstrates how to create a `FeatureView` resource.

### REST

``` 
  # TODO(developer): Update and uncomment the following lines:
  # Set feature_view_id
  # Example: "feature_view_test"
  # FEATURE_VIEW_ID = "your-feature-view-id"
  #
  # The big_query_uri generated in the above BigQuery table schema creation step
  # The format should be "bq://" + BigQuery table ID
  # Example: "bq://tester.ragtest1.rag_testdata"
  # BIG_QUERY_URI=YOUR_BIG_QUERY_URI

  # Call CreateFeatureView API to create a FeatureView
  curl -X POST -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" \
  https://us-central1-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/us-central1/featureOnlineStores/${FEATURE_ONLINE_STORE_ID}/featureViews?feature_view_id=${FEATURE_VIEW_ID} \
    -d '{
          "vertex_rag_source": {
            "uri": '\""${BIG_QUERY_URI}"\"'
          }
      }'

  # Call ListFeatureViews API to verify the FeatureView is created successfully
  curl -X GET -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" -H "Content-Type: application/json" https://us-central1-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/us-central1/featureOnlineStores/${FEATURE_ONLINE_STORE_ID}/featureViews
```

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    
    def create_feature_view_from_rag_source(
        project: str,
        location: str,
        existing_feature_online_store_id: str,
        feature_view_id: str,
        bq_table_uri: str,
    ):
        aiplatform.init(project=project, location=location)
        fos = feature_store.FeatureOnlineStore(existing_feature_online_store_id)
        fv = fos.create_feature_view(
            name=feature_view_id,
            source=feature_store.utils.FeatureViewVertexRagSource(uri=bq_table_uri),
        )
        return fv

### Upload data and online serving

The RAG API handles data upload and online serving. To learn more about the Gemini Enterprise Agent Platform RAG Engine API, see the following:

  - [`GenerateContentResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse)

  - [`RagEngineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagEngineConfig)

  - [`RagChunk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagChunk)

  - [`RagContexts`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagContexts)

  - [`RagFileTransformationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagFileTransformationConfig)

  - [`RagQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagQuery)

## Use Vertex AI Feature Store in RAG Engine

After the Vertex AI Feature Store instance is set up, the following sections show you how to set it up as the vector database to use with the RAG application.

### Use the Vertex AI Feature Store instance as the vector database to create a RAG corpus

To create the RAG corpus, you must use `FEATURE_VIEW_RESOURCE_NAME` . The RAG corpus is created and automatically associated with the Vertex AI Feature Store instance. RAG APIs use the generated `rag_corpus_id` to handle the data upload to the Vertex AI Feature Store instance and to retrieve relevant contexts from the `rag_corpus_id` .

This code sample demonstrates how to use the Vertex AI Feature Store instance as the vector database to create a RAG corpus.

### REST

    # TODO(developer): Update and uncomment the following lines:
    # CORPUS_DISPLAY_NAME = "your-corpus-display-name"
    #
    # Full feature view resource name
    # Format: projects/${PROJECT_ID}/locations/us-central1/featureOnlineStores/${FEATURE_ONLINE_STORE_ID}/featureViews/${FEATURE_VIEW_ID}
    # FEATURE_VIEW_RESOURCE_NAME = "your-feature-view-resource-name"
    
    # Call CreateRagCorpus API to create a new RAG corpus
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
      https://us-central1-aiplatform.googleapis.com/v1beta1/projects/{PROJECT_ID}/locations/us-central1/ragCorpora -d '{
        "display_name" : '\""${CORPUS_DISPLAY_NAME}"\"',
        "rag_vector_db_config" : {
          "vertex_feature_store": {
            "feature_view_resource_name":'\""${FEATURE_VIEW_RESOURCE_NAME}"\"'
          }
        }
      }'
    
    # Call ListRagCorpora API to verify the RAG corpus is created successfully
    curl -sS -X GET \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    "https://us-central1-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/us-central1/ragCorpora"

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from vertexai.preview import rag
    import vertexai
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # feature_view_name = "projects/{PROJECT_ID}/locations/{LOCATION}/featureOnlineStores/{FEATURE_ONLINE_STORE_ID}/featureViews/{FEATURE_VIEW_ID}"
    # display_name = "test_corpus"
    # description = "Corpus Description"
    
    # Initialize Vertex AI API once per session
    vertexai.init(project=PROJECT_ID, location="us-central1")
    
    # Configure embedding model (Optional)
    embedding_model_config = rag.EmbeddingModelConfig(
        publisher_model="publishers/google/models/text-embedding-004"
    )
    
    # Configure Vector DB
    vector_db = rag.VertexFeatureStore(resource_name=feature_view_name)
    
    corpus = rag.create_corpus(
        display_name=display_name,
        description=description,
        embedding_model_config=embedding_model_config,
        vector_db=vector_db,
    )
    print(corpus)
    # Example response:
    # RagCorpus(name='projects/1234567890/locations/us-central1/ragCorpora/1234567890',
    # display_name='test_corpus', description='Corpus Description', embedding_model_config=...
    # ...

### Import files into the BigQuery table using the RAG API

Use the `ImportRagFiles` API to import files from Google Cloud Storage or Google Drive into the BigQuery table of the Vertex AI Feature Store instance. The files are embedded and stored in the BigQuery table.

This code sample demonstrates how to import files into the BigQuery table using the RAG API.

### REST

    # TODO(developer): Update and uncomment the following lines:
    # RAG_CORPUS_ID = "your-rag-corpus-id"
    #
    # Google Cloud Storage bucket/file location.
    # For example, "gs://rag-fos-test/"
    # GCS_URIS= "your-gcs-uris"
    
    # Call ImportRagFiles API to embed files and store in the BigQuery table
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://us-central1-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/us-central1/ragCorpora/${RAG_CORPUS_ID}/ragFiles:import \
    -d '{
      "import_rag_files_config": {
        "gcs_source": {
          "uris": '\""${GCS_URIS}"\"'
        },
        "rag_file_chunking_config": {
          "chunk_size": 512
        }
      }
    }'
    
    # Call ListRagFiles API to verify the files are imported successfully
    curl -X GET \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://us-central1-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/us-central1/ragCorpora/${RAG_CORPUS_ID}/ragFiles

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from vertexai import rag
    import vertexai
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # corpus_name = "projects/{PROJECT_ID}/locations/us-central1/ragCorpora/{rag_corpus_id}"
    # paths = ["https://drive.google.com/file/123", "gs://my_bucket/my_files_dir"]  # Supports Google Cloud Storage and Google Drive Links
    
    # Initialize Vertex AI API once per session
    vertexai.init(project=PROJECT_ID, location="us-central1")
    
    response = rag.import_files(
        corpus_name=corpus_name,
        paths=paths,
        transformation_config=rag.TransformationConfig(
            rag.ChunkingConfig(chunk_size=512, chunk_overlap=100)
        ),
        import_result_sink="gs://sample-existing-folder/sample_import_result_unique.ndjson",  # Optional, this has to be an existing storage bucket folder, and file name has to be unique (non-existent).
        max_embedding_requests_per_min=900,  # Optional
    )
    print(f"Imported {response.imported_rag_files_count} files.")
    # Example response:
    # Imported 2 files.

### Run a synchronization process to construct a `FeatureOnlineStore` index

After uploading your data into the BigQuery table, run a synchronization process to make your data available for online serving. You must generate a `FeatureOnlineStore` index using the `FeatureView` , and the synchronization process might take 20 minutes to complete.

This code sample demonstrates how to run a synchronization process to construct a `FeatureOnlineStore` index.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.
  - FEATUREVIEW\_NAME : The name of the feature view where you want to manually start the data sync.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:sync

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:sync"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:sync" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "featureViewSync": "projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/featureViewSyncs/OPERATION_ID"
    }

### Retrieve relevant contexts using the RAG API

After the synchronization process completes, you can retrieve relevant contexts from the `FeatureOnlineStore` index through the `RetrieveContexts` API.

### REST

    # TODO(developer): Update and uncomment the following lines:
    # RETRIEVAL_QUERY="your-retrieval-query"
    #
    # Full RAG corpus resource name
    # Format:
    # "projects/${PROJECT_ID}/locations/us-central1/ragCorpora/${RAG_CORPUS_ID}"
    # RAG_CORPUS_RESOURCE="your-rag-corpus-resource"
    
    # Call RetrieveContexts API to retrieve relevant contexts
    curl -X POST \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://us-central1-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/us-central1:retrieveContexts \
      -d '{
        "vertex_rag_store": {
          "rag_resources": {
              "rag_corpus": '\""${RAG_CORPUS_RESOURCE}"\"',
            },
        },
        "query": {
          "text": '\""${RETRIEVAL_QUERY}"\"',
          "similarity_top_k": 10
        }
      }'

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from vertexai import rag
    import vertexai
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # corpus_name = "projects/[PROJECT_ID]/locations/us-central1/ragCorpora/[rag_corpus_id]"
    
    # Initialize Vertex AI API once per session
    vertexai.init(project=PROJECT_ID, location="us-central1")
    
    response = rag.retrieval_query(
        rag_resources=[
            rag.RagResource(
                rag_corpus=corpus_name,
                # Optional: supply IDs from `rag.list_files()`.
                # rag_file_ids=["rag-file-1", "rag-file-2", ...],
            )
        ],
        text="Hello World!",
        rag_retrieval_config=rag.RagRetrievalConfig(
            top_k=10,
            filter=rag.utils.resources.Filter(vector_distance_threshold=0.5),
        ),
    )
    print(response)
    # Example response:
    # contexts {
    #   contexts {
    #     source_uri: "gs://your-bucket-name/file.txt"
    #     text: "....
    #   ....

### Generate content using Agent Platform Gemini API

Call the Agent Platform `GenerateContent` API to use Gemini models to generate content, and specify `RAG_CORPUS_RESOURCE` in the request to retrieve data from the `FeatureOnlineStore` index.

### REST

    # TODO(developer): Update and uncomment the following lines:
    # MODEL_ID=gemini-2.0-flash
    # GENERATE_CONTENT_PROMPT="your-generate-content-prompt"
    
    # GenerateContent with contexts retrieved from the FeatureStoreOnline index
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json"  https://us-central1-aiplatform.googleapis.com/v1beta1/projects/${PROJECT_ID}/locations/us-central1/publishers/google/models/${MODEL_ID}:generateContent \
    -d '{
      "contents": {
        "role": "user",
        "parts": {
          "text": '\""${GENERATE_CONTENT_PROMPT}"\"'
        }
      },
      "tools": {
        "retrieval": {
          "vertex_rag_store": {
            "rag_resources": {
                "rag_corpus": '\""${RAG_CORPUS_RESOURCE}"\"',
              },
            "similarity_top_k": 8,
          }
        }
      }
    }'

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from vertexai import rag
    from vertexai.generative_models import GenerativeModel, Tool
    import vertexai
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # corpus_name = "projects/{PROJECT_ID}/locations/us-central1/ragCorpora/{rag_corpus_id}"
    
    # Initialize Vertex AI API once per session
    vertexai.init(project=PROJECT_ID, location="us-central1")
    
    rag_retrieval_tool = Tool.from_retrieval(
        retrieval=rag.Retrieval(
            source=rag.VertexRagStore(
                rag_resources=[
                    rag.RagResource(
                        rag_corpus=corpus_name,
                        # Optional: supply IDs from `rag.list_files()`.
                        # rag_file_ids=["rag-file-1", "rag-file-2", ...],
                    )
                ],
                rag_retrieval_config=rag.RagRetrievalConfig(
                    top_k=10,
                    filter=rag.utils.resources.Filter(vector_distance_threshold=0.5),
                ),
            ),
        )
    )
    
    rag_model = GenerativeModel(
        model_name="gemini-2.0-flash-001", tools=[rag_retrieval_tool]
    )
    response = rag_model.generate_content("Why is the sky blue?")
    print(response.text)
    # Example response:
    #   The sky appears blue due to a phenomenon called Rayleigh scattering.
    #   Sunlight, which contains all colors of the rainbow, is scattered
    #   by the tiny particles in the Earth's atmosphere....
    #   ...

## What's next

  - [Use a Weaviate database with Gemini Enterprise Agent Platform RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-weaviate-db)
