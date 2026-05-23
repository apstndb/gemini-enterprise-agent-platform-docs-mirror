---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/updateExplanationDataset
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/updateExplanationDataset
title: 'Method: models.updateExplanationDataset'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.updateExplanationDataset

Incrementally update the dataset used for an examples model.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{model}:updateExplanationDataset`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`model` `string`

Required. The resource name of the Model to update. Format: `projects/{project}/locations/{location}/models/{model}`

### Request body

The request body contains data with the following structure:

Fields

`examples` ` object ( Examples  ` )

The example config containing the location of the dataset.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
