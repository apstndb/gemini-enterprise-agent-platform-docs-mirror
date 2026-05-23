---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.agents/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.agents/patch
title: 'Method: agents.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.agents.patch

Updates an agent.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{agent.name}`  

`PATCH https://{service-endpoint}/v1beta1/{agent.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`agent.name` `string`

Identifier. The resource name of the agent. Format: `projects/{project}/locations/{location}/agents/{agent}` .

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. The list of fields to update. If not present, all fields are updated.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  Agent  ` .

### Response body

If successful, the response body contains an instance of `  Agent  ` .
