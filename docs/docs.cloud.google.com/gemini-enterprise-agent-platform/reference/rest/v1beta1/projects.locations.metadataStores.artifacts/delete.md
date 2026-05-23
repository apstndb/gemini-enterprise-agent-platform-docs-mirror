---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.artifacts/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.artifacts/delete
title: 'Method: artifacts.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.artifacts.delete

Deletes an Artifact.

### Endpoint

delete `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the Artifact to delete. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`

### Query parameters

`etag` `string`

Optional. The etag of the Artifact to delete. If this is provided, it must match the server's etag. Otherwise, the request will fail with a FAILED\_PRECONDITION.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
