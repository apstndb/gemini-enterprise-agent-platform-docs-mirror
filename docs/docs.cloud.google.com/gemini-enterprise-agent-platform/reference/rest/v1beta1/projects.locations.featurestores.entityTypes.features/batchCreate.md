---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes.features/batchCreate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes.features/batchCreate
title: 'Method: features.batchCreate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.features.batchCreate

Creates a batch of Features in a given EntityType.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /features:batchCreate`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` `projects/{project}/locations/{location}/featureGroups/{featureGroup}`

### Request body

The request body contains data with the following structure:

Fields

`requests[]` ` object ( CreateFeatureRequest  ` )

Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The `parent` field in each child request message can be omitted. If `parent` is set in a child request, then the value must match the `parent` value in this request message.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
