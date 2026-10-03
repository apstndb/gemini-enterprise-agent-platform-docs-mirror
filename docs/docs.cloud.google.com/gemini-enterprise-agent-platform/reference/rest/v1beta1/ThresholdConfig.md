---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ThresholdConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ThresholdConfig
title: ThresholdConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The config for feature monitoring threshold.

Fields

`threshold` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`value` `number`

Specify a threshold value that can trigger the alert. If this threshold config is for feature distribution distance: 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. Each feature must have a non-zero threshold if they need to be monitored. Otherwise no alert will be triggered for that feature.

End of mutually exclusive fields.

**JSON representation**

```
{

  // threshold
  "value": number
  // Union type
}
```
