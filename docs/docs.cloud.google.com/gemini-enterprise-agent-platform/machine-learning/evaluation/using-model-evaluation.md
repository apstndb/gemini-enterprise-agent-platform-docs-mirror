---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/using-model-evaluation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/using-model-evaluation
title: Evaluate models using Agent Platform
description: Create a model evaluation, then view and compare evaluation metrics in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page describes how to evaluate models using Gemini Enterprise Agent Platform. For an overview, see [model evaluation in Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/introduction) .

## Prerequisites

1.  Follow the steps at [Set up a project and a development environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/cloud-environment) . In addition, enable the following services:
    
      - [Compute Engine API](https://console.cloud.google.com/apis/enableflow?apiid=compute.googleapis.com)
      - [Dataflow API](https://console.cloud.google.com/apis/enableflow?apiid=dataflow.googleapis.com)

2.  Agent Platform can evaluate models that are trained either through AutoML or custom training. For the Google Cloud console guide, you should have a trained model [imported to Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) .

3.  Upload your test dataset to [BigQuery](https://docs.cloud.google.com/bigquery/docs/loading-data) or [Cloud Storage](https://docs.cloud.google.com/storage/docs/uploading-objects) . The test dataset should contain the ground truth, which is the actual result expected for an inference. Obtain the link to the file or the dataset ID.

4.  Have a [batch inference output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions) in the form of a BigQuery table or Cloud Storage URI.

5.  Make sure your [default Compute Engine service account](https://docs.cloud.google.com/iam/docs/service-account-types#default) has the following [IAM permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/iam-permissions) :
    
      - Agent Platform Administrator ( `aiplatform.admin` )
      - Agent Platform Service Agent ( `aiplatform.serviceAgent` )
      - Storage Object Admin ( `storage.objectAdmin` )
      - Dataflow Worker ( `dataflow.worker` )
      - BigQuery Data Editor ( `bigquery.dataEditor` ) (only required if you are providing data in the form of BigQuery tables)

## Create an evaluation

### Console

1.  In the Google Cloud console, go to the Gemini Enterprise Agent Platform Models page.

2.  Click the name of the model you want to evaluate.

3.  Click the version number for the model.

4.  On the **Evaluate** tab, click **Create Evaluation** .

5.  Enter an **Evaluation name** .

6.  Select an **Objective** , such as classification or regression.

7.  Enter the **Evaluation target column name** , which is the column from the training data that the model is trained to predict.

8.  For **Select source** , select the source for your test dataset.
    
    1.  For **BigQuery table** , enter the **BigQuery path** .
    
    2.  For **File on Cloud Storage** , enter the **Cloud Storage path** .

9.  For **Batch prediction output** , select an output format.
    
    1.  Enter the BigQuery path or Cloud Storage URI.

10. Click **Start Evaluation** .

### Python

To view the Agent Platform API model evaluation workflow in Gemini Enterprise Agent Platform Pipelines, see the example notebooks for the following model types:

  - [AutoML tabular classification](https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_classification_model_evaluation.ipynb)

  - [AutoML tabular regression](https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_regression_model_evaluation.ipynb)

  - [Custom tabular classification](https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_classification_model_evaluation.ipynb)

  - [Custom tabular regression](https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_regression_model_evaluation.ipynb)

### Python SDK

The SDK for evaluating models with Agent Platform is in Experimental. To sign up for the Experimental, fill out the [onboarding form](https://docs.google.com/forms/d/159DJxDx8cQpsjwsNkS7j-qCwsz2uTDVwVQPv4ZfWM50/viewform?edit_requested=true) .

Agent Platform automatically sends an email notification when a model evaluation job is complete.

## View evaluation metrics

> **Note:** For [BigQuery ML models](https://docs.cloud.google.com/bigquery/docs/model_eval) that are registered to Model Registry, Gemini Enterprise Agent Platform only shows evaluation metrics for regression and binary classification models.

### Console

1.  In the Google Cloud console, go to the Gemini Enterprise Agent Platform Models page.

2.  Navigate to the model version.

3.  View metrics in the **Evaluate** tab.

### Python

To view the Agent Platform API model evaluation workflow in Gemini Enterprise Agent Platform Pipelines, see the example notebooks for the following model types:

  - [AutoML tabular classification](https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_classification_model_evaluation.ipynb)

  - [AutoML tabular regression](https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_regression_model_evaluation.ipynb)

  - [Custom tabular classification](https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_classification_model_evaluation.ipynb)

  - [Custom tabular regression](https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_regression_model_evaluation.ipynb)

### Python SDK

The SDK for evaluating models with Agent Platform is in Experimental. To sign up for the Experimental, fill out the [onboarding form](https://docs.google.com/forms/d/159DJxDx8cQpsjwsNkS7j-qCwsz2uTDVwVQPv4ZfWM50/viewform?edit_requested=true) .

## Compare evaluation metrics

You can compare evaluation results across different models, model versions, and evaluation jobs. For more information about model versioning, see [Versioning in Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/versioning) .

You can only compare models of the same type, such as classification, regression, or forecasting. When comparing different models, all the model versions must be the same type.

You can only compare 5 or fewer evaluations at a time.

1.  Go to the Gemini Enterprise Agent Platform Model Registry in the Google Cloud console:

2.  Navigate to your model or model version:
    
      - To compare across different models on the **Models** page, select the checkboxes next to the names of the models you want to compare.
    
      - To compare across different model versions:
        
        1.  Click the name of your model on the **Models** page to open the list of model versions.
        
        2.  Select the checkboxes next to the versions you want to compare.
    
      - To compare across evaluation jobs for the same model version:
        
        1.  Click the name of your model on the **Models** page to open the list of model versions.
        
        2.  Click the version number.
        
        3.  Select the checkboxes next to the evaluation jobs you want to compare.

3.  Click **Compare** .

## What's next

  - Learn how to [iterate on your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/evaluating-automl-models#iterate) .
