---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoClassificationPredictionParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoClassificationPredictionParams
title: VideoClassificationPredictionParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction model parameters for Video Classification.

Fields

`confidenceThreshold` `number`

The Model only returns predictions with at least this confidence score. Default value is 0.0

`maxPredictions` `integer`

The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10,000.

`segmentClassification` `boolean`

Set to true to request segment-level classification. Agent Platform returns labels and their confidence scores for the entire time segment of the video that user specified in the input instance. Default value is true

`shotClassification` `boolean`

Set to true to request shot-level classification. Agent Platform determines the boundaries for each camera shot in the entire time segment of the video that user specified in the input instance. Agent Platform then returns labels and their confidence scores for each detected shot, along with the start and end time of the shot. WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false

`oneSecIntervalClassification` `boolean`

Set to true to request classification for a video at one-second intervals. Agent Platform returns labels and their confidence scores for each second of the entire time segment of the video that user specified in the input WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false

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
  &quot;confidenceThreshold&quot;: number,
  &quot;maxPredictions&quot;: integer,
  &quot;segmentClassification&quot;: boolean,
  &quot;shotClassification&quot;: boolean,
  &quot;oneSecIntervalClassification&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>
