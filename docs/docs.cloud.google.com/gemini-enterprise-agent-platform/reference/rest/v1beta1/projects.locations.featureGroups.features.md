---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features
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

`valueType` `enum ( `[`ValueType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features#Feature.ValueType)` )`

Immutable. Only applicable for Agent Platform feature Store (Legacy). type of feature value.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. Only applicable for Agent Platform feature Store (Legacy). timestamp when this EntityType was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. Only applicable for Agent Platform feature Store (Legacy). timestamp when this EntityType was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your Features.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information on and examples of labels. No more than 64 user labels can be associated with one feature (System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`etag` `string`

Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`monitoringConfig `**`(deprecated)`** `object ( `[`FeaturestoreMonitoringConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeaturestoreMonitoringConfig)` )`

> This item is deprecated!

Optional. Only applicable for Agent Platform feature Store (Legacy). Deprecated: The custom monitoring configuration for this feature, if not set, use the monitoringConfig defined for the EntityType this feature belongs to. Only Features with type ( [`feature.ValueType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features#Feature.ValueType) ) BOOL, STRING, DOUBLE or INT64 can enable monitoring.

If this is populated with \[FeaturestoreMonitoringConfig.disabled\]\[\] = true, snapshot analysis monitoring is disabled; if \[FeaturestoreMonitoringConfig.monitoring_interval\]\[\] specified, snapshot analysis monitoring is enabled. Otherwise, snapshot analysis monitoring config is same as the EntityType's this feature belongs to.

`disableMonitoring` `boolean`

Optional. Only applicable for Agent Platform feature Store (Legacy). If not set, use the monitoringConfig defined for the EntityType this feature belongs to. Only Features with type ( [`feature.ValueType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features#Feature.ValueType) ) BOOL, STRING, DOUBLE or INT64 can enable monitoring.

If set to true, all types of data monitoring are disabled despite the config on EntityType.

`monitoringStats[]` `object ( `[`FeatureStatsAnomaly`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureStatsAnomaly)` )`

Output only. Only applicable for Agent Platform feature Store (Legacy). A list of historical [`SnapshotAnalysis`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeaturestoreMonitoringConfig#SnapshotAnalysis) stats requested by user, sorted by [`FeatureStatsAnomaly.start_time`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureStatsAnomaly#FIELDS.start_time) descending.

`monitoringStatsAnomalies[]` `object ( `[`MonitoringStatsAnomaly`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features#Feature.MonitoringStatsAnomaly)` )`

Output only. Only applicable for Agent Platform feature Store (Legacy). The list of historical stats and anomalies with specified objectives.

`featureStatsAndAnomaly[]` `object ( `[`FeatureStatsAndAnomaly`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureStatsAndAnomaly)` )`

Output only. Only applicable for Agent Platform feature Store. The list of historical stats and anomalies.

`versionColumnName` `string`

Only applicable for Agent Platform feature Store. The name of the BigQuery Table/View column hosting data for this version. If no value is provided, will use featureId.

`pointOfContact` `string`

Entity responsible for maintaining this feature. Can be comma separated list of email addresses or URIs.

**JSON representation**

```
{
  "name": string,
  "description": string,
  "valueType": enum (ValueType),
  "createTime": string,
  "updateTime": string,
  "labels": {
    string: string,
    ...
  },
  "etag": string,
  "monitoringConfig": {
    object (FeaturestoreMonitoringConfig)
  },
  "disableMonitoring": boolean,
  "monitoringStats": [
    {
      object (FeatureStatsAnomaly)
    }
  ],
  "monitoringStatsAnomalies": [
    {
      object (MonitoringStatsAnomaly)
    }
  ],
  "featureStatsAndAnomaly": [
    {
      object (FeatureStatsAndAnomaly)
    }
  ],
  "versionColumnName": string,
  "pointOfContact": string
}
```

### ValueType

Only applicable for Agent Platform Legacy feature Store. An enum representing the value type of a feature.

| Enums                    |                                             |
|--------------------------|---------------------------------------------|
| `VALUE_TYPE_UNSPECIFIED` | The value type is unspecified.              |
| `BOOL`                   | Used for feature that is a boolean.         |
| `BOOL_ARRAY`             | Used for feature that is a list of boolean. |
| `DOUBLE`                 | Used for feature that is double.            |
| `DOUBLE_ARRAY`           | Used for feature that is a list of double.  |
| `INT64`                  | Used for feature that is INT64.             |
| `INT64_ARRAY`            | Used for feature that is a list of INT64.   |
| `STRING`                 | Used for feature that is string.            |
| `STRING_ARRAY`           | Used for feature that is a list of String.  |
| `BYTES`                  | Used for feature that is bytes.             |
| `STRUCT`                 | Used for feature that is struct.            |

### MonitoringStatsAnomaly

A list of historical [`SnapshotAnalysis`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeaturestoreMonitoringConfig#SnapshotAnalysis) or [`ImportFeaturesAnalysis`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeaturestoreMonitoringConfig#ImportFeaturesAnalysis) stats requested by user, sorted by [`FeatureStatsAnomaly.start_time`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureStatsAnomaly#FIELDS.start_time) descending.

Fields

`objective` `enum ( `[`Objective`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features#Feature.Objective)` )`

Output only. The objective for each stats.

`featureStatsAnomaly` `object ( `[`FeatureStatsAnomaly`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureStatsAnomaly)` )`

Output only. The stats and anomalies generated at specific timestamp.

**JSON representation**

```
{
  "objective": enum (Objective),
  "featureStatsAnomaly": {
    object (FeatureStatsAnomaly)
  }
}
```

### Objective

If the objective in the request is both Import feature Analysis and Snapshot Analysis, this objective could be one of them. Otherwise, this objective should be the same as the objective in the request.

| Enums                     |                                                               |
|---------------------------|---------------------------------------------------------------|
| `OBJECTIVE_UNSPECIFIED`   | If it's OBJECTIVE_UNSPECIFIED, monitoringStats will be empty. |
| `IMPORT_FEATURE_ANALYSIS` | Stats are generated by Import feature Analysis.               |
| `SNAPSHOT_ANALYSIS`       | Stats are generated by Snapshot Analysis.                     |

| Methods                                                                                                                                                      |                                                      |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|
| [`batchCreate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/batchCreate) | Creates a batch of Features in a given FeatureGroup. |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/create)           | Creates a new Feature in a given FeatureGroup.       |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/delete)           | Deletes a single Feature.                            |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/get)                 | Gets details of a single Feature.                    |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/list)               | Lists Features in a given FeatureGroup.              |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/patch)             | Updates the parameters of a single Feature.          |
