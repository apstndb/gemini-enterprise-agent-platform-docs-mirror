---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes.features/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes.features/create
title: 'Method: features.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.features.create

Creates a new feature in a given EntityType.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /features`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the EntityType or FeatureGroup to create a feature. Format for entityType as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` Format for featureGroup as parent: `projects/{project}/locations/{location}/featureGroups/{featureGroup}`

### Query parameters

`featureId` `string`

Required. The id to use for the feature, which will become the final component of the feature's resource name.

This value may be up to 128 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.

The value must be unique within an EntityType/FeatureGroup.

### Request body

The request body contains an instance of `  Feature  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
