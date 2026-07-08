---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-quickstart
title: RAG quickstart
description: Run Retrieval Augmented Generation (RAG) tasks on Gemini Enterprise Agent Platform. Configure IAM, install Vertex AI SDK, and run RAG Engine on Gemini Enterprise Agent Platform code.
data_source: docs.cloud.google.com
---

> The [VPC-SC security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) and CMEK are supported by Agent Platform RAG Engine. Data residency and AXT security controls aren't supported.

> To see an example of using RAG Engine, run the "Intro to RAG Engine in Agent Platform" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/rag-engine/intro_rag_engine.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Frag-engine%2Fintro_rag_engine.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Frag-engine%2Fintro_rag_engine.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/rag-engine/intro_rag_engine.ipynb)

> **Important:** By default, a RAG corpus uses `RagManagedDb` . For more information, see [Understanding RagManagedDb](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/understanding-ragmanageddb) .

This page shows you how to use the Vertex AI SDK to run RAG Engine on Gemini Enterprise Agent Platform tasks.

You can also follow along using this notebook [Intro to RAG Engine](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/rag-engine/intro_rag_engine.ipynb) .

## Required roles

Grant roles to your user account. Run the following command once for each of the following IAM roles: `roles/aiplatform.user`

    gcloud projects add-iam-policy-binding PROJECT_ID --member="user:USER_IDENTIFIER" --role=ROLE

Replace the following:

  - `  PROJECT_ID  ` : Your project ID.
  - `  USER_IDENTIFIER  ` : The identifier for your user account. For example, `myemail@example.com` .
  - `  ROLE  ` : The IAM role that you grant to your user account.

## Prepare your Google Cloud console

To use RAG Engine, do the following:

1.  [Install the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk) .

2.  Run this command in the Google Cloud console to set up your project.
    
    `gcloud config set project {project}`

3.  Run this command to authorize your login.
    
    `gcloud auth application-default login`

## Run RAG Engine

Copy and paste this sample code into the Google Cloud console to run RAG Engine.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import agentplatform
    
    from agentplatform import types
    from google import genai
    from google.genai import types as genai_types
    
    
    # Create a RAG Corpus, Import Files, and Generate a response
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # MODEL_ID = "gemini-3.5-flash"
    # display_name = "test_corpus"
    # gcs_path = "gs://my_bucket/my_files_dir/*"
    # google_drive_path ="https://drive.google.com/file/d/123"
    
    # Initialize Agent Platform client once per session
    client = agentplatform.Client(project=PROJECT_ID, location="us-east4")
    
    # Configure embedding model, for example "text-embedding-005".
    embedding_model_config = types.RagEmbeddingModelConfig(
        vertex_prediction_endpoint=types.RagEmbeddingModelConfigVertexPredictionEndpoint(
            endpoint="publishers/google/models/text-embedding-005"
        ),
    )
    
    # Create RagCorpus
    rag_corpus = client.rag.create_corpus(
        rag_corpus=types.RagCorpus(
            display_name=display_name,
            rag_vector_db_config=types.RagVectorDbConfig(
                rag_embedding_model_config=embedding_model_config
            )
        )
    )
    
    # Import Files to the RagCorpus
    client.rag.import_files(
        name=rag_corpus.name,
        import_config=types.ImportRagFilesConfig(
            gcs_source=genai_types.GcsSource(uris=[gcs_path]),
            rag_file_transformation_config=types.RagFileTransformationConfig(
                rag_file_chunking_config=types.RagFileChunkingConfig(
                    chunk_size=512,
                    chunk_overlap=100,
                )
            ), # optional
            max_embedding_requests_per_min=1000, # optional
        )
    )
    
    # Direct context retrieval
    rag_retrieval_config = genai_types.RagRetrievalConfig(
        top_k=3,  # Optional
        filter=genai_types.RagRetrievalConfigFilter(
            vector_distance_threshold=0.5
        ),  # Optional
    )
    response = client.rag.retrieve_contexts(
        vertex_rag_store=genai_types.VertexRagStore(
            rag_resources=[
                genai_types.VertexRagStoreRagResource(
                    rag_corpus=rag_corpus.name,
                )
            ],
        ),
        query=types.RagQuery(
            text="What is RAG and why it is helpful?",
            rag_retrieval_config=rag_retrieval_config,   
        )
    )
    print(response)
    
    # Enhance generation
    # Create a RAG retrieval tool
    rag_retrieval_tool = genai_types.Tool(
        retrieval=genai_types.Retrieval(
            vertex_rag_store=genai_types.VertexRagStore(
                rag_resources=[
                    genai_types.VertexRagStoreRagResource(
                        rag_corpus=rag_corpus.name,
                        # Optional: supply IDs from `rag.list_files()`.
                        # rag_file_ids=["rag-file-1", "rag-file-2", ...],
                    )
                ],
                rag_retrieval_config=rag_retrieval_config,
            ),
        )
    )
    
    # Call generate_content with the tool using the GenAI SDK
    
    # Create a GenAI SDK client
    genai_client = genai.Client(enterprise=True, project=PROJECT_ID, location="us-east4")
    
    
    response = genai_client.models.generate_content(
        model=MODEL_ID,
        contents="What is RAG and why it is helpful?",
        config=genai_types.GenerateContentConfig(
            tools=[rag_retrieval_tool]
        )
    )
    print(response.text)
    # Example response:
    #   RAG stands for Retrieval-Augmented Generation.
    #   It's a technique used in AI to enhance the quality of responses
    # ...

