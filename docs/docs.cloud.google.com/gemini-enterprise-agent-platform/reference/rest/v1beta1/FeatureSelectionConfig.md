---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureSelectionConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureSelectionConfig
title: FeatureSelectionConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

feature selection configuration for the FeatureMonitor.

Fields

`featureConfigs[]` `object ( `[`FeatureConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureSelectionConfig#FeatureConfig)` )`

Optional. A list of features to be monitored and each feature's drift threshold.

**JSON representation**

```
{
  "featureConfigs": [
    {
      object (FeatureConfig)
    }
  ]
}
```

## FeatureConfig

feature configuration.

Fields

`featureId` `string`

Required. The id of the feature resource. Final component of the feature's resource name.

`driftThreshold` `number`

Optional. Drift threshold. If calculated difference with baseline data larger than threshold, it will be considered as the feature has drift. If not present, the threshold will be default to 0.3. Must be in range \[0, 1).

**JSON representation**

```
{
  "featureId": string,
  "driftThreshold": number
}
```
