---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/undeployIndex
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/undeployIndex
title: 'Method: indexEndpoints.undeployIndex'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.indexEndpoints.undeployIndex

Undeploys an Index from an IndexEndpoint, removing a DeployedIndex from it, and freeing all resources it's using.

### Endpoint

post `https: / /{service-endpoint} /v1 /{indexEndpoint}:undeployIndex`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`indexEndpoint` `string`

Required. The name of the IndexEndpoint resource from which to undeploy an Index. Format: `projects/{project}/locations/{location}/indexEndpoints/{indexEndpoint}`

### Request body

The request body contains data with the following structure:

Fields

`deployedIndexId` `string`

Required. The id of the DeployedIndex to be undeployed from the IndexEndpoint.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
