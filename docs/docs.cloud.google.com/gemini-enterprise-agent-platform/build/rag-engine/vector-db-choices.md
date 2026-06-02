---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/vector-db-choices
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/vector-db-choices
title: Vector database choices in RAG Engine
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> The [VPC-SC security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) and CMEK are supported by Agent Platform RAG Engine. Data residency and AXT security controls aren't supported.

> The RAG Engine-managed Spanner instance is used as a vector database and is GA with billing enabled. For more information, see [RAG Engine on Gemini Enterprise Agent Platform billing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-engine-billing) .

This page introduces the vector databases supported on RAG Engine. You can also see how to connect a vector database (vector store) to your RAG corpus.

Vector databases play a crucial role in enabling retrieval for RAG applications. Vector databases offer a specialized way to store and query vector embeddings, which are mathematical representations of text or other data that capture semantic meaning and relationships. Vector embeddings allow RAG systems to quickly and accurately find the most relevant information within a vast knowledge base, even when dealing with complex or nuanced queries. When combined with an embedding model, vector databases can help overcome the limitations of LLMs, and provide more accurate, relevant, and comprehensive responses.

## Supported vector databases

When creating a RAG corpus, RAG Engine offers the enterprise-ready `RagManagedDb` as the default vector database, which requires no additional provisioning or managing. `RagManagedDb` offers both KNN and ANN search options and allows switching to a basic tier for some quick prototyping and experimentation. To learn more about choosing a retrieval strategy on `RagManagedDb` or for updating the tier, see [Use `RagManagedDb` with RAG](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-ragmanageddb-with-rag) . For RAG Engine to automatically create and manage the vector database for you, see [REST Resource: projects.locations.ragCorpora](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora) .

In addition to the default `RagManagedDb` , RAG Engine lets you provision and use your vector database within your RAG corpus. In this case, you are responsible for the lifecycle and scalability of your vector database.

## Compare vector database options

