---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileParsingConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileParsingConfig
title: RagFileParsingConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Specifies the parsing config for RagFiles.

Fields

` useAdvancedPdfParsing (deprecated)  ` `boolean`

> This item is deprecated\!

Whether to use advanced PDF parsing.

`parser` `Union type`

The parser to use for RagFiles. `parser` can be only one of the following:

`advancedParser` ` object ( AdvancedParser  ` )

The Advanced Parser to use for RagFiles.

`layoutParser` ` object ( LayoutParser  ` )

The Layout Parser to use for RagFiles.

`llmParser` ` object ( LlmParser  ` )

The LLM Parser to use for RagFiles.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;useAdvancedPdfParsing&quot;: boolean,// parser&quot;advancedParser&quot;: {object (AdvancedParser)},&quot;layoutParser&quot;: {object (LayoutParser)},&quot;llmParser&quot;: {object (LlmParser)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## AdvancedParser

Specifies the advanced parsing for RagFiles.

Fields

`useAdvancedPdfParsing` `boolean`

Whether to use advanced PDF parsing.

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
  &quot;useAdvancedPdfParsing&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## LayoutParser

Document AI Layout Parser config.

Fields

`processorName` `string`

The full resource name of a Document AI processor or processor version. The processor must have type `LAYOUT_PARSER_PROCESSOR` . If specified, the `additionalConfig.parse_as_scanned_pdf` field must be false. Format: \* `projects/{projectId}/locations/{location}/processors/{processorId}` \* `projects/{projectId}/locations/{location}/processors/{processorId}/processorVersions/{processor_version_id}`

`maxParsingRequestsPerMin` `integer`

The maximum number of requests the job is allowed to make to the Document AI processor per minute. Consult <https://cloud.google.com/document-ai/quotas> and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 120 QPM would be used.

`globalMaxParsingRequestsPerMin` `integer`

The maximum number of requests the job is allowed to make to the Document AI processor per minute in this project. Consult <https://cloud.google.com/document-ai/quotas> and the Quota page for your project to set an appropriate value here. If this value is not specified, maxParsingRequestsPerMin will be used by indexing pipeline as the global limit.

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
  &quot;processorName&quot;: string,
  &quot;maxParsingRequestsPerMin&quot;: integer,
  &quot;globalMaxParsingRequestsPerMin&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
