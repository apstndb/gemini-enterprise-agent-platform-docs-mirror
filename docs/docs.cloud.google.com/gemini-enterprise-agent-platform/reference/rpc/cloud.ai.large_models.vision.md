---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/cloud.ai.large_models.vision
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/cloud.ai.large_models.vision
title: Package cloud.ai.large_models.vision
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  GenerateVideoResponse  ` (message)
  - `  Image  ` (message)
  - `  Image.ImageSize  ` (message)
  - `  ImageRAIScores  ` (message)
  - `  Media  ` (message)
  - `  NamedBoundingBox  ` (message)
  - `  RaiInfo  ` (message)
  - `  SemanticFilterResponse  ` (message)
  - `  Video  ` (message)

## GenerateVideoResponse

Generate video response.

Fields

`generated_samples[]`

`  Media  `

The generates samples.

`rai_media_filtered_count`

`int32`

Returns if any videos were filtered due to RAI policies.

`rai_media_filtered_reasons[]`

`string`

Returns rai failure reasons if any.

## Image

Image.

Fields

`encoding`

`string`

Image encoding, encoded as "image/png" or "image/jpg".

`image_rai_scores`

`  ImageRAIScores  `

RAI scores for generated image.

`rai_info`

`  RaiInfo  `

RAI info for image.

`semantic_filter_response`

`  SemanticFilterResponse  `

Semantic filter info for image.

`text`

`string`

Text/Expanded text input for imagen.

`image_size`

`  ImageSize  `

Image size. The size of the image. Can be self reported, or computed from the image bytes.

Union field `content` .

`content` can be only one of the following:

`image`

`bytes`

Raw bytes.

`uri`

`string`

Path to another storage (typically Google Cloud Storage).

## ImageSize

Image size.

Fields

`width`

`int32`

`height`

`int32`

`channels`

`int32`

## ImageRAIScores

RAI scores for generated image returned.

Fields

`agile_watermark_detection_score`

`double`

Agile watermark score for image.

## Media

Media.

Fields

Union field `type` .

`type` can be only one of the following:

`image`

`  Image  `

Image.

`video`

`  Video  `

Video

## NamedBoundingBox

Fields

`x1`

`float`

`x2`

`float`

`y1`

`float`

`y2`

`float`

`classes[]`

`string`

`entities[]`

`string`

`scores[]`

`float`

## RaiInfo

Next ID: 6

Fields

`rai_categories[]`

`string`

List of rai categories' information to return

`scores[]`

`float`

List of rai scores mapping to the rai categories. Rounded to 1 decimal place.

`blocked_entities[]`

`string`

List of blocked entities from the blocklist if it is detected.

`model_name`

`string`

The model name used to indexing into the RaiFilterConfig map. Would either be one of <imagegeneration@002-006> , imagen-3.0-... api endpoint names, or internal names used for mapping to different filter configs (genselfie, ai\_watermark) than its api endpoint.

## SemanticFilterResponse

Fields

`passed_semantic_filter`

`bool`

This response is added when semantic filter config is turned on in EditConfig. It reports if this image is passed semantic filter response. If passed\_semantic\_filter is false, the bounding box information will be populated for user to check what caused the semantic filter to fail.

`named_bounding_boxes[]`

`  NamedBoundingBox  `

Class labels of the bounding boxes that failed the semantic filtering. Bounding box coordinates.

## Video

Video

Fields

`encoding`

`string`

Video encoding, for example "video/mp4".

`text`

`string`

Text/Expanded text input for Help Me Write.

Union field `content` .

`content` can be only one of the following:

`video`

`bytes`

Raw bytes.

`uri`

`string`

Path to another storage (typically Google Cloud Storage).

`encoded_video`

`string`

Base 64 encoded video bytes.
