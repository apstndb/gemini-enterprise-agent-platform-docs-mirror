---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.instance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.instance
title: Package google.cloud.aiplatform.v1beta1.schema.predict.instance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  ImageClassificationPredictionInstance  ` (message)
  - `  ImageObjectDetectionPredictionInstance  ` (message)
  - `  ImageSegmentationPredictionInstance  ` (message)
  - `  TextClassificationPredictionInstance  ` (message)
  - `  TextEmbeddingPredictionInstance  ` (message)
  - `  TextEmbeddingPredictionInstance.TaskType  ` (enum)
  - `  TextExtractionPredictionInstance  ` (message)
  - `  TextSentimentPredictionInstance  ` (message)
  - `  VideoActionRecognitionPredictionInstance  ` (message)
  - `  VideoClassificationPredictionInstance  ` (message)
  - `  VideoGenerationModelInstance  ` (message)
  - `  VideoGenerationModelInstance.Image  ` (message)
  - `  VideoGenerationModelInstance.Mask  ` (message)
  - `  VideoGenerationModelInstance.ReferenceImage  ` (message)
  - `  VideoGenerationModelInstance.Video  ` (message)
  - `  VideoObjectTrackingPredictionInstance  ` (message)
  - `  VisionEmbeddingModelInstance  ` (message)
  - `  VisionEmbeddingModelInstance.Image  ` (message)
  - `  VisionEmbeddingModelInstance.Video  ` (message)
  - `  VisionEmbeddingModelInstance.Video.VideoSegmentConfig  ` (message)

## ImageClassificationPredictionInstance

Prediction input format for Image Classification.

Fields

`content`

`string`

The image bytes or Cloud Storage URI to make the prediction on.

`mime_type`

`string`

The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon

## ImageObjectDetectionPredictionInstance

Prediction input format for Image Object Detection.

Fields

`content`

`string`

The image bytes or Cloud Storage URI to make the prediction on.

`mime_type`

`string`

The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon

## ImageSegmentationPredictionInstance

Prediction input format for Image Segmentation.

Fields

`content`

`string`

The image bytes to make the predictions on.

`mime_type`

`string`

The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/png

## TextClassificationPredictionInstance

Prediction input format for Text Classification.

Fields

`content`

`string`

The text snippet to make the predictions on.

`mime_type`

`string`

The MIME type of the text snippet. The supported MIME types are listed below. - text/plain

## TextEmbeddingPredictionInstance

Prediction input format for Text Embedding. An embedding is a numerical representation (a vector of floating-point numbers) of text that captures its semantic meaning, enabling tasks like semantic search, classification, and clustering. LINT.IfChange

Fields

`content`

`string`

The text passage to generate the embedding for. This can be a phrase, sentence, or document.

`title`

`string`

The title for the text passage in the `content` field. If you are embedding documents for the `RETRIEVAL_DOCUMENT` task type, providing a title can improve the quality of the embedding.

`task_type`

`  TaskType  `

The task that the generated embeddings will be used for. The model uses this hint to generate embeddings that are optimized for your use case. If not set, the default task type is used.

## TaskType

Represents the downstream task the embeddings will be used for. Specifying the task type helps the model generate embeddings that are optimized for your use case. New task types may be added in the future.

Enums

`DEFAULT`

Task type not specified. The model will use a default value suitable for semantic similarity and retrieval.

`RETRIEVAL_QUERY`

Specifies the given text is a query in a search/retrieval setting. Use this task type for embeddings that will be used to search a corpus of documents.

`RETRIEVAL_DOCUMENT`

Specifies the given text is a document from the corpus being searched. Use this task type for texts that are part of a corpus that will be searched.

`SEMANTIC_SIMILARITY`

Use this task type for Semantic Textual Similarity (STS). These embeddings will be compared with each other to measure semantic similarity.

`CLASSIFICATION`

Specifies that the given text will be classified. Use this task type to generate embeddings that will be used as input to a classification model (e.g., classifying text as spam or not spam).

`CLUSTERING`

Specifies that the embeddings will be used for clustering. Use this task type to generate embeddings that will be used to group similar texts together.

`QUESTION_ANSWERING`

Specifies that the embeddings will be used for question answering. Use this task type to generate embeddings for texts that are part of a question answering system.

`FACT_VERIFICATION`

Specifies that the embeddings will be used for fact verification. Use this task type to generate embeddings for texts that are part of a fact verification system.

`CODE_RETRIEVAL_QUERY`

Specifies that the embeddings will be used for code retrieval. Use this task type for embeddings that will be used to search a corpus of code.

## TextExtractionPredictionInstance

Prediction input format for Text Extraction.

Fields

`content`

`string`

The text snippet to make the predictions on.

`mime_type`

`string`

The MIME type of the text snippet. The supported MIME types are listed below. - text/plain

`key`

`string`

This field is only used for batch prediction. If a key is provided, the batch prediction result will by mapped to this key. If omitted, then the batch prediction result will contain the entire input instance. Agent Platform will not check if keys in the request are duplicates, so it is up to the caller to ensure the keys are unique.

## TextSentimentPredictionInstance

Prediction input format for Text Sentiment.

Fields

`content`

`string`

The text snippet to make the predictions on.

`mime_type`

`string`

The MIME type of the text snippet. The supported MIME types are listed below. - text/plain

## VideoActionRecognitionPredictionInstance

Prediction input format for Video Action Recognition.

Fields

`content`

`string`

The Google Cloud Storage location of the video on which to perform the prediction.

`mime_type`

`string`

The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime

`time_segment_start`

`string`

The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision.

`time_segment_end`

`string`

The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video.

## VideoClassificationPredictionInstance

Prediction input format for Video Classification.

Fields

`content`

`string`

The Google Cloud Storage location of the video on which to perform the prediction.

`mime_type`

`string`

The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime

`time_segment_start`

`string`

The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision.

`time_segment_end`

`string`

The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video.

## VideoGenerationModelInstance

An instance for a video generation prediction request.

Fields

`prompt`

`string`

A text description of the video you want to generate. The prompt should specify the subject, style, and any specific elements or actions that should appear in the video.

`image`

`  Image  `

An optional image to use as a starting point for video generation, used as the first frame of the generated video. If `image` is provided, `video` and `reference_images` cannot be used.

`video`

`  Video  `

An optional input video to use as a starting point for video generation. If `video` is provided, `image` and `reference_images` cannot be used. If `mask` is also provided, the input video will be edited based on the mask. If `mask` is not provided, the input video will be extended in duration.

`last_frame`

`  Image  `

Image to use as the last frame of the generated video. This field can only be used if `image` is also provided.

`camera_control`

`string`

The camera motion to apply to the generated video. This field can only be used if `image` is also provided. Supported values: - `fixed` : No camera motion. - `pan_left` : Pan camera to the left. - `pan_right` : Pan camera to the right. - `tilt_up` : Tilt camera up. - `tilt_down` : Tilt camera down. - `truck_left` : Move camera to the left. - `truck_right` : Move camera to the right. - `pedestal_up` : Move camera up. - `pedestal_down` : Move camera down. - `push_in` : Move camera closer to the subject. - `pull_out` : Move camera away from the subject.

`mask`

`  Mask  `

An optional mask to apply to the input `video` for video editing tasks like inserting or removing objects, or outpainting.

`reference_images[]`

`  ReferenceImage  `

Optional reference images to guide video generation. If `reference_images` are provided, `prompt` must also be provided, and `image` , `video` , and `last_frame` cannot be used. You can provide up to 3 `asset` images or 1 `style` image.

## Image

Defines the input image format.

Fields

`mime_type`

`string`

The MIME type of the image. Supported MIME types: - image/jpeg - image/png

Union field `data` . The image data. The image can be provided as either base64 encoded bytes or a Google Cloud Storage URI. `data` can be only one of the following:

`bytes_base64_encoded`

`string`

The image bytes encoded in base64.

`gcs_uri`

`string`

A Google Cloud Storage URI pointing to the image file.

## Mask

Defines the input mask format for video editing. A mask specifies regions of a video or image to modify or preserve.

Fields

`mime_type`

`string`

The MIME type of the mask. Supported MIME types: - image/png - image/jpeg - image/webp - video/mov - video/mpeg - video/mp4 - video/mpg - video/avi - video/wmv - video/mpegps - video/flv

`mask_mode`

`string`

Specifies how the mask is applied to the input video for editing. For `insert` , `remove` , and `remove_static` modes, the mask must have the same aspect ratio as the input video. For `outpaint` mode, the mask can be 9:16 or 16:9. Supported values: - `insert` : The mask defines a rectangular region in the first frame of the input video. The object described in the `prompt` is inserted into this region and appears in subsequent frames. - `remove` : The mask identifies an object in the first frame to track and remove from the video. - `remove_static` : The mask identifies a static region in the video from which to remove objects. - `outpaint` : The mask defines a region where the input video is placed. The area outside this region is generated based on the `prompt` . Video masks are not supported for outpainting.

Union field `data` . The mask data. The mask can be provided as either base64 encoded bytes or a Google Cloud Storage URI. `data` can be only one of the following:

`bytes_base64_encoded`

`string`

The mask bytes encoded in base64.

`gcs_uri`

`string`

A Google Cloud Storage URI pointing to the mask file.

## ReferenceImage

Defines the input reference image format. A reference image provides additional context to guide video generation, such as style or assets.

Fields

`image`

`  Image  `

The image data for the reference image.

`reference_type`

`string`

The type of reference image, which defines how it influences video generation. Supported values: - `asset` : The reference image provides assets to the generated video, such as the scene, an object, or a character. - `style` : The aesthetics of the reference image (e.g., colors, lighting, texture) are used to define the style of the generated video, such as 'anime', 'photography', or 'origami'.

## Video

Defines the input video format.

Fields

`mime_type`

`string`

The MIME type of the video. Supported MIME types: - video/mov - video/mpeg - video/mp4 - video/mpg - video/avi - video/wmv - video/mpegps - video/flv

Union field `data` . The video data. The video can be provided as either base64 encoded bytes or a Google Cloud Storage URI. `data` can be only one of the following:

`gcs_uri`

`string`

A Google Cloud Storage URI pointing to the video file.

`bytes_base64_encoded`

`string`

The video bytes encoded in base64.

## VideoObjectTrackingPredictionInstance

Prediction input format for Video Object Tracking.

Fields

`content`

`string`

The Google Cloud Storage location of the video on which to perform the prediction.

`mime_type`

`string`

The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime

`time_segment_start`

`string`

The beginning, inclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision.

`time_segment_end`

`string`

The end, exclusive, of the video's time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with "s" appended at the end. Fractions are allowed, up to a microsecond precision, and "inf" or "Infinity" is allowed, which means the end of the video.

## VisionEmbeddingModelInstance

Input format for requesting embeddings from vision models. An embedding is a list of numbers that represents the semantic meaning of text, an image, or a video. Embeddings can be used for many applications, like searching for similar images or getting recommendations. Each instance must specify exactly one of `text` , `image` , or `video` field.

Fields

`image`

`  Image  `

An image to generate embeddings for.

`text`

`string`

Text to generate embeddings for.

`video`

`  Video  `

A video to generate embeddings for.

## Image

Represents an image input for embedding generation.

Fields

`mime_type`

`string`

The MIME type of the image.

The supported MIME types are:

  - `image/jpeg`
  - `image/png`

Union field `data` .

`data` can be only one of the following:

`bytes_base64_encoded`

`string`

Base64-encoded bytes of the image.

`gcs_uri`

`string`

A Cloud Storage URI pointing to the image file. Format: `gs://bucket/object`

## Video

Represents a video input for embedding generation.

Fields

`video_segment_config`

`  VideoSegmentConfig  `

Configuration for processing a video segment. If specified, embeddings are generated for the segment. If not specified, embeddings are generated for the entire video.

Union field `data` .

`data` can be only one of the following:

`bytes_base64_encoded`

`string`

Base64-encoded bytes of the video.

`gcs_uri`

`string`

A Cloud Storage URI pointing to the video file. Format: `gs://bucket/object`

## VideoSegmentConfig

Configuration for processing a segment of a video.

Fields

`start_offset_sec`

`int32`

The start offset of the video segment in seconds.

`end_offset_sec`

`int32`

The end offset of the video segment in seconds.

`interval_sec`

`int32`

The interval of the video for which the embedding will be generated. The minimum value for `interval_sec` is 4. If the interval is less than 4, an `InvalidArgumentError` is returned. There are no limitations on the maximum value of the interval. However, if the interval is larger than `min(video_length, 120s)` , it might affect the quality of the generated embeddings.
