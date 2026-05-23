---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.datasetVersions/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.datasetVersions/patch
title: 'Method: datasetVersions.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.datasetVersions.patch

Updates a DatasetVersion.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{datasetVersion.name}`  

`PATCH https://{service-endpoint}/v1beta1/{datasetVersion.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`datasetVersion.name` `string`

Output only. Identifier. The resource name of the DatasetVersion. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{datasetVersion}`

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. The update mask applies to the resource. For the `FieldMask` definition, see `  google.protobuf.FieldMask  ` . Updatable fields:

  - `displayName`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  DatasetVersion  ` .

### Response body

If successful, the response body contains an instance of `  DatasetVersion  ` .
