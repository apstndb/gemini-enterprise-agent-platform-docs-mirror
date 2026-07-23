---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.prediction
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema/predict.prediction
title: Package google.cloud.aiplatform.v1beta1.schema.predict.prediction
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  ClassificationPredictionResult  ` (message)
  - `  ImageObjectDetectionPredictionResult  ` (message)
  - `  ImageSegmentationPredictionResult  ` (message)
  - `  TabularClassificationPredictionResult  ` (message)
  - `  TabularRegressionPredictionResult  ` (message)
  - `  TextEmbedding  ` (message)
  - `  TextEmbedding.Statistics  ` (message)
  - `  TextEmbeddingPredictionResult  ` (message)
  - `  TextExtractionPredictionResult  ` (message)
  - `  TextSentimentPredictionResult  ` (message)
  - `  TftFeatureImportance  ` (message)
  - `  TimeSeriesForecastingPredictionResult  ` (message)
  - `  VideoActionRecognitionPredictionResult  ` (message)
  - `  VideoClassificationPredictionResult  ` (message)
  - `  VideoGenerationModelResult  ` (message)
  - `  VideoObjectTrackingPredictionResult  ` (message)
  - `  VideoObjectTrackingPredictionResult.Frame  ` (message)
  - `  VirtualTryOnModelResult  ` (message)
  - `  VirtualTryOnModelResult.Image  ` (message)
  - `  VisionEmbeddingModelResult  ` (message)
  - `  VisionEmbeddingModelResult.VideoEmbedding  ` (message)

## ClassificationPredictionResult

Prediction output format for Image and Text Classification.

Fields

`ids[]`

`int64`

The resource IDs of the AnnotationSpecs that had been identified.

`display_names[]`

`string`

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

`confidences[]`

`float`

The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

## ImageObjectDetectionPredictionResult

Prediction output format for Image Object Detection.

Fields

`ids[]`

`int64`

The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly.

`display_names[]`

`string`

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

`confidences[]`

`float`

The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

`bboxes[]`

`  ListValue  `

Bounding boxes, i.e. the rectangles over the image, that pinpoint the found AnnotationSpecs. Given in order that matches the IDs. Each bounding box is an array of 4 numbers `xMin` , `xMax` , `yMin` , and `yMax` , which represent the extremal coordinates of the box. They are relative to the image size, and the point 0,0 is in the top left of the image.

## ImageSegmentationPredictionResult

Prediction output format for Image Segmentation.

Fields

`category_mask`

`string`

A PNG image where each pixel in the mask represents the category in which the pixel in the original image was predicted to belong to. The size of this image will be the same as the original image. The mapping between the AnntoationSpec and the color can be found in model's metadata. The model will choose the most likely category and if none of the categories reach the confidence threshold, the pixel will be marked as background.

`confidence_mask`

`string`

A one channel image which is encoded as an 8bit lossless PNG. The size of the image will be the same as the original image. For a specific pixel, darker color means less confidence in correctness of the cateogry in the categoryMask for the corresponding pixel. Black means no confidence and white means complete confidence.

## TabularClassificationPredictionResult

Prediction output format for Tabular Classification.

Fields

`classes[]`

`string`

The name of the classes being classified, contains all possible values of the target column.

`scores[]`

`float`

The model's confidence in each class being correct, higher value means higher confidence. The N-th score corresponds to the N-th class in classes.

## TabularRegressionPredictionResult

Prediction output format for Tabular Regression.

Fields

`value`

`float`

The regression value.

`lower_bound`

`float`

The lower bound of the prediction interval.

`upper_bound`

`float`

The upper bound of the prediction interval.

`quantile_values[]`

`float`

Quantile values.

`quantile_predictions[]`

`float`

Quantile predictions, in 1-1 correspondence with quantile\_values.

## TextEmbedding

An embedding is a vector (list) of floating-point numbers that represents the semantic meaning of text. Embeddings can be used to compare text for similarity, classify text, or cluster text. Text with similar meaning will have similar embedding vectors.

Fields

`values[]`

`float`

The embedding vector. The size of the vector is fixed and determined by the model used for embedding generation.

`statistics`

`  Statistics  `

Statistics about the input text.

## Statistics

Statistics about the input text.

Fields

`token_count`

`int32`

The number of tokens in the input text.

`truncated`

`bool`

Whether the input text was truncated. If true, the embedding was generated from a truncated version of the input text. This can happen if the input text was longer than the model's input token limit.

## TextEmbeddingPredictionResult

Prediction output format for Text Embedding. LINT.IfChange Represents the prediction result for a text embedding request.

Fields

`embeddings`

`  TextEmbedding  `

The embedding generated from the input text.

## TextExtractionPredictionResult

Prediction output format for Text Extraction.

Fields

`ids[]`

`int64`

The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly.

`display_names[]`

`string`

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

`text_segment_start_offsets[]`

`int64`

The start offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet.

`text_segment_end_offsets[]`

`int64`

The end offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet.

`confidences[]`

`float`

The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

## TextSentimentPredictionResult

Prediction output format for Text Sentiment

Fields

`sentiment`

`int32`

The integer sentiment labels between 0 (inclusive) and sentimentMax label (inclusive), while 0 maps to the least positive sentiment and sentimentMax maps to the most positive one. The higher the score is, the more positive the sentiment in the text snippet is. Note: sentimentMax is an integer value between 1 (inclusive) and 10 (inclusive).

## TftFeatureImportance

Fields

`context_weights[]`

`float`

TFT feature importance values. Each pair for {context/horizon/attribute} should have the same shape since the weight corresponds to the column names.

`context_columns[]`

`string`

`horizon_weights[]`

`float`

`horizon_columns[]`

`string`

`attribute_weights[]`

`float`

`attribute_columns[]`

`string`

## TimeSeriesForecastingPredictionResult

Prediction output format for Time Series Forecasting.

Fields

`value`

`float`

The regression value.

`quantile_values[]`

`float`

Quantile values.

`quantile_predictions[]`

`float`

Quantile predictions, in 1-1 correspondence with quantile\_values.

`tft_feature_importance`

`  TftFeatureImportance  `

Only use these if TFt is enabled.

## VideoActionRecognitionPredictionResult

Prediction output format for Video Action Recognition.

Fields

`id`

`string`

The resource ID of the AnnotationSpec that had been identified.

`display_name`

`string`

The display name of the AnnotationSpec that had been identified.

`time_segment_start`

`  Duration  `

The beginning, inclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

`time_segment_end`

`  Duration  `

The end, exclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

`confidence`

`  FloatValue  `

The Model's confidence in correction of this prediction, higher value means higher confidence.

## VideoClassificationPredictionResult

Prediction output format for Video Classification.

Fields

`id`

`string`

The resource ID of the AnnotationSpec that had been identified.

`display_name`

`string`

The display name of the AnnotationSpec that had been identified.

`type`

`string`

The type of the prediction. The requested types can be configured via parameters. This will be one of - segment-classification - shot-classification - one-sec-interval-classification

`time_segment_start`

`  Duration  `

The beginning, inclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. Note that for 'segment-classification' prediction type, this equals the original 'timeSegmentStart' from the input instance, for other types it is the start of a shot or a 1 second interval respectively.

`time_segment_end`

`  Duration  `

The end, exclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. Note that for 'segment-classification' prediction type, this equals the original 'timeSegmentEnd' from the input instance, for other types it is the end of a shot or a 1 second interval respectively.

`confidence`

`  FloatValue  `

The Model's confidence in correction of this prediction, higher value means higher confidence.

## VideoGenerationModelResult

Prediction result from a video generation model. When you request a prediction from a video generation model, the model generates videos based on your input and returns URIs to these videos in Google Cloud Storage.

Fields

`gcs_uris[]`

`string`

A list of Google Cloud Storage URIs for generated videos. For each input instance in your prediction request, the model may generate one or more videos. This field provides the Google Cloud Storage URIs for each of these videos.

## VideoObjectTrackingPredictionResult

Prediction output format for Video Object Tracking.

Fields

`id`

`string`

The resource ID of the AnnotationSpec that had been identified.

`display_name`

`string`

The display name of the AnnotationSpec that had been identified.

`time_segment_start`

`  Duration  `

The beginning, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

`time_segment_end`

`  Duration  `

The end, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

`confidence`

`  FloatValue  `

The Model's confidence in correction of this prediction, higher value means higher confidence.

`frames[]`

`  Frame  `

All of the frames of the video in which a single object instance has been detected. The bounding boxes in the frames identify the same object.

## Frame

The fields `xMin` , `xMax` , `yMin` , and `yMax` refer to a bounding box, i.e. the rectangle over the video frame pinpointing the found AnnotationSpec. The coordinates are relative to the frame size, and the point 0,0 is in the top left of the frame.

Fields

`time_offset`

`  Duration  `

A time (frame) of a video in which the object has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

`x_min`

`  FloatValue  `

The leftmost coordinate of the bounding box.

`x_max`

`  FloatValue  `

The rightmost coordinate of the bounding box.

`y_min`

`  FloatValue  `

The topmost coordinate of the bounding box.

`y_max`

`  FloatValue  `

The bottommost coordinate of the bounding box.

## VirtualTryOnModelResult

Represents the output of a Virtual Try-On prediction.

Fields

`images[]`

`  Image  `

A list of generated images. The number of images returned is equal to the `sample_count` parameter provided in the request.

## Image

Contains a generated image or information about why the image was filtered out.

Fields

`mime_type`

`string`

The MIME type of the generated image.

Supported values are: \* `image/png` \* `image/jpeg`

Union field `data` . The generated image data or filtering reason. `data` can be only one of the following:

`bytes_base64_encoded`

`string`

The generated image encoded as a base64 encoded bytes string.

`gcs_uri`

`string`

The Google Cloud Storage URI where the generated image is stored.

`rai_filtered_reason`

`string`

The reason why the generated image was filtered out by Responsible AI checks. If this field is present, no image is returned.

## VisionEmbeddingModelResult

The prediction result for a large vision model embedding request. An embedding is a vectorized representation of data such as image, text or video. The embeddings produced by this model can be used for tasks such as image retrieval, similarity comparison, and classification. The embedding vectors have 1024 dimensions.

Fields

`image_embedding`

`  ListValue  `

The embedding generated from the input image. This field is populated if the prediction request contained an image.

`text_embedding`

`  ListValue  `

The embedding generated from the input text. This field is populated if the prediction request contained text.

`video_embeddings[]`

`  VideoEmbedding  `

The embeddings generated from the input video. This field is populated if the prediction request contained a video. The video is divided into 1-second segments, and an embedding is generated for each segment.

## VideoEmbedding

Contains embedding data for a specific time segment of a video.

Fields

`start_offset_sec`

`int32`

The start time of the video segment that this embedding represents, measured in seconds from the beginning of the video.

`end_offset_sec`

`int32`

The end time of the video segment that this embedding represents, measured in seconds from the beginning of the video.

`embedding`

`  ListValue  `

The 1024-dimension embedding vector for this video segment.
