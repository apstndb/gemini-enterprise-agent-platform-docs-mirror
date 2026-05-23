---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoClassificationPredictionInstance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoClassificationPredictionInstance
title: VideoClassificationPredictionInstance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction input format for Video Classification.

Fields

`content` `string`

The Google Cloud Storage location of the video on which to perform the prediction.

`mimeType` `string`

The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime

`timeSegmentStart` `string`

The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision.

`timeSegmentEnd` `string`

The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video.

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
  &quot;content&quot;: string,
  &quot;mimeType&quot;: string,
  &quot;timeSegmentStart&quot;: string,
  &quot;timeSegmentEnd&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
