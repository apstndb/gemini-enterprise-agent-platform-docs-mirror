---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/undeployModel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/undeployModel
title: 'Method: endpoints.undeployModel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.undeployModel

Undeploys a Model from an Endpoint, removing a DeployedModel from it, and freeing all resources it's using.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint}:undeployModel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint resource from which to undeploy a Model. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains data with the following structure:

Fields

`deployedModelId` `string`

Required. The id of the DeployedModel to be undeployed from the Endpoint.

`trafficSplit` `map (key: string, value: integer)`

If this field is provided, then the Endpoint's `  trafficSplit  ` will be overwritten with it. If last DeployedModel is being undeployed from the Endpoint, the \[Endpoint.traffic\_split\] will always end up empty when this call returns. A DeployedModel will be successfully undeployed only if it doesn't have any traffic assigned to it when this method executes, or if this field unassigns any traffic to it.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
