---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials
title: Tutorials overview
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Each of the tutorials presented here walks you through a specific artificial intelligence (AI) workflow, created to represent the most common tasks and to illustrate the capabilities of Gemini Enterprise Agent Platform. Choose the tutorial that best matches your data type and AI task. After following the tutorial, you can use the patterns that you have learned to solve your own AI problem. Gemini Enterprise Agent Platform offers Google Cloud console tutorials and notebook tutorials that use the Python SDK. You can open a notebook tutorial directly in Colab, download the notebook to your preferred environment, or [open the notebook tutorial in Vertex AI Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials#workbench) .

## Train a classification model for tabular data

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/images/automl-tables.svg" alt="Tabular classification training introduction" /></td>
<td><p>Create a Gemini Enterprise Agent Platform dataset from tabular data, and then train a classification model with AutoML. Deploy the model to an endpoint and make online predictions.</p>
<p><strong>Google Cloud console</strong> : You can choose tutorial guides with step-by-step instructions for the Google Cloud console.<br />
<a href="https://docs.cloud.google.com/vertex-ai/docs/tutorials/tabular-automl/overview">Show on cloud.google.com</a> | <a href="https://console.cloud.google.com/?walkthrough_id=vertex_tabular_part1">Show in an interactive format in Google Cloud console</a></p>
<p><strong>Notebook</strong> : You can choose to run this tutorial as a notebook.<br />
<a href="https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl-tabular-classification.ipynb">Run in Colab</a> | <a href="https://console.cloud.google.com/vertex-ai/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml-tabular-classification.ipynb">Open in Colab Enterprise</a> | <a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl-tabular-classification.ipynb">View on GitHub</a> | <a href="https://console.cloud.google.com/vertex-ai/notebooks/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/automl-tabular-classification.ipynb">Open in Gemini Enterprise Agent Platform Workbench</a></p></td>
</tr>
</tbody>
</table>

## Train a regression model for tabular data

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/images/automl-tables.svg" alt="Tabular regression training introduction" /></td>
<td><p>Create a Gemini Enterprise Agent Platform dataset from tabular data, and then train a regression model with AutoML. Deploy the model to an endpoint and make online predictions or make predictions in batch format.</p>
<p><strong>Notebook</strong> : You can choose to run this tutorial and make <strong>online predictions</strong> using a notebook.<br />
<a href="https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_online_bq.ipynb">Run in Colab</a> | <a href="https://console.cloud.google.com/vertex-ai/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_regression_online_bq.ipynb">Open in Colab Enterprise</a> | <a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_online_bq.ipynb">View on GitHub</a> | <a href="https://console.cloud.google.com/vertex-ai/notebooks/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/sdk_automl_tabular_regression_online_bq.ipynb">Open in Gemini Enterprise Agent Platform Workbench</a></p>
<p><strong>Notebook</strong> : You can choose to run this tutorial and make <strong>batch predictions</strong> using a notebook.<br />
<a href="https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_batch_bq.ipynb">Run in Colab</a> | <a href="https://console.cloud.google.com/vertex-ai/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_regression_batch_bq.ipynb">Open in Colab Enterprise</a> | <a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_batch_bq.ipynb">View on GitHub</a> | <a href="https://console.cloud.google.com/vertex-ai/notebooks/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/sdk_automl_tabular_regression_batch_bq.ipynb">Open in Gemini Enterprise Agent Platform Workbench</a></p></td>
</tr>
</tbody>
</table>

## Train a time-series forecasting model for tabular data

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/images/automl-tables.svg" alt="Tabular forecasting training introduction" /></td>
<td><p>Create a Gemini Enterprise Agent Platform dataset from tabular data, and then train a forecasting model with AutoML. Make predictions in batch format.</p>
<p><strong>Notebook</strong> : You can choose to run this tutorial as a notebook.<br />
<a href="https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_forecasting_batch.ipynb">Run in Colab</a> | <a href="https://console.cloud.google.com/vertex-ai/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_forecasting_batch.ipynb">Open in Colab Enterprise</a> | <a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_forecasting_batch.ipynb">View on GitHub</a> | <a href="https://console.cloud.google.com/vertex-ai/notebooks/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/sdk_automl_tabular_forecasting_batch.ipynb">Open in Gemini Enterprise Agent Platform Workbench</a></p></td>
</tr>
</tbody>
</table>

## Train a classification model for image data

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/images/automl-vision.svg" alt="Image classification training introduction" /></td>
<td><p>Create a Gemini Enterprise Agent Platform dataset for image data, and then train a classification model with AutoML. Deploy the model to an endpoint and make online predictions.</p>
<p><strong>Google Cloud console</strong> : You can choose tutorial guides with step-by-step instructions for the Google Cloud console.<br />
<a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-automl/overview">Show on cloud.google.com</a></p></td>
</tr>
</tbody>
</table>

## How to open a notebook in Gemini Enterprise Agent Platform Workbench

To open a notebook tutorial in a Vertex AI Workbench instance:

1.  Click the **Vertex AI Workbench** link in the [notebook list](https://docs.cloud.google.com/vertex-ai/docs/tutorials/jupyter-notebooks) . The link opens the Vertex AI Workbench console.
2.  In the **Deploy to notebook** screen, type a name for your new Vertex AI Workbench instance and click **Create** .
3.  In the **Ready to open notebook** dialog that appears after the instance starts, click **Open** .
4.  On the **Confirm deployment to notebook server** page, select **Confirm** .
5.  Before running the notebook, select **Kernel \> Restart Kernel and Clear all Outputs** .

## What's next

  - View the full list of [Gemini Enterprise Agent Platform notebook tutorials](https://docs.cloud.google.com/vertex-ai/docs/tutorials/jupyter-notebooks) .
  - Learn more about [model training](https://docs.cloud.google.com/vertex-ai/docs/training-overview) .
