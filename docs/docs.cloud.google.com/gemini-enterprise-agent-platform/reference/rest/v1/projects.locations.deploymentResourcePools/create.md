---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.deploymentResourcePools/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.deploymentResourcePools/create
title: 'Method: deploymentResourcePools.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.deploymentResourcePools.create

Create a DeploymentResourcePool.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /deploymentResourcePools`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent location resource where this DeploymentResourcePool will be created. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`deploymentResourcePool` ` object ( DeploymentResourcePool  ` )

Required. The DeploymentResourcePool to create.

`deploymentResourcePoolId` `string`

Required. The id to use for the DeploymentResourcePool, which will become the final component of the DeploymentResourcePool's resource name.

The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
