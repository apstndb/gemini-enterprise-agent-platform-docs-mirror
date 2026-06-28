---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-training-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-training-overview
title: AutoML training overview
description: AutoML on Gemini Enterprise Agent Platform enables training high-quality machine learning models with minimal effort and expertise, and this page provides an overview of the workflow for training and using your own models on Agent Platform.
data_source: docs.cloud.google.com
---

AutoML (Automated Machine Learning) on Gemini Enterprise Agent Platform provides a way to train high-quality machine learning models with minimal effort and machine learning expertise. This page provides an overview of the workflow for training and using your own models on Gemini Enterprise Agent Platform.

## Types of models you can build using AutoML

The types of models you can build depend on the type of data that you have. Gemini Enterprise Agent Platform offers AutoML solutions for the following data types and model objectives:

| Data type    | Supported objectives                    |
| ------------ | --------------------------------------- |
| Image data   | Classification, object detection.       |
| Tabular data | Classification/regression, forecasting. |

> **Note:** If you need help with setting up your machine learning problem from a Google data scientist, contact your Google Account manager.

The workflow for training and using an AutoML model is the same, regardless of your data type or objective:

1.  Prepare your training data.
2.  Create a dataset.
3.  Train a model.
4.  Evaluate and iterate on your model.
5.  Get inferences from your model.
6.  Interpret inference results.

## Image data

AutoML uses machine learning to analyze the content of image data. You can use AutoML to train an ML model to classify image data or find objects in image data.

Gemini Enterprise Agent Platform lets you get online inferences and batch inferences from your image-based models. Online inferences are synchronous requests made to a model endpoint. Use online inferences when you are making requests in response to application input or in situations that require timely inferences. Batch inferences are asynchronous requests. You request batch inferences directly from the model resource without needing to deploy the model to an endpoint. For image data, use batch inferences when you don't require an immediate response and want to process accumulated data by using a single request.

### Classification for images

A **classification** model analyzes image data and returns a list of content categories that apply to the image. For example, you can train a model that classifies images as containing a cat or not containing a cat, or you could train a model to classify images of dogs by breed.

Documentation: [Prepare data](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data) | [Create dataset](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/create-dataset) | [Train model](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/train-model) | [Evaluate model](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/evaluate-model) | [Get inferences](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/get-predictions) | [Interpret results](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/interpret-results)

> To see an example of how to train an image classification model and get batch predictions as part of a more comprehensive workflow, run the "AutoML training image classification model for batch prediction" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_classification_batch_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml_image_classification_batch_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml_image_classification_batch_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_classification_batch_prediction.ipynb)

### Object detection for images

An **object detection** model analyzes your image data and returns annotations for all objects found in an image, consisting of a label and bounding box location for each object. For example, you can train a model to find the location of the cats in image data.

Documentation: [Prepare data](https://docs.cloud.google.com/vertex-ai/docs/image-data/object-detection/prepare-data) | [Create dataset](https://docs.cloud.google.com/vertex-ai/docs/image-data/object-detection/create-dataset) | [Train model](https://docs.cloud.google.com/vertex-ai/docs/image-data/object-detection/train-model) | [Evaluate model](https://docs.cloud.google.com/vertex-ai/docs/image-data/object-detection/evaluate-model) | [Get inferences](https://docs.cloud.google.com/vertex-ai/docs/image-data/object-detection/get-predictions) | [Interpret results](https://docs.cloud.google.com/vertex-ai/docs/image-data/object-detection/interpret-results)

> To see an example of how to train an object detection model and get online inferences as part of a more comprehensive workflow, run the "AutoML training image object detection model for online prediction" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_object_detection_online_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml_image_object_detection_online_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml_image_object_detection_online_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_object_detection_online_prediction.ipynb)

> To see an example of how to train an object detection model and get batch inferences as part of a more comprehensive workflow, run the "AutoML training image object detection model for batch prediction" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_image_object_detection_batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_image_object_detection_batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_image_object_detection_batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_image_object_detection_batch.ipynb)

## Tabular data

Agent Platform lets you perform machine learning with tabular data using straightforward processes and interfaces. You can create the following model types for your tabular data problems:

  - **Binary classification** models predict a binary outcome (one of two classes). Use this model type for yes or no questions. For example, you might want to build a binary classification model to predict whether a customer would buy a subscription. Generally, a binary classification problem requires less data than other model types.
  - **Multi-class classification** models predict one class from three or more discrete classes. Use this model type for categorization. For example, as a retailer, you might want to build a multi-class classification model to segment customers into different personas.
  - **Regression** models predict a continuous value. For example, as a retailer, you might want to build a regression model to predict how much a customer will spend next month.
  - **Forecasting** models predict a sequence of values. For example, as a retailer, you might want to forecast daily demand of your products for the next 3 months so that you can appropriately stock product inventories in advance.

To learn more, see [Tabular data overview](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/overview) .

If your tabular data is stored in BigQuery ML, you can train an AutoML tabular model directly in BigQuery ML. To learn more, see [AutoML Tabular reference documentation](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl) .

## What's next

  - [AutoML beginner's guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/beginner/beginners-guide)
