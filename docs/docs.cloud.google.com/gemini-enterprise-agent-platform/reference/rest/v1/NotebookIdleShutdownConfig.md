---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NotebookIdleShutdownConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NotebookIdleShutdownConfig
title: NotebookIdleShutdownConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The idle shutdown configuration of NotebookRuntimeTemplate, which contains the idleTimeout as required field.

Fields

`idleTimeout` ` string ( Duration  ` format)

Required. Duration is accurate to the second. In Notebook, Idle Timeout is accurate to minute so the range of idleTimeout (second) is: 10 \* 60 \~ 1440 \* 60.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`idleShutdownDisabled` `boolean`

Whether Idle Shutdown is disabled in this NotebookRuntimeTemplate.

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
  &quot;idleTimeout&quot;: string,
  &quot;idleShutdownDisabled&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>
