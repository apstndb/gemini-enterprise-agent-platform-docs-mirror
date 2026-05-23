---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/patch
title: 'Method: datasets.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.patch

Updates a Dataset.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{dataset.name}`  

`PATCH https://{service-endpoint}/v1beta1/{dataset.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`dataset.name` `string`

Output only. Identifier. The resource name of the Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. The update mask applies to the resource. For the `FieldMask` definition, see `  google.protobuf.FieldMask  ` . Updatable fields:

  - `displayName`
  - `description`
  - `labels`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  Dataset  ` .

### Response body

If successful, the response body contains an instance of `  Dataset  ` .
