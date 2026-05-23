---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/patch
title: 'Method: reasoningEngines.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.patch

Updates a reasoning engine.

### Endpoint

patch `https: / /{service-endpoint} /v1 /{reasoningEngine.name}`  

`PATCH https://{service-endpoint}/v1/{reasoningEngine.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`reasoningEngine.name` `string`

Identifier. The resource name of the ReasoningEngine. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. Mask specifying which fields to update.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  ReasoningEngine  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
