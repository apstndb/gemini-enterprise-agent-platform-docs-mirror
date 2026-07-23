---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelParams
title: VirtualTryOnModelParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents the parameters for a Virtual Try-On prediction request.

Fields

`outputOptions` ` object ( OutputOptions  ` )

Options for configuring the output image format.

`sampleCount` `integer`

The number of images to generate. Accepted values are in the range \[1,4\].

If not set, defaults to `1` .

`storageUri` `string`

The Google Cloud Storage location where the generated images are stored.

`seed` `integer`

The random seed for image generation. This avoids randomness in generating the output images.

If a `  seed  ` value is provided, `  addWatermark  ` must be set to `false` .

`baseSteps` `integer`

The number of diffusion steps to run. The higher the number of steps, the higher the quality of the generated image, but the greater the latency.

If not set, defaults to `32` .

`safetySetting` `string`

Safety filter level for generated images. The filter blocks images that contain objectionable content.

The following values are supported:

  - `block-low-and-above` : Strongest filtering level, most strict blocking.
  - `block-medium-and-above` : Block some problematic content prompts and responses.
  - `block-only-high` : Reduces the number of requests blocked due to safety filters. May increase objectionable content in generated images.
  - `block-none` : Block very few problematic prompts and responses. Access to this feature is restricted.

If not set, defaults to `block_medium_and_above` .

`personGeneration` `string`

Controls whether or not faces or people are included in generated images.

The following values are supported:

  - `dont-allow` : Disallow the inclusion of faces or people in generated images.
  - `allow-adult` : Allow generation of adults only.
  - `allow-all` : Allow generation of people of all ages.

If not set, defaults to `allow-adult` .

`addWatermark` `boolean`

Whether to add a watermark to the generated images.

If not set, defaults to `true` .

`enhancePrompt` `boolean`

Whether to enhance the user-provided prompt internally for models that support it.

If not set, defaults to `true` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outputOptions&quot;: {object (OutputOptions)},&quot;sampleCount&quot;: integer,&quot;storageUri&quot;: string,&quot;seed&quot;: integer,&quot;baseSteps&quot;: integer,&quot;safetySetting&quot;: string,&quot;personGeneration&quot;: string,&quot;addWatermark&quot;: boolean,&quot;enhancePrompt&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>
