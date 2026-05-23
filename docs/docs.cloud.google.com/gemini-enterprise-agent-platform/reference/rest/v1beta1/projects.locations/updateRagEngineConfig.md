---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/updateRagEngineConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/updateRagEngineConfig
title: 'Method: locations.updateRagEngineConfig'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.updateRagEngineConfig

Updates a RagEngineConfig.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{ragEngineConfig.name}`  

`PATCH https://{service-endpoint}/v1beta1/{ragEngineConfig.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`ragEngineConfig.name` `string`

Identifier. The name of the RagEngineConfig. Format: `projects/{project}/locations/{location}/ragEngineConfig`

### Request body

The request body contains an instance of `  RagEngineConfig  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
