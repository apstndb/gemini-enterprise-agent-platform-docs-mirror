---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/patch
title: 'Method: ragCorpora.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.patch

Updates a RagCorpus.

### Endpoint

patch `https: / /{service-endpoint} /v1 /{ragCorpus.name}`  

`PATCH https://{service-endpoint}/v1/{ragCorpus.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`ragCorpus.name` `string`

Output only. The resource name of the RagCorpus.

### Request body

The request body contains an instance of `  RagCorpus  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
