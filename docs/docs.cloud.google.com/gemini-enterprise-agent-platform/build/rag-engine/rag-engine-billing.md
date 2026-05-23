---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-engine-billing
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-engine-billing
title: Vertex AI RAG Engine billing
description: Understand Agent Platform RAG Engine billing. Review costs for data ingestion, LLM parsing, embedding, Spanner vector search, and LLM reranking.
data_source: docs.cloud.google.com
---

> The [VPC-SC security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) and CMEK are supported by Agent Platform RAG Engine. Data residency and AXT security controls aren't supported.

This page describes the Vertex AI RAG Engine pricing and billing based on the Vertex AI RAG Engine components you use, such as models, reranking, and vector storage.

For more information, see the [Vertex AI RAG Engine overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/%7Brag-overview) page.

## Pricing and billing

This table explains how billing works when you use the RAG components.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Component</strong></th>
<th><strong>How billing works with Vertex AI RAG Engine</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-data-ingestion">Data ingestion</a></td>
<td>Vertex AI RAG Engine supports ingesting data from different data sources. For example, uploading local files, Cloud Storage, and Google Drive. Accessing files in these data sources from Vertex AI RAG Engine is free, but these data sources might charge for data transfer. For example, data egress costs.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/fine-tune-rag-transformations">Data transformation</a> (file parsing)</td>
<td><ul>
<li><strong>Default parser</strong> : Free.</li>
<li><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/llm-parser">LLM Parser</a></strong> : Vertex AI RAG Engine uses the LLM model that you specified to parse your file, and you will see and pay LLM model costs directly from your project.</li>
<li><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/layout-parser-integration">Document AI layout parser</a></strong> : Vertex AI RAG Engine uses the Document AI layout parser that you specified to process your file, and you will see and pay for the use of the Document AI layout parser directly from your project.</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/fine-tune-rag-transformations">Data transformation</a> (file chunking)</td>
<td>Supports fixed-size chunking, which is free.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-embedding-models">Embedding generation</a></td>
<td><p>Vertex AI RAG Engine orchestrates the embedding generation using the embedding model that you specified, and your project is billed for the costs associated with that model.</p>
<p>For more pricing information, see <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Cost of building and deploying AI models in Gemini Enterprise Agent Platform</a> .</p></td>
</tr>
<tr class="odd">
<td>Data indexing and retrieval</td>
<td><blockquote>
<strong>Note:</strong> The Vertex AI RAG Engine uses Spanner as a backend for its data indexing and retrieval operations. Using Spanner results in associated billing charges. For more information, see <a href="https://docs.cloud.google.com/spanner/pricing">Spanner pricing</a> .
</blockquote>
<p>RAG Engine supports two categories of vector databases for vector search:</p>
<ul>
<li>RAG-managed database</li>
<li>Bring-Your-Own vector database</li>
</ul>
<p>A RAG-managed database has two purposes:</p>
<ul>
<li>A RAG-managed database stores RAG resources, such as RAG corpora and RAG files. File contents are excluded.</li>
<li>Upon your choice, embedding indexing and retrieval for vector search.</li>
</ul>
<p>A RAG-managed database uses a Spanner instance as the backend.</p>
<p>For each of your projects, Vertex AI RAG Engine provisions a customer-specific Google Cloud project and manages RAG-managed resources that are stored in Vertex AI RAG Engine, so that your data is physically isolated.</p>
<p>If you choose the <code dir="ltr" translate="no">RagManagedDB</code> Basic tier or Scaled tier, Vertex AI RAG Engine provisions a Spanner Enterprise edition instance in the corresponding project:</p>
<ul>
<li><strong>Basic tier</strong> : 100 processing units with backup</li>
<li><strong>Scaled tier</strong> : Starting at 1 node (1,000 processing units) and autoscaling up to 10 nodes with backup</li>
</ul>
<p>If any RAG corpus in your project chooses to use a RAG-managed database for the vector search, you will be charged for the RAG-managed Spanner instance.</p>
<p>Vertex AI RAG Engine surfaces Spanner costs from your corresponding RAG-managed project to your Google Cloud project, so that you can see and pay Spanner instance costs.</p>
<p>For more pricing details on Spanner, see <a href="https://docs.cloud.google.com/spanner/pricing">Spanner pricing</a> .</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-engine/retrieval-and-ranking">Reranking for Vertex AI RAG Engine</a></td>
<td><p>The following ranking tools are supported post retrieval:</p>
<ul>
<li><strong>LLM Reranker</strong> : Vertex AI RAG Engine uses the LLM model that you specified to rerank the retrieval results, and you will see and pay LLM model costs directly from your project.</li>
<li><strong>Agent Search ranking API</strong> : Vertex AI RAG Engine uses the Agent Search ranking API to rerank the retrieval results, and you will see and pay for the <a href="https://docs.cloud.google.com/generative-ai-app-builder/pricing#ranking_api_pricing">Ranking API</a> directly from your project.</li>
</ul></td>
</tr>
</tbody>
</table>

## Delete Vertex AI RAG Engine

The following code samples demonstrate how to delete a Vertex AI RAG Engine for the Google Cloud console, Python, and REST:

  - Version 1 (v1) API [parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/updateRagEngineConfig) and [code samples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/updateRagEngineConfig) .

  - v1beta1 API [parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/updateRagEngineConfig) and [code samples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/updateRagEngineConfig) .

## What's next

  - To learn how to use the Vertex AI SDK to run Vertex AI RAG Engine tasks, see [RAG quickstart for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-quickstart) .

  - To learn about grounding, see [Grounding overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/gemini-enterprise-agent-platform/models/grounding/overview) .

  - To learn more about the responses from RAG, see [Retrieval and Generation Output of Vertex AI RAG Engine](https://docs.cloud.google.com/vertex-ai/docs/model-reference/rag-output-explained) .

  - To learn about the RAG architecture:
    
      - [Infrastructure for a RAG-capable generative AI application using Agent Platform and Vector Search](https://docs.cloud.google.com/architecture/gen-ai-rag-vertex-ai-vector-search)
    
      - [Infrastructure for a RAG-capable generative AI application using Agent Platform and AlloyDB for PostgreSQL](https://docs.cloud.google.com/architecture/rag-capable-gen-ai-app-using-vertex-ai) .
