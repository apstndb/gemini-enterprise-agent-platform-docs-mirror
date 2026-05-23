---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes
title: 'REST Resource: projects.locations.featurestores.entityTypes'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: EntityType

An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver.

Fields

`name` `string`

Immutable. name of the EntityType. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}`

The last part entityType is assigned by the client. The entityType can be up to 64 characters long and can consist only of ASCII Latin letters A-Z and a-z and underscore(\_), and ASCII digits 0-9 starting with a letter. The value will be unique given a featurestore.

`description` `string`

Optional. description of the EntityType.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this EntityType was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this EntityType was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your EntityTypes.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information on and examples of labels. No more than 64 user labels can be associated with one EntityType (System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`etag` `string`

Optional. Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`monitoringConfig` ` object ( FeaturestoreMonitoringConfig  ` )

Optional. The default monitoring configuration for all Features with value type ( `  feature.ValueType  ` ) BOOL, STRING, DOUBLE or INT64 under this EntityType.

If this is populated with \[FeaturestoreMonitoringConfig.monitoring\_interval\] specified, snapshot analysis monitoring is enabled. Otherwise, snapshot analysis monitoring is disabled.

`offlineStorageTtlDays` `integer`

Optional. Config for data retention policy in offline storage. TTL in days for feature values that will be stored in offline storage. The feature Store offline storage periodically removes obsolete feature values older than `offlineStorageTtlDays` since the feature generation time. If unset (or explicitly set to 0), default to 4000 days TTL.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;description&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;labels&quot;: {string: string,...},&quot;etag&quot;: string,&quot;monitoringConfig&quot;: {object (FeaturestoreMonitoringConfig)},&quot;offlineStorageTtlDays&quot;: integer,&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## FeaturestoreMonitoringConfig

Configuration of how features in Featurestore are monitored.

Fields

`snapshotAnalysis` ` object ( SnapshotAnalysis  ` )

The config for Snapshot Analysis Based feature Monitoring.

`importFeaturesAnalysis` ` object ( ImportFeaturesAnalysis  ` )

The config for ImportFeatures Analysis Based feature Monitoring.

`numericalThresholdConfig` ` object ( ThresholdConfig  ` )

Threshold for numerical features of anomaly detection. This is shared by all objectives of Featurestore Monitoring for numerical features (i.e. Features with type ( `  feature.ValueType  ` ) DOUBLE or INT64).

`categoricalThresholdConfig` ` object ( ThresholdConfig  ` )

Threshold for categorical features of anomaly detection. This is shared by all types of Featurestore Monitoring for categorical features (i.e. Features with type ( `  feature.ValueType  ` ) BOOL or STRING).

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;snapshotAnalysis&quot;: {object (SnapshotAnalysis)},&quot;importFeaturesAnalysis&quot;: {object (ImportFeaturesAnalysis)},&quot;numericalThresholdConfig&quot;: {object (ThresholdConfig)},&quot;categoricalThresholdConfig&quot;: {object (ThresholdConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## SnapshotAnalysis

Configuration of the Featurestore's Snapshot Analysis Based Monitoring. This type of analysis generates statistics for each feature based on a snapshot of the latest feature value of each entities every monitoringInterval.

Fields

`disabled` `boolean`

The monitoring schedule for snapshot analysis. For EntityType-level config: unset / disabled = true indicates disabled by default for Features under it; otherwise by default enable snapshot analysis monitoring with monitoringInterval for Features under it. feature-level config: disabled = true indicates disabled regardless of the EntityType-level config; unset monitoringInterval indicates going with EntityType-level config; otherwise run snapshot analysis monitoring with monitoringInterval regardless of the EntityType-level config. Explicitly Disable the snapshot analysis based monitoring.

`monitoringIntervalDays` `integer`

Configuration of the snapshot analysis based monitoring pipeline running interval. The value indicates number of days.

`stalenessDays` `integer`

Customized export features time window for snapshot analysis. Unit is one day. Default value is 3 weeks. Minimum value is 1 day. Maximum value is 4000 days.

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
  &quot;disabled&quot;: boolean,
  &quot;monitoringIntervalDays&quot;: integer,
  &quot;stalenessDays&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## ImportFeaturesAnalysis

Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each feature imported by every `  entityTypes.importFeatureValues  ` operation.

Fields

`state` ` enum ( State  ` )

Whether to enable / disable / inherite default hebavior for import features analysis.

`anomalyDetectionBaseline` ` enum ( Baseline  ` )

The baseline used to do anomaly detection for the statistics generated by import features analysis.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;state&quot;: enum (State),&quot;anomalyDetectionBaseline&quot;: enum (Baseline)}</code></pre></td>
</tr>
</tbody>
</table>

## State

The state defines whether to enable ImportFeature analysis.

Enums

`STATE_UNSPECIFIED`

Should not be used.

`DEFAULT`

The default behavior of whether to enable the monitoring. EntityType-level config: disabled. feature-level config: inherited from the configuration of EntityType this feature belongs to.

`ENABLED`

Explicitly enables import features analysis. EntityType-level config: by default enables import features analysis for all Features under it. feature-level config: enables import features analysis regardless of the EntityType-level config.

`DISABLED`

Explicitly disables import features analysis. EntityType-level config: by default disables import features analysis for all Features under it. feature-level config: disables import features analysis regardless of the EntityType-level config.

## Baseline

Defines the baseline to do anomaly detection for feature values imported by each `  entityTypes.importFeatureValues  ` operation.

Enums

`BASELINE_UNSPECIFIED`

Should not be used.

`LATEST_STATS`

Choose the later one statistics generated by either most recent snapshot analysis or previous import features analysis. If non of them exists, skip anomaly detection and only generate a statistics.

`MOST_RECENT_SNAPSHOT_STATS`

Use the statistics generated by the most recent snapshot analysis if exists.

`PREVIOUS_IMPORT_FEATURES_STATS`

Use the statistics generated by the previous import features analysis if exists.

## ThresholdConfig

The config for Featurestore Monitoring threshold.

Fields

`threshold` `Union type`

`threshold` can be only one of the following:

`value` `number`

Specify a threshold value that can trigger the alert. 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. Each feature must have a non-zero threshold if they need to be monitored. Otherwise no alert will be triggered for that feature.

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

  // threshold
  &quot;value&quot;: number
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates a new EntityType in a given Featurestore.

### `            delete           `

Deletes a single EntityType.

### `            deleteFeatureValues           `

Delete Feature values from Featurestore.

### `            exportFeatureValues           `

Exports Feature values from all the entities of a target EntityType.

### `            get           `

Gets details of a single EntityType.

### `            getIamPolicy           `

Gets the access control policy for a resource.

### `            importFeatureValues           `

Imports Feature values into the Featurestore from a source storage.

### `            list           `

Lists EntityTypes in a given Featurestore.

### `            patch           `

Updates the parameters of a single EntityType.

### `            readFeatureValues           `

Reads Feature values of a specific entity of an EntityType.

### `            setIamPolicy           `

Sets the access control policy on the specified resource.

### `            streamingReadFeatureValues           `

Reads Feature values for multiple entities.

### `            testIamPermissions           `

Returns permissions that a caller has on the specified resource.

### `            writeFeatureValues           `

Writes Feature values of one or more entities of an EntityType.
