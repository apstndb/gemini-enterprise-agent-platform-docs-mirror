---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.publishers.models/enableModel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.publishers.models/enableModel
title: 'Method: models.enableModel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.publishers.models.enableModel

Enables model for the project if prerequisites are met (e.g. completed questionnaire and consents, or an active Private Offer).

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /{name}:enableModel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The project requesting access for named model. Format: `projects/{project}`

`name` `string`

Required. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisherModel}`

### Request body

The request body contains data with the following structure:

Fields

`service `**`(deprecated)`** `string`

Optional. The id links the Marketplace listing to the underlying Agent Platform model endpoint. Format: `services/{serviceId}` Format: `services/{serviceId}`

### Response body

Response message for [`ModelGardenService.EnableModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.publishers.models/enableModel#google.cloud.aiplatform.v1beta1.ModelGardenService.EnableModel) .

If successful, the response body contains data with the following structure:

Fields

`publisherEndpoint` `string`

Output only. The publisher endpoint that the project is enabled for. Format: `projects/{project}/locations/{location}/publishers/{publisher}/models/{publisherModel}`

`enablementState` `enum ( `[`EnablementState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.publishers.models/enableModel#EnablementState)` )`

Output only. The result of the model enablement.

**JSON representation**

```
{
  "publisherEndpoint": string,
  "enablementState": enum (EnablementState)
}
```

## EnablementState

state of the models.enable response.

| Enums                          |                                                                                  |
|--------------------------------|----------------------------------------------------------------------------------|
| `ENABLEMENT_STATE_UNSPECIFIED` | The PublisherModel enable status is unclear. The API will default to this value. |
| `ENABLEMENT_STATE_SUCCEEDED`   | The PublisherModel is enabled successfully.                                      |
| `ENABLEMENT_STATE_FAILED`      | The PublisherModel is failed to enable                                           |
