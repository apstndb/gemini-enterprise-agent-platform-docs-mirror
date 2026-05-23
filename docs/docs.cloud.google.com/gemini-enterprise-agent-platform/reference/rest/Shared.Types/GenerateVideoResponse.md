---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GenerateVideoResponse
title: GenerateVideoResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Generate video response.

Fields

`generatedSamples[]` ` object ( Media  ` )

The generates samples.

`raiMediaFilteredCount` `integer`

Returns if any videos were filtered due to RAI policies.

`raiMediaFilteredReasons[]` `string`

Returns rai failure reasons if any.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;generatedSamples&quot;: [{object (Media)}],&quot;raiMediaFilteredCount&quot;: integer,&quot;raiMediaFilteredReasons&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

## Media

Media.

Fields

`type` `Union type`

`type` can be only one of the following:

`image` ` object ( Image  ` )

Image.

`video` ` object ( Video  ` )

Video

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// type&quot;image&quot;: {object (Image)},&quot;video&quot;: {object (Video)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Image

Image.

Fields

`encoding` `string`

Image encoding, encoded as "image/png" or "image/jpg".

`imageRaiScores` ` object ( ImageRAIScores  ` )

RAI scores for generated image.

`raiInfo` ` object ( RaiInfo  ` )

RAI info for image.

`semanticFilterResponse` ` object ( SemanticFilterResponse  ` )

Semantic filter info for image.

`text` `string`

Text/Expanded text input for imagen.

`imageSize` ` object ( ImageSize  ` )

Image size. The size of the image. Can be self reported, or computed from the image bytes.

`content` `Union type`

`content` can be only one of the following:

`image` `string ( bytes format)`

Raw bytes.

A base64-encoded string.

`uri` `string`

Path to another storage (typically Google Cloud Storage).

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;encoding&quot;: string,&quot;imageRaiScores&quot;: {object (ImageRAIScores)},&quot;raiInfo&quot;: {object (RaiInfo)},&quot;semanticFilterResponse&quot;: {object (SemanticFilterResponse)},&quot;text&quot;: string,&quot;imageSize&quot;: {object (ImageSize)},// content&quot;image&quot;: string,&quot;uri&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ImageRAIScores

RAI scores for generated image returned.

Fields

`agileWatermarkDetectionScore` `number`

Agile watermark score for image.

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
  &quot;agileWatermarkDetectionScore&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## RaiInfo

Next id: 6

Fields

`raiCategories[]` `string`

List of rai categories' information to return

`scores[]` `number`

List of rai scores mapping to the rai categories. Rounded to 1 decimal place.

`blockedEntities[]` `string`

List of blocked entities from the blocklist if it is detected.

`modelName` `string`

The model name used to indexing into the RaiFilterConfig map. Would either be one of <imagegeneration@002-006> , imagen-3.0-... api endpoint names, or internal names used for mapping to different filter configs (genselfie, ai\_watermark) than its api endpoint.

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
  &quot;raiCategories&quot;: [
    string
  ],
  &quot;scores&quot;: [
    number
  ],
  &quot;blockedEntities&quot;: [
    string
  ],
  &quot;modelName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## SemanticFilterResponse

Fields

`passedSemanticFilter` `boolean`

This response is added when semantic filter config is turned on in EditConfig. It reports if this image is passed semantic filter response. If passedSemanticFilter is false, the bounding box information will be populated for user to check what caused the semantic filter to fail.

`namedBoundingBoxes[]` ` object ( NamedBoundingBox  ` )

Class labels of the bounding boxes that failed the semantic filtering. Bounding box coordinates.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;passedSemanticFilter&quot;: boolean,&quot;namedBoundingBoxes&quot;: [{object (NamedBoundingBox)}]}</code></pre></td>
</tr>
</tbody>
</table>

## NamedBoundingBox

Fields

`x1` `number`

`x2` `number`

`y1` `number`

`y2` `number`

`classes[]` `string`

`entities[]` `string`

`scores[]` `number`

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
  &quot;x1&quot;: number,
  &quot;x2&quot;: number,
  &quot;y1&quot;: number,
  &quot;y2&quot;: number,
  &quot;classes&quot;: [
    string
  ],
  &quot;entities&quot;: [
    string
  ],
  &quot;scores&quot;: [
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## ImageSize

Image size.

Fields

`width` `integer`

`height` `integer`

`channels` `integer`

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
  &quot;width&quot;: integer,
  &quot;height&quot;: integer,
  &quot;channels&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## Video

Video

Fields

`encoding` `string`

Video encoding, for example "video/mp4".

`text` `string`

Text/Expanded text input for Help Me Write.

`content` `Union type`

`content` can be only one of the following:

`video` `string ( bytes format)`

Raw bytes.

A base64-encoded string.

`uri` `string`

Path to another storage (typically Google Cloud Storage).

`encodedVideo` `string`

Base 64 encoded video bytes.

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
  &quot;encoding&quot;: string,
  &quot;text&quot;: string,

  // content
  &quot;video&quot;: string,
  &quot;uri&quot;: string,
  &quot;encodedVideo&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>
