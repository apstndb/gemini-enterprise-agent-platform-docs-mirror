---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/get
title: 'Method: models.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.get

Gets a Model.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the Model resource. Format: `projects/{project}/locations/{location}/models/{model}`

In order to retrieve a specific version of the model, also provide the version id or version alias. Example: `projects/{project}/locations/{location}/models/{model}@2` or `projects/{project}/locations/{location}/models/{model}@golden` If no version id or alias is specified, the "default" version will be returned. The "default" version alias is created for the first version of the model, and can be moved to other versions later on. There will be exactly one default version.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Model  ` .
