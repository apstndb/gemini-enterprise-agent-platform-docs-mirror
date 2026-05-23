---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoGenerationModelInstance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoGenerationModelInstance
title: VideoGenerationModelInstance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

An instance for a video generation prediction request.

Fields

`prompt` `string`

A text description of the video you want to generate. The prompt should specify the subject, style, and any specific elements or actions that should appear in the video.

`image` ` object ( Image  ` )

An optional image to use as a starting point for video generation, used as the first frame of the generated video. If `image` is provided, `video` and `referenceImages` cannot be used.

`video` ` object ( Video  ` )

An optional input video to use as a starting point for video generation. If `video` is provided, `image` and `referenceImages` cannot be used. If `mask` is also provided, the input video will be edited based on the mask. If `mask` is not provided, the input video will be extended in duration.

`lastFrame` ` object ( Image  ` )

Image to use as the last frame of the generated video. This field can only be used if `image` is also provided.

`cameraControl` `string`

The camera motion to apply to the generated video. This field can only be used if `image` is also provided. Supported values: - `fixed` : No camera motion. - `pan_left` : Pan camera to the left. - `pan_right` : Pan camera to the right. - `tilt_up` : Tilt camera up. - `tilt_down` : Tilt camera down. - `truck_left` : Move camera to the left. - `truck_right` : Move camera to the right. - `pedestal_up` : Move camera up. - `pedestal_down` : Move camera down. - `push_in` : Move camera closer to the subject. - `pull_out` : Move camera away from the subject.

`mask` ` object ( Mask  ` )

An optional mask to apply to the input `video` for video editing tasks like inserting or removing objects, or outpainting.

`referenceImages[]` ` object ( ReferenceImage  ` )

Optional reference images to guide video generation. If `referenceImages` are provided, `prompt` must also be provided, and `image` , `video` , and `lastFrame` cannot be used. You can provide up to 3 `asset` images or 1 `style` image.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;prompt&quot;: string,&quot;image&quot;: {object (Image)},&quot;video&quot;: {object (Video)},&quot;lastFrame&quot;: {object (Image)},&quot;cameraControl&quot;: string,&quot;mask&quot;: {object (Mask)},&quot;referenceImages&quot;: [{object (ReferenceImage)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Image

Defines the input image format.

Fields

`mimeType` `string`

The MIME type of the image. Supported MIME types: - image/jpeg - image/png

`data` `Union type`

The image data. The image can be provided as either base64 encoded bytes or a Google Cloud Storage URI. `data` can be only one of the following:

`bytesBase64Encoded` `string`

The image bytes encoded in base64.

`gcsUri` `string`

A Google Cloud Storage URI pointing to the image file.

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

Defines the input video format.

Fields

`mimeType` `string`

The MIME type of the video. Supported MIME types: - video/mov - video/mpeg - video/mp4 - video/mpg - video/avi - video/wmv - video/mpegps - video/flv

`data` `Union type`

The video data. The video can be provided as either base64 encoded bytes or a Google Cloud Storage URI. `data` can be only one of the following:

`gcsUri` `string`

A Google Cloud Storage URI pointing to the video file.

`bytesBase64Encoded` `string`

The video bytes encoded in base64.

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
  &quot;gcsUri&quot;: string,
  &quot;bytesBase64Encoded&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## Mask

Defines the input mask format for video editing. A mask specifies regions of a video or image to modify or preserve.

Fields

`mimeType` `string`

The MIME type of the mask. Supported MIME types: - image/png - image/jpeg - image/webp - video/mov - video/mpeg - video/mp4 - video/mpg - video/avi - video/wmv - video/mpegps - video/flv

`maskMode` `string`

Specifies how the mask is applied to the input video for editing. For `insert` , `remove` , and `remove_static` modes, the mask must have the same aspect ratio as the input video. For `outpaint` mode, the mask can be 9:16 or 16:9. Supported values: - `insert` : The mask defines a rectangular region in the first frame of the input video. The object described in the `prompt` is inserted into this region and appears in subsequent frames. - `remove` : The mask identifies an object in the first frame to track and remove from the video. - `remove_static` : The mask identifies a static region in the video from which to remove objects. - `outpaint` : The mask defines a region where the input video is placed. The area outside this region is generated based on the `prompt` . Video masks are not supported for outpainting.

`data` `Union type`

The mask data. The mask can be provided as either base64 encoded bytes or a Google Cloud Storage URI. `data` can be only one of the following:

`bytesBase64Encoded` `string`

The mask bytes encoded in base64.

`gcsUri` `string`

A Google Cloud Storage URI pointing to the mask file.

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
  &quot;maskMode&quot;: string,

  // data
  &quot;bytesBase64Encoded&quot;: string,
  &quot;gcsUri&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## ReferenceImage

Defines the input reference image format. A reference image provides additional context to guide video generation, such as style or assets.

Fields

`image` ` object ( Image  ` )

The image data for the reference image.

`referenceType` `string`

The type of reference image, which defines how it influences video generation. Supported values: - `asset` : The reference image provides assets to the generated video, such as the scene, an object, or a character. - `style` : The aesthetics of the reference image (e.g., colors, lighting, texture) are used to define the style of the generated video, such as 'anime', 'photography', or 'origami'.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;image&quot;: {object (Image)},&quot;referenceType&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
