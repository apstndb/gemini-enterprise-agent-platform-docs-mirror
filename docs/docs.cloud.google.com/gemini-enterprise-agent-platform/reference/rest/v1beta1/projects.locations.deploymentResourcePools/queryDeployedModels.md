---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/queryDeployedModels
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/queryDeployedModels
title: 'Method: deploymentResourcePools.queryDeployedModels'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.deploymentResourcePools.queryDeployedModels

List DeployedModels that have been deployed on this DeploymentResourcePool.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{deploymentResourcePool}:queryDeployedModels`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`deploymentResourcePool` `string`

Required. The name of the target DeploymentResourcePool to query. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deploymentResourcePool}`

### Query parameters

`pageSize` `integer`

The maximum number of DeployedModels to return. The service may return fewer than this value.

`pageToken` `string`

A page token, received from a previous `deploymentResourcePools.queryDeployedModels` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `deploymentResourcePools.queryDeployedModels` must match the call that provided the page token.

### Request body

The request body must be empty.

### Response body

Response message for deploymentResourcePools.queryDeployedModels method.

If successful, the response body contains data with the following structure:

Fields

`deployedModels[] `**`(deprecated)`** `object ( `[`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints#DeployedModel)` )`

> This item is deprecated!

DEPRECATED Use deployedModelRefs instead.

`nextPageToken` `string`

A token, which can be sent as `pageToken` to retrieve the next page. If this field is omitted, there are no subsequent pages.

`deployedModelRefs[]` `object ( `[`DeployedModelRef`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.DeployedModelRef)` )`

References to the DeployedModels that share the specified deploymentResourcePool.

`totalDeployedModelCount` `integer`

The total number of DeployedModels on this DeploymentResourcePool.

`totalEndpointCount` `integer`

The total number of endpoints that have DeployedModels on this DeploymentResourcePool.

**JSON representation**

```
{
  "deployedModels": [
    {
      object (DeployedModel)
    }
  ],
  "nextPageToken": string,
  "deployedModelRefs": [
    {
      object (DeployedModelRef)
    }
  ],
  "totalDeployedModelCount": integer,
  "totalEndpointCount": integer
}
```
