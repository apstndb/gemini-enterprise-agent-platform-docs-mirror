---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureSelectionConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureSelectionConfig
title: FeatureSelectionConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

feature selection configuration for the FeatureMonitor.

Fields

`featureConfigs[]` ` object ( FeatureConfig  ` )

Optional. A list of features to be monitored and each feature's drift threshold.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureConfigs&quot;: [{object (FeatureConfig)}]}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureConfig

feature configuration.

Fields

`featureId` `string`

Required. The id of the feature resource. Final component of the feature's resource name.

`driftThreshold` `number`

Optional. Drift threshold. If calculated difference with baseline data larger than threshold, it will be considered as the feature has drift. If not present, the threshold will be default to 0.3. Must be in range \[0, 1).

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;featureId&quot;: string,
  &quot;driftThreshold&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
