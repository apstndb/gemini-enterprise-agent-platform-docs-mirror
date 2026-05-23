---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/overview
title: Vector Search 2.0
description: Learn about Vector Search 2.0
data_source: docs.cloud.google.com
---

> To see an example of Vector Search 2.0, run the "Vector Search 2.0 Quickstart" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/embeddings/vector-search-2-intro.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fembeddings%2Fvector-search-2-intro.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fembeddings%2Fvector-search-2-intro.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/embeddings/vector-search-2-intro.ipynb)

> **Note:** Vector Search 2.0 supports VPC Service Controls. For more information about VPC Service Controls, see the [VPC Service Controls documentation](https://docs.cloud.google.com/vpc-service-controls/docs/overview) .

Vector Search 2.0 is a Google Cloud product designed from the ground up as a self-tuning, fully managed, AI-native search engine. While Google Cloud's existing Vector Search is a powerful approximate nearest neighbor (ANN) index-as-a-service system, Vector Search 2.0 evolves this concept into a comprehensive storage and retrieval system. Instead of managing indexes as the primary resource, you'll work with *Collections* of *Data Objects* .

The search engine architecture provides a replicated, scalable storage engine, making Vector Search 2.0 a single, unified data source for your AI applications and removing the need for auxiliary data storage.

Key benefits include:

  - **Developer Friendly:** Get started quickly with intuitive client libraries that require minimal code. The system is auto-tuned to maintain high performance, abstracting away the underlying infrastructure so you don't have to configure VMs or replicas.

  - **Fast Onboarding & Evaluation:** Create Collections, add your data, and start searching quickly.

  - **Unified Data Storage:** Store, retrieve, and filter your documents by vector similarity and payload data, all in one place.

  - **Powerful Features:** Automatically populate embedding fields using built-in models, explore your data with rich query capabilities, bring your own embeddings (BYOE), and quickly create indexes to scale performance.

  - **Simplified Pricing:** Adaptable pricing features two models: usage-based for smaller workloads and resource-based for tuned performance.

Vector Search 2.0 maintains the [high performance and massive scalability](https://cloud.google.com/blog/products/ai-machine-learning/build-fast-and-scalable-ai-applications-with-vertex-ai) available in Vector Search 1.0, making it seamless to get started and scale.

## Concepts

Before you begin, it's helpful to understand the following Vector Search 2.0 concepts:

  - [**Collection:**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections) A container for a set of related JSON objects. This is similar to a table in a relational database. You can create many Collections within a single database.

  - [**Data Object:**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects) An individual JSON object stored within a Collection.

  - [**Collection: schema:**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections#collection_schema) Defines the structure and constraints of the Data Objects within a Collection. It can be configured for both strict and relaxed schema validations.

  - **Collection Index:** Enables efficient approximate nearest neighbor (ANN) search across Data Objects within a Collection. A Collection can have multiple Indexes, such as one for each vector field in your Data Objects.

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
