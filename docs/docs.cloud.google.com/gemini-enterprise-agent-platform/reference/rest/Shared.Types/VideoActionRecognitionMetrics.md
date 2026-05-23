---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionRecognitionMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionRecognitionMetrics
title: VideoActionRecognitionMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Model evaluation metrics for video action recognition.

Fields

`videoActionMetrics[]` ` object ( VideoActionMetrics  ` )

The metric entries for precision window lengths: 1s,2s,3s.

`evaluatedActionCount` `integer`

The number of ground truth actions used to create this evaluation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;videoActionMetrics&quot;: [{object (VideoActionMetrics)}],&quot;evaluatedActionCount&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>
