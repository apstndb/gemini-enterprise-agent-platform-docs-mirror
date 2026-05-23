---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/create
title: 'Method: featureViews.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.create

Creates a new FeatureView in a given FeatureOnlineStore.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /featureViews`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the FeatureOnlineStore to create FeatureViews. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}`

### Query parameters

`featureViewId` `string`

Required. The id to use for the FeatureView, which will become the final component of the FeatureView's resource name.

This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.

The value must be unique within a FeatureOnlineStore.

`runSyncImmediately` `boolean`

Immutable. If set to true, one on demand sync will be run immediately, regardless whether the `  FeatureView.sync_config  ` is configured or not.

### Request body

The request body contains an instance of `  FeatureView  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
