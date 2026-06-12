---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/try-it
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/try-it
title: Agent Retrieval interactive demo
description: Experience Agent Retrieval (formerly Vector Search 2.0)'s state-of-the-art technology with the interactive demo, which uses real-world datasets to learn how Agent Retrieval (formerly Vector Search 2.0) works, explore semantic and hybrid search, and see re-ranking in action by submitting a description of an item.
data_source: docs.cloud.google.com
---

This interactive demo lets you explore [Agent Retrieval (formerly Vector Search 2.0)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/overview) , the fully managed vector database for Google Cloud. Use the demo to search across millions of product listings with semantic search (powered with [Gemini auto-embeddings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/embeddings/autogenerating-embeddings) keyword text search or hybrid search that uses [Reciprocal Rank Fusion (RRF)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/about-hybrid-search#rrf) to combine both semantic search and keyword text search. Results can be reranked which uses the [Gemini Enterprise Agent Platform Ranking API](https://cloud.google.com/generative-ai-app-builder/docs/ranking) for reranking.

## Agent Retrieval benefits

Vector Search required separate embedding generation, index deployment, and a Vertex AI Feature Store for metadata. Agent Retrieval provides unified storage for data and embeddings, automatic embedding generation, and built-in text search without requiring you to manage infrastructure.

## Try it\!

To run:

1.  In the **Query** field, describe the items you want to query for (for example, `vintage 1970s pinball machine` ). Alternatively, click **Generate Query** to auto-generate a description.

2.  Click **Submit** or press Enter .

Experiment with the different options in the demo to get a head start understanding Agent Retrieval and the basics of vector search technology. For more information, go to [User Interface](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/try-it#ui) .

## User interface

This section describes settings in the UI you can use to control the results Agent Retrieval (formerly Vector Search 2.0) returns and how they are ranked.

### Dataset

Use the **Dataset** drop-down to choose which dataset Agent Retrieval will run your query against. For information about each dataset, go to [Datasets](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/try-it#datasets) .

### Query

To run a query:

1.  Click **Dataset** and choose which dataset to run your query against.

2.  In the **Query** field, add a description, ask a question, or enter one or more keywords to specify the items Agent Retrieval to return results for. Alternatively, click **Generate Query** to auto-generate a query.

3.  Do one of the following:
    
    1.  To return semantically similar results, select **Semantic** .
    2.  To return results based on the query's text syntax, select **Text** .
    3.  To perform a hybrid search, selectic both **Semantic** and **Text** .

4.  If you are semantically querying either the **Mercari 3M items (128-dim Gemini text embeddings)** or **Mercari 3M items (768-dim Gemini text embeddings)** dataset, click **Query Task Type** and select either **QUESTION\_ANSWERING** or **RETRIEVAL\_QUERY** .

5.  Click **Submit** or press Enter to run the query.

#### Modify

There are many options you can use to modify the results Agent Retrieval (formerly Vector Search 2.0) returns from a query.

  - Click **Rows** and choose the maximum number of search results that you want Agent Retrieval (formerly Vector Search 2.0) to return.

  - Select **Semantic** to return semantically similar results.

  - Select **Text** to return results based on your query's text syntax.

  - Select both **Semantic** and **Text** to enable hybrid search.

  - Select **Rerank** to rerank search results based on their query relevance. For more information, see [Improve search and RAG quality with ranking API](https://docs.cloud.google.com/generative-ai-app-builder/docs/ranking) .

  - Select **Use kNN** to use the [k-nearest neighbors algorithm](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm) to retrieve search results. Because kNN provides a 100% recall rate, it is very useful when debugging or testing.

  - Click **Query Task Type** and select the which query task type to use. This is only available when using the **Mercari 3M items (128-dim Gemini text embeddings)** and **Mercari 3M items (768-dim Gemini text embeddings)** datasets. For more information about query task types, go to [Choose an embeddings task type](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/embeddings/task-types) .

  - In the **RRF Alpha** field, enter a value between 0.0 and 1.0 to specify the RRF ranking effect. This is only available for hybrid search (both **Semantic** and **Text** are selected).  
    Alpha values of:
    
      - `1.0` - Rank results purely by semantic (dense) similarity.
      - `0.0` - Rank results purely by keyword (sparse) relevance.
      - `0.5` - Ranks results with requal weight is given to semantic (dense) similarity and keyword (sparse) relevance.
    
    For more information, see [What is Reciprocal Rank Fusion?](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/about-hybrid-search#rrf)

### Metrics

After a query runs, you are provided with latency metrics that breakdown the time it took for different stages of the search to complete.

This includes:

  - The total latency from all sources.
  - The amount of time it took to generate embeddings and perform a vector search.
  - The amount of time reranking took if **Rerank** is selected.
  - The total amount of latency from the network and other sources.

## Embeddings

Agent Retrieval supports the following embedding types:

  - **Multimodal:** Multimodal semantic search on item images. For details, go to [What is Multimodal Search: "LLMs with vision" change businesses](https://cloud.google.com/blog/products/ai-machine-learning/multimodal-generative-ai-search) .

  - **Text (semantic similarity):** Text semantic search on item names and descriptions based on semantic similarity. To learn more, go to [Vertex AI Embeddings for Text: Grounding LLMs made easy](https://cloud.google.com/blog/products/ai-machine-learning/how-to-use-grounding-for-your-llms-with-text-embeddings) .

  - **Text (retrieval document):** Asymmetric search based on a question or short phrase. To learn more, go to [Vertex AI Embeddings for Text: Grounding LLMs made easy](https://cloud.google.com/blog/products/ai-machine-learning/how-to-use-grounding-for-your-llms-with-text-embeddings) .

  - **Word:** Word-level semantic understanding with very fast inference and highly compact.

## Query process

In Agent Retrieval, the query process depends on the kind of searches being done and the embedding models.

### Semantic and hybrid search

Embedding generation and search happen in a single API call. Agent Retrieval auto-generates the query embedding server-side using the model specified in the `vertex_embedding_config` for the [Collection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections) , performs the search, and returns results with full metadata without needing a separate Vertex AI Feature Store fetch.

### Word2Vec and multimodal

The client generates the query embedding and sends it to Agent Retrieval for vector search. The results still include full metadata from the Collection and a Vertex AI Feature Store fetch isn't needed.

### Text

Agent Retrieval performs built-in keyword matching directly. Embeddings are not generated.

## Datasets

> **Note:** Datasets are provided by [Mercari](https://www.mercari.com/) , a popular online marketplace in the US and Japan.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Dataset</th>
<th style="text-align: left;">Description</th>
<th style="text-align: left;">Embedding Model</th>
<th style="text-align: left;">Embedding Task Type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Mercari 1M items<br />
(768-dim Gemini text embeddings)</td>
<td style="text-align: left;">Uses the Gemini Embedding 2 embedding model with separate text and image embeddings. This dataset supports text-to-text and text-to-image search using different vector fields.</td>
<td style="text-align: left;"><a href="https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/embedding-2"><code dir="ltr" translate="no">gemini-embedding-2-preview</code></a></td>
<td style="text-align: left;">SEMANTIC_SIMILARITY</td>
</tr>
<tr class="even">
<td style="text-align: left;">Mercari 3M items<br />
(128-dim Gemini text embeddings)</td>
<td style="text-align: left;">Has a reduced number of embedding dimensions that provides a smaller index size and storage cost. This dataset may have lower accuracy than Mercari 3M items (768-dim Gemini text embeddings).</td>
<td style="text-align: left;"><a href="https://developers.googleblog.com/gemini-embedding-available-gemini-api/"><code dir="ltr" translate="no">gemini-embedding-001</code></a></td>
<td style="text-align: left;">RETRIEVAL_DOCUMENT</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Mercari 3M items<br />
(768-dim Gemini text embeddings)</td>
<td style="text-align: left;">Has full-dimension embeddings with auto-embeddings and high text semantic accuracy. This dataset uses RETRIEVAL_DOCUMENT for asymmetric query-document matching.</td>
<td style="text-align: left;"><a href="https://developers.googleblog.com/gemini-embedding-available-gemini-api/"><code dir="ltr" translate="no">gemini-embedding-001</code></a></td>
<td style="text-align: left;">RETRIEVAL_DOCUMENT</td>
</tr>
<tr class="even">
<td style="text-align: left;">Mercari 3M items<br />
(768-dim Gemini text embeddings, semantic similarity)</td>
<td style="text-align: left;">Uses the SEMANTIC_SIMILARITY task type for similarity matching. This dataset is the best for use cases that need "find similar items" functionality where query and documents have same semantics.</td>
<td style="text-align: left;"><a href="https://developers.googleblog.com/gemini-embedding-available-gemini-api/"><code dir="ltr" translate="no">gemini-embedding-001</code></a></td>
<td style="text-align: left;">SEMANTIC_SIMILARITY</td>
</tr>
<tr class="odd">
<td style="text-align: left;">Mercari 3M items<br />
(1408-dim Vertex AI multimodal embeddings)</td>
<td style="text-align: left;">Has Vertex AI multimodal embeddings that encodes item images for image search.</td>
<td style="text-align: left;"><a href="https://docs.cloud.google.com/vertex-ai/generative-ai/docs/embeddings/get-multimodal-embeddings"><code dir="ltr" translate="no">multimodal-embedding-001</code></a></td>
<td style="text-align: left;">N/A</td>
</tr>
<tr class="even">
<td style="text-align: left;">Mercari 3M items<br />
(100-dim Word2Vec text embeddings)</td>
<td style="text-align: left;">Uses the Gensim Word2Vec embedding model. This dataset has the fastest inference. It provides only word-level semantic understanding but is very compact.</td>
<td style="text-align: left;">Gensim <a href="https://radimrehurek.com/gensim/auto_examples/tutorials/run_word2vec.html">Word2Vec</a></td>
<td style="text-align: left;">N/A</td>
</tr>
</tbody>
</table>

## See also

  - [Collections](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections)
  - [Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects)
  - [Querying Collections for Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query)
  - [Searching for Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search)
