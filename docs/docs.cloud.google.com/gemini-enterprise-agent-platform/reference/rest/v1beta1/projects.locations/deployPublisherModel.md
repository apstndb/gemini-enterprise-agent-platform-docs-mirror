---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/deployPublisherModel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/deployPublisherModel
title: 'Method: locations.deployPublisherModel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> This item is deprecated\!

**Full name** : projects.locations.deployPublisherModel

Deploys publisher models.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{destination}:deployPublisherModel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`destination` `string`

Required. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`model` `string`

Required. The model to deploy. Format: 1. `publishers/{publisher}/models/{publisherModel}@{versionId}` , or `publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001` . 2. Hugging Face model id like `google/gemma-2-2b-it` . 3. Custom model Google Cloud Storage URI like `gs://bucket` . 4. Custom model zip file like `https://example.com/a.zip` .

`endpointDisplayName` `string`

Optional. The user-specified display name of the endpoint. If not set, a default name will be used.

`dedicatedResources` ` object ( DedicatedResources  ` )

Optional. The dedicated resources to use for the endpoint. If not set, the default resources will be used.

`modelDisplayName` `string`

Optional. The user-specified display name of the uploaded model. If not set, a default name will be used.

`huggingFaceAccessToken` `string`

Optional. The Hugging Face read access token used to access the model artifacts of gated models.

`acceptEula` `boolean`

Optional. Whether the user accepts the End user License Agreement (EULA) for the model.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
