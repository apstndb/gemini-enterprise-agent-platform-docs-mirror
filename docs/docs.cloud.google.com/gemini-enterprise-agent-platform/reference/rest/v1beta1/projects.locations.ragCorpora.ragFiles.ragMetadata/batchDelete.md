---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/batchDelete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/batchDelete
title: 'Method: ragMetadata.batchDelete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.ragFiles.ragMetadata.batchDelete

Batch Deletes one or more RagMetadata.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /ragMetadata:batchDelete`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the RagFile from which to delete the RagMetadata. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}/ragFiles/{ragFile}`

### Request body

The request body contains data with the following structure:

Fields

`names[]` `string`

Required. The RagMetadata to delete. A maximum of 500 rag metadata can be deleted in a batch.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
