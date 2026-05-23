---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/delete
title: 'Method: featurestores.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.delete

Deletes a single Featurestore. The Featurestore must not contain any EntityTypes or `force` must be set to true for the request to succeed.

### Endpoint

delete `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the Featurestore to be deleted. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`

### Query parameters

`force` `boolean`

If set to true, any EntityTypes and Features for this Featurestore will also be deleted. (Otherwise, the request will only work if the Featurestore has no EntityTypes.)

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
