---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/delete
title: 'Method: featureOnlineStores.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.delete

Deletes a single FeatureOnlineStore. The FeatureOnlineStore must not contain any FeatureViews.

### Endpoint

delete `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the FeatureOnlineStore to be deleted. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}`

### Query parameters

`force` `boolean`

If set to true, any FeatureViews and Features for this FeatureOnlineStore will also be deleted. (Otherwise, the request will only work if the FeatureOnlineStore has no FeatureViews.)

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
