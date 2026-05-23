---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoGenerationModelParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoGenerationModelParams
title: VideoGenerationModelParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`sampleCount` `integer`

The number of videos to generate. If not specified, 1 video is generated.

`storageUri` `string`

The Google Cloud Storage URI for saving the generated videos. The URI must start with `gs://` and point to a bucket or folder. If this field is specified, generated videos are uploaded to the specified location.

`fps` `integer`

The frame rate of the generated videos in frames per second (fps). This value can affect the smoothness of motion in the video. If not specified, a default value appropriate for the model is used.

`durationSeconds` `number`

The target duration of the generated videos in seconds. The actual duration of the generated videos may vary slightly. If not specified, a default value appropriate for the model is used.

`seed` `integer`

Seed for random number generation. Providing the same seed with the same input parameters will produce consistent video generation results. If not specified, a random seed is used, resulting in different videos each time. If `sampleCount` is greater than 1, a different random seed is used for each generated video, even if a `seed` is provided.

`aspectRatio` `string`

The aspect ratio of the generated videos. Supported values: \* `16:9` (landscape) \* `9:16` (portrait)

`resolution` `string`

The resolution of the generated videos. Supported values: \* `720p` \* `1080p`

`personGeneration` `string`

Controls whether videos of people can be generated, based on age appearance. Supported values: \* `dont_allow` : Prevents generation of videos with people. \* `allow_adult` : Allows generation of videos with people who appear to be adults. \* `allowAll` : Allows generation of videos with people of all ages. If not specified, `allow_adult` is used.

`pubsubTopic` `string`

The Cloud Pub/Sub topic to publish video generation progress to. If this field is specified, messages are published to the topic detailing the progress of video generation. The topic must be in the format `projects/{project}/topics/{topic}` .

`negativePrompt` `string`

Things that shouldn't appear in the generated videos. For example: "low quality", "ugly", "deformed".

` enablePromptRewriting (deprecated)  ` `boolean`

> This item is deprecated\!

Deprecated: This field is deprecated and has no effect. Use `enhancePrompt` instead.

`enhancePrompt` `boolean`

Whether to automatically enhance the prompt before generating videos. If true, the prompt is improved to generate higher quality videos. If prompt enhancement is enabled, providing a `seed` won't guarantee consistent results. Defaults to true.

`generateAudio` `boolean`

Whether to generate audio along with the video. If true, an audio track is generated for the videos. Defaults to true.

`compressionQuality` `string`

The compression quality of the generated videos. A lower quality might result in a smaller file size, while a higher quality might result in a better-looking video. Supported values: \* `optimized` : (Default) Optimized for quality and file size. \* `lossless` : Highest quality, larger file size.

`task` `string`

The task to perform. If not specified, the task is inferred from other input fields. Supported values: \* `textToVideo` : Generate a video from a text prompt. \* `imageToVideo` : Generate a video from an start frame, an optional end frame, and a text prompt. \* `referenceToVideo` : Generate a video from one to three reference images, an optional reference audio and a text prompt. \* `edit` : Edit a video based on a mask and a text prompt. \* `extend` : Extend a video based on a text prompt. \* `upscale` : Upscale a video to a higher resolution.

`resizeMode` `string`

The resize mode for the generated videos. Supported values: \* `pad` : Pad the video to the specified aspect ratio. \* `crop` : Crop the video to the specified aspect ratio. If not specified, `pad` is used.

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
  &quot;sampleCount&quot;: integer,
  &quot;storageUri&quot;: string,
  &quot;fps&quot;: integer,
  &quot;durationSeconds&quot;: number,
  &quot;seed&quot;: integer,
  &quot;aspectRatio&quot;: string,
  &quot;resolution&quot;: string,
  &quot;personGeneration&quot;: string,
  &quot;pubsubTopic&quot;: string,
  &quot;negativePrompt&quot;: string,
  &quot;enablePromptRewriting&quot;: boolean,
  &quot;enhancePrompt&quot;: boolean,
  &quot;generateAudio&quot;: boolean,
  &quot;compressionQuality&quot;: string,
  &quot;task&quot;: string,
  &quot;resizeMode&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
