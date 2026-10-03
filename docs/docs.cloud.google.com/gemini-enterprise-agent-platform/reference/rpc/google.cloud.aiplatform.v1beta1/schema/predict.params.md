---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params
title: Package google.cloud.aiplatform.v1beta1.schema.predict.params
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

- [`ImageClassificationPredictionParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.ImageClassificationPredictionParams) (message)
- [`ImageObjectDetectionPredictionParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.ImageObjectDetectionPredictionParams) (message)
- [`ImageSegmentationPredictionParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.ImageSegmentationPredictionParams) (message)
- [`OutputOptions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.OutputOptions) (message)
- [`TextEmbeddingPredictionParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.TextEmbeddingPredictionParams) (message)
- [`VideoActionRecognitionPredictionParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.VideoActionRecognitionPredictionParams) (message)
- [`VideoClassificationPredictionParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.VideoClassificationPredictionParams) (message)
- [`VideoGenerationModelParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.VideoGenerationModelParams) (message)
- [`VideoObjectTrackingPredictionParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.VideoObjectTrackingPredictionParams) (message)
- [`VirtualTryOnModelParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.VirtualTryOnModelParams) (message)
- [`VisionEmbeddingModelParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.VisionEmbeddingModelParams) (message)

## ImageClassificationPredictionParams

Prediction model parameters for Image Classification.

| Fields                 |                                                                                                                                                                                              |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `confidence_threshold` | `float` The Model only returns predictions with at least this confidence score. Default value is 0.0                                                                                         |
| `max_predictions`      | `int32` The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10. |

## ImageObjectDetectionPredictionParams

Prediction model parameters for Image Object Detection.

| Fields                 |                                                                                                                                                                                                                  |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `confidence_threshold` | `float` The Model only returns predictions with at least this confidence score. Default value is 0.0                                                                                                             |
| `max_predictions`      | `int32` The Model only returns up to that many top, by confidence score, predictions per instance. Note that number of returned predictions is also limited by metadata's predictionsLimit. Default value is 10. |

## ImageSegmentationPredictionParams

Prediction model parameters for Image Segmentation.

| Fields                 |                                                                                                                                                                                                                                      |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `confidence_threshold` | `float` When the model predicts category of pixels of the image, it will only provide predictions for pixels that it is at least this much confident about. All other pixels will be classified as background. Default value is 0.5. |

## OutputOptions

Configuration options for the output image.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>mime_type</code></td>
<td><p><code>string</code></p>
<p>The MIME type of the output image.</p>
<p>The following values are supported:</p>
<ul>
<li><code>image/jpeg</code></li>
<li><code>image/png</code></li>
</ul>
<p>If not set, defaults to <code>image/png</code> .</p></td>
</tr>
<tr class="even">
<td><code>compression_quality</code></td>
<td><p><code>int32</code></p>
<p>Specifies the compression quality for JPEG images. Accepted values are in the range [0, 100].</p>
<p>If not set, defaults to <code>75</code> .</p></td>
</tr>
</tbody>
</table>

## TextEmbeddingPredictionParams

Prediction model parameters for Text Embedding. Text embeddings are numerical representations of text that capture semantic meaning, used for tasks like semantic search, classification, and clustering.

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                             |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `auto_truncate`         | `bool` Optional. Whether to silently truncate inputs longer than the maximum input token limit. This behavior is enabled by default. If this option is set to false, inputs longer than the limit will cause an INVALID_ARGUMENT error.                                                                                                                                     |
| `output_dimensionality` | `int32` Parameter to reduce the dimensionality of the output embedding. Some models support this feature, which can reduce storage and computation costs. If you specify this parameter, you must use a value supported by the model. If the model does not support it, or if you specify an unsupported dimension, the request will fail with an `INVALID_ARGUMENT` error. |

## VideoActionRecognitionPredictionParams

Prediction model parameters for Video Action Recognition.

| Fields                 |                                                                                                                                                                                                                  |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `confidence_threshold` | `float` The Model only returns predictions with at least this confidence score. Default value is 0.0                                                                                                             |
| `max_predictions`      | `int32` The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50. |

## VideoClassificationPredictionParams

Prediction model parameters for Video Classification.

| Fields                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `confidence_threshold`            | `float` The Model only returns predictions with at least this confidence score. Default value is 0.0                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `max_predictions`                 | `int32` The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10,000.                                                                                                                                                                                                                                                                                                                                                       |
| `segment_classification`          | `bool` Set to true to request segment-level classification. Agent Platform returns labels and their confidence scores for the entire time segment of the video that user specified in the input instance. Default value is true                                                                                                                                                                                                                                                                                                                        |
| `shot_classification`             | `bool` Set to true to request shot-level classification. Agent Platform determines the boundaries for each camera shot in the entire time segment of the video that user specified in the input instance. Agent Platform then returns labels and their confidence scores for each detected shot, along with the start and end time of the shot. WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false |
| `one_sec_interval_classification` | `bool` Set to true to request classification for a video at one-second intervals. Agent Platform returns labels and their confidence scores for each second of the entire time segment of the video that user specified in the input WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false                                                                                                            |

## VideoGenerationModelParams

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>sample_count</code></td>
<td><p><code>int32</code></p>
<p>The number of videos to generate. If not specified, 1 video is generated.</p></td>
</tr>
<tr class="even">
<td><code>storage_uri</code></td>
<td><p><code>string</code></p>
<p>The Google Cloud Storage URI for saving the generated videos. The URI must start with <code>gs://</code> and point to a bucket or folder. If this field is specified, generated videos are uploaded to the specified location.</p></td>
</tr>
<tr class="odd">
<td><code>fps</code></td>
<td><p><code>int32</code></p>
<p>The frame rate of the generated videos in frames per second (fps). This value can affect the smoothness of motion in the video. If not specified, a default value appropriate for the model is used.</p></td>
</tr>
<tr class="even">
<td><code>duration_seconds</code></td>
<td><p><code>double</code></p>
<p>The target duration of the generated videos in seconds. The actual duration of the generated videos may vary slightly. If not specified, a default value appropriate for the model is used.</p></td>
</tr>
<tr class="odd">
<td><code>seed</code></td>
<td><p><code>int32</code></p>
<p>Seed for random number generation. Providing the same seed with the same input parameters will produce consistent video generation results. If not specified, a random seed is used, resulting in different videos each time. If <code>sample_count</code> is greater than 1, a different random seed is used for each generated video, even if a <code>seed</code> is provided.</p></td>
</tr>
<tr class="even">
<td><code>aspect_ratio</code></td>
<td><p><code>string</code></p>
<p>The aspect ratio of the generated videos. Supported values: * <code>16:9</code> (landscape) * <code>9:16</code> (portrait)</p></td>
</tr>
<tr class="odd">
<td><code>resolution</code></td>
<td><p><code>string</code></p>
<p>The resolution of the generated videos. Supported values: * <code>720p</code> * <code>1080p</code></p></td>
</tr>
<tr class="even">
<td><code>person_generation</code></td>
<td><p><code>string</code></p>
<p>Controls whether videos of people can be generated, based on age appearance. Supported values: * <code>dont_allow</code> : Prevents generation of videos with people. * <code>allow_adult</code> : Allows generation of videos with people who appear to be adults. * <code>allow_all</code> : Allows generation of videos with people of all ages. If not specified, <code>allow_adult</code> is used.</p></td>
</tr>
<tr class="odd">
<td><code>pubsub_topic</code></td>
<td><p><code>string</code></p>
<p>The Cloud Pub/Sub topic to publish video generation progress to. If this field is specified, messages are published to the topic detailing the progress of video generation. The topic must be in the format <code>projects/{project}/topics/{topic}</code> .</p></td>
</tr>
<tr class="even">
<td><code>negative_prompt</code></td>
<td><p><code>string</code></p>
<p>Things that shouldn't appear in the generated videos. For example: "low quality", "ugly", "deformed".</p></td>
</tr>
<tr class="odd">
<td><code>enable_prompt_rewriting </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>bool</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated: This field is deprecated and has no effect. Use <code>enhance_prompt</code> instead.</p></td>
</tr>
<tr class="even">
<td><code>enhance_prompt</code></td>
<td><p><code>bool</code></p>
<p>Whether to automatically enhance the prompt before generating videos. If true, the prompt is improved to generate higher quality videos. If prompt enhancement is enabled, providing a <code>seed</code> won't guarantee consistent results. Defaults to true.</p></td>
</tr>
<tr class="odd">
<td><code>generate_audio</code></td>
<td><p><code>bool</code></p>
<p>Whether to generate audio along with the video. If true, an audio track is generated for the videos. Defaults to true.</p></td>
</tr>
<tr class="even">
<td><code>compression_quality</code></td>
<td><p><code>string</code></p>
<p>The compression quality of the generated videos. A lower quality might result in a smaller file size, while a higher quality might result in a better-looking video. Supported values: * <code>optimized</code> : (Default) Optimized for quality and file size. * <code>lossless</code> : Highest quality, larger file size.</p></td>
</tr>
<tr class="odd">
<td><code>task</code></td>
<td><p><code>string</code></p>
<p>The task to perform. If not specified, the task is inferred from other input fields. Supported values: * <code>text_to_video</code> : Generate a video from a text prompt. * <code>image_to_video</code> : Generate a video from an start frame, an optional end frame, and a text prompt. * <code>reference_to_video</code> : Generate a video from one to three reference images, an optional reference audio and a text prompt. * <code>edit</code> : Edit a video based on a mask and a text prompt. * <code>extend</code> : Extend a video based on a text prompt. * <code>upscale</code> : Upscale a video to a higher resolution.</p></td>
</tr>
<tr class="even">
<td><code>resize_mode</code></td>
<td><p><code>string</code></p>
<p>The resize mode for the generated videos. Supported values: * <code>pad</code> : Pad the video to the specified aspect ratio. * <code>crop</code> : Crop the video to the specified aspect ratio. If not specified, <code>pad</code> is used.</p></td>
</tr>
</tbody>
</table>

## VideoObjectTrackingPredictionParams

Prediction model parameters for Video Object Tracking.

| Fields                  |                                                                                                                                                                                                                  |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `confidence_threshold`  | `float` The Model only returns predictions with at least this confidence score. Default value is 0.0                                                                                                             |
| `max_predictions`       | `int32` The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50. |
| `min_bounding_box_size` | `float` Only bounding boxes with shortest edge at least that long as a relative value of video frame size are returned. Default value is 0.0.                                                                    |

## VirtualTryOnModelParams

Represents the parameters for a Virtual Try-On prediction request.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>output_options</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.OutputOptions"><code>OutputOptions</code></a></p>
<p>Options for configuring the output image format.</p></td>
</tr>
<tr class="even">
<td><code>sample_count</code></td>
<td><p><code>int32</code></p>
<p>The number of images to generate. Accepted values are in the range [1,4].</p>
<p>If not set, defaults to <code>1</code> .</p></td>
</tr>
<tr class="odd">
<td><code>storage_uri</code></td>
<td><p><code>string</code></p>
<p>The Google Cloud Storage location where the generated images are stored.</p></td>
</tr>
<tr class="even">
<td><code>seed</code></td>
<td><p><code>int32</code></p>
<p>The random seed for image generation. This avoids randomness in generating the output images.</p>
<p>If a <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.VirtualTryOnModelParams.FIELDS.int32.google.cloud.aiplatform.v1beta1.schema.predict.params.VirtualTryOnModelParams.seed"><code>seed</code></a> value is provided, <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params#google.cloud.aiplatform.v1beta1.schema.predict.params.VirtualTryOnModelParams.FIELDS.bool.google.cloud.aiplatform.v1beta1.schema.predict.params.VirtualTryOnModelParams.add_watermark"><code>add_watermark</code></a> must be set to <code>false</code> .</p></td>
</tr>
<tr class="odd">
<td><code>base_steps</code></td>
<td><p><code>int32</code></p>
<p>The number of diffusion steps to run. The higher the number of steps, the higher the quality of the generated image, but the greater the latency.</p>
<p>If not set, defaults to <code>32</code> .</p></td>
</tr>
<tr class="even">
<td><code>safety_setting</code></td>
<td><p><code>string</code></p>
<p>Safety filter level for generated images. The filter blocks images that contain objectionable content.</p>
<p>The following values are supported:</p>
<ul>
<li><code>block-low-and-above</code> : Strongest filtering level, most strict blocking.</li>
<li><code>block-medium-and-above</code> : Block some problematic content prompts and responses.</li>
<li><code>block-only-high</code> : Reduces the number of requests blocked due to safety filters. May increase objectionable content in generated images.</li>
<li><code>block-none</code> : Block very few problematic prompts and responses. Access to this feature is restricted.</li>
</ul>
<p>If not set, defaults to <code>block_medium_and_above</code> .</p></td>
</tr>
<tr class="odd">
<td><code>person_generation</code></td>
<td><p><code>string</code></p>
<p>Controls whether or not faces or people are included in generated images.</p>
<p>The following values are supported:</p>
<ul>
<li><code>dont-allow</code> : Disallow the inclusion of faces or people in generated images.</li>
<li><code>allow-adult</code> : Allow generation of adults only.</li>
<li><code>allow-all</code> : Allow generation of people of all ages.</li>
</ul>
<p>If not set, defaults to <code>allow-adult</code> .</p></td>
</tr>
<tr class="even">
<td><code>add_watermark</code></td>
<td><p><code>bool</code></p>
<p>Whether to add a watermark to the generated images.</p>
<p>If not set, defaults to <code>true</code> .</p></td>
</tr>
<tr class="odd">
<td><code>enhance_prompt</code></td>
<td><p><code>bool</code></p>
<p>Whether to enhance the user-provided prompt internally for models that support it.</p>
<p>If not set, defaults to <code>true</code> .</p></td>
</tr>
</tbody>
</table>

## VisionEmbeddingModelParams

This type has no fields.

Parameter format for large vision model embedding api.
