---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ListFeaturesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ListFeaturesResponse
title: ListFeaturesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`FeaturestoreService.ListFeatures`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes.features/list#google.cloud.aiplatform.v1beta1.FeaturestoreService.ListFeatures) . Response message for [`FeatureRegistryService.ListFeatures`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/list#google.cloud.aiplatform.v1beta1.FeatureRegistryService.ListFeatures) .

Fields

`features[]` `object ( `[`Feature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features#Feature)` )`

The Features matching the request.

`nextPageToken` `string`

A token, which can be sent as [`ListFeaturesRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/list#body.QUERY_PARAMETERS.page_token) to retrieve the next page. If this field is omitted, there are no subsequent pages.

**JSON representation**

```
{
  "features": [
    {
      object (Feature)
    }
  ],
  "nextPageToken": string
}
```
