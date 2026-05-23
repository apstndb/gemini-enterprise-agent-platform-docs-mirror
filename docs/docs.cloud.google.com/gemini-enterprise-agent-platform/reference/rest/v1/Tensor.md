---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Tensor
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Tensor
title: Tensor
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A tensor value type.

Fields

`dtype` ` enum ( DataType  ` )

The data type of tensor.

`shape[]` `string ( int64 format)`

Shape of the tensor.

`boolVal[]` `boolean`

type specific representations that make it easy to create tensor protos in all languages. Only the representation corresponding to "dtype" can be set. The values hold the flattened representation of the tensor in row major order.

`  BOOL  `

`stringVal[]` `string`

`  STRING  `

`bytesVal[]` `string ( bytes format)`

`  STRING  `

A base64-encoded string.

`floatVal[]` `number`

`  FLOAT  `

`doubleVal[]` `number`

`  DOUBLE  `

`intVal[]` `integer`

`  INT_8  ` `  INT_16  ` `  INT_32  `

`int64Val[]` `string ( int64 format)`

`  INT64  `

`uintVal[]` `integer ( uint32 format)`

`  UINT8  ` `  UINT16  ` `  UINT32  `

`uint64Val[]` `string`

`  UINT64  `

`listVal[]` ` object ( Tensor  ` )

A list of tensor values.

`structVal` ` map (key: string, value: object ( Tensor  ` ))

A map of string to tensor.

`tensorVal` `string ( bytes format)`

Serialized raw tensor content.

A base64-encoded string.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dtype&quot;: enum (DataType),&quot;shape&quot;: [string],&quot;boolVal&quot;: [boolean],&quot;stringVal&quot;: [string],&quot;bytesVal&quot;: [string],&quot;floatVal&quot;: [number],&quot;doubleVal&quot;: [number],&quot;intVal&quot;: [integer],&quot;int64Val&quot;: [string],&quot;uintVal&quot;: [integer],&quot;uint64Val&quot;: [string],&quot;listVal&quot;: [{object (Tensor)}],&quot;structVal&quot;: {string: {object (Tensor)},...},&quot;tensorVal&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## DataType

data type of the tensor.

Enums

`DATA_TYPE_UNSPECIFIED`

Not a legal value for datatype. Used to indicate a datatype field has not been set.

`BOOL`

data types that all computation devices are expected to be capable to support.

`STRING`

`FLOAT`

`DOUBLE`

`INT8`

`INT16`

`INT32`

`INT64`

`UINT8`

`UINT16`

`UINT32`

`UINT64`
