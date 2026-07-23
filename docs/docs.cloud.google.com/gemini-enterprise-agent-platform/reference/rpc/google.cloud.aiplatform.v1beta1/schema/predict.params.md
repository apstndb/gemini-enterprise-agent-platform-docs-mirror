---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.params
title: Package google.cloud.aiplatform.v1beta1.schema.predict.params
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  ImageClassificationPredictionParams  ` (message)
  - `  ImageObjectDetectionPredictionParams  ` (message)
  - `  ImageSegmentationPredictionParams  ` (message)
  - `  OutputOptions  ` (message)
  - `  TextEmbeddingPredictionParams  ` (message)
  - `  VideoActionRecognitionPredictionParams  ` (message)
  - `  VideoClassificationPredictionParams  ` (message)
  - `  VideoGenerationModelParams  ` (message)
  - `  VideoObjectTrackingPredictionParams  ` (message)
  - `  VirtualTryOnModelParams  ` (message)
  - `  VisionEmbeddingModelParams  ` (message)

## ImageClassificationPredictionParams

Prediction model parameters for Image Classification.

Fields

`confidence_threshold`

`float`

The Model only returns predictions with at least this confidence score. Default value is 0.0

`max_predictions`

`int32`

The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10.

## ImageObjectDetectionPredictionParams

Prediction model parameters for Image Object Detection.

Fields

`confidence_threshold`

`float`

The Model only returns predictions with at least this confidence score. Default value is 0.0

`max_predictions`

`int32`

The Model only returns up to that many top, by confidence score, predictions per instance. Note that number of returned predictions is also limited by metadata's predictionsLimit. Default value is 10.

## ImageSegmentationPredictionParams

Prediction model parameters for Image Segmentation.

Fields

`confidence_threshold`

`float`

When the model predicts category of pixels of the image, it will only provide predictions for pixels that it is at least this much confident about. All other pixels will be classified as background. Default value is 0.5.

## OutputOptions

Configuration options for the output image.

Fields

`mime_type`

`string`

The MIME type of the output image.

The following values are supported:

  - `image/jpeg`
  - `image/png`

If not set, defaults to `image/png` .

`compression_quality`

`int32`

Specifies the compression quality for JPEG images. Accepted values are in the range \[0, 100\].

If not set, defaults to `75` .

## TextEmbeddingPredictionParams

Prediction model parameters for Text Embedding. Text embeddings are numerical representations of text that capture semantic meaning, used for tasks like semantic search, classification, and clustering.

Fields

`auto_truncate`

`bool`

Optional. Whether to silently truncate inputs longer than the maximum input token limit. This behavior is enabled by default. If this option is set to false, inputs longer than the limit will cause an INVALID\_ARGUMENT error.

`output_dimensionality`

`int32`

Parameter to reduce the dimensionality of the output embedding. Some models support this feature, which can reduce storage and computation costs. If you specify this parameter, you must use a value supported by the model. If the model does not support it, or if you specify an unsupported dimension, the request will fail with an `INVALID_ARGUMENT` error.

## VideoActionRecognitionPredictionParams

Prediction model parameters for Video Action Recognition.

Fields

`confidence_threshold`

`float`

The Model only returns predictions with at least this confidence score. Default value is 0.0

`max_predictions`

`int32`

The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50.

## VideoClassificationPredictionParams

Prediction model parameters for Video Classification.

Fields

`confidence_threshold`

`float`

The Model only returns predictions with at least this confidence score. Default value is 0.0

`max_predictions`

`int32`

The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10,000.

`segment_classification`

`bool`

Set to true to request segment-level classification. Agent Platform returns labels and their confidence scores for the entire time segment of the video that user specified in the input instance. Default value is true

`shot_classification`

`bool`

Set to true to request shot-level classification. Agent Platform determines the boundaries for each camera shot in the entire time segment of the video that user specified in the input instance. Agent Platform then returns labels and their confidence scores for each detected shot, along with the start and end time of the shot. WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false

`one_sec_interval_classification`

`bool`

Set to true to request classification for a video at one-second intervals. Agent Platform returns labels and their confidence scores for each second of the entire time segment of the video that user specified in the input WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false

## VideoGenerationModelParams

Fields

`sample_count`

`int32`

The number of videos to generate. If not specified, 1 video is generated.

`storage_uri`

`string`

The Google Cloud Storage URI for saving the generated videos. The URI must start with `gs://` and point to a bucket or folder. If this field is specified, generated videos are uploaded to the specified location.

`fps`

`int32`

The frame rate of the generated videos in frames per second (fps). This value can affect the smoothness of motion in the video. If not specified, a default value appropriate for the model is used.

`duration_seconds`

`double`

The target duration of the generated videos in seconds. The actual duration of the generated videos may vary slightly. If not specified, a default value appropriate for the model is used.

`seed`

`int32`

