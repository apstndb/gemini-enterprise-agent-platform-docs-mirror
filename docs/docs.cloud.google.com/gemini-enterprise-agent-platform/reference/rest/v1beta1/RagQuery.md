---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagQuery
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagQuery
title: RagQuery
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A query to retrieve relevant contexts.

Fields

`similarityTopK `**`(deprecated)`** `integer`

> This item is deprecated!

Optional. The number of contexts to retrieve.

`ranking `**`(deprecated)`** `object ( `[`Ranking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagQuery#Ranking)` )`

> This item is deprecated!

Optional. Configurations for hybrid search results ranking.

`ragRetrievalConfig` `object ( `[`RagRetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#RagRetrievalConfig)` )`

Optional. The retrieval config for the query.

`query` `Union type`

The query to retrieve contexts. Currently only text query is supported. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` `string`

Optional. The query in text format to get relevant contexts.

End of mutually exclusive fields.

**JSON representation**

```
{
  "similarityTopK": integer,
  "ranking": {
    object (Ranking)
  },
  "ragRetrievalConfig": {
    object (RagRetrievalConfig)
  },

  // query
  "text": string
  // Union type
}
```

## Ranking

Configurations for hybrid search results ranking.

Fields

`alpha` `number`

Optional. Alpha value controls the weight between dense and sparse vector search results. The range is \[0, 1\], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally.

**JSON representation**

```
{
  "alpha": number
}
```
