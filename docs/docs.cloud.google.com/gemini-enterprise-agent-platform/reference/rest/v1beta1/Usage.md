---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage
title: Usage
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Statistics on the interaction request's token usage.

Fields

`totalInputTokens` `integer`

Number of tokens in the prompt (context).

`inputTokensByModality[]` ` object ( ModalityTokens  ` )

A breakdown of input token usage by modality.

`totalCachedTokens` `integer`

Number of tokens in the cached part of the prompt (the cached content).

`cachedTokensByModality[]` ` object ( ModalityTokens  ` )

A breakdown of cached token usage by modality.

`totalOutputTokens` `integer`

Total number of tokens across all the generated responses.

`outputTokensByModality[]` ` object ( ModalityTokens  ` )

A breakdown of output token usage by modality.

`totalToolUseTokens` `integer`

Number of tokens present in tool-use prompt(s).

`toolUseTokensByModality[]` ` object ( ModalityTokens  ` )

A breakdown of tool-use token usage by modality.

`totalThoughtTokens` `integer`

Number of tokens of thoughts for thinking models.

`totalTokens` `integer`

Total token count for the interaction request (prompt + responses + other internal tokens).

`groundingToolCount[]` ` object ( GroundingToolCount  ` )

Grounding tool count.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;totalInputTokens&quot;: integer,&quot;inputTokensByModality&quot;: [{object (ModalityTokens)}],&quot;totalCachedTokens&quot;: integer,&quot;cachedTokensByModality&quot;: [{object (ModalityTokens)}],&quot;totalOutputTokens&quot;: integer,&quot;outputTokensByModality&quot;: [{object (ModalityTokens)}],&quot;totalToolUseTokens&quot;: integer,&quot;toolUseTokensByModality&quot;: [{object (ModalityTokens)}],&quot;totalThoughtTokens&quot;: integer,&quot;totalTokens&quot;: integer,&quot;groundingToolCount&quot;: [{object (GroundingToolCount)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ModalityTokens

The token count for a single response modality.

Fields

`modality` ` enum ( ResponseModality  ` )

The modality associated with the token count.

`tokens` `integer`

Number of tokens for the modality.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modality&quot;: enum (ResponseModality),&quot;tokens&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

## GroundingToolCount

The number of grounding tool counts.

Fields

`type` ` enum ( Type  ` )

The grounding tool type associated with the count.

`count` `integer`

The number of grounding tool counts.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (Type),&quot;count&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

## Type

The type of grounding tool.

Enums

`TYPE_UNSPECIFIED`

Default value. This value is unused.

`GOOGLE_SEARCH`

Grounding with Google Web Search and Image Search, & Web Grounding for Enterprise.

`GOOGLE_MAPS`

Grounding with Google Maps.

`RETRIEVAL`

Grounding with customer's data, for example, VertexAISearch.
