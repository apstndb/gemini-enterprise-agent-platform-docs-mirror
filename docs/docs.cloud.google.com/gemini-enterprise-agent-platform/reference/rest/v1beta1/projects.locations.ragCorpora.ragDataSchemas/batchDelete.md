---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas/batchDelete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas/batchDelete
title: 'Method: ragDataSchemas.batchDelete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.ragDataSchemas.batchDelete

Batch Deletes one or more RagDataSchemas

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /ragDataSchemas:batchDelete`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the RagCorpus from which to delete the RagDataSchemas. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

### Request body

The request body contains data with the following structure:

Fields

`names[]` `string`

Required. The RagDataSchemas to delete. A maximum of 500 schemas can be deleted in a batch. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}/ragDataSchemas/{ragDataSchema}`

### Response body

If successful, the response body contains an instance of `  Operation  ` .
