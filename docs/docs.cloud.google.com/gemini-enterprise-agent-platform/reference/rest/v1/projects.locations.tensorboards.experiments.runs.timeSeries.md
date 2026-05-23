---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries
title: 'REST Resource: projects.locations.tensorboards.experiments.runs.timeSeries'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: TensorboardTimeSeries

TensorboardTimeSeries maps to times series produced in training runs

Fields

`name` `string`

Output only. name of the TensorboardTimeSeries.

`displayName` `string`

Required. user provided name of this TensorboardTimeSeries. This value should be unique among all TensorboardTimeSeries resources belonging to the same TensorboardRun resource (parent resource).

`description` `string`

description of this TensorboardTimeSeries.

`valueType` ` enum ( ValueType  ` )

Required. Immutable. type of TensorboardTimeSeries value.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this TensorboardTimeSeries was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this TensorboardTimeSeries was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`pluginName` `string`

Immutable. name of the plugin this time series pertain to. Such as Scalar, Tensor, blob

`pluginData` `string ( bytes format)`

data of the current plugin, with the size limited to 65KB.

A base64-encoded string.

`metadata` ` object ( Metadata  ` )

Output only. Scalar, Tensor, or blob metadata for this TensorboardTimeSeries.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;valueType&quot;: enum (ValueType),&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;pluginName&quot;: string,&quot;pluginData&quot;: string,&quot;metadata&quot;: {object (Metadata)}}</code></pre></td>
</tr>
</tbody>
</table>

## ValueType

An enum representing the value type of a TensorboardTimeSeries.

Enums

`VALUE_TYPE_UNSPECIFIED`

The value type is unspecified.

`SCALAR`

Used for TensorboardTimeSeries that is a list of scalars. E.g. accuracy of a model over epochs/time.

`TENSOR`

Used for TensorboardTimeSeries that is a list of tensors. E.g. histograms of weights of layer in a model over epoch/time.

`BLOB_SEQUENCE`

Used for TensorboardTimeSeries that is a list of blob sequences. E.g. set of sample images with labels over epochs/time.

## Metadata

Describes metadata for a TensorboardTimeSeries.

Fields

`maxStep` `string ( int64 format)`

Output only. Max step index of all data points within a TensorboardTimeSeries.

`maxWallTime` ` string ( Timestamp  ` format)

Output only. Max wall clock timestamp of all data points within a TensorboardTimeSeries.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`maxBlobSequenceLength` `string ( int64 format)`

Output only. The largest blob sequence length (number of blobs) of all data points in this time series, if its ValueType is BLOB\_SEQUENCE.

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
  &quot;maxStep&quot;: string,
  &quot;maxWallTime&quot;: string,
  &quot;maxBlobSequenceLength&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates a TensorboardTimeSeries.

### `            delete           `

Deletes a TensorboardTimeSeries.

### `            exportTensorboardTimeSeries           `

Exports a TensorboardTimeSeries' data.

### `            get           `

Gets a TensorboardTimeSeries.

### `            list           `

Lists TensorboardTimeSeries in a Location.

### `            patch           `

Updates a TensorboardTimeSeries.

### `            read           `

Reads a TensorboardTimeSeries' data.

### `            readBlobData           `

Gets bytes of TensorboardBlobs.
