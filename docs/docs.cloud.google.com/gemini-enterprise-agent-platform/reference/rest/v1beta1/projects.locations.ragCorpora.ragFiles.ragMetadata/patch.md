---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/patch
title: 'Method: ragMetadata.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.ragFiles.ragMetadata.patch

Updates a RagMetadata.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{ragMetadata.name}`  

`PATCH https://{service-endpoint}/v1beta1/{ragMetadata.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`ragMetadata.name` `string`

Identifier. Resource name of the RagMetadata. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}/ragFiles/{ragFile}/ragMetadata/{ragMetadata}`

### Request body

The request body contains an instance of `  RagMetadata  ` .

### Response body

If successful, the response body contains an instance of `  RagMetadata  ` .
