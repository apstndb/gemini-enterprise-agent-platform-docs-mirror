---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featurestores.entityTypes
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
