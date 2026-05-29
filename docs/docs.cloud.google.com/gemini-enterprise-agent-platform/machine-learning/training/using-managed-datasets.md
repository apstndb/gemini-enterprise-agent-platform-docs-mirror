---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-managed-datasets
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-managed-datasets
title: Use managed datasets
description: Learn how to use Agent Platform managed datasets to train custom models.
data_source: docs.cloud.google.com
---

This page shows you how to use Agent Platform managed datasets to train your custom models. Managed datasets offer the following benefits:

  - Manage your datasets in a central location.
  - Create labels and multiple annotation sets.
  - Create tasks for human labeling using integrated data labeling.
  - Track lineage to models for governance and iterative development.
  - Compare model performance by training AutoML and custom models using the same datasets.
  - Generate data statistics and visualizations.
  - Automatically split data into training, test, and validation sets.

## Before you begin

Before you can use a managed dataset in your training application, you must [create your dataset](https://docs.cloud.google.com/vertex-ai/docs/datasets/overview) . You must create the dataset and the training pipeline that you use for training in the same region. You must use a [region where `Dataset` resources are available](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .

## Access a dataset from your training application

> To see an example of using environment variables to access datasets as part of a more comprehensive workflow, run the ": Track parameters and metrics for custom training jobs" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/sdk-metric-parameter-tracking-for-custom-jobs.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fml_metadata%2Fsdk-metric-parameter-tracking-for-custom-jobs.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fml_metadata%2Fsdk-metric-parameter-tracking-for-custom-jobs.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/sdk-metric-parameter-tracking-for-custom-jobs.ipynb)

When you [create a serverless training pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) , you can specify that your training application uses an Agent Platform dataset.

At runtime, Agent Platform passes metadata about your dataset to your training application by setting the following environment variables in your training container.

  - `AIP_DATA_FORMAT` : The format that your dataset is exported in. Possible values include: `jsonl` , `csv` , or `bigquery` .
  - `AIP_TRAINING_DATA_URI` : The BigQuery URI of your training data or the Cloud Storage URI of your training data file.
  - `AIP_VALIDATION_DATA_URI` : The BigQuery URI for your validation data or the Cloud Storage URI of your validation data file.
  - `AIP_TEST_DATA_URI` : The BigQuery URI for your test data or the Cloud Storage URI of your test data file.

If the `AIP_DATA_FORMAT` of your dataset is `jsonl` or `csv` , the data URI values refer to Cloud Storage URIs, like `gs:// bucket_name / path /training-*` . To keep the size of each data file relatively small, Agent Platform splits your dataset into multiple files. Because your training, validation, or test data may be split into multiple files, the URIs are provided in wildcard format.

