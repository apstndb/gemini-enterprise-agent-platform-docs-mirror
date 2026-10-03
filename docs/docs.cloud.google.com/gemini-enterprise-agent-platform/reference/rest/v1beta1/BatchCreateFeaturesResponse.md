---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchCreateFeaturesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchCreateFeaturesResponse
title: BatchCreateFeaturesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`FeaturestoreService.BatchCreateFeatures`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes.features/batchCreate#google.cloud.aiplatform.v1beta1.FeaturestoreService.BatchCreateFeatures) .

Fields

`features[]` `object ( `[`Feature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features#Feature)` )`

The Features created.

**JSON representation**

```
{
  "features": [
    {
      object (Feature)
    }
  ]
}
```
