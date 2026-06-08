---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/patch
title: 'Method: sessions.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.sessions.patch

Updates the specific `  Session  ` .

### Endpoint

patch `https: / /{service-endpoint} /v1 /{session.name}`  

`PATCH https://{service-endpoint}/v1/{session.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`session.name` `string`

Identifier. The resource name of the session. Format: 'projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sessions/{session}'.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. Field mask is used to control which fields get updated. If the mask is not present, all fields will be updated.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  Session  ` .

### Response body

If successful, the response body contains an instance of `  Session  ` .
