---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/delete
title: 'Method: entityTypes.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.delete

Deletes a single EntityType. The EntityType must not have any Features or `force` must be set to true for the request to succeed.

### Endpoint

delete `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the EntityType to be deleted. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}`

### Query parameters

`force` `boolean`

If set to true, any Features for this EntityType will also be deleted. (Otherwise, the request will only work if the EntityType has no Features.)

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
