---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/batchprediction-component
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/batchprediction-component
title: Batch prediction components
description: Learn how to serve batch predictions in your ML workflows using batch prediction components in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

> To learn more, run the "Learn how to use prebuilt Pipeline Components to train a custom model" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/custom_model_training_and_batch_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fcustom_model_training_and_batch_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fcustom_model_training_and_batch_prediction.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/custom_model_training_and_batch_prediction.ipynb)

The `BatchPredictionJob` resource lets you run an asynchronous prediction request. Request batch predictions directly from the `model` resource. You don't need to deploy the model to an `endpoint` . For data types that support both batch and online predictions you can use batch predictions. This is useful when you don't require an immediate response and want to process accumulated data by using a single request.

To make a batch prediction, specify an input source and an output location for Gemini Enterprise Agent Platform to store predictions results. The inputs and outputs depend on the `model` type that you're working with. For example, batch predictions for the AutoML image model type require an input [JSON Lines](https://jsonlines.org/) file and the name of a Cloud Storage bucket to store the output. For more information about batch prediction, see [Get batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/batch-predictions) .

You can use the [`ModelBatchPredictOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/batch_predict_job.html#v1.batch_predict_job.ModelBatchPredictOp) component to access this resource through Gemini Enterprise Agent Platform Pipelines.

## API reference

  - For component reference, see the [Google Cloud SDK reference for Batch prediction components](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/batch_predict_job.html) .
  - For Agent Platform API reference, see the [`BatchPredictionJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs) page.

## Tutorials

  - [Custom training with prebuilt Google Cloud Pipeline Components](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/custom_model_training_and_batch_prediction.ipynb)

### Version history and release notes

To learn more about the version history and changes to the Google Cloud Pipeline Components SDK, see the [Google Cloud Pipeline Components SDK Release Notes](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/release.html) .

### Technical support contacts

If you have any questions, reach out to [kubeflow-pipelines-components@google.com](mailto:%20kubeflow-pipelines-components@google.com) .
