---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FlexStart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FlexStart
title: FlexStart
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

FlexStart is used to schedule the deployment workload on DWS resource. It contains the max duration of the deployment.

Fields

`maxRuntimeDuration` ` string ( Duration  ` format)

The max duration of the deployment is maxRuntimeDuration. The deployment will be terminated after the duration. The maxRuntimeDuration can be set up to 7 days.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

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
  &quot;maxRuntimeDuration&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
