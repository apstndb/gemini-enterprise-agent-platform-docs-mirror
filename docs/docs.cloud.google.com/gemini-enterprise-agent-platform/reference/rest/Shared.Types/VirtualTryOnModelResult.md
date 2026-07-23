---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelResult
title: VirtualTryOnModelResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents the output of a Virtual Try-On prediction.

Fields

`images[]` ` object ( Image  ` )

A list of generated images. The number of images returned is equal to the `sampleCount` parameter provided in the request.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;images&quot;: [{object (Image)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Image

Contains a generated image or information about why the image was filtered out.

Fields

`mimeType` `string`

The MIME type of the generated image.

Supported values are: \* `image/png` \* `image/jpeg`

`data` `Union type`

The generated image data or filtering reason. `data` can be only one of the following:

`bytesBase64Encoded` `string`

The generated image encoded as a base64 encoded bytes string.

`gcsUri` `string`

The Google Cloud Storage URI where the generated image is stored.

`raiFilteredReason` `string`

The reason why the generated image was filtered out by Responsible AI checks. If this field is present, no image is returned.

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
  &quot;gcsUri&quot;: string,
  &quot;raiFilteredReason&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>
