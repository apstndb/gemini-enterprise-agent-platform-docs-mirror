---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DirectContentsSource
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DirectContentsSource
title: DirectContentsSource
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a direct source of content from which to generate the memories.

Fields

`events[]` ` object ( Event  ` )

Required. The source content (i.e. chat history) to generate memories from.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;events&quot;: [{object (Event)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Event

A single piece of conversation from which to generate memories.

Fields

`content` ` object ( Content  ` )

Required. A single piece of content from which to generate memories.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;content&quot;: {object (Content)}}</code></pre></td>
</tr>
</tbody>
</table>
