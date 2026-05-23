---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/serverless-mode
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/serverless-mode
title: Serverless mode
description: Manage your Serverless mode deployment in RAG Engine on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> Some of the RAG features are Preview offerings, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as-is" and may have limited support, and changes to Pre-GA products and features may not be compatible with other Pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) . By using the Gemini API on Gemini Enterprise Agent Platform, you agree to the Generative AI Preview [terms and conditions](https://cloud.google.com/trustedtester/aitos) (Preview Terms).

> The [VPC-SC security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) and CMEK are supported by Agent Platform RAG Engine. Data residency and AXT security controls aren't supported.

Serverless mode is the recommended way to get started with RAG Engine. It provides a fully-managed and highly scalable database to back your RAG Engine resources, without the hassle of provisioning or managing any infrastructure configurations. It offers quick onboarding and is suitable for most users, including enterprise scale.

Serverless mode is a preview feature and is available in `us-central1` only. It is available to everyone and does not require any allowlist.

With Serverless mode, your RAG Engine CUJ remains identical to that with Spanner mode, except for the following key differences:

1.  `RagManagedDb` is not available as a choice of vector database when using Serverless mode. Instead, the new default vector database is the fully-managed and highly scalable `RagManagedVertexVectorSearch` . To learn more about this vector DB, refer to [Use Vector Search 2.0 with RAG](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-rag-managed-vertex-ai-vector-search) .
2.  Customer-Managed Encryption Keys (CMEK) are not supported in Serverless mode.

## Switching to Serverless mode

To switch to Serverless mode as your choice of deployment mode, refer to the [Switching your modes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/switching-modes) page.

## Delete your data

To delete your data from Serverless deployment mode, follow these steps:

1.  Ensure your active mode is set to Serverless.
2.  Call the `ListRagCorpora` API to view your resources under this mode,
3.  Delete each corpus using the `DeleteRagCorpus` API.

## Pricing

There is no additional charge when using Serverless deployment mode. However, if you have an active Spanner mode, you might still get charged for it. Additionally, you might incur charges from your choice of models, reranking, and vector storage on RAG Engine. For more information, refer to the [RAG Engine on Gemini Enterprise Agent Platform billing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-engine-billing) page.
