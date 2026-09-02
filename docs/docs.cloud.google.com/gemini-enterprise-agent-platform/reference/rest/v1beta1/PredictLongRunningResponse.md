---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictLongRunningResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictLongRunningResponse
title: PredictLongRunningResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for \[PredictionService.PredictLongRunning\]

Fields

`response` `Union type`

The response of the long running operation. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`generateVideoResponse` ` object ( GenerateVideoResponse  ` )

The response of the video generation prediction.

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// response&quot;generateVideoResponse&quot;: {object (GenerateVideoResponse)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>
