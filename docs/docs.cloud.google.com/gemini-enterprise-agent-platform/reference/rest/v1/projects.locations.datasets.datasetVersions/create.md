---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.datasetVersions/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets.datasetVersions/create
title: 'Method: datasetVersions.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.datasetVersions.create

Create a version from a Dataset.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /datasetVersions`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the Dataset resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

### Request body

The request body contains an instance of `  DatasetVersion  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
