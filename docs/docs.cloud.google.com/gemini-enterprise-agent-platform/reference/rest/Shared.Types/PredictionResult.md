---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PredictionResult
title: PredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a line of JSONL in the batch prediction output file.

Fields

`prediction` ` value ( Value  ` format)

The prediction result. value is used here instead of Any so that JsonFormat does not append an extra "@type" field when we convert the proto to JSON and so we can represent array of objects. Do not set error if this is set.

`error` ` object ( Error  ` )

The error result. Do not set prediction if this is set.

`input` `Union type`

Some identifier from the input so that the prediction can be mapped back to the input instance. `input` can be only one of the following:

`instance` ` object ( Struct  ` format)

user's input instance. Struct is used here instead of Any so that JsonFormat does not append an extra "@type" field when we convert the proto to JSON.

`key` `string`

Optional user-provided key from the input instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;prediction&quot;: value,&quot;error&quot;: {object (Error)},// input&quot;instance&quot;: {object},&quot;key&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Error

Fields

`status` ` enum ( Code  ` )

Error status. This will be serialized into the enum name e.g. "NOT\_FOUND".

`message` `string`

Error message with additional details.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;status&quot;: enum (Code),&quot;message&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
