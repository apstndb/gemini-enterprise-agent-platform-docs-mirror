---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/spanner-mode
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/spanner-mode
title: Managing Spanner mode
description: Manage your Spanner mode deployment in RAG Engine.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> Some of the RAG features are Preview offerings, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as-is" and may have limited support, and changes to Pre-GA products and features may not be compatible with other Pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) . By using the Gemini API on Gemini Enterprise Agent Platform, you agree to the Generative AI Preview [terms and conditions](https://cloud.google.com/trustedtester/aitos) (Preview Terms).

> The [VPC-SC security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) and CMEK are supported by Agent Platform RAG Engine. Data residency and AXT security controls aren't supported.

In Spanner deployment mode, RAG Engine uses `RagManagedDb` , which is an enterprise-ready, fully managed Google Cloud Spanner instance that's used for resource storage by RAG Engine on Gemini Enterprise Agent Platform. Optionally use it as the vector database of choice for your RAG corpora.

Through Spanner, RAG Engine offers a consistent, highly available, and highly scalable, dedicated database to support your application. To learn more about Google Cloud Spanner, see [Spanner](https://cloud.google.com/spanner) .

## Data storage and vector search

RAG Engine stores your RAG corpus and RAG file resource metadata in `RagManagedDb` , regardless of your choice of vector database. Vector databases are only used for storage and retrieval of embeddings. In addition to resource storage, `RagManagedDb` can also be used to store and manage vector representations of your documents. The vector database is then used to retrieve relevant documents based on the document's semantic similarity to a given query.

## Available tiers

RAG Engine lets you scale your `RagManagedDb` instance based on your usage and performance requirements using a choice of two tiers. You can also use it to delete your RAG Engine data with a third tier.

The tier is a project-level setting that's available in the `RagEngineConfig` resource that impacts RAG corpora using `RagManagedDb` . The following tiers are available in `RagEngineConfig` :

  - **Scaled tier:** This tier offers production-scale performance along with autoscaling functionality. It's suitable for customers with large amounts of data or performance-sensitive workloads. Internally, this tier sets the Spanner instance to autoscaling configuration with a minimum of 1 node (1,000 processing units) and a maximum of 10 nodes (10,000 processing units).

  - **Basic tier (default):** This tier offers a cost-effective and low-compute tier, which might be suitable for some of the following cases:
    
      - Experimenting with `RagManagedDb`
      - Small data sizes
      - Latency-insensitive workloads
      - Using RAG Engine with only other vector databases

To offer the Basic tier, `RagManagedDb` sets the underlying Spanner instance to a fixed configuration of 100 processing units, which is equivalent to 0.1 nodes.

  - **Unprovisioned tier:** This tier deletes the `RagManagedDb` and its underlying Spanner instance. The Unprovisioned tier disables the RAG Engine service and deletes your data held within this service regardless of the vector database used for your `RagCorpora` . This stops the billing of the service. For more information on billing, see [RAG Engine on Gemini Enterprise Agent Platform billing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-engine-billing) .

After the data is deleted, it can't be recovered. To start using RAG Engine again, you must update the tier by calling the `UpdateRagEngineConfig` API or switch the mode to Serverless.

## Managing tiers

To read and update your tiers, use the `GetRagEngineConfig` and `UpdateRagEngineConfig` API. Refer to the [Switching between modes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/switching-modes) page for code samples on how to use these APIs.
