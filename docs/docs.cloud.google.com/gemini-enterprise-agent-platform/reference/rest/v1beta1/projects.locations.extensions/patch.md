---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/patch
title: 'Method: extensions.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.extensions.patch

Updates an Extension.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{extension.name}`  

`PATCH https://{service-endpoint}/v1beta1/{extension.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`extension.name` `string`

Identifier. The resource name of the Extension.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. Mask specifying which fields to update. Supported fields:

  - `displayName`
  - `description`
  - `runtimeConfig`
  - `toolUseExamples`
  - `manifest.description`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  Extension  ` .

### Response body

If successful, the response body contains an instance of `  Extension  ` .
