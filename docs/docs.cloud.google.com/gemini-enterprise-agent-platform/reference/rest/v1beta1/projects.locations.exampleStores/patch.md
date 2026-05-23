---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/patch
title: 'Method: exampleStores.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.exampleStores.patch

Update an ExampleStore.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{exampleStore.name}`  

`PATCH https://{service-endpoint}/v1beta1/{exampleStore.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`exampleStore.name` `string`

Identifier. The resource name of the ExampleStore. This is a unique identifier. Format: projects/{project}/locations/{location}/exampleStores/{exampleStore}

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. Mask specifying which fields to update. Supported fields:

  - `displayName`
  - `description`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  ExampleStore  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
