---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1beta1/schema
title: Package google.cloud.aiplatform.v1beta1.schema
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  AnnotationSpecColor  ` (message)
  - `  ImageBoundingBoxAnnotation  ` (message)
  - `  ImageClassificationAnnotation  ` (message)
  - `  ImageDataItem  ` (message)
  - `  ImageDatasetMetadata  ` (message)
  - `  ImageSegmentationAnnotation  ` (message)
  - `  ImageSegmentationAnnotation.MaskAnnotation  ` (message)
  - `  ImageSegmentationAnnotation.PolygonAnnotation  ` (message)
  - `  ImageSegmentationAnnotation.PolylineAnnotation  ` (message)
  - `  MultimodalDatasetMetadata  ` (message)
  - `  MultimodalDatasetMetadata.BigQuerySource  ` (message)
  - `  MultimodalDatasetMetadata.MultimodalDatasetInputConfig  ` (message)
  - `  PredictionResult  ` (message)
  - `  PredictionResult.Error  ` (message)
  - `  TablesDatasetMetadata  ` (message)
  - `  TablesDatasetMetadata.BigQuerySource  ` (message)
  - `  TablesDatasetMetadata.GcsSource  ` (message)
  - `  TablesDatasetMetadata.InputConfig  ` (message)
  - `  TextClassificationAnnotation  ` (message)
  - `  TextDataItem  ` (message)
  - `  TextDatasetMetadata  ` (message)
  - `  TextExtractionAnnotation  ` (message)
  - `  TextSegment  ` (message)
  - `  TextSentimentAnnotation  ` (message)
  - `  TextSentimentSavedQueryMetadata  ` (message)
  - `  TimeSegment  ` (message)
  - `  TimeSeriesDatasetMetadata  ` (message)
  - `  TimeSeriesDatasetMetadata.BigQuerySource  ` (message)
  - `  TimeSeriesDatasetMetadata.GcsSource  ` (message)
  - `  TimeSeriesDatasetMetadata.InputConfig  ` (message)
  - `  Vertex  ` (message)
  - `  VideoActionRecognitionAnnotation  ` (message)
  - `  VideoClassificationAnnotation  ` (message)
  - `  VideoDataItem  ` (message)
  - `  VideoDatasetMetadata  ` (message)
  - `  VideoObjectTrackingAnnotation  ` (message)
  - `  VisualInspectionClassificationLabelSavedQueryMetadata  ` (message)
  - `  VisualInspectionMaskSavedQueryMetadata  ` (message)

## AnnotationSpecColor

An entry of mapping between color and AnnotationSpec. The mapping is used in segmentation mask.

Fields

`color`

`  Color  `

The color of the AnnotationSpec in a segmentation mask.

`display_name`

`string`

The display name of the AnnotationSpec represented by the color in the segmentation mask.

`id`

`string`

The ID of the AnnotationSpec represented by the color in the segmentation mask.

## ImageBoundingBoxAnnotation

Annotation details specific to image object detection.

Fields

`annotation_spec_id`

`string`

The resource Id of the AnnotationSpec that this Annotation pertains to.

`display_name`

`string`

The display name of the AnnotationSpec that this Annotation pertains to.

`x_min`

`double`

The leftmost coordinate of the bounding box.

`x_max`

`double`

The rightmost coordinate of the bounding box.

`y_min`

`double`

The topmost coordinate of the bounding box.

`y_max`

`double`

The bottommost coordinate of the bounding box.

## ImageClassificationAnnotation

Annotation details specific to image classification.

Fields

`annotation_spec_id`

`string`

The resource Id of the AnnotationSpec that this Annotation pertains to.

`display_name`

`string`

The display name of the AnnotationSpec that this Annotation pertains to.

## ImageDataItem

Payload of Image DataItem.

Fields

`gcs_uri`

`string`

Required. Google Cloud Storage URI points to the original image in user's bucket. The image is up to 30MB in size.

`mime_type`

`string`

Output only. The mime type of the content of the image. Only the images in below listed mime types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon

## ImageDatasetMetadata

The metadata of Datasets that contain Image DataItems.

Fields

`data_item_schema_uri`

`string`

Points to a YAML file stored on Google Cloud Storage describing payload of the Image DataItems that belong to this Dataset.

`gcs_bucket`

`string`

Google Cloud Storage Bucket name that contains the blob data of this Dataset.

## ImageSegmentationAnnotation

Annotation details specific to image segmentation.

Fields

Union field `annotation` .

`annotation` can be only one of the following:

`mask_annotation`

`  MaskAnnotation  `

Mask based segmentation annotation. Only one mask annotation can exist for one image.

`polygon_annotation`

`  PolygonAnnotation  `

Polygon annotation.

`polyline_annotation`

`  PolylineAnnotation  `

Polyline annotation.

## MaskAnnotation

The mask based segmentation annotation.

Fields

`mask_gcs_uri`

`string`

Google Cloud Storage URI that points to the mask image. The image must be in PNG format. It must have the same size as the DataItem's image. Each pixel in the image mask represents the AnnotationSpec which the pixel in the image DataItem belong to. Each color is mapped to one AnnotationSpec based on annotation\_spec\_colors.

`annotation_spec_colors[]`

`  AnnotationSpecColor  `

The mapping between color and AnnotationSpec for this Annotation.

## PolygonAnnotation

Represents a polygon in image.

Fields

`vertexes[]`

`  Vertex  `

The vertexes are connected one by one and the last vertex is connected to the first one to represent a polygon.

`annotation_spec_id`

`string`

The resource Id of the AnnotationSpec that this Annotation pertains to.

`display_name`

`string`

The display name of the AnnotationSpec that this Annotation pertains to.

## PolylineAnnotation

Represents a polyline in image.

Fields

`vertexes[]`

`  Vertex  `

The vertexes are connected one by one and the last vertex in not connected to the first one.

`annotation_spec_id`

`string`

The resource Id of the AnnotationSpec that this Annotation pertains to.

`display_name`

`string`

The display name of the AnnotationSpec that this Annotation pertains to.

## MultimodalDatasetMetadata

The metadata of Multimodal Datasets.

Fields

`input_config`

`  MultimodalDatasetInputConfig  `

Specifies the input source and configuration.

`gemini_request_read_config`

`  GeminiRequestReadConfig  `

The configuration for how to read Gemini requests from the dataset.

`key_column_name`

`string`

The name of the column in the BigQuery table that contains the keys of the rows.

## BigQuerySource

Specifies the BigQuery source.

Fields

`uri`

`string`

The URI of a BigQuery table. e.g. <bq://project.bqDataset.bqTable>

## MultimodalDatasetInputConfig

Specifies the input source and configuration.

Fields

Union field `source` . The source of the input. We only support BigQuery as source for now. `source` can be only one of the following:

`bigquery_source`

`  BigQuerySource  `

BigQuery source table.

## PredictionResult

Represents a line of JSONL in the batch prediction output file.

Fields

`prediction`

`  Value  `

The prediction result. Value is used here instead of Any so that JsonFormat does not append an extra "@type" field when we convert the proto to JSON and so we can represent array of objects. Do not set error if this is set.

`error`

`  Error  `

The error result. Do not set prediction if this is set.

Union field `input` . Some identifier from the input so that the prediction can be mapped back to the input instance. `input` can be only one of the following:

`instance`

`  Struct  `

User's input instance. Struct is used here instead of Any so that JsonFormat does not append an extra "@type" field when we convert the proto to JSON.

`key`

`string`

Optional user-provided key from the input instance.

## Error

Fields

`status`

`  Code  `

Error status. This will be serialized into the enum name e.g. "NOT\_FOUND".

`message`

`string`

Error message with additional details.

## TablesDatasetMetadata

The metadata of Datasets that contain tables data.

Fields

`input_config`

`  InputConfig  `

## BigQuerySource

Fields

`uri`

`string`

The URI of a BigQuery table. e.g. <bq://projectId.bqDatasetId.bqTableId>

## GcsSource

Fields

`uri[]`

`string`

Cloud Storage URI of one or more files. Only CSV files are supported. The first line of the CSV file is used as the header. If there are multiple files, the header is the first line of the lexicographically first file, the other files must either contain the exact same header or omit the header.

## InputConfig

The tables Dataset's data source. The Dataset doesn't store the data directly, but only pointer(s) to its data.

Fields

Union field `source` .

`source` can be only one of the following:

`gcs_source`

`  GcsSource  `

`bigquery_source`

`  BigQuerySource  `

## TextClassificationAnnotation

Annotation details specific to text classification.

Fields

`annotation_spec_id`

`string`

The resource Id of the AnnotationSpec that this Annotation pertains to.

`display_name`

`string`

The display name of the AnnotationSpec that this Annotation pertains to.

## TextDataItem

Payload of Text DataItem.

Fields

`gcs_uri`

`string`

Output only. Google Cloud Storage URI points to a copy of the original text in the Vertex-managed bucket in the user's project. The text file is up to 10MB in size.

## TextDatasetMetadata

The metadata of Datasets that contain Text DataItems.

Fields

`data_item_schema_uri`

`string`

Points to a YAML file stored on Google Cloud Storage describing payload of the Text DataItems that belong to this Dataset.

`gcs_bucket`

`string`

Google Cloud Storage Bucket name that contains the blob data of this Dataset.

## TextExtractionAnnotation

Annotation details specific to text extraction.

Fields

`text_segment`

`  TextSegment  `

The segment of the text content.

`annotation_spec_id`

`string`

The resource Id of the AnnotationSpec that this Annotation pertains to.

`display_name`

`string`

The display name of the AnnotationSpec that this Annotation pertains to.

## TextSegment

The text segment inside of DataItem.

Fields

`start_offset`

`uint64`

Zero-based character index of the first character of the text segment (counting characters from the beginning of the text).

`end_offset`

`uint64`

Zero-based character index of the first character past the end of the text segment (counting character from the beginning of the text). The character at the end\_offset is NOT included in the text segment.

`content`

`string`

The text content in the segment for output only.

## TextSentimentAnnotation

Annotation details specific to text sentiment.

Fields

`sentiment`

`int32`

The sentiment score for text.

`sentiment_max`

`int32`

The sentiment max score for text.

`annotation_spec_id`

`string`

The resource Id of the AnnotationSpec that this Annotation pertains to.

`display_name`

`string`

The display name of the AnnotationSpec that this Annotation pertains to.

## TextSentimentSavedQueryMetadata

The metadata of SavedQuery contains TextSentiment Annotations.

Fields

`sentiment_max`

`int32`

The maximum sentiment of sentiment Anntoation in this SavedQuery.

## TimeSegment

A time period inside of a DataItem that has a time dimension (e.g. video).

Fields

`start_time_offset`

`  Duration  `

Start of the time segment (inclusive), represented as the duration since the start of the DataItem.

`end_time_offset`

`  Duration  `

End of the time segment (exclusive), represented as the duration since the start of the DataItem.

## TimeSeriesDatasetMetadata

The metadata of Datasets that contain time series data.

Fields

`input_config`

`  InputConfig  `

`time_series_identifier_column`

`string`

The column name of the time series identifier column that identifies the time series.

`time_column`

`string`

The column name of the time column that identifies time order in the time series.

## BigQuerySource

Fields

`uri`

`string`

The URI of a BigQuery table.

## GcsSource

Fields

`uri[]`

`string`

Cloud Storage URI of one or more files. Only CSV files are supported. The first line of the CSV file is used as the header. If there are multiple files, the header is the first line of the lexicographically first file, the other files must either contain the exact same header or omit the header.

## InputConfig

The time series Dataset's data source. The Dataset doesn't store the data directly, but only pointer(s) to its data.

Fields

Union field `source` .

`source` can be only one of the following:

`gcs_source`

`  GcsSource  `

`bigquery_source`

`  BigQuerySource  `

## Vertex

Represents a 2D point in the image. Vertex coordinates are normalized to be relative to the original image dimensions and range from 0 to 1. The origin of the coordinate system (0,0) is the top-left corner of the image. x increases to the right, and y increases to the bottom.

Fields

`x`

`double`

X coordinate of the vertex, normalized to \[0.0, 1.0\].

`y`

`double`

Y coordinate of the vertex, normalized to \[0.0, 1.0\].

## VideoActionRecognitionAnnotation

Annotation details specific to video action recognition.

Fields

`time_segment`

`  TimeSegment  `

This Annotation applies to the time period represented by the TimeSegment. If it's not set, the Annotation applies to the whole video.

`annotation_spec_id`

`string`

The resource Id of the AnnotationSpec that this Annotation pertains to.

`display_name`

`string`

The display name of the AnnotationSpec that this Annotation pertains to.

## VideoClassificationAnnotation

Annotation details specific to video classification.

Fields

`time_segment`

`  TimeSegment  `

This Annotation applies to the time period represented by the TimeSegment. If it's not set, the Annotation applies to the whole video.

`annotation_spec_id`

`string`

The resource Id of the AnnotationSpec that this Annotation pertains to.

`display_name`

`string`

The display name of the AnnotationSpec that this Annotation pertains to.

## VideoDataItem

Payload of Video DataItem.

Fields

`gcs_uri`

`string`

Required. Google Cloud Storage URI points to the original video in user's bucket. The video is up to 50 GB in size and up to 3 hour in duration.

`mime_type`

`string`

Output only. The mime type of the content of the video. Only the videos in below listed mime types are supported. Supported mime\_type: - video/mp4 - video/avi - video/quicktime

## VideoDatasetMetadata

The metadata of Datasets that contain Video DataItems.

Fields

`data_item_schema_uri`

`string`

Points to a YAML file stored on Google Cloud Storage describing payload of the Video DataItems that belong to this Dataset.

`gcs_bucket`

`string`

Google Cloud Storage Bucket name that contains the blob data of this Dataset.

## VideoObjectTrackingAnnotation

Annotation details specific to video object tracking.

Fields

`time_offset`

`  Duration  `

A time (frame) of a video to which this annotation pertains. Represented as the duration since the video's start.

`x_min`

`double`

The leftmost coordinate of the bounding box.

`x_max`

`double`

The rightmost coordinate of the bounding box.

`y_min`

`double`

The topmost coordinate of the bounding box.

`y_max`

`double`

The bottommost coordinate of the bounding box.

`instance_id`

`int64`

The instance of the object, expressed as a positive integer. Used to track the same object across different frames.

`annotation_spec_id`

`string`

The resource Id of the AnnotationSpec that this Annotation pertains to.

`display_name`

`string`

The display name of the AnnotationSpec that this Annotation pertains to.

## VisualInspectionClassificationLabelSavedQueryMetadata

Fields

`multi_label`

`bool`

Whether or not the classification label is multi\_label.

## VisualInspectionMaskSavedQueryMetadata

This type has no fields.
