---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/list
title: 'Method: deploymentResourcePools.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.deploymentResourcePools.list

List DeploymentResourcePools in a location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /deploymentResourcePools`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent Location which owns this collection of DeploymentResourcePools. Format: `projects/{project}/locations/{location}`

### Query parameters

`pageSize` `integer`

The maximum number of DeploymentResourcePools to return. The service may return fewer than this value.

`pageToken` `string`

A page token, received from a previous `deploymentResourcePools.list` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `deploymentResourcePools.list` must match the call that provided the page token.

### Request body

The request body must be empty.

### Response body

Response message for deploymentResourcePools.list method.

If successful, the response body contains data with the following structure:

Fields

`deploymentResourcePools[]` `object ( `[`DeploymentResourcePool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools#DeploymentResourcePool)` )`

The DeploymentResourcePools from the specified location.

`nextPageToken` `string`

A token, which can be sent as `pageToken` to retrieve the next page. If this field is omitted, there are no subsequent pages.

**JSON representation**

```
{
  "deploymentResourcePools": [
    {
      object (DeploymentResourcePool)
    }
  ],
  "nextPageToken": string
}
```
