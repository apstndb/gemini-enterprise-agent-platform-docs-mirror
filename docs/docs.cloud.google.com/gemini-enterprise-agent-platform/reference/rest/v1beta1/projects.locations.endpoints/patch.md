---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/patch
title: 'Method: endpoints.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.patch

Updates an Endpoint.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{endpoint.name}`  

`PATCH https://{service-endpoint}/v1beta1/{endpoint.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint.name` `string`

Identifier. The resource name of the Endpoint.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. The update mask applies to the resource. See `  google.protobuf.FieldMask  ` .

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  Endpoint  ` .

### Response body

If successful, the response body contains an instance of `  Endpoint  ` .
