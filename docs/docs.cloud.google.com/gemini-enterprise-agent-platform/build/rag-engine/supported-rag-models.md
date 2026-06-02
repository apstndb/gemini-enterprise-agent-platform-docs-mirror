---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/supported-rag-models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/supported-rag-models
title: RAG Engine on Gemini Enterprise Agent Platform supported models
description: Understand RAG Engine on Gemini Enterprise Agent Platform support for Gemini, self-deployed, and managed API models, including code samples.
data_source: docs.cloud.google.com
---

> The [VPC-SC security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) and CMEK are supported by Agent Platform RAG Engine. Data residency and AXT security controls aren't supported.

This page lists Gemini models, self-deployed models, and models with managed APIs on Agent Platform that support RAG Engine on Gemini Enterprise Agent Platform.

## Gemini models

The following models support RAG Engine:

#### Click to expand supported models

  - [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
  - [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)
  - [Gemini 3.1 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro) preview
  - [Gemini 3 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-flash) preview
  - [Gemini 2.5 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro)
  - [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash) preview
  - [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite) preview
  - [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash)
  - [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite)

Fine-tuned Gemini models are unsupported when the Gemini models use RAG Engine on Gemini Enterprise Agent Platform.

## Self-deployed models

RAG Engine on Gemini Enterprise Agent Platform supports all models in [Model Garden](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/explore-models) .

Use RAG Engine with your self-deployed open model endpoints.

Replace the variables used in the code sample:

  - **PROJECT\_ID** : Your project ID.

  - **LOCATION** : The region to process your request.

  - **ENDPOINT\_ID** : Your endpoint ID.
    
    ``` 
      # Create a model instance with your self-deployed open model endpoint
      rag_model = GenerativeModel(
          "projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID",
          tools=[rag_retrieval_tool]
      )
    ```

## Models with managed APIs on Agent Platform

The models with managed APIs on Agent Platform that support RAG Engine include the following:

  - [Mistral on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral)
  - [Llama 3.1 and 3.2](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama)

The following code sample demonstrates how to use the Gemini `GenerateContent` API to create a generative model instance. The model ID, `/publisher/meta/models/llama-3.1-405B-instruct-maas` , is found in the [model card](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/explore-models) .

Replace the variables used in the code sample:

  - **PROJECT\_ID** : Your project ID.

  - **LOCATION** : The region to process your request.

  - **RAG\_RETRIEVAL\_TOOL** : Your RAG retrieval tool.
    
    ``` 
      # Create a model instance with Llama 3.1 MaaS endpoint
      rag_model = GenerativeModel(
          "projects/PROJECT_ID/locations/LOCATION/publisher/meta/models/llama-3.1-405B-instruct-maas",
          tools=RAG_RETRIEVAL_TOOL
      )
    ```

The following code sample demonstrates how to use the OpenAI compatible `ChatCompletions` API to generate a model response.

Replace the variables used in the code sample:

  - **PROJECT\_ID** : Your project ID.

  - **LOCATION** : The region to process your request.

  - **MODEL\_ID** : LLM model for content generation. For example, `meta/llama-3.1-405b-instruct-maas` .

  - **INPUT\_PROMPT** : The text sent to the LLM for content generation. Use a prompt relevant to the documents in Agent Search.

  - **RAG\_CORPUS\_ID** : The ID of the RAG corpus resource.

  - **ROLE** : Your role.

  - **USER** : Your username.

  - **CONTENT** : Your content.
    
    ``` 
      # Generate a response with Llama 3.1 MaaS endpoint
      response = client.chat.completions.create(
          model="MODEL_ID",
          messages=[{"ROLE": "USER", "content": "CONTENT"}],
          extra_body={
              "extra_body": {
                  "google": {
                      "vertex_rag_store": {
                          "rag_resources": {
                              "rag_corpus": "RAG_CORPUS_ID"
                          },
                          "similarity_top_k": 10
                      }
                  }
              }
          },
      )
    ```

## What's next

  - [Use Embedding models with RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-embedding-models) .
