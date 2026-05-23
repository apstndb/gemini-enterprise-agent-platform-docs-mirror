---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features
title: 'REST Resource: projects.locations.featureGroups.features'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Feature

feature metadata information. For example, color is a feature that describes an apple.

Fields

`name` `string`

Immutable. name of the feature. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}/features/{feature}` `projects/{project}/locations/{location}/featureGroups/{featureGroup}/features/{feature}`

The last part feature is assigned by the client. The feature can be up to 64 characters long and can consist only of ASCII Latin letters A-Z and a-z, underscore(\_), and ASCII digits 0-9 starting with a letter. The value will be unique given an entity type.

`description` `string`

description of the feature.

`valueType` ` enum ( ValueType  ` )

Immutable. Only applicable for Agent Platform feature Store (Legacy). type of feature value.

`createTime` ` string ( Timestamp  ` format)

Output only. Only applicable for Agent Platform feature Store (Legacy). timestamp when this EntityType was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. Only applicable for Agent Platform feature Store (Legacy). timestamp when this EntityType was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your Features.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information on and examples of labels. No more than 64 user labels can be associated with one feature (System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`etag` `string`

Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`disableMonitoring` `boolean`

Optional. Only applicable for Agent Platform feature Store (Legacy). If not set, use the monitoringConfig defined for the EntityType this feature belongs to. Only Features with type ( `  feature.ValueType  ` ) BOOL, STRING, DOUBLE or INT64 can enable monitoring.

If set to true, all types of data monitoring are disabled despite the config on EntityType.

`monitoringStatsAnomalies[]` ` object ( MonitoringStatsAnomaly  ` )

Output only. Only applicable for Agent Platform feature Store (Legacy). The list of historical stats and anomalies with specified objectives.

`versionColumnName` `string`

Only applicable for Agent Platform feature Store. The name of the BigQuery Table/View column hosting data for this version. If no value is provided, will use featureId.

`pointOfContact` `string`

Entity responsible for maintaining this feature. Can be comma separated list of email addresses or URIs.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;description&quot;: string,&quot;valueType&quot;: enum (ValueType),&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;labels&quot;: {string: string,...},&quot;etag&quot;: string,&quot;disableMonitoring&quot;: boolean,&quot;monitoringStatsAnomalies&quot;: [{object (MonitoringStatsAnomaly)}],&quot;versionColumnName&quot;: string,&quot;pointOfContact&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

### ValueType

Only applicable for Agent Platform Legacy feature Store. An enum representing the value type of a feature.

Enums

`VALUE_TYPE_UNSPECIFIED`

The value type is unspecified.

`BOOL`

Used for feature that is a boolean.

`BOOL_ARRAY`

Used for feature that is a list of boolean.

`DOUBLE`

Used for feature that is double.

`DOUBLE_ARRAY`

Used for feature that is a list of double.

`INT64`

Used for feature that is INT64.

`INT64_ARRAY`

Used for feature that is a list of INT64.

`STRING`

Used for feature that is string.

`STRING_ARRAY`

Used for feature that is a list of String.

`BYTES`

Used for feature that is bytes.

`STRUCT`

Used for feature that is struct.

### MonitoringStatsAnomaly

A list of historical `  SnapshotAnalysis  ` or `  ImportFeaturesAnalysis  ` stats requested by user, sorted by `  FeatureStatsAnomaly.start_time  ` descending.

Fields

`objective` ` enum ( Objective  ` )

Output only. The objective for each stats.

`featureStatsAnomaly` ` object ( FeatureStatsAnomaly  ` )

Output only. The stats and anomalies generated at specific timestamp.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;objective&quot;: enum (Objective),&quot;featureStatsAnomaly&quot;: {object (FeatureStatsAnomaly)}}</code></pre></td>
</tr>
</tbody>
</table>

### Objective

If the objective in the request is both Import feature Analysis and Snapshot Analysis, this objective could be one of them. Otherwise, this objective should be the same as the objective in the request.

Enums

`OBJECTIVE_UNSPECIFIED`

If it's OBJECTIVE\_UNSPECIFIED, monitoringStats will be empty.

`IMPORT_FEATURE_ANALYSIS`

Stats are generated by Import feature Analysis.

`SNAPSHOT_ANALYSIS`

Stats are generated by Snapshot Analysis.

### FeatureStatsAnomaly

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

## Methods

### `            batchCreate           `

Creates a batch of Features in a given FeatureGroup.

### `            create           `

Creates a new Feature in a given FeatureGroup.

### `            delete           `

Deletes a single Feature.

### `            get           `

Gets details of a single Feature.

### `            list           `

Lists Features in a given FeatureGroup.

### `            patch           `

Updates the parameters of a single Feature.
