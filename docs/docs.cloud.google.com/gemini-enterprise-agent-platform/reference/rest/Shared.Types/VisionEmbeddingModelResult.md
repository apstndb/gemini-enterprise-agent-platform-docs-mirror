---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelResult
title: VisionEmbeddingModelResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The prediction result for a large vision model embedding request. An embedding is a vectorized representation of data such as image, text or video. The embeddings produced by this model can be used for tasks such as image retrieval, similarity comparison, and classification. The embedding vectors have 1024 dimensions.

Fields

`imageEmbedding` ` array ( ListValue  ` format)

The embedding generated from the input image. This field is populated if the prediction request contained an image.

`textEmbedding` ` array ( ListValue  ` format)

The embedding generated from the input text. This field is populated if the prediction request contained text.

`videoEmbeddings[]` ` object ( VideoEmbedding  ` )

The embeddings generated from the input video. This field is populated if the prediction request contained a video. The video is divided into 1-second segments, and an embedding is generated for each segment.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;imageEmbedding&quot;: array,&quot;textEmbedding&quot;: array,&quot;videoEmbeddings&quot;: [{object (VideoEmbedding)}]}</code></pre></td>
</tr>
</tbody>
</table>

## VideoEmbedding

Contains embedding data for a specific time segment of a video.

Fields

`startOffsetSec` `integer`

The start time of the video segment that this embedding represents, measured in seconds from the beginning of the video.

`endOffsetSec` `integer`

The end time of the video segment that this embedding represents, measured in seconds from the beginning of the video.

`embedding` ` array ( ListValue  ` format)

The 1024-dimension embedding vector for this video segment.

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
  &quot;startOffsetSec&quot;: integer,
  &quot;endOffsetSec&quot;: integer,
  &quot;embedding&quot;: array
}</code></pre></td>
</tr>
</tbody>
</table>
