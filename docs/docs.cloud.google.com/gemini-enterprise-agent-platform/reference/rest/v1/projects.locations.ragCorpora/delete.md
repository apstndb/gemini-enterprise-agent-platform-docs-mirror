---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/delete
title: 'Method: ragCorpora.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.delete

Deletes a RagCorpus.

### Endpoint

delete `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the RagCorpus resource to be deleted. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

### Query parameters

`force` `boolean`

Optional. If set to true, any RagFiles in this RagCorpus will also be deleted. Otherwise, the request will only work if the RagCorpus has no RagFiles.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
