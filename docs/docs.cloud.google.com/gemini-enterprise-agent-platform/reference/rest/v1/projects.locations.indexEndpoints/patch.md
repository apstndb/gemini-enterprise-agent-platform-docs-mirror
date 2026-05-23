---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/patch
title: 'Method: indexEndpoints.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.indexEndpoints.patch

Updates an IndexEndpoint.

### Endpoint

patch `https: / /{service-endpoint} /v1 /{indexEndpoint.name}`  

`PATCH https://{service-endpoint}/v1/{indexEndpoint.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`indexEndpoint.name` `string`

Output only. The resource name of the IndexEndpoint.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. The update mask applies to the resource. See `  google.protobuf.FieldMask  ` .

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  IndexEndpoint  ` .

### Response body

If successful, the response body contains an instance of `  IndexEndpoint  ` .
