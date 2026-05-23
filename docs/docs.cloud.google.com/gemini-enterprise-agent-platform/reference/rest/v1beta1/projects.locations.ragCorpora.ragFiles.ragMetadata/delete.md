---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/delete
title: 'Method: ragMetadata.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.ragFiles.ragMetadata.delete

Deletes a RagMetadata.

### Endpoint

delete `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the RagMetadata resource to be deleted. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}/ragFiles/{ragFile}/ragMetadata/{ragMetadata}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.
