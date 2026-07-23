---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelInstance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelInstance
title: VirtualTryOnModelInstance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Media generation input format for the Virtual Try On model.

Fields

`prompt` `string`

The text prompt describing the desired image.

`productImages[]` ` object ( ProductImage  ` )

Required. A single product image to try on the person.

`personImage` ` object ( PersonImage  ` )

The image of the person to virtually try-on clothing.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;prompt&quot;: string,&quot;productImages&quot;: [{object (ProductImage)}],&quot;personImage&quot;: {object (PersonImage)}}</code></pre></td>
</tr>
</tbody>
</table>

## ProductImage

A ProductImage is used to provide the product image and its associated configuration options for Virtual Try On.

Fields

`image` ` object ( Image  ` )

Required. An image of a product to virtually try on a person. The following values are supported: - A `bytesBase64` encoded string that encodes the image. - A `gcsUri` string URI to a Google Cloud Storage bucket location.

`maskImage` ` object ( Image  ` )

(Optional) The mask image associated with this product. If provided, the mask image is used to guide the image editing.

`productImageConfig` ` object ( ProductImageConfig  ` )

The configuration for the product image.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;image&quot;: {object (Image)},&quot;maskImage&quot;: {object (Image)},&quot;productImageConfig&quot;: {object (ProductImageConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## Image

Represents the input image and metadata for virtual try-on.

Fields

`mimeType` `string`

The MIME type of the image. The following values are supported: - image/jpeg - image/png

`data` `Union type`

Image content for virtual try-on. The following values are supported: - A `bytesBase64` encoded string that encodes the image. - A `gcsUri` string URI to a Google Cloud Storage bucket location. `data` can be only one of the following:

`bytesBase64Encoded` `string`

The base64-encoded bytes of the image.

`gcsUri` `string`

The Google Cloud Storage URI of the image. The URI must be in `gs://` format.

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

## ProductImageConfig

Configuration for the product image.

Fields

`maskMode` ` enum ( MaskMode  ` )

Mode used to control the segmentation logic.

`dilation` `number`

(Optional) Factor for dilating the mask. Valid values are in \[0.0, 1.0\]. If unset, dilation defaults to `0` .

`productDescription` `string`

(Optional) A text description of the product.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;maskMode&quot;: enum (MaskMode),&quot;dilation&quot;: number,&quot;productDescription&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## PersonImage

An image of a person. The model generates a virtual try-on image with the supplied image of the person wearing the garments from `productImages` .

Fields

`image` ` object ( Image  ` )

Required. An image of a person to try-on the clothing product. The following values are supported: - A `bytesBase64` encoded string that encodes the image. - A `gcsUri` string URI to a Google Cloud Storage bucket location.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;image&quot;: {object (Image)}}</code></pre></td>
</tr>
</tbody>
</table>
