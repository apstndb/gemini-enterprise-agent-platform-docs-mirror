---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources/create
title: 'Method: persistentResources.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.persistentResources.create

Creates a PersistentResource.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /persistentResources`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to create the PersistentResource in. Format: `projects/{project}/locations/{location}`

### Query parameters

`persistentResourceId` `string`

Required. The id to use for the PersistentResource, which become the final component of the PersistentResource's resource name.

The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .

### Request body

The request body contains an instance of `  PersistentResource  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
