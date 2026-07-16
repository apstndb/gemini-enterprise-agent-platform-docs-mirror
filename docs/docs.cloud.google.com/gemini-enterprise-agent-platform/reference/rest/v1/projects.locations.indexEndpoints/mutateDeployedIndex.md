---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/mutateDeployedIndex
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexEndpoints/mutateDeployedIndex
title: 'Method: indexEndpoints.mutateDeployedIndex'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.indexEndpoints.mutateDeployedIndex

Update an existing DeployedIndex under an IndexEndpoint.

### Endpoint

post `https: / /{service-endpoint} /v1 /{indexEndpoint}:mutateDeployedIndex`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`indexEndpoint` `string`

Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: `projects/{project}/locations/{location}/indexEndpoints/{indexEndpoint}`

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. The update mask applies to the resource. The supported paths are `automaticResources` , `dedicatedResources` , `enableAccessLogging` and `deployedIndexAuthConfig` . When omitted, the service will perform a full update of all fields. See `  google.protobuf.FieldMask  ` .

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  DeployedIndex  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
