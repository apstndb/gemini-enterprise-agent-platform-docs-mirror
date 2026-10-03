---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema
title: Package google.cloud.aiplatform.v1beta1.schema
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

- [`AnnotationSpecColor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.AnnotationSpecColor) (message)
- [`ImageBoundingBoxAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageBoundingBoxAnnotation) (message)
- [`ImageClassificationAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageClassificationAnnotation) (message)
- [`ImageDataItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageDataItem) (message)
- [`ImageDatasetMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageDatasetMetadata) (message)
- [`ImageSegmentationAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageSegmentationAnnotation) (message)
- [`ImageSegmentationAnnotation.MaskAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageSegmentationAnnotation.MaskAnnotation) (message)
- [`ImageSegmentationAnnotation.PolygonAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageSegmentationAnnotation.PolygonAnnotation) (message)
- [`ImageSegmentationAnnotation.PolylineAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageSegmentationAnnotation.PolylineAnnotation) (message)
- [`MultimodalDatasetMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.MultimodalDatasetMetadata) (message)
- [`MultimodalDatasetMetadata.BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.MultimodalDatasetMetadata.BigQuerySource) (message)
- [`MultimodalDatasetMetadata.MultimodalDatasetInputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.MultimodalDatasetMetadata.MultimodalDatasetInputConfig) (message)
- [`PredictionResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.PredictionResult) (message)
- [`PredictionResult.Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.PredictionResult.Error) (message)
- [`TablesDatasetMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TablesDatasetMetadata) (message)
- [`TablesDatasetMetadata.BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TablesDatasetMetadata.BigQuerySource) (message)
- [`TablesDatasetMetadata.GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TablesDatasetMetadata.GcsSource) (message)
- [`TablesDatasetMetadata.InputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TablesDatasetMetadata.InputConfig) (message)
- [`TextClassificationAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TextClassificationAnnotation) (message)
- [`TextDataItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TextDataItem) (message)
- [`TextDatasetMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TextDatasetMetadata) (message)
- [`TextExtractionAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TextExtractionAnnotation) (message)
- [`TextSegment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TextSegment) (message)
- [`TextSentimentAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TextSentimentAnnotation) (message)
- [`TextSentimentSavedQueryMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TextSentimentSavedQueryMetadata) (message)
- [`TimeSegment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TimeSegment) (message)
- [`TimeSeriesDatasetMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TimeSeriesDatasetMetadata) (message)
- [`TimeSeriesDatasetMetadata.BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TimeSeriesDatasetMetadata.BigQuerySource) (message)
- [`TimeSeriesDatasetMetadata.GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TimeSeriesDatasetMetadata.GcsSource) (message)
- [`TimeSeriesDatasetMetadata.InputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TimeSeriesDatasetMetadata.InputConfig) (message)
- [`Vertex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.Vertex) (message)
- [`VideoActionRecognitionAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.VideoActionRecognitionAnnotation) (message)
- [`VideoClassificationAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.VideoClassificationAnnotation) (message)
- [`VideoDataItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.VideoDataItem) (message)
- [`VideoDatasetMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.VideoDatasetMetadata) (message)
- [`VideoObjectTrackingAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.VideoObjectTrackingAnnotation) (message)
- [`VisualInspectionClassificationLabelSavedQueryMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.VisualInspectionClassificationLabelSavedQueryMetadata) (message)
- [`VisualInspectionMaskSavedQueryMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.VisualInspectionMaskSavedQueryMetadata) (message)

## AnnotationSpecColor

An entry of mapping between color and AnnotationSpec. The mapping is used in segmentation mask.

