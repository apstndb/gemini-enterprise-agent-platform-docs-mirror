---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/sync
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/sync
title: 'Method: featureViews.sync'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.sync

Triggers on-demand sync for the FeatureView.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{featureView}:sync`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`featureView` `string`

Required. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`

### Request body

The request body must be empty.

### Response body

Response message for [`FeatureOnlineStoreAdminService.SyncFeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/sync#google.cloud.aiplatform.v1beta1.FeatureOnlineStoreAdminService.SyncFeatureView) .

If successful, the response body contains data with the following structure:

Fields

`featureViewSync` `string`

Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}/featureViewSyncs/{featureViewSync}`

**JSON representation**

```
{
  "featureViewSync": string
}
```
