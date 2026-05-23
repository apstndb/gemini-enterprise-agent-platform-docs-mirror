---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TaskType
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TaskType
title: TaskType
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents the downstream task the embeddings will be used for. Specifying the task type helps the model generate embeddings that are optimized for your use case. New task types may be added in the future.

Enums

`DEFAULT`

Task type not specified. The model will use a default value suitable for semantic similarity and retrieval.

`RETRIEVAL_QUERY`

Specifies the given text is a query in a search/retrieval setting. Use this task type for embeddings that will be used to search a corpus of documents.

`RETRIEVAL_DOCUMENT`

Specifies the given text is a document from the corpus being searched. Use this task type for texts that are part of a corpus that will be searched.

`SEMANTIC_SIMILARITY`

Use this task type for Semantic Textual Similarity (STS). These embeddings will be compared with each other to measure semantic similarity.

`CLASSIFICATION`

Specifies that the given text will be classified. Use this task type to generate embeddings that will be used as input to a classification model (e.g., classifying text as spam or not spam).

`CLUSTERING`

Specifies that the embeddings will be used for clustering. Use this task type to generate embeddings that will be used to group similar texts together.

`QUESTION_ANSWERING`

Specifies that the embeddings will be used for question answering. Use this task type to generate embeddings for texts that are part of a question answering system.

`FACT_VERIFICATION`

Specifies that the embeddings will be used for fact verification. Use this task type to generate embeddings for texts that are part of a fact verification system.

`CODE_RETRIEVAL_QUERY`

Specifies that the embeddings will be used for code retrieval. Use this task type for embeddings that will be used to search a corpus of code.
