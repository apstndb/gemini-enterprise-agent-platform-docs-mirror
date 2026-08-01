---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value
title: Value
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

`value` represents a dynamically typed value which can be either null, a number, a string, a boolean, a recursive struct value, or a list of values. A producer of value is expected to set one of these variants. Absence of any variant indicates an error.

Fields

`kind` `Union type`

The kind of value. `kind` can be only one of the following:

`nullValue` `null`

Represents a null value.

`numberValue` `number`

Represents a double value.

`stringValue` `string`

Represents a string value.

`boolValue` `boolean`

Represents a boolean value.

`structValue` ` object ( Struct  ` )

Represents a structured value.

`listValue` ` object ( ListValue  ` )

Represents a repeated `value` .

`contentValue` ` object ( Content  ` )

Represents rich content (text, image, etc.).

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// kind&quot;nullValue&quot;: null,&quot;numberValue&quot;: number,&quot;stringValue&quot;: string,&quot;boolValue&quot;: boolean,&quot;structValue&quot;: {object (Struct)},&quot;listValue&quot;: {object (ListValue)},&quot;contentValue&quot;: {object (Content)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ListValue

`ListValue` is a wrapper around a repeated field of values.

Fields

`values[]` ` object ( Value  ` )

Repeated field of dynamically typed values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;values&quot;: [{object (Value)}]}</code></pre></td>
</tr>
</tbody>
</table>
