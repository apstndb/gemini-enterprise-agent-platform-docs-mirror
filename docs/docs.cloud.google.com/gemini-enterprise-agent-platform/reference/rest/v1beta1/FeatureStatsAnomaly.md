---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureStatsAnomaly
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureStatsAnomaly
title: FeatureStatsAnomaly
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Stats and Anomaly generated at specific timestamp for specific feature. The startTime and endTime are used to define the time range of the dataset that current stats belongs to, e.g. prediction traffic is bucketed into prediction datasets by time window. If the Dataset is not defined by time window, startTime = endTime. timestamp of the stats and anomalies always refers to endTime. Raw stats and anomalies are stored in statsUri or anomalyUri in the tensorflow defined protos. Field dataStats contains almost identical information with the raw stats in Agent Platform defined proto, for UI to display.

Fields

`score` `number`

feature importance score, only populated when cross-feature monitoring is enabled. For now only used to represent feature attribution score within range \[0, 1\] for `  ModelDeploymentMonitoringObjectiveType.FEATURE_ATTRIBUTION_SKEW  ` and `  ModelDeploymentMonitoringObjectiveType.FEATURE_ATTRIBUTION_DRIFT  ` .

`statsUri` `string`

Path of the stats file for current feature values in Cloud Storage bucket. Format: gs:// / /stats. Example: gs://monitoring\_bucket/featureName/stats. Stats are stored as binary format with Protobuf message [tensorflow.metadata.v0.FeatureNameStatistics](https://github.com/tensorflow/metadata/blob/master/tensorflow_metadata/proto/v0/statistics.proto) .

`anomalyUri` `string`

Path of the anomaly file for current feature values in Cloud Storage bucket. Format: gs:// / /anomalies. Example: gs://monitoring\_bucket/featureName/anomalies. Stats are stored as binary format with Protobuf message Anoamlies are stored as binary format with Protobuf message [tensorflow.metadata.v0.AnomalyInfo](https://github.com/tensorflow/metadata/blob/master/tensorflow_metadata/proto/v0/anomalies.proto) .

`distributionDeviation` `number`

Deviation from the current stats to baseline stats. 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence.

`anomalyDetectionThreshold` `number`

This is the threshold used when detecting anomalies. The threshold can be changed by user, so this one might be different from `  ThresholdConfig.value  ` .

`startTime` ` string ( Timestamp  ` format)

The start timestamp of window where stats were generated. For objectives where time window doesn't make sense (e.g. Featurestore Snapshot Monitoring), startTime is only used to indicate the monitoring intervals, so it always equals to (endTime - monitoringInterval).

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

The end timestamp of window where stats were generated. For objectives where time window doesn't make sense (e.g. Featurestore Snapshot Monitoring), endTime indicates the timestamp of the data used to generate stats (e.g. timestamp we take snapshots for feature values).

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

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
  &quot;score&quot;: number,
  &quot;statsUri&quot;: string,
  &quot;anomalyUri&quot;: string,
  &quot;distributionDeviation&quot;: number,
  &quot;anomalyDetectionThreshold&quot;: number,
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