This table lists your choices of vector databases that are supported within RAG Engine and provides links to pages that explain how to use the vector databases within your RAG corpus.

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Vector database</th>
<th>Benefits</th>
<th>Best for</th>
<th>Disadvantages</th>
<th>Supported distance metrics</th>
<th>Search type</th>
<th>Launch stage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-ragmanageddb-with-rag"><code dir="ltr" translate="no">RagManagedDb</code></a> (default) is a regionally-distributed scalable database service that offers very high consistency and high availability and can be used for a vector search. easy simple fast quick</td>
<td><ul>
<li>No setup required.</li>
<li>Good for enterprise-scale and small-scale use cases.</li>
<li>Very high consistency.</li>
<li>High availability.</li>
<li>Low latency.</li>
<li>Excellent for transactional workloads.</li>
<li>CMEK enabled.</li>
</ul></td>
<td><ul>
<li>Generating high-volume documents.</li>
<li>Building enterprise-scale RAG.</li>
<li>Developing a quick proof of concept.</li>
<li>Providing low provisioning and maintenance overhead.</li>
<li>Using with chat bots.</li>
<li>Building RAG applications.</li>
</ul></td>
<td><ul>
<li>For optimal recall, the ANN feature requires that the index be rebuilt after major changes to your data.</li>
</ul></td>
<td><code dir="ltr" translate="no">cosine</code></td>
<td>KNN (default) and ANN</td>
<td>Generally available</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-vertexai-vector-search">Vector Search</a> is the vector database service within Agent Platform that's optimized for machine-learning tasks.</td>
<td><ul>
<li>Integrates with other Google Cloud services.</li>
<li>Scalability and reliability are supported by Google Cloud infrastructure.</li>
<li>Uses pay-as-you-go pricing.</li>
</ul></td>
<td><ul>
<li>Generating high-volume documents.</li>
<li>Building enterprise-scale RAG.</li>
<li>Managing vector database infrastructure.</li>
<li>Existing Google Cloud customers or anyone looking to use multiple Google Cloud services.</li>
</ul></td>
<td><ul>
<li>Updates aren't reflected immediately.</li>
<li>Vendor lock-in with Google Cloud.</li>
<li>Could be more expensive depending on your use cases.</li>
</ul></td>
<td><code dir="ltr" translate="no">cosine</code><br />
<br />
<code dir="ltr" translate="no">dot-product</code></td>
<td>ANN</td>
<td>Generally available</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-feature-store-with-rag">Vertex AI Feature Store</a> is a managed service for organizing, storing, and serving machine-learning features.</td>
<td><ul>
<li>Integrates with Gemini Enterprise Agent Platform and other Google Cloud services.</li>
<li>Scalability and reliability are supported by Google Cloud infrastructure.</li>
<li>Leverages existing BigQuery infrastructure.</li>
</ul></td>
<td><ul>
<li>Generating high-volume documents.</li>
<li>Building enterprise-scale RAG.</li>
<li>Managing vector database infrastructure.</li>
<li>Existing Google Cloud customers or customers looking to use multiple Google Cloud services.</li>
</ul></td>
<td><ul>
<li>Changes are only available in the online store after a manual synchronization is performed.</li>
<li>Vendor lock-in with Google Cloud.</li>
</ul></td>
<td><code dir="ltr" translate="no">cosine</code><br />
<br />
<code dir="ltr" translate="no">dot-product</code><br />
<br />
<code dir="ltr" translate="no">L2 squared</code></td>
<td>ANN</td>
<td>Preview</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-weaviate-db">Weaviate</a> is an open-source vector database that's flexible and modular.</td>
<td><ul>
<li>Supports various data types and offers built-in graph capabilities.</li>
<li>Provides open source and a vibrant community.</li>
<li>Highly flexible and customizable.</li>
<li>Supports diverse data types and modules for different modalities, such as text and images.</li>
<li>Can choose among Cloud providers, such as Google Cloud, AWS, and Azure.</li>
</ul></td>
<td><ul>
<li>Generating high-volume documents.</li>
<li>Building enterprise-scale RAG.</li>
<li>Managing vector database infrastructure.</li>
<li>Existing Weaviate customers.</li>
</ul></td>
<td><ul>
<li>Updates aren't reflected immediately.</li>
<li>Can be more complex to set up and manage.</li>
<li>Performance can vary depending on the configuration.</li>
</ul></td>
<td><code dir="ltr" translate="no">cosine</code><br />
<br />
<code dir="ltr" translate="no">dot-product</code><br />
<br />
<code dir="ltr" translate="no">L2 squared</code><br />
<br />
<code dir="ltr" translate="no">hamming</code><br />
<br />
<code dir="ltr" translate="no">manhattan</code></td>
<td>ANN + Hybrid search support</td>
<td>Preview</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-pinecone">Pinecone</a> is a fully-managed cloud-native vector database designed for a high-performance similarity search.</td>
<td><ul>
<li>Get started quickly.</li>
<li>Excellent scalability and performance.</li>
<li>Focus on vector search with advanced features like filtering and a metadata search.</li>
<li>Can choose among Cloud providers, such as Google Cloud, AWS, and Azure.</li>
</ul></td>
<td><ul>
<li>Generating high-volume documents.</li>
<li>Building enterprise-scale RAG.</li>
<li>Managing vector database infrastructure.</li>
<li>Existing Pinecone customers.</li>
</ul></td>
<td><ul>
<li>Updates aren't reflected immediately.</li>
<li>Can be more expensive than other options.</li>
<li>Quotas and limits restrict scale and performance.</li>
<li>Limited control over the underlying infrastructure.</li>
</ul></td>
<td><code dir="ltr" translate="no">cosine</code><br />
<br />
<code dir="ltr" translate="no">euclidean</code><br />
<br />
<code dir="ltr" translate="no">dot-product</code></td>
<td>ANN</td>
<td>Generally available</td>
</tr>
</tbody>
</table>

## What's next

  - To create a RAG corpus, see [Method: ragCorpora.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/create)

  - To list RAG corpus, see [Method: ragCorpora.list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/list)
