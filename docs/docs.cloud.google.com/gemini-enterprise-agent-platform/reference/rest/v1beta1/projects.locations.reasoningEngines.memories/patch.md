---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/patch
title: 'Method: memories.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.memories.patch

Update a Memory.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{memory.name}`  

`PATCH https://{service-endpoint}/v1beta1/{memory.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`memory.name` `string`

Identifier. Represents the resource name of the Memory. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/memories/{memory}`

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. Mask specifying which fields to update. The following fields are immutable:

  - `scope`
  - `memoryType`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  Memory  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
