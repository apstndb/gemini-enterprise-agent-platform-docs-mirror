---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/prepare-data
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/prepare-data
title: Prepare image training data for classification
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page describes how to prepare image training data for use in a Gemini Enterprise Agent Platform dataset to train an image classification model.

The following objective sections include information about data requirements, the input/output schema file, and the format of the data import files ( [JSON Lines](https://jsonlines.org/) & CSV) that are defined by the schema.

### Permissions

To use images from a Cloud Storage bucket, you must grant the [Agent Platform Service Agent](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#service-agents) the `Storage Object Viewer` role for the bucket. The Service Agent is a Google-managed service account that Agent Platform uses to access your data on your behalf. For a more detailed explanation, see [Service agents](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#service-agents) .

### Single-label classification

### Data requirements

**Training data** : The following image formats are supported when training your model. After Vertex AI API preprocesses these imported images they serve as the data used to train a model. Maximum file size per image is 30MB.

  - JPEG
  - GIF
  - PNG
  - BMP
  - ICO

**Prediction data** : The following image formats are supported when requesting a prediction from (querying) your model. Maximum file size is 1.5MB.

  - JPEG
  - GIF
  - PNG
  - WEBP
  - BMP
  - TIFF
  - ICO

> **Note** : The Vertex AI API currently only supports sending base64-encoded image content to the predict method.

## Best practices for image data used to train AutoML models

The following best practices apply to datasets that train models using AutoML.

AutoML models are optimized for photographs of objects in the real world.

The training data should be as close as possible to the data on which predictions are to be made. For example, if your use case involves blurry and low-resolution images (such as from a security camera), your training data should be composed of blurry, low-resolution images. In general, you should also consider providing multiple angles, resolutions, and backgrounds for your training images.

Vertex AI models can't generally predict labels that humans can't assign. So, if a human can't be trained to assign labels by looking at the image for 1-2 seconds, the model likely can't be trained to do it either.

We recommend about 1000 training images per label. The minimum per label is 10. In general it takes more examples per label to train models with multiple labels per image, and resulting scores are harder to interpret.

The model works best when there are at most 100x more images for the most common label than for the least common label. We recommend removing very low frequency labels.

Consider including a **None\_of\_the\_above** label and images that don't match any of your defined labels. For example, for a flower dataset, include images of flowers outside of your labeled varieties, and label them as **None\_of\_the\_above** .

### YAML schema file

Use the following publicly accessible schema file to import single-label image classification annotations. This schema file dictates the format of the data input files. This file's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[`gs://google-cloud-aiplatform/schema/dataset/ioformat/image_classification_single_label_io_format_1.0.0.yaml`](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/image_classification_single_label_io_format_1.0.0.yaml)

#### Full schema file

    title: ImageClassificationSingleLabel
    description: >
     Import and export format for importing/exporting images together with
     single-label classification annotation. Can be used in
     Dataset.import_schema_uri field.
    type: object
    required:
    - imageGcsUri
    properties:
     imageGcsUri:
       type: string
       description: >
         A Cloud Storage URI pointing to an image. Up to 30MB in size.
         Supported file mime types: `image/jpeg`, `image/gif`, `image/png`,
         `image/webp`, `image/bmp`, `image/tiff`, `image/vnd.microsoft.icon`.
     classificationAnnotation:
       type: object
       description: Single classification Annotation on the image.
       properties:
         displayName:
           type: string
           description: >
             It will be imported as/exported from AnnotationSpec's display name,
             i.e. the name of the label/class.
         annotationResourceLabels:
           description: Resource labels on the Annotation.
           type: object
           additionalProperties:
             type: string
     dataItemResourceLabels:
       description: Resource labels on the DataItem.
       type: object
       additionalProperties:
         type: string

### Input files

### JSON Lines

JSON on each line:

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

  - `imageGcsUri` - The only required field.

  - `annotationResourceLabels` - Can contain any number of key-value string pairs. The only system-reserved key-value pair is the following:
    
      - "aiplatform.googleapis.com/annotation\_set\_name" : " value "
    
    Where value is one of the display names of the existing annotation sets in the dataset.

  - `dataItemResourceLabels` - Can contain any number of key-value string pairs. The only system-reserved key-value pair is the following which specifies the machine learning use set of the data item:
    
      - "aiplatform.googleapis.com/ml\_use" : " training/test/validation "

#### Example JSON Lines - `image_classification_single_label.jsonl` :

    {"imageGcsUri": "gs://bucket/filename1.jpeg",  "classificationAnnotation": {"displayName": "daisy"}, "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "test"}}
    {"imageGcsUri": "gs://bucket/filename2.gif",  "classificationAnnotation": {"displayName": "dandelion"}, "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename3.png",  "classificationAnnotation": {"displayName": "roses"}, "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename4.bmp",  "classificationAnnotation": {"displayName": "sunflowers"}, "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename5.tiff",  "classificationAnnotation": {"displayName": "tulips"}, "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "validation"}}
    ...

### CSV

CSV format:

    [ML_USE],GCS_FILE_PATH,[LABEL]

**List of columns**

  - `ML_USE` (Optional) - For data split purposes when training a model. Use TRAINING, TEST, or VALIDATION. For more information about manual data splitting, see [About data splits for AutoML models](https://docs.cloud.google.com/vertex-ai/docs/general/ml-use) .
  - `GCS_FILE_PATH` - This field contains the Cloud Storage URI for the image. Cloud Storage URIs are case-sensitive.
  - `LABEL` (Optional) - Labels must start with a letter and only contain letters, numbers, and underscores.

#### Example CSV - `image_classification_single_label.csv` :

``` 
test,gs://bucket/filename1.jpeg,daisy
training,gs://bucket/filename2.gif,dandelion
gs://bucket/filename3.png
gs://bucket/filename4.bmp,sunflowers
validation,gs://bucket/filename5.tiff,tulips
...
    
```

### Multi-label classification

### Data requirements

**Training data** : The following image formats are supported when training your model. After Vertex AI API preprocesses these imported images they serve as the data used to train a model. Maximum file size per image is 30MB.

  - JPEG
  - GIF
  - PNG
  - BMP
  - ICO

**Prediction data** : The following image formats are supported when requesting a prediction from (querying) your model. Maximum file size is 1.5MB.

  - JPEG
  - GIF
  - PNG
  - WEBP
  - BMP
  - TIFF
  - ICO

> **Note** : The Vertex AI API currently only supports sending base64-encoded image content to the predict method.

## Best practices for image data used to train AutoML models

The following best practices apply to datasets that train models using AutoML.

AutoML models are optimized for photographs of objects in the real world.

The training data should be as close as possible to the data on which predictions are to be made. For example, if your use case involves blurry and low-resolution images (such as from a security camera), your training data should be composed of blurry, low-resolution images. In general, you should also consider providing multiple angles, resolutions, and backgrounds for your training images.

Vertex AI models can't generally predict labels that humans can't assign. So, if a human can't be trained to assign labels by looking at the image for 1-2 seconds, the model likely can't be trained to do it either.

We recommend about 1000 training images per label. The minimum per label is 10. In general it takes more examples per label to train models with multiple labels per image, and resulting scores are harder to interpret.

The model works best when there are at most 100x more images for the most common label than for the least common label. We recommend removing very low frequency labels.

Consider including a **None\_of\_the\_above** label and images that don't match any of your defined labels. For example, for a flower dataset, include images of flowers outside of your labeled varieties, and label them as **None\_of\_the\_above** .

### YAML schema file

Use the following publicly accessible schema file to import multi-label image classification annotations. This schema file dictates the format of the data input files. This file's structure follows the [OpenAPI schema](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schema) .

[`gs://google-cloud-aiplatform/schema/dataset/ioformat/image_classification_multi_label_io_format_1.0.0.yaml`](https://storage.cloud.google.com/google-cloud-aiplatform/schema/dataset/ioformat/image_classification_multi_label_io_format_1.0.0.yaml)

#### Full schema file

    title: ImageClassificationMultiLabel
    description: >
     Import and export format for importing/exporting images together with
     multi-label classification annotations. Can be used in
     Dataset.import_schema_uri field.
    type: object
    required:
    - imageGcsUri
    properties:
     imageGcsUri:
       type: string
       description: >
         A Cloud Storage URI pointing to an image. Up to 30MB in size.
         Supported file mime types: `image/jpeg`, `image/gif`, `image/png`,
         `image/webp`, `image/bmp`, `image/tiff`, `image/vnd.microsoft.icon`.
     classificationAnnotations:
       type: array
       description: Multiple classification Annotations on the image.
       items:
         type: object
         description: Classification annotation.
         properties:
           displayName:
             type: string
             description: >
               It will be imported as/exported from AnnotationSpec's display name,
               i.e. the name of the label/class.
           annotationResourceLabels:
             description: Resource labels on the Annotation.
             type: object
             additionalProperties:
               type: string
     dataItemResourceLabels:
       description: Resource labels on the DataItem.
       type: object
       additionalProperties:
         type: string

### Input files

### JSON Lines

JSON on each line:

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

  - `imageGcsUri` - The only required field.

  - `annotationResourceLabels` - Can contain any number of key-value string pairs. The only system-reserved key-value pair is the following:
    
      - "aiplatform.googleapis.com/annotation\_set\_name" : " value "
    
    Where value is one of the display names of the existing annotation sets in the dataset.

  - `dataItemResourceLabels` - Can contain any number of key-value string pairs. The only system-reserved key-value pair is the following which specifies the machine learning use set of the data item:
    
      - "aiplatform.googleapis.com/ml\_use" : " training/test/validation "

#### Example JSON Lines - `image_classification_multi_label.jsonl` :

    {"imageGcsUri": "gs://bucket/filename1.jpeg",  "classificationAnnotations": [{"displayName": "daisy"}, {"displayName": "full_shot"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "test"}}
    {"imageGcsUri": "gs://bucket/filename2.gif",  "classificationAnnotations": [{"displayName": "dandelion"}, {"displayName": "medium_shot"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename3.png",  "classificationAnnotations": [{"displayName": "roses"}, {"displayName": "extreme_closeup"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename4.bmp",  "classificationAnnotations": [{"displayName": "sunflowers"}, {"displayName": "closeup"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "training"}}
    {"imageGcsUri": "gs://bucket/filename5.tiff",  "classificationAnnotations": [{"displayName": "tulips"}, {"displayName": "extreme_closeup"}], "dataItemResourceLabels": {"aiplatform.googleapis.com/ml_use": "validation"}}
    ...

### CSV

CSV format:

    [ML_USE],GCS_FILE_PATH,[LABEL1,LABEL2,...LABELn]

**List of columns**

  - `ML_USE` (Optional) - For data split purposes when training a model. Use TRAINING, TEST, or VALIDATION. For more information about manual data splitting, see [About data splits for AutoML models](https://docs.cloud.google.com/vertex-ai/docs/general/ml-use) .
  - `GCS_FILE_PATH` - This field contains the Cloud Storage URI for the image. Cloud Storage URIs are case-sensitive.
  - `LABEL` (Optional) - Labels must start with a letter and only contain letters, numbers, and underscores.

#### Example CSV - `image_classification_multi_label.csv` :

``` 
test,gs://bucket/filename1.jpeg,daisy,full_shot
training,gs://bucket/filename2.gif,dandelion,medium_shot
gs://bucket/filename3.png
gs://bucket/filename4.bmp,sunflowers,closeup
validation,gs://bucket/filename5.tiff,tulips,extreme_closeup
...
    
```
