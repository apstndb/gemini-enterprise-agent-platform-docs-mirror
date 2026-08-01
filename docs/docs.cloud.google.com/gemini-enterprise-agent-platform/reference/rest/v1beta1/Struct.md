---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct
title: Struct
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

`Struct` represents a structured data value, consisting of fields which map to dynamically typed values.

Fields

`fields[]` ` object ( Field  ` )

Dynamically typed fields. List instead of map because LLMs are sensitive to ordering, and we want to give users full control.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;fields&quot;: [{object (Field)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Field

Represents a single field in a struct.

Fields

`name` `string`

`value` ` object ( Value  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;value&quot;: {object (Value)}}</code></pre></td>
</tr>
</tbody>
</table>
