---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/deleteVersion
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/deleteVersion
title: 'Method: models.deleteVersion'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.deleteVersion

Deletes a Model version.

Model version can only be deleted if there are no `  DeployedModels  ` created from it. Deleting the only version in the Model is not allowed. Use `  models.delete  ` for deleting the Model instead.

### Endpoint

delete `https: / /{service-endpoint} /v1 /{name}:deleteVersion`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the model version to be deleted, with a version id explicitly included.

Example: `projects/{project}/locations/{location}/models/{model}@1234`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
