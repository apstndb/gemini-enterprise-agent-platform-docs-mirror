---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.datasetVersions/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.datasetVersions/get
title: 'Method: datasetVersions.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.datasetVersions.get

Gets a Dataset version.

### Endpoint

get `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the Dataset version to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{datasetVersion}`

### Query parameters

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  DatasetVersion  ` .
