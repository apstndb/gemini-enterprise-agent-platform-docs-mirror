---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Fact
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Fact
title: Fact
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The fact used in grounding.

Fields

`query` `string`

Query that is used to retrieve this fact.

`title` `string`

If present, it refers to the title of this fact.

`uri` `string`

If present, this uri links to the source of the fact.

`summary` `string`

If present, the summary/snippet of the fact.

`vectorDistance `**`(deprecated)`** `number`

> This item is deprecated!

If present, the distance between the query vector and this fact vector.

`score` `number`

If present, according to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the fact and its range depends on the metric type.

For example, if the metric type is COSINE_DISTANCE, it represents the distance between the query and the fact. The larger the distance, the less relevant the fact is to the query. The range is \[0, 2\], while 0 means the most relevant and 2 means the least relevant.

`chunk` `object ( `[`RagChunk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagChunk)` )`

If present, chunk properties.

**JSON representation**

```
{
  "query": string,
  "title": string,
  "uri": string,
  "summary": string,
  "vectorDistance": number,
  "score": number,
  "chunk": {
    object (RagChunk)
  }
}
```