### curl

1.  Create a RAG corpus.
    
    ``` 
      export LOCATION=LOCATION
      export PROJECT_ID=PROJECT_ID
      export CORPUS_DISPLAY_NAME=CORPUS_DISPLAY_NAME
    
      // CreateRagCorpus
      // Output: CreateRagCorpusOperationMetadata
      curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora \
      -d '{
            "display_name" : "'"CORPUS_DISPLAY_NAME"'"
        }'
    ```
    
    For more information, see [Create a RAG corpus example](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/create) .

2.  Import a RAG file.
    
    ``` 
      // ImportRagFiles
      // Import a single Cloud Storage file or all files in a Cloud Storage bucket.
      // Input: LOCATION, PROJECT_ID, RAG_CORPUS_ID, GCS_URIS
      export RAG_CORPUS_ID=RAG_CORPUS_ID
      export GCS_URIS=GCS_URIS
      export CHUNK_SIZE=CHUNK_SIZE
      export CHUNK_OVERLAP=CHUNK_OVERLAP
      export EMBEDDING_MODEL_QPM_RATE=EMBEDDING_MODEL_QPM_RATE
    
      // Output: ImportRagFilesOperationMetadataNumber
      // Use ListRagFiles, or import_result_sink to get the correct rag_file_id.
      curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import \
      -d '{
        "import_rag_files_config": {
          "gcs_source": {
            "uris": "GCS_URIS"
          },
          "rag_file_chunking_config": {
            "chunk_size": CHUNK_SIZE,
            "chunk_overlap": CHUNK_OVERLAP
          },
          "max_embedding_requests_per_min": EMBEDDING_MODEL_QPM_RATE
        }
      }'
    ```
    
    For more information, see [Import RAG files example](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles/import) .

3.  Run a RAG retrieval query.
    
    ``` 
      export RAG_CORPUS_RESOURCE=RAG_CORPUS_RESOURCE
      export VECTOR_DISTANCE_THRESHOLD=VECTOR_DISTANCE_THRESHOLD
      export SIMILARITY_TOP_K=SIMILARITY_TOP_K
    
      {
      "vertex_rag_store": {
          "rag_resources": {
            "rag_corpus": "RAG_CORPUS_RESOURCE"
          },
          "vector_distance_threshold": VECTOR_DISTANCE_THRESHOLD
        },
        "query": {
        "text": TEXT
        "similarity_top_k": SIMILARITY_TOP_K
        }
      }
    
      curl -X POST \
          -H "Authorization: Bearer $(gcloud auth print-access-token)" \
          -H "Content-Type: application/json; charset=utf-8" \
          -d @request.json \
          "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION:retrieveContexts"
    ```
    
    For more information, see [RAG Engine API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/retrieveContexts) .

4.  Generate content.
    
        {
        "contents": {
          "role": "USER",
          "parts": {
            "text": "INPUT_PROMPT"
          }
        },
        "tools": {
          "retrieval": {
          "disable_attribution": false,
          "vertex_rag_store": {
            "rag_resources": {
              "rag_corpus": "RAG_CORPUS_RESOURCE"
            },
            "similarity_top_k": "SIMILARITY_TOP_K",
            "vector_distance_threshold": VECTOR_DISTANCE_THRESHOLD
          }
          }
        }
        }
        
        curl -X POST \
            -H "Authorization: Bearer $(gcloud auth print-access-token)" \
            -H "Content-Type: application/json; charset=utf-8" \
            -d @request.json \
            "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATION_METHOD"
    
    For more information, see [RAG Engine API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/retrieveContexts) .

## What's next

  - To learn more about the RAG API, see [RAG Engine API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora) .

  - To learn more about the responses from RAG, see [Retrieval and Generation Output of RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-output-explained) .

  - To learn about the RAG Engine, see the [RAG Engine overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview) .