[Learn more about downloading objects using the Cloud Storage code samples](https://docs.cloud.google.com/storage/docs/downloading-objects#code-samples) .

If your `AIP_DATA_FORMAT` is `bigquery` , the data URI values refer to BigQuery URIs, like ` bq:// project . dataset . table  ` .

[Learn more about paging through BigQuery data](https://docs.cloud.google.com/bigquery/docs/paging-results) .

## Dataset format

Use the following sections to learn more about how Agent Platform formats your data when passing a dataset to your training application.

### Image datasets

Image datasets are passed to your training application in [JSON Lines](https://jsonlines.org/) format. Select the tab for your dataset's objective, to learn more about how Agent Platform formats your dataset.

### Single-label classification

Agent Platform uses the following publicly accessible schema when exporting a single-label image classification dataset. This schema dictates the format of the data export files. The schema's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[gs://google-cloud-aiplatform/schema/dataset/ioformat/image\_classification\_single\_label\_io\_format\_1.0.0.yaml](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/image_classification_single_label_io_format_1.0.0.yaml)

Each data item in your exported dataset uses the following format. This example includes line breaks for readability.

    {
      "imageGcsUri": "gs://bucket/filename.ext",
      "classificationAnnotation": {
        "displayName": "LABEL",
        "annotationResourceLabels": {
            "aiplatform.googleapis.com/annotation_set_name": "displayName",
            "env": "prod"
          }
       },
      "dataItemResourceLabels": {
        "aiplatform.googleapis.com/ml_use": "training/test/validation"
      }
    }

**Field notes** :

  - `imageGcsUri` : The Cloud Storage URI of this image.
  - `annotationResourceLabels` : Contains any number of key-value string pairs. Agent Platform uses this field to specify the annotation set.
  - `dataItemResourceLabels` - Contains any number of key-value string pairs. Specifies the machine learning use of the data item, such as training, test, or validation.

#### Example JSON Lines

    {"imageGcsUri": "gs://bucket/filename1.jpeg",  "classificationAnnotation": {"displayName": "daisy"}, "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "test"}}
    {"imageGcsUri": "gs://bucket/filename2.gif",  "classificationAnnotation": {"displayName": "dandelion"}, "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename3.png",  "classificationAnnotation": {"displayName": "roses"}, "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename4.bmp",  "classificationAnnotation": {"displayName": "sunflowers"}, "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename5.tiff",  "classificationAnnotation": {"displayName": "tulips"}, "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "validation"}}
    ...

### Multi-label classification

Agent Platform uses the following publicly accessible schema when exporting a multi-label image classification dataset. This schema dictates the format of the data export files. The schema's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[gs://google-cloud-aiplatform/schema/dataset/ioformat/image\_classification\_multi\_label\_io\_format\_1.0.0.yaml](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/image_classification_multi_label_io_format_1.0.0.yaml)

Each data item in your exported dataset uses the following format. This example includes line breaks for readability.

    {
      "imageGcsUri": "gs://bucket/filename.ext",
      "classificationAnnotations": [
        {
          "displayName": "LABEL1",
          "annotationResourceLabels": {
            "aiplatform.googleapis.com/annotation_set_name":"displayName",
            "label_type": "flower_type"
          }
        },
        {
          "displayName": "LABEL2",
          "annotationResourceLabels": {
            "aiplatform.googleapis.com/annotation_set_name":"displayName",
            "label_type": "image_shot_type"
          }
        }
      ],
      "dataItemResourceLabels": {
        "aiplatform.googleapis.com/ml_use": "training/test/validation"
      }
    }

**Field notes** :

  - `imageGcsUri` : The Cloud Storage URI of this image.
  - `annotationResourceLabels` : Contains any number of key-value string pairs. Agent Platform uses this field to specify the annotation set.
  - `dataItemResourceLabels` - Contains any number of key-value string pairs. Specifies the machine learning use of the data item, such as training, test, or validation.

#### Example JSON Lines

    {"imageGcsUri": "gs://bucket/filename1.jpeg",  "classificationAnnotations": [{"displayName": "daisy"}, {"displayName": "full_shot"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "test"}}
    {"imageGcsUri": "gs://bucket/filename2.gif",  "classificationAnnotations": [{"displayName": "dandelion"}, {"displayName": "medium_shot"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename3.png",  "classificationAnnotations": [{"displayName": "roses"}, {"displayName": "extreme_closeup"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename4.bmp",  "classificationAnnotations": [{"displayName": "sunflowers"}, {"displayName": "closeup"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename5.tiff",  "classificationAnnotations": [{"displayName": "tulips"}, {"displayName": "extreme_closeup"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "validation"}}
    ...

### Object detection

Agent Platform uses the following publicly accessible schema when exporting an object detection dataset. This schema dictates the format of the data export files. The schema's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[gs://google-cloud-aiplatform/schema/dataset/ioformat/image\_bounding\_box\_io\_format\_1.0.0.yaml](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/image_bounding_box_io_format_1.0.0.yaml)

Each data item in your exported dataset uses the following format. This example includes line breaks for readability.

    {
      "imageGcsUri": "gs://bucket/filename.ext",
      "boundingBoxAnnotations": [
        {
          "displayName": "OBJECT1_LABEL",
          "xMin": "X_MIN",
          "yMin": "Y_MIN",
          "xMax": "X_MAX",
          "yMax": "Y_MAX",
          "annotationResourceLabels": {
            "aiplatform.googleapis.com/annotation_set_name": "displayName",
            "env": "prod"
          }
        },
        {
          "displayName": "OBJECT2_LABEL",
          "xMin": "X_MIN",
          "yMin": "Y_MIN",
          "xMax": "X_MAX",
          "yMax": "Y_MAX"
        }
      ],
      "dataItemResourceLabels": {
        "aiplatform.googleapis.com/ml_use": "test/train/validation"
      }
    }

**Field notes** :

  - `imageGcsUri` : The Cloud Storage URI of this image.
  - `annotationResourceLabels` : Contains any number of key-value string pairs. Agent Platform uses this field to specify the annotation set.
  - `dataItemResourceLabels` - Contains any number of key-value string pairs. Specifies the machine learning use of the data item, such as training, test, or validation.

#### Example JSON Lines

    {"imageGcsUri": "gs://bucket/filename1.jpeg", "boundingBoxAnnotations": [{"displayName": "Tomato", "xMin": "0.3", "yMin": "0.3", "xMax": "0.7", "yMax": "0.6"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "test"}}
    {"imageGcsUri": "gs://bucket/filename2.gif", "boundingBoxAnnotations": [{"displayName": "Tomato", "xMin": "0.8", "yMin": "0.2", "xMax": "1.0", "yMax": "0.4"},{"displayName": "Salad", "xMin": "0.0", "yMin": "0.0", "xMax": "1.0", "yMax": "1.0"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename3.png", "boundingBoxAnnotations": [{"displayName": "Baked goods", "xMin": "0.5", "yMin": "0.7", "xMax": "0.8", "yMax": "0.8"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename4.tiff", "boundingBoxAnnotations": [{"displayName": "Salad", "xMin": "0.1", "yMin": "0.2", "xMax": "0.8", "yMax": "0.9"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "validation"}}
    ...

### Tabular datasets

Agent Platform passes tabular data to your training application in CSV format or as a URI to a BigQuery table or view. For more information about the data source format and requirements, see [Preparing your import source](https://docs.cloud.google.com/vertex-ai/docs/datasets/overview#tabular_data) . Refer to the dataset in Google Cloud console for more information about the dataset schema.

### Text datasets

Text datasets are passed to your training application in JSON Lines format. Select the tab for your dataset's objective, to learn more about how Agent Platform formats your dataset.

### Single-label classification

Agent Platform uses the following publicly accessible schema when exporting a single-label text classification dataset. This schema dictates the format of the data export files. The schema's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[gs://google-cloud-aiplatform/schema/dataset/ioformat/text\_classification\_single\_label\_io\_format\_1.0.0.yaml](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/text_classification_single_label_io_format_1.0.0.yaml)

Each data item in your exported dataset uses the following format. This example includes line breaks for readability.

    {
      "classificationAnnotation": {
        "displayName": "label"
      },
      "textContent": "inline_text",
      "dataItemResourceLabels": {
        "aiplatform.googleapis.com/ml_use": "training|test|validation"
      }
    }
    {
      "classificationAnnotation": {
        "displayName": "label2"
      },
      "textGcsUri": "gcs_uri_to_file",
      "dataItemResourceLabels": {
        "aiplatform.googleapis.com/ml_use": "training|test|validation"
      }
    }

### Multi-label classification

Agent Platform uses the following publicly accessible schema when exporting a multi-label text classification dataset. This schema dictates the format of the data export files. The schema's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[gs://google-cloud-aiplatform/schema/dataset/ioformat/text\_classification\_multi\_label\_io\_format\_1.0.0.yaml](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/text_classification_multi_label_io_format_1.0.0.yaml)

Each data item in your exported dataset uses the following format. This example includes line breaks for readability.

    {
      "classificationAnnotations": [{
        "displayName": "label1"
        },{
        "displayName": "label2"
      }],
      "textGcsUri": "gcs_uri_to_file",
      "dataItemResourceLabels": {
        "aiplatform.googleapis.com/ml_use": "training|test|validation"
      }
    }
    {
      "classificationAnnotations": [{
        "displayName": "label2"
        },{
        "displayName": "label3"
      }],
      "textContent": "inline_text",
      "dataItemResourceLabels": {
        "aiplatform.googleapis.com/ml_use": "training|test|validation"
      }
    }

### Entity extraction

Agent Platform uses the following publicly accessible schema when exporting an entity extraction dataset. This schema dictates the format of the data export files. The schema's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[gs://google-cloud-aiplatform/schema/dataset/ioformat/text\_extraction\_io\_format\_1.0.0.yaml](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/text_extraction_io_format_1.0.0.yaml) .

Each data item in your exported dataset uses the following format. This example includes line breaks for readability.

    {
        "textSegmentAnnotations": [
          {
            "startOffset":number,
            "endOffset":number,
            "displayName": "label"
          },
          ...
        ],
        "textContent": "inline_text",
        "dataItemResourceLabels": {
          "aiplatform.googleapis.com/ml_use": "training|test|validation"
        }
    }
    {
        "textSegmentAnnotations": [
          {
            "startOffset":number,
            "endOffset":number,
            "displayName": "label"
          },
          ...
        ],
        "textGcsUri": "gcs_uri_to_file",
        "dataItemResourceLabels": {
          "aiplatform.googleapis.com/ml_use": "training|test|validation"
        }
    }

### Sentiment analysis

Agent Platform uses the following publicly accessible schema when exporting a sentiment analysis dataset. This schema dictates the format of the data export files. The schema's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[gs://google-cloud-aiplatform/schema/trainingjob/definition/automl\_text\_sentiment\_1.0.0.yaml](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/automl_text_sentiment_1.0.0.yaml)

Each data item in your exported dataset uses the following format. This example includes line breaks for readability.

    {
      "sentimentAnnotation": {
        "sentiment": number,
        "sentimentMax": number
      },
      "textContent": "inline_text",
      "dataItemResourceLabels": {
        "aiplatform.googleapis.com/ml_use": "training|test|validation"
      }
    }
    {
      "sentimentAnnotation": {
        "sentiment": number,
        "sentimentMax": number
      },
      "textGcsUri": "gcs_uri_to_file",
      "dataItemResourceLabels": {
        "aiplatform.googleapis.com/ml_use": "training|test|validation"
      }
    }

### Video datasets

Video datasets are passed to your training application in JSON Lines format. Select the tab for your dataset's objective, to learn more about how Agent Platform formats your dataset.

### Action recognition

Agent Platform uses the following publicly accessible schema when exporting an action recognition dataset. This schema dictates the format of the data export files. The schema's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[gs://google-cloud-aiplatform/schema/dataset/ioformat/video\_action\_recognition\_io\_format\_1.0.0.yaml](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/video_action_recognition_io_format_1.0.0.yaml)

Each data item in your exported dataset uses the following format. This example includes line breaks for readability.

    {
      "videoGcsUri': "gs://bucket/filename.ext",
      "timeSegments": [{
        "startTime": "start_time_of_fully_annotated_segment",
        "endTime": "end_time_of_segment"}],
      "timeSegmentAnnotations": [{
        "displayName": "LABEL",
        "startTime": "start_time_of_segment",
        "endTime": "end_time_of_segment"
      }],
      "dataItemResourceLabels": {
        "ml_use": "train|test"
      }
    }

Note: The time segments here are used to calculate the timestamps of the actions. `startTime` and `endTime` of `timeSegmentAnnotations` can be equal, and corresponds to the key frame of the action.

#### Example JSON Lines

    {"videoGcsUri": "gs://demo/video1.mp4", "timeSegmentAnnotations": [{"displayName": "cartwheel", "startTime": "1.0s", "endTime": "12.0s"}], "dataItemResourceLabels": {"ml_use": "training"}}
    {"videoGcsUri": "gs://demo/video2.mp4", "timeSegmentAnnotations": [{"displayName": "swing", "startTime": "4.0s", "endTime": "9.0s"}], "dataItemResourceLabels": {"ml_use": "test"}}
    ...

### Classification

Agent Platform uses the following publicly accessible schema when exporting a classification dataset. This schema dictates the format of the data export files. The schema's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[gs://google-cloud-aiplatform/schema/dataset/ioformat/video\_classification\_io\_format\_1.0.0.yaml](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/video_classification_io_format_1.0.0.yaml)

Each data item in your exported dataset uses the following format. This example includes line breaks for readability.

    {
        "videoGcsUri": "gs://bucket/filename.ext",
        "timeSegmentAnnotations": [{
            "displayName": "LABEL",
            "startTime": "start_time_of_segment",
            "endTime": "end_time_of_segment"
        }],
        "dataItemResourceLabels": {
            "aiplatform.googleapis.com/ml_use": "train|test"
        }
    }

#### Example JSON Lines - Video classification:

    {"videoGcsUri": "gs://demo/video1.mp4", "timeSegmentAnnotations": [{"displayName": "cartwheel", "startTime": "1.0s", "endTime": "12.0s"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"videoGcsUri": "gs://demo/video2.mp4", "timeSegmentAnnotations": [{"displayName": "swing", "startTime": "4.0s", "endTime": "9.0s"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "test"}}
    ...

### Object tracking

Agent Platform uses the following publicly accessible schema when exporting an object tracking dataset. This schema dictates the format of the data export files. The schema's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[gs://google-cloud-aiplatform/schema/dataset/ioformat/object\_tracking\_io\_format\_1.0.0.yaml](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/video_object_tracking_io_format_1.0.0.yaml)

Each data item in your exported dataset uses the following format. This example includes line breaks for readability.

    {
        "videoGcsUri": "gs://bucket/filename.ext",
        "TemporalBoundingBoxAnnotations": [{
            "displayName": "LABEL",
            "xMin": "leftmost_coordinate_of_the_bounding box",
            "xMax": "rightmost_coordinate_of_the_bounding box",
            "yMin": "topmost_coordinate_of_the_bounding box",
            "yMax": "bottommost_coordinate_of_the_bounding box",
            "timeOffset": "timeframe_object-detected"
                    "instanceId": "instance_of_object
                    "annotationResourceLabels": "resource_labels"
        }],
        "dataItemResourceLabels": {
            "aiplatform.googleapis.com/ml_use": "train|test"
        }
    }

#### Example JSON Lines

    {'videoGcsUri': 'gs://demo-data/video1.mp4', 'temporal_bounding_box_annotations': [{'displayName': 'horse', 'instance_id': '-1', 'time_offset': '4.000000s', 'xMin': '0.668912', 'yMin': '0.560642', 'xMax': '1.000000', 'yMax': '1.000000'}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {'videoGcsUri': 'gs://demo-data/video2.mp4', 'temporal_bounding_box_annotations': [{'displayName': 'horse', 'instance_id': '-1', 'time_offset': '71.000000s', 'xMin': '0.679056', 'yMin': '0.070957', 'xMax': '0.801716', 'yMax': '0.290358'}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "test"}}
    ...

## What's next

  - Learn how to [use a managed dataset in serverless training by creating a training pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) .
