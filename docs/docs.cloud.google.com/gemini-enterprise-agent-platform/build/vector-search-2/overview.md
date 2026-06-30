---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/overview
title: Agent Retrieval (formerly Vector Search 2.0)
description: Learn about Agent Retrieval (formerly Vector Search 2.0)
data_source: docs.cloud.google.com
---

> To see an example of Vector Search 2.0, run the "Vector Search 2.0 Quickstart" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/embeddings/vector-search-2-intro.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fembeddings%2Fvector-search-2-intro.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fembeddings%2Fvector-search-2-intro.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/embeddings/vector-search-2-intro.ipynb)

> **Note:** Agent Retrieval supports VPC Service Controls. For more information about VPC Service Controls, see the [VPC Service Controls documentation](https://docs.cloud.google.com/vpc-service-controls/docs/overview) .

Agent Retrieval (formerly Vector Search 2.0) is a Google Cloud product designed from the ground up as a self-tuning, fully managed, AI-native search engine. While Google Cloud's existing Vector Search is a powerful approximate nearest neighbor (ANN) index-as-a-service system, Agent Retrieval evolves this concept into a comprehensive storage and retrieval system. Instead of managing indexes as the primary resource, you'll work with *Collections* of *Data Objects* .

The search engine architecture provides a replicated, scalable storage engine, making Agent Retrieval a single, unified data source for your AI applications and removing the need for auxiliary data storage.

Key benefits include:

  - **Developer Friendly:** Get started quickly with intuitive client libraries that require minimal code. The system is auto-tuned to maintain high performance, abstracting away the underlying infrastructure so you don't have to configure VMs or replicas.

  - **Fast Onboarding & Evaluation:** Create Collections, add your data, and start searching quickly.

  - **Unified Data Storage:** Store, retrieve, and filter your documents by vector similarity and payload data, all in one place.

  - **Powerful Features:** Automatically populate embedding fields using built-in models, explore your data with rich query capabilities, bring your own embeddings (BYOE), and quickly create indexes to scale performance.

  - **Simplified Pricing:** Adaptable pricing features two models: usage-based for smaller workloads and resource-based for tuned performance. For information on how to estimate costs for your use case, go to [Pricing estimate](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/overview#pricing) .

Agent Retrieval maintains the [high performance and massive scalability](https://cloud.google.com/blog/products/ai-machine-learning/build-fast-and-scalable-ai-applications-with-vertex-ai) available in Vector Search 1.0, making it seamless to get started and scale.

## Concepts

Before you begin, it's helpful to understand the following Agent Retrieval concepts:

  - [**Collection:**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections) A container for a set of related JSON objects. This is similar to a table in a relational database. You can create many Collections within a single database.

  - [**Data Object:**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects) An individual JSON object stored within a Collection.

  - [**Collection: schema:**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections#collection_schema) Defines the structure and constraints of the Data Objects within a Collection. It can be configured for both strict and relaxed schema validations.

  - **Collection Index:** Enables efficient approximate nearest neighbor (ANN) search across Data Objects within a Collection. A Collection can have multiple Indexes, such as one for each vector field in your Data Objects.

## Pricing estimate

[Agent Retrieval pricing and pricing calculator](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing?e=48754805#agent-retrieval) : Agent Retrieval pricing includes the cost of virtual machines used to host deployed indexes, as well as expenses for building and updating indexes. Even a minimal setup (under $100 per month) can accommodate high throughput for moderate-sized use cases. To estimate your monthly costs:

1.  Go to the [Agent Platform Agent Retrieval pricing calculator](https://cloud.google.com/products/calculator?e=48754805&dl=CjhDaVJtWkRGaU1UVXhOaTFoTm1aakxUUmpOREF0T0RBME1pMWhZamt4WmpGaU1HRTBOVGtRQVE9PRApGiRDOUY1MjA3My04MzZDLTRGRkYtOUMxMy04RjNFMjU5OUE4MEI) .
2.  Update the settings to:
      - Describe your [Collection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections#creating_a_collection)
      - Choose your search method: KNN or ANN
      - Deployment (only available for the ANN search method)
      - Monthly traffic
      - Data ingestion
3.  The cost estimate will update in the **Cost Details** pane.

## Supported regions

The following regions are supported:

  - `asia-east1`
  - `asia-northeast1`
  - `asia-southeast1`
  - `europe-north1`
  - `europe-west2`
  - `europe-west4`
  - `us-central1`
  - `us-east4`
  - `us-west1`

## What's next?

  - Try out the [interactive demo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/try-it) .
  - Learn how to [create a Collection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections#creating_a_collection) .
