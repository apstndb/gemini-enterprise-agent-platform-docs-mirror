---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExamplesArrayFilter
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExamplesArrayFilter
title: ExamplesArrayFilter
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Filters for examples' array metadata fields. An array field is example metadata where multiple values are attributed to a single example.

Fields

`values[]` `string`

Required. The values by which to filter examples.

`arrayOperator` ` enum ( ArrayOperator  ` )

Required. The operator logic to use for filtering.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;values&quot;: [string],&quot;arrayOperator&quot;: enum (ArrayOperator)}</code></pre></td>
</tr>
</tbody>
</table>

## ArrayOperator

The logic to use for filtering.

Enums

`ARRAY_OPERATOR_UNSPECIFIED`

Not specified. This value should not be used.

`CONTAINS_ANY`

The metadata array field in the example must contain at least one of the values.

`CONTAINS_ALL`

The metadata array field in the example must contain all of the values.
