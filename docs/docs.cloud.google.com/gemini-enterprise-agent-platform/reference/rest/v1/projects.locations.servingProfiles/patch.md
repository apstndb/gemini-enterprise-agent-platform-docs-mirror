---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.servingProfiles/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.servingProfiles/patch
title: 'Method: servingProfiles.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.servingProfiles.patch

Updates a ServingProfile.

### Endpoint

patch `https: / /{service-endpoint} /v1 /{servingProfile.name}`  

`PATCH https://{service-endpoint}/v1/{servingProfile.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`servingProfile.name` `string`

Identifier. The resource name of the ServingProfile.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. The list of fields to update; see <https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#fieldmask> . If omitted, all populated (non-empty) mutable fields are updated; if set to `["*"]` , all mutable fields are fully replaced (unpopulated values are cleared).

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  ServingProfile  ` .

### Response body

If successful, the response body contains an instance of `  ServingProfile  ` .
