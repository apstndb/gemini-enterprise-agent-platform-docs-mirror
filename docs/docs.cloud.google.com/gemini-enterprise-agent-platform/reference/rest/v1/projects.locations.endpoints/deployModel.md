---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel
title: 'Method: endpoints.deployModel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.deployModel

Deploys a Model into this Endpoint, creating a DeployedModel within it.

### Endpoint

post `https: / /{service-endpoint} /v1 /{endpoint}:deployModel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint resource into which to deploy a Model. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains data with the following structure:

Fields

`deployedModel` ` object ( DeployedModel  ` )

Required. The DeployedModel to be created within the Endpoint. Note that `  Endpoint.traffic_split  ` must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via `  EndpointService.UpdateEndpoint  ` .

`trafficSplit` `map (key: string, value: integer)`

A map from a DeployedModel's id to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel.

If this field is non-empty, then the Endpoint's `  trafficSplit  ` will be overwritten with it. To refer to the id of the just being deployed Model, a "0" should be used, and the actual id of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100.

If this field is empty, then the Endpoint's `  trafficSplit  ` is not updated.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
