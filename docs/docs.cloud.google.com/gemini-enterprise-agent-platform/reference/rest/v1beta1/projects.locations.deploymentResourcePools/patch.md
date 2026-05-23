---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.deploymentResourcePools/patch
title: 'Method: deploymentResourcePools.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.deploymentResourcePools.patch

Update a DeploymentResourcePool.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{deploymentResourcePool.name}`  

`PATCH https://{service-endpoint}/v1beta1/{deploymentResourcePool.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`deploymentResourcePool.name` `string`

Immutable. The resource name of the DeploymentResourcePool. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deploymentResourcePool}`

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. The list of fields to update.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  DeploymentResourcePool  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