| Fields         |                                                                                                                                                                               |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `color`        | [`Color`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.type#google.type.Color) The color of the AnnotationSpec in a segmentation mask. |
| `display_name` | `string` The display name of the AnnotationSpec represented by the color in the segmentation mask.                                                                            |
| `id`           | `string` The ID of the AnnotationSpec represented by the color in the segmentation mask.                                                                                      |

## ImageBoundingBoxAnnotation

Annotation details specific to image object detection.

| Fields               |                                                                                   |
|----------------------|-----------------------------------------------------------------------------------|
| `annotation_spec_id` | `string` The resource Id of the AnnotationSpec that this Annotation pertains to.  |
| `display_name`       | `string` The display name of the AnnotationSpec that this Annotation pertains to. |
| `x_min`              | `double` The leftmost coordinate of the bounding box.                             |
| `x_max`              | `double` The rightmost coordinate of the bounding box.                            |
| `y_min`              | `double` The topmost coordinate of the bounding box.                              |
| `y_max`              | `double` The bottommost coordinate of the bounding box.                           |

## ImageClassificationAnnotation

Annotation details specific to image classification.

| Fields               |                                                                                   |
|----------------------|-----------------------------------------------------------------------------------|
| `annotation_spec_id` | `string` The resource Id of the AnnotationSpec that this Annotation pertains to.  |
| `display_name`       | `string` The display name of the AnnotationSpec that this Annotation pertains to. |

## ImageDataItem

Payload of Image DataItem.

| Fields      |                                                                                                                                                                                                                                  |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `gcs_uri`   | `string` Required. Google Cloud Storage URI points to the original image in user's bucket. The image is up to 30MB in size.                                                                                                      |
| `mime_type` | `string` Output only. The mime type of the content of the image. Only the images in below listed mime types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon |

## ImageDatasetMetadata

The metadata of Datasets that contain Image DataItems.

| Fields                 |                                                                                                                                      |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| `data_item_schema_uri` | `string` Points to a YAML file stored on Google Cloud Storage describing payload of the Image DataItems that belong to this Dataset. |
| `gcs_bucket`           | `string` Google Cloud Storage Bucket name that contains the blob data of this Dataset.                                               |

## ImageSegmentationAnnotation

Annotation details specific to image segmentation.

| Fields                                                                    |                                                                                                                                                                                                                                                                                                                 |
|---------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `annotation` . `annotation` can be only one of the following: |                                                                                                                                                                                                                                                                                                                 |
| `mask_annotation`                                                         | [`MaskAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageSegmentationAnnotation.MaskAnnotation) Mask based segmentation annotation. Only one mask annotation can exist for one image. |
| `polygon_annotation`                                                      | [`PolygonAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageSegmentationAnnotation.PolygonAnnotation) Polygon annotation.                                                             |
| `polyline_annotation`                                                     | [`PolylineAnnotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.ImageSegmentationAnnotation.PolylineAnnotation) Polyline annotation.                                                          |

## MaskAnnotation

The mask based segmentation annotation.

| Fields                     |                                                                                                                                                                                                                                                                                                                                               |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mask_gcs_uri`             | `string` Google Cloud Storage URI that points to the mask image. The image must be in PNG format. It must have the same size as the DataItem's image. Each pixel in the image mask represents the AnnotationSpec which the pixel in the image DataItem belong to. Each color is mapped to one AnnotationSpec based on annotation_spec_colors. |
| `annotation_spec_colors[]` | [`AnnotationSpecColor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.AnnotationSpecColor) The mapping between color and AnnotationSpec for this Annotation.                                                                     |

## PolygonAnnotation

Represents a polygon in image.

| Fields               |                                                                                                                                                                                                                                                                                               |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `vertexes[]`         | [`Vertex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.Vertex) The vertexes are connected one by one and the last vertex is connected to the first one to represent a polygon. |
| `annotation_spec_id` | `string` The resource Id of the AnnotationSpec that this Annotation pertains to.                                                                                                                                                                                                              |
| `display_name`       | `string` The display name of the AnnotationSpec that this Annotation pertains to.                                                                                                                                                                                                             |

## PolylineAnnotation

Represents a polyline in image.

| Fields               |                                                                                                                                                                                                                                                                            |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `vertexes[]`         | [`Vertex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.Vertex) The vertexes are connected one by one and the last vertex in not connected to the first one. |
| `annotation_spec_id` | `string` The resource Id of the AnnotationSpec that this Annotation pertains to.                                                                                                                                                                                           |
| `display_name`       | `string` The display name of the AnnotationSpec that this Annotation pertains to.                                                                                                                                                                                          |

## MultimodalDatasetMetadata

The metadata of Multimodal Datasets.

| Fields                       |                                                                                                                                                                                                                                                                                                   |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `input_config`               | [`MultimodalDatasetInputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.MultimodalDatasetMetadata.MultimodalDatasetInputConfig) Specifies the input source and configuration. |
| `gemini_request_read_config` | [`GeminiRequestReadConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1#google.cloud.aiplatform.v1beta1.GeminiRequestReadConfig) The configuration for how to read Gemini requests from the dataset.                             |
| `key_column_name`            | `string` The name of the column in the BigQuery table that contains the keys of the rows.                                                                                                                                                                                                         |

## BigQuerySource

Specifies the BigQuery source.

| Fields |                                                                                                             |
|--------|-------------------------------------------------------------------------------------------------------------|
| `uri`  | `string` The URI of a BigQuery table. e.g. [bq://project.bqDataset.bqTable](bq://project.bqDataset.bqTable) |

## MultimodalDatasetInputConfig

Specifies the input source and configuration.

| Fields                                                                                                                                 |                                                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `source` . The source of the input. We only support BigQuery as source for now. `source` can be only one of the following: |                                                                                                                                                                                                                                                |
| `bigquery_source`                                                                                                                      | [`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.MultimodalDatasetMetadata.BigQuerySource) BigQuery source table. |

## PredictionResult

Represents a line of JSONL in the batch prediction output file.

| Fields                                                                                                                                                          |                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `prediction`                                                                                                                                                    | [`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value) The prediction result. Value is used here instead of Any so that JsonFormat does not append an extra "@type" field when we convert the proto to JSON and so we can represent array of objects. Do not set error if this is set. |
| `error`                                                                                                                                                         | [`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.PredictionResult.Error) The error result. Do not set prediction if this is set.                                                      |
| Union field `input` . Some identifier from the input so that the prediction can be mapped back to the input instance. `input` can be only one of the following: |                                                                                                                                                                                                                                                                                                           |
| `instance`                                                                                                                                                      | [`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct) User's input instance. Struct is used here instead of Any so that JsonFormat does not append an extra "@type" field when we convert the proto to JSON.                                                                        |
| `key`                                                                                                                                                           | `string` Optional user-provided key from the input instance.                                                                                                                                                                                                                                              |

## Error

| Fields    |                                                                                                                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `status`  | [`Code`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.rpc#google.rpc.Code) Error status. This will be serialized into the enum name e.g. "NOT_FOUND". |
| `message` | `string` Error message with additional details.                                                                                                                                              |

## TablesDatasetMetadata

The metadata of Datasets that contain tables data.

| Fields         |                                                                                                                                                                                                               |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `input_config` | [`InputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TablesDatasetMetadata.InputConfig) |

## BigQuerySource

| Fields |                                                                                                                         |
|--------|-------------------------------------------------------------------------------------------------------------------------|
| `uri`  | `string` The URI of a BigQuery table. e.g. [bq://projectId.bqDatasetId.bqTableId](bq://projectId.bqDatasetId.bqTableId) |

## GcsSource

| Fields  |                                                                                                                                                                                                                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uri[]` | `string` Cloud Storage URI of one or more files. Only CSV files are supported. The first line of the CSV file is used as the header. If there are multiple files, the header is the first line of the lexicographically first file, the other files must either contain the exact same header or omit the header. |

## InputConfig

The tables Dataset's data source. The Dataset doesn't store the data directly, but only pointer(s) to its data.

| Fields                                                            |                                                                                                                                                                                                                     |
|-------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `source` . `source` can be only one of the following: |                                                                                                                                                                                                                     |
| `gcs_source`                                                      | [`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TablesDatasetMetadata.GcsSource)           |
| `bigquery_source`                                                 | [`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TablesDatasetMetadata.BigQuerySource) |

## TextClassificationAnnotation

Annotation details specific to text classification.

| Fields               |                                                                                   |
|----------------------|-----------------------------------------------------------------------------------|
| `annotation_spec_id` | `string` The resource Id of the AnnotationSpec that this Annotation pertains to.  |
| `display_name`       | `string` The display name of the AnnotationSpec that this Annotation pertains to. |

## TextDataItem

Payload of Text DataItem.

| Fields    |                                                                                                                                                                               |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `gcs_uri` | `string` Output only. Google Cloud Storage URI points to a copy of the original text in the Vertex-managed bucket in the user's project. The text file is up to 10MB in size. |

## TextDatasetMetadata

The metadata of Datasets that contain Text DataItems.

| Fields                 |                                                                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `data_item_schema_uri` | `string` Points to a YAML file stored on Google Cloud Storage describing payload of the Text DataItems that belong to this Dataset. |
| `gcs_bucket`           | `string` Google Cloud Storage Bucket name that contains the blob data of this Dataset.                                              |

## TextExtractionAnnotation

Annotation details specific to text extraction.

| Fields               |                                                                                                                                                                                                                          |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text_segment`       | [`TextSegment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TextSegment) The segment of the text content. |
| `annotation_spec_id` | `string` The resource Id of the AnnotationSpec that this Annotation pertains to.                                                                                                                                         |
| `display_name`       | `string` The display name of the AnnotationSpec that this Annotation pertains to.                                                                                                                                        |

## TextSegment

The text segment inside of DataItem.

| Fields         |                                                                                                                                                                                                                       |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_offset` | `uint64` Zero-based character index of the first character of the text segment (counting characters from the beginning of the text).                                                                                  |
| `end_offset`   | `uint64` Zero-based character index of the first character past the end of the text segment (counting character from the beginning of the text). The character at the end_offset is NOT included in the text segment. |
| `content`      | `string` The text content in the segment for output only.                                                                                                                                                             |

## TextSentimentAnnotation

Annotation details specific to text sentiment.

| Fields               |                                                                                   |
|----------------------|-----------------------------------------------------------------------------------|
| `sentiment`          | `int32` The sentiment score for text.                                             |
| `sentiment_max`      | `int32` The sentiment max score for text.                                         |
| `annotation_spec_id` | `string` The resource Id of the AnnotationSpec that this Annotation pertains to.  |
| `display_name`       | `string` The display name of the AnnotationSpec that this Annotation pertains to. |

## TextSentimentSavedQueryMetadata

The metadata of SavedQuery contains TextSentiment Annotations.

| Fields          |                                                                           |
|-----------------|---------------------------------------------------------------------------|
| `sentiment_max` | `int32` The maximum sentiment of sentiment Anntoation in this SavedQuery. |

## TimeSegment

A time period inside of a DataItem that has a time dimension (e.g. video).

| Fields              |                                                                                                                                                                                     |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time_offset` | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) Start of the time segment (inclusive), represented as the duration since the start of the DataItem. |
| `end_time_offset`   | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) End of the time segment (exclusive), represented as the duration since the start of the DataItem.   |

## TimeSeriesDatasetMetadata

The metadata of Datasets that contain time series data.

| Fields                          |                                                                                                                                                                                                                   |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `input_config`                  | [`InputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TimeSeriesDatasetMetadata.InputConfig) |
| `time_series_identifier_column` | `string` The column name of the time series identifier column that identifies the time series.                                                                                                                    |
| `time_column`                   | `string` The column name of the time column that identifies time order in the time series.                                                                                                                        |

## BigQuerySource

| Fields |                                       |
|--------|---------------------------------------|
| `uri`  | `string` The URI of a BigQuery table. |

## GcsSource

| Fields  |                                                                                                                                                                                                                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uri[]` | `string` Cloud Storage URI of one or more files. Only CSV files are supported. The first line of the CSV file is used as the header. If there are multiple files, the header is the first line of the lexicographically first file, the other files must either contain the exact same header or omit the header. |

## InputConfig

The time series Dataset's data source. The Dataset doesn't store the data directly, but only pointer(s) to its data.

| Fields                                                            |                                                                                                                                                                                                                         |
|-------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `source` . `source` can be only one of the following: |                                                                                                                                                                                                                         |
| `gcs_source`                                                      | [`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TimeSeriesDatasetMetadata.GcsSource)           |
| `bigquery_source`                                                 | [`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TimeSeriesDatasetMetadata.BigQuerySource) |

## Vertex

Represents a 2D point in the image. Vertex coordinates are normalized to be relative to the original image dimensions and range from 0 to 1. The origin of the coordinate system (0,0) is the top-left corner of the image. x increases to the right, and y increases to the bottom.

| Fields |                                                                  |
|--------|------------------------------------------------------------------|
| `x`    | `double` X coordinate of the vertex, normalized to \[0.0, 1.0\]. |
| `y`    | `double` Y coordinate of the vertex, normalized to \[0.0, 1.0\]. |

## VideoActionRecognitionAnnotation

Annotation details specific to video action recognition.

| Fields               |                                                                                                                                                                                                                                                                                                                                |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `time_segment`       | [`TimeSegment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TimeSegment) This Annotation applies to the time period represented by the TimeSegment. If it's not set, the Annotation applies to the whole video. |
| `annotation_spec_id` | `string` The resource Id of the AnnotationSpec that this Annotation pertains to.                                                                                                                                                                                                                                               |
| `display_name`       | `string` The display name of the AnnotationSpec that this Annotation pertains to.                                                                                                                                                                                                                                              |

## VideoClassificationAnnotation

Annotation details specific to video classification.

| Fields               |                                                                                                                                                                                                                                                                                                                                |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `time_segment`       | [`TimeSegment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema#google.cloud.aiplatform.v1beta1.schema.TimeSegment) This Annotation applies to the time period represented by the TimeSegment. If it's not set, the Annotation applies to the whole video. |
| `annotation_spec_id` | `string` The resource Id of the AnnotationSpec that this Annotation pertains to.                                                                                                                                                                                                                                               |
| `display_name`       | `string` The display name of the AnnotationSpec that this Annotation pertains to.                                                                                                                                                                                                                                              |

## VideoDataItem

Payload of Video DataItem.

| Fields      |                                                                                                                                                                                           |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `gcs_uri`   | `string` Required. Google Cloud Storage URI points to the original video in user's bucket. The video is up to 50 GB in size and up to 3 hour in duration.                                 |
| `mime_type` | `string` Output only. The mime type of the content of the video. Only the videos in below listed mime types are supported. Supported mime_type: - video/mp4 - video/avi - video/quicktime |

## VideoDatasetMetadata

The metadata of Datasets that contain Video DataItems.

| Fields                 |                                                                                                                                      |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| `data_item_schema_uri` | `string` Points to a YAML file stored on Google Cloud Storage describing payload of the Video DataItems that belong to this Dataset. |
| `gcs_bucket`           | `string` Google Cloud Storage Bucket name that contains the blob data of this Dataset.                                               |

## VideoObjectTrackingAnnotation

Annotation details specific to video object tracking.

| Fields               |                                                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `time_offset`        | [`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration) A time (frame) of a video to which this annotation pertains. Represented as the duration since the video's start. |
| `x_min`              | `double` The leftmost coordinate of the bounding box.                                                                                                                                             |
| `x_max`              | `double` The rightmost coordinate of the bounding box.                                                                                                                                            |
| `y_min`              | `double` The topmost coordinate of the bounding box.                                                                                                                                              |
| `y_max`              | `double` The bottommost coordinate of the bounding box.                                                                                                                                           |
| `instance_id`        | `int64` The instance of the object, expressed as a positive integer. Used to track the same object across different frames.                                                                       |
| `annotation_spec_id` | `string` The resource Id of the AnnotationSpec that this Annotation pertains to.                                                                                                                  |
| `display_name`       | `string` The display name of the AnnotationSpec that this Annotation pertains to.                                                                                                                 |

## VisualInspectionClassificationLabelSavedQueryMetadata

| Fields        |                                                                |
|---------------|----------------------------------------------------------------|
| `multi_label` | `bool` Whether or not the classification label is multi_label. |

## VisualInspectionMaskSavedQueryMetadata

This type has no fields.
