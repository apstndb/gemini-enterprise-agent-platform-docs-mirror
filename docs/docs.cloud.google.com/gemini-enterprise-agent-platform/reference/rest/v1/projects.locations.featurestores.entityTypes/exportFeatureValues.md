---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/exportFeatureValues
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores.entityTypes/exportFeatureValues
title: 'Method: entityTypes.exportFeatureValues'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.entityTypes.exportFeatureValues

Exports feature values from all the entities of a target EntityType.

### Endpoint

post `https: / /{service-endpoint} /v1 /{entityType}:exportFeatureValues`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`entityType` `string`

Required. The resource name of the EntityType from which to export feature values. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}`

### Request body

The request body contains data with the following structure:

Fields

`destination` ` object ( FeatureValueDestination  ` )

Required. Specifies destination location and format.

`featureSelector` ` object ( FeatureSelector  ` )

Required. Selects Features to export values of.

`settings[]` ` object ( DestinationFeatureSetting  ` )

Per-feature export settings.

`mode` `Union type`

Required. The mode in which Feature values are exported. `mode` can be only one of the following:

`snapshotExport` ` object ( SnapshotExport  ` )

Exports the latest feature values of all entities of the EntityType within a time range.

`fullExport` ` object ( FullExport  ` )

Exports all historical values of all entities of the EntityType within a time range

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## SnapshotExport

Describes exporting the latest feature values of all entities of the EntityType between \[startTime, snapshotTime\].

Fields

`snapshotTime` ` string ( Timestamp  ` format)

Exports feature values as of this timestamp. If not set, retrieve values as of now. timestamp, if present, must not have higher than millisecond precision.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime` ` string ( Timestamp  ` format)

Excludes feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in feature Store. timestamp, if present, must not have higher than millisecond precision.

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
  &quot;snapshotTime&quot;: string,
  &quot;startTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## FullExport

Describes exporting all historical feature values of all entities of the EntityType between \[startTime, endTime\].

Fields

`startTime` ` string ( Timestamp  ` format)

Excludes feature values with feature generation timestamp before this timestamp. If not set, retrieve oldest values kept in feature Store. timestamp, if present, must not have higher than millisecond precision.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

Exports feature values as of this timestamp. If not set, retrieve values as of now. timestamp, if present, must not have higher than millisecond precision.

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
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
