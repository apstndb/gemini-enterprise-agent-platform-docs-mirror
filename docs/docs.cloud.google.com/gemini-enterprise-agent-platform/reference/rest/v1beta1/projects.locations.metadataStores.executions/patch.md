---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.executions/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.executions/patch
title: 'Method: executions.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.executions.patch

Updates a stored Execution.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{execution.name}`  

`PATCH https://{service-endpoint}/v1beta1/{execution.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`execution.name` `string`

Output only. The resource name of the Execution.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. A FieldMask indicating which fields should be updated.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`allowMissing` `boolean`

If set to true, and the `  Execution  ` is not found, a new `  Execution  ` is created.

### Request body

The request body contains an instance of `  Execution  ` .

### Response body

If successful, the response body contains an instance of `  Execution  ` .
