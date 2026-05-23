---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiRequestReadConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiRequestReadConfig
title: GeminiRequestReadConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Configuration for how to read Gemini requests from a multimodal dataset.

Fields

`read_config` `Union type`

The read config for the dataset. `read_config` can be only one of the following:

`templateConfig` ` object ( GeminiTemplateConfig  ` )

Gemini request template with placeholders.

`assembledRequestColumnName` `string`

Optional. column name in the dataset table that contains already fully assembled Gemini requests.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// read_config&quot;templateConfig&quot;: {object (GeminiTemplateConfig)},&quot;assembledRequestColumnName&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## GeminiTemplateConfig

Template configuration to create Gemini examples from a multimodal dataset.

Fields

`geminiExample` ` object ( GeminiExample  ` )

Required. The template that will be used for assembling the request to use for downstream applications.

`fieldMapping` `map (key: string, value: string)`

Required. Map of template parameters to the columns in the dataset table.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;geminiExample&quot;: {object (GeminiExample)},&quot;fieldMapping&quot;: {string: string,...}}</code></pre></td>
</tr>
</tbody>
</table>
