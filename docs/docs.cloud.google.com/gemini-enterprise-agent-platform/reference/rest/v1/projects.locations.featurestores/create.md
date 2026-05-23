---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/create
title: 'Method: featurestores.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.create

Creates a new Featurestore in a given project and location.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /featurestores`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to create Featurestores. Format: `projects/{project}/locations/{location}`

### Query parameters

`featurestoreId` `string`

Required. The id to use for this Featurestore, which will become the final component of the Featurestore's resource name.

This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.

The value must be unique within the project and location.

### Request body

The request body contains an instance of `  Featurestore  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
