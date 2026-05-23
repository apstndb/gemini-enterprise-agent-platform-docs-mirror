---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes.features
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes.features
title: 'REST Resource: projects.locations.featurestores.entityTypes.features'
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

## Methods

### `            batchCreate           `

Creates a batch of Features in a given EntityType.

### `            create           `

Creates a new Feature in a given EntityType.

### `            delete           `

Deletes a single Feature.

### `            get           `

Gets details of a single Feature.

### `            list           `

Lists Features in a given EntityType.

### `            patch           `

Updates the parameters of a single Feature.
