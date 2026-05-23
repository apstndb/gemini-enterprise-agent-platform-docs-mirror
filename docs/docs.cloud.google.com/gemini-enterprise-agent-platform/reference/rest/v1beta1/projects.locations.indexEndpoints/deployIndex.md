---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexEndpoints/deployIndex
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexEndpoints/deployIndex
title: 'Method: indexEndpoints.deployIndex'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.indexEndpoints.deployIndex

Deploys an Index into this IndexEndpoint, creating a DeployedIndex within it.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{indexEndpoint}:deployIndex`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`indexEndpoint` `string`

Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: `projects/{project}/locations/{location}/indexEndpoints/{indexEndpoint}`

### Request body

The request body contains data with the following structure:

Fields

`deployedIndex` ` object ( DeployedIndex  ` )

Required. The DeployedIndex to be created within the IndexEndpoint.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
