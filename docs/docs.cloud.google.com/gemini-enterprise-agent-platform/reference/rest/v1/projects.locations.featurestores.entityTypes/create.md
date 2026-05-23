---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/create
title: 'Method: entityTypes.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.create

Creates a new EntityType in a given Featurestore.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /entityTypes`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Featurestore to create EntityTypes. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`

### Query parameters

`entityTypeId` `string`

Required. The id to use for the EntityType, which will become the final component of the EntityType's resource name.

This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.

The value must be unique within a featurestore.

### Request body

The request body contains an instance of `  EntityType  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
