---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelInstance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelInstance
title: VisionEmbeddingModelInstance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Input format for requesting embeddings from vision models. An embedding is a list of numbers that represents the semantic meaning of text, an image, or a video. Embeddings can be used for many applications, like searching for similar images or getting recommendations. Each instance must specify exactly one of `text` , `image` , or `video` field.

Fields

`image` ` object ( Image  ` )

An image to generate embeddings for.

`text` `string`

Text to generate embeddings for.

`video` ` object ( Video  ` )

A video to generate embeddings for.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;image&quot;: {object (Image)},&quot;text&quot;: string,&quot;video&quot;: {object (Video)}}</code></pre></td>
</tr>
</tbody>
</table>

## Image

Represents an image input for embedding generation.

Fields

`mimeType` `string`

The MIME type of the image.

The supported MIME types are:

  - `image/jpeg`
  - `image/png`

`data` `Union type`

`data` can be only one of the following:

`bytesBase64Encoded` `string`

Base64-encoded bytes of the image.

`gcsUri` `string`

A Cloud Storage URI pointing to the image file. Format: `gs://bucket/object`

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
  &quot;mimeType&quot;: string,

  // data
  &quot;bytesBase64Encoded&quot;: string,
  &quot;gcsUri&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## Video

Represents a video input for embedding generation.

Fields

`videoSegmentConfig` ` object ( VideoSegmentConfig  ` )

Configuration for processing a video segment. If specified, embeddings are generated for the segment. If not specified, embeddings are generated for the entire video.

`data` `Union type`

`data` can be only one of the following:

`bytesBase64Encoded` `string`

Base64-encoded bytes of the video.

`gcsUri` `string`

A Cloud Storage URI pointing to the video file. Format: `gs://bucket/object`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;videoSegmentConfig&quot;: {object (VideoSegmentConfig)},// data&quot;bytesBase64Encoded&quot;: string,&quot;gcsUri&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## VideoSegmentConfig

Configuration for processing a segment of a video.

Fields

`startOffsetSec` `integer`

The start offset of the video segment in seconds.

`endOffsetSec` `integer`

The end offset of the video segment in seconds.

`intervalSec` `integer`

The interval of the video for which the embedding will be generated. The minimum value for `intervalSec` is 4. If the interval is less than 4, an `InvalidArgumentError` is returned. There are no limitations on the maximum value of the interval. However, if the interval is larger than `min(videoLength, 120s)` , it might affect the quality of the generated embeddings.

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
  &quot;intervalSec&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