Seed for random number generation. Providing the same seed with the same input parameters will produce consistent video generation results. If not specified, a random seed is used, resulting in different videos each time. If `sample_count` is greater than 1, a different random seed is used for each generated video, even if a `seed` is provided.

`aspect_ratio`

`string`

The aspect ratio of the generated videos. Supported values: \* `16:9` (landscape) \* `9:16` (portrait)

`resolution`

`string`

The resolution of the generated videos. Supported values: \* `720p` \* `1080p`

`person_generation`

`string`

Controls whether videos of people can be generated, based on age appearance. Supported values: \* `dont_allow` : Prevents generation of videos with people. \* `allow_adult` : Allows generation of videos with people who appear to be adults. \* `allow_all` : Allows generation of videos with people of all ages. If not specified, `allow_adult` is used.

`pubsub_topic`

`string`

The Cloud Pub/Sub topic to publish video generation progress to. If this field is specified, messages are published to the topic detailing the progress of video generation. The topic must be in the format `projects/{project}/topics/{topic}` .

`negative_prompt`

`string`

Things that shouldn't appear in the generated videos. For example: "low quality", "ugly", "deformed".

` enable_prompt_rewriting (deprecated)  `

`bool`

> This item is deprecated\!

Deprecated: This field is deprecated and has no effect. Use `enhance_prompt` instead.

`enhance_prompt`

`bool`

Whether to automatically enhance the prompt before generating videos. If true, the prompt is improved to generate higher quality videos. If prompt enhancement is enabled, providing a `seed` won't guarantee consistent results. Defaults to true.

`generate_audio`

`bool`

Whether to generate audio along with the video. If true, an audio track is generated for the videos. Defaults to true.

`compression_quality`

`string`

The compression quality of the generated videos. A lower quality might result in a smaller file size, while a higher quality might result in a better-looking video. Supported values: \* `optimized` : (Default) Optimized for quality and file size. \* `lossless` : Highest quality, larger file size.

`task`

`string`

The task to perform. If not specified, the task is inferred from other input fields. Supported values: \* `text_to_video` : Generate a video from a text prompt. \* `image_to_video` : Generate a video from an start frame, an optional end frame, and a text prompt. \* `reference_to_video` : Generate a video from one to three reference images, an optional reference audio and a text prompt. \* `edit` : Edit a video based on a mask and a text prompt. \* `extend` : Extend a video based on a text prompt. \* `upscale` : Upscale a video to a higher resolution.

`resize_mode`

`string`

The resize mode for the generated videos. Supported values: \* `pad` : Pad the video to the specified aspect ratio. \* `crop` : Crop the video to the specified aspect ratio. If not specified, `pad` is used.

## VideoObjectTrackingPredictionParams

Prediction model parameters for Video Object Tracking.

Fields

`confidence_threshold`

`float`

The Model only returns predictions with at least this confidence score. Default value is 0.0

`max_predictions`

`int32`

The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50.

`min_bounding_box_size`

`float`

Only bounding boxes with shortest edge at least that long as a relative value of video frame size are returned. Default value is 0.0.

## VirtualTryOnModelParams

Represents the parameters for a Virtual Try-On prediction request.

Fields

`output_options`

`  OutputOptions  `

Options for configuring the output image format.

`sample_count`

`int32`

The number of images to generate. Accepted values are in the range \[1,4\].

If not set, defaults to `1` .

`storage_uri`

`string`

The Google Cloud Storage location where the generated images are stored.

`seed`

`int32`

The random seed for image generation. This avoids randomness in generating the output images.

If a `  seed  ` value is provided, `  add_watermark  ` must be set to `false` .

`base_steps`

`int32`

The number of diffusion steps to run. The higher the number of steps, the higher the quality of the generated image, but the greater the latency.

If not set, defaults to `32` .

`safety_setting`

`string`

Safety filter level for generated images. The filter blocks images that contain objectionable content.

The following values are supported:

  - `block-low-and-above` : Strongest filtering level, most strict blocking.
  - `block-medium-and-above` : Block some problematic content prompts and responses.
  - `block-only-high` : Reduces the number of requests blocked due to safety filters. May increase objectionable content in generated images.
  - `block-none` : Block very few problematic prompts and responses. Access to this feature is restricted.

If not set, defaults to `block_medium_and_above` .

`person_generation`

`string`

Controls whether or not faces or people are included in generated images.

The following values are supported:

  - `dont-allow` : Disallow the inclusion of faces or people in generated images.
  - `allow-adult` : Allow generation of adults only.
  - `allow-all` : Allow generation of people of all ages.

If not set, defaults to `allow-adult` .

`add_watermark`

`bool`

Whether to add a watermark to the generated images.

If not set, defaults to `true` .

`enhance_prompt`

`bool`

Whether to enhance the user-provided prompt internally for models that support it.

If not set, defaults to `true` .

## VisionEmbeddingModelParams

This type has no fields.

Parameter format for large vision model embedding api.
