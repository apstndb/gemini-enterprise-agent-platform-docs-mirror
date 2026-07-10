---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/overview
title: Classification and regression overview
description: Learn about the workflow for creating a classification or regression model and making inferences in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

**Binary classification** models predict a binary outcome (one of two classes). Use this model type for yes or no questions. For example, you might want to build a binary classification model to predict whether a customer would buy a subscription. Generally, a binary classification problem requires less data than other model types.

**Multi-class classification** models predict one class from three or more discrete classes. Use this model type for categorization. For example, as a retailer, you might want to build a multi-class classification model to segment customers into different personas.

**Regression** models predict a continuous value. For example, as a retailer, you might want to build a regression model to predict how much a customer will spend next month.

## Workflow for creating a classification or regression model and making inferences

The process for creating a classification or regression model in Agent Platform is as follows:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Steps</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1. <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/prepare-data">Prepare training data</a></td>
<td>Prepare your training data for model training.</td>
</tr>
<tr class="even">
<td>2. <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/create-dataset">Create a dataset</a></td>
<td>Create a new dataset and associate your prepared training data with it.</td>
</tr>
<tr class="odd">
<td>3. <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model">Train a model</a></td>
<td>Train a classification or regression model in Gemini Enterprise Agent Platform using your dataset.</td>
</tr>
<tr class="even">
<td>4. <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/evaluate-model">Evaluate your model</a></td>
<td>Evaluate your newly trained model for inference accuracy.</td>
</tr>
<tr class="odd">
<td>5. <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging">View model architecture</a></td>
<td>View the hyperparameter logs of the tuning trials and the hyperparameter logs of the final model.</td>
</tr>
<tr class="even">
<td>6. Get inferences from your model</td>
<td><p>To get real-time inferences, deploy your model and <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions">get online inferences</a> .</p>
<p>If you don't need real-time inferences, make <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions">batch inference requests</a> directly to your model.</p></td>
</tr>
</tbody>
</table>

> To see an example of how to create, train, and use an AutoML classification model for online predictions, run the "AutoML tabular training and prediction" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl-tabular-classification.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml-tabular-classification.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml-tabular-classification.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl-tabular-classification.ipynb)

> To see an example of how to create, train, and use an AutoML regression model for batch predictions, run the "AutoML training tabular regression model for batch prediction using BigQuery" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_batch_bq.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_regression_batch_bq.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_regression_batch_bq.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_batch_bq.ipynb)

> To see an example of how to create, train, and use an AutoML regression model for online predictions, run the "AutoML training tabular regression model for online prediction using BigQuery" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_online_bq.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_regression_online_bq.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_regression_online_bq.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_online_bq.ipynb)
