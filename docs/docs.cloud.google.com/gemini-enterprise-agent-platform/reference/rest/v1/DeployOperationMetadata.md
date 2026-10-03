---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployOperationMetadata
title: DeployOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation information for [`ModelGardenService.Deploy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/deploy#google.cloud.aiplatform.v1.ModelGardenService.Deploy) .

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenericOperationMetadata)` )`

The operation generic information.

`publisherModel` `string`

Output only. The name of the model resource.

`destination` `string`

Output only. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`

`projectNumber` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The project number where the deploy model request is sent.

`modelId` `string`

Output only. The model id to be used at query time.

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "publisherModel": string,
  "destination": string,
  "projectNumber": string,
  "modelId": string
}
```
