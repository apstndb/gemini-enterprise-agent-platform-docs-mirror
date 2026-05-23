---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.publishers.models/export
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.publishers.models/export
title: 'Method: models.export'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.publishers.models.export

Exports a publisher model to a user provided Google Cloud Storage bucket.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /{name}:export`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The Location to export the model weights from Format: `projects/{project}/locations/{location}`

`name` `string`

Required. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisherModel}@{versionId}` , or `publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001`

### Request body

The request body contains data with the following structure:

Fields

`destination` `object ( GcsDestination` )

Required. The target where we are exporting the model weights to

### Response body

If successful, the response body contains an instance of `  Operation  ` .
