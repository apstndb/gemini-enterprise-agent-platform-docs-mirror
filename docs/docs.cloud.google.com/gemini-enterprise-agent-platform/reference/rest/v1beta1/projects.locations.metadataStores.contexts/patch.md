---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts/patch
title: 'Method: contexts.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.contexts.patch

Updates a stored Context.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{context.name}`  

`PATCH https://{service-endpoint}/v1beta1/{context.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`context.name` `string`

Immutable. The resource name of the Context.

### Query parameters

`updateMask` `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)`

Optional. A FieldMask indicating which fields should be updated.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`allowMissing` `boolean`

If set to true, and the [`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts#Context) is not found, a new [`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts#Context) is created.

### Request body

The request body contains an instance of [`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts#Context) .

### Response body

If successful, the response body contains an instance of [`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts#Context) .
