---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureValue
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureValue
title: FeatureValue
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

value for a feature.

Fields

`metadata` ` object ( Metadata  ` )

metadata of feature value.

`value` `Union type`

Value for the feature. `value` can be only one of the following:

`boolValue` `boolean`

Bool type feature value.

`doubleValue` `number`

Double type feature value.

`int64Value` `string ( int64 format)`

Int64 feature value.

`stringValue` `string`

String feature value.

`boolArrayValue` ` object ( BoolArray  ` )

A list of bool type feature value.

`doubleArrayValue` ` object ( DoubleArray  ` )

A list of double type feature value.

`int64ArrayValue` ` object ( Int64Array  ` )

A list of int64 type feature value.

`stringArrayValue` ` object ( StringArray  ` )

A list of string type feature value.

`bytesValue` `string ( bytes format)`

Bytes feature value.

A base64-encoded string.

`structValue` ` object ( StructValue  ` )

A struct type feature value.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metadata&quot;: {object (Metadata)},// value&quot;boolValue&quot;: boolean,&quot;doubleValue&quot;: number,&quot;int64Value&quot;: string,&quot;stringValue&quot;: string,&quot;boolArrayValue&quot;: {object (BoolArray)},&quot;doubleArrayValue&quot;: {object (DoubleArray)},&quot;int64ArrayValue&quot;: {object (Int64Array)},&quot;stringArrayValue&quot;: {object (StringArray)},&quot;bytesValue&quot;: string,&quot;structValue&quot;: {object (StructValue)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## BoolArray

A list of boolean values.

Fields

`values[]` `boolean`

A list of bool values.

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
  &quot;values&quot;: [
    boolean
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## DoubleArray

A list of double values.

Fields

`values[]` `number`

A list of double values.

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
  &quot;values&quot;: [
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## Int64Array

A list of int64 values.

Fields

`values[]` `string ( int64 format)`

A list of int64 values.

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
  &quot;values&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## StringArray

A list of string values.

Fields

`values[]` `string`

A list of string values.

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
  &quot;values&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## StructValue

Struct (or object) type feature value.

Fields

`values[]` ` object ( StructFieldValue  ` )

A list of field values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;values&quot;: [{object (StructFieldValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## StructFieldValue

One field of a Struct (or object) type feature value.

Fields

`name` `string`

name of the field in the struct feature.

`value` ` object ( FeatureValue  ` )

The value for this field.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;value&quot;: {object (FeatureValue)}}</code></pre></td>
</tr>
</tbody>
</table>

## Metadata

metadata of feature value.

Fields

`generateTime` ` string ( Timestamp  ` format)

feature generation timestamp. Typically, it is provided by user at feature ingestion time. If not, feature store will use the system timestamp when the data is ingested into feature store.

Legacy feature Store: For streaming ingestion, the time, aligned by days, must be no older than five years (1825 days) and no later than one year (366 days) in the future.

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
  &quot;generateTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
