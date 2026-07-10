---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/jupyter-notebooks
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/jupyter-notebooks
title: Agent Platform notebook tutorials
description: Find a notebook tutorial to help you get started using Agent Platform.
data_source: docs.cloud.google.com
---

This document contains a list of available Gemini Enterprise Agent Platform notebook tutorials. These end-to-end tutorials help you get started using Agent Platform and can give you ideas for how to implement a specific project.

There are many environments in which you can host notebooks. You can run them in the cloud using a service like [Colaboratory (Colab)](https://research.google.com/colaboratory/) , [Colab Enterprise](https://docs.cloud.google.com/colab/docs/introduction) , or [Gemini Enterprise Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction) . Or you can download the notebooks from GitHub and run them on your local machine or on a JupyterLab implementation in your local network.

### Colab

To open a notebook tutorial in Colab, click the **Colab** link in the [notebook list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/jupyter-notebooks#notebook-list) . Colab creates a VM instance with all needed dependencies, launches the Colab environment, and loads the notebook.

### Colab Enterprise

To open a notebook tutorial in Colab Enterprise, do the following:

1.  [Set up a Google Cloud project and enable the required APIs.](https://docs.cloud.google.com/colab/docs/create-console-quickstart#before-you-begin)
2.  Click the **Colab Enterprise** link in the [notebook list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/jupyter-notebooks#notebook-list) . Colab Enterprise loads the notebook.

### Agent Platform Workbench

To open a notebook tutorial in Agent Platform Workbench, do the following:

1.  [Create a Agent Platform Workbench instance.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-console-quickstart)
2.  Click the **Agent Platform Workbench** link in the [notebook list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/jupyter-notebooks#notebook-list) .
3.  Select an active Agent Platform Workbench instance. If none of your instances are running, select an instance and then click **Start** . After the instance starts, select it again.
4.  Click **Deploy** .
5.  On the **Confirm deployment to notebook server** page, select **Confirm** . Agent Platform Workbench loads the notebook.
6.  In the **Select kernel** dialog, select **Python 3** , and then click **Select** .

### GitHub

To download a notebook tutorial from GitHub, do the following:

1.  Click the **GitHub** link in the [notebook list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/jupyter-notebooks#notebook-list) .
2.  In GitHub, click the download **Download raw file** button.
3.  Complete the dialog to download the notebook.

## List of notebooks

Select a service Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform Gemini Enterprise Agent Platform

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Services</th>
<th>Description</th>
<th>Open in</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Classification for tabular data<br />
</td>
<td><strong>AutoML tabular training and prediction</strong> .<br />
Learn how to train and make predictions on an AutoML model based on a tabular dataset. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/overview">Classification for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform model training job.</li>
<li>Train an AutoML Tabular model.</li>
<li>Deploy the model resource to a serving endpoint resource.</li>
<li>Make a prediction by sending data.</li>
<li>Undeploy the model resource.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl-tabular-classification.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml-tabular-classification.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl-tabular-classification.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/automl-tabular-classification.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Get predictions from an image classification model<br />
</td>
<td><strong>AutoML training image classification model for batch prediction</strong> .<br />
In this tutorial, you create an AutoML image classification model from a Python script, and then do a batch prediction using the Vertex SDK. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/get-predictions">Get predictions from an image classification model</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Vertex dataset resource.</li>
<li>Train the model.</li>
<li>View the model evaluation.</li>
<li>Make a batch prediction.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_classification_batch_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml_image_classification_batch_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_classification_batch_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/automl_image_classification_batch_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Get predictions from an image classification model<br />
</td>
<td><strong>AutoML training image classification model for online prediction</strong> .<br />
In this tutorial, you create an AutoML image classification model and deploy for online prediction from a Python script using the Vertex SDK. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/get-predictions">Get predictions from an image classification model</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Vertex <code dir="ltr" translate="no">Dataset</code> resource.</li>
<li>Train the model.</li>
<li>View the model evaluation.</li>
<li>Deploy the <code dir="ltr" translate="no">Model</code> resource to a serving <code dir="ltr" translate="no">Endpoint</code> resource.</li>
<li>Make a prediction.</li>
<li>Undeploy the <code dir="ltr" translate="no">Model</code> .</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_classification_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml_image_classification_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_classification_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl//automl_image_classification_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>AutoML<br />
</td>
<td><strong>AutoML training image object detection model for export to edge</strong> .<br />
In this tutorial, you create an AutoML image object detection model from a Python script using the Vertex SDK, and then export the model as an Edge model in TFLite format.
<p>Tutorial steps</p>
<ul>
<li>Create a Vertex dataset resource.</li>
<li>Train the model.</li>
<li>Export the edge model from the model resource to Cloud Storage.</li>
<li>Download the model locally.</li>
<li>Make a local prediction.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_object_detection_export_edge.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml_image_object_detection_export_edge.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_object_detection_export_edge.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl//automl_image_object_detection_export_edge.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Object detection for image data<br />
</td>
<td><strong>AutoML training image object detection model for online prediction</strong> .<br />
In this tutorial, you create an AutoML image object detection model and deploy for online prediction from a Python script using the Agent Platform SDK. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview#object_detection_for_images">Object detection for image data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform dataset resource.</li>
<li>Train the model.</li>
<li>View the model evaluation.</li>
<li>Deploy the model resource to a serving endpoint resource.</li>
<li>Make a prediction.</li>
<li>Undeploy the model.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_object_detection_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml_image_object_detection_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_image_object_detection_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/automl_image_object_detection_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Tabular Workflow for E2E AutoML<br />
</td>
<td><strong>AutoML Tabular Workflow pipelines</strong> .<br />
Learn how to create two regression models using Gemini Enterprise Agent Platform Pipelines downloaded from Google Cloud Pipeline Components . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/e2e-automl">Tabular Workflow for E2E AutoML</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a training pipeline that reduces the search space from the default to save time.</li>
<li>Create a training pipeline that reuses the architecture search results from the previous pipeline to save time.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_tabular_on_vertex_pipelines.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fautoml_tabular_on_vertex_pipelines.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_tabular_on_vertex_pipelines.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/automl_tabular_on_vertex_pipelines.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>AutoML training<br />
</td>
<td><strong>Get started with AutoML training</strong> .<br />
Learn how to use <code dir="ltr" translate="no">AutoML</code> for training with <code dir="ltr" translate="no">Gemini Enterprise Agent Platform</code> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview">AutoML training</a> .
<p>Tutorial steps</p>
<ul>
<li>Train an image model</li>
<li>Export the image model as an edge model</li>
<li>Train a tabular model</li>
<li>Export the tabular model as a cloud model</li>
<li>Train a text model</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/get_started_automl_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fget_started_automl_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/get_started_automl_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/get_started_automl_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Hierarchical forecasting for tabular data<br />
</td>
<td><strong>Gemini Enterprise Agent Platform AutoML training hierarchical forecasting for batch prediction</strong> .<br />
In this tutorial, you create an AutoML hierarchical forecasting model and deploy it for batch prediction using the Agent Platform SDK for Python. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/hierarchical">Hierarchical forecasting for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform TimeSeriesDataset resource.</li>
<li>Train the model.</li>
<li>View the model evaluation.</li>
<li>Make a batch prediction.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_forecasting_hierarchical_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_forecasting_hierarchical_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_forecasting_hierarchical_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/sdk_automl_forecasting_hierarchical_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Object detection for image data<br />
</td>
<td><strong>AutoML training image object detection model for batch prediction</strong> .<br />
In this tutorial, you create an AutoML image object detection model from a Python script, and then do a batch prediction using the Agent Platform SDK for Python. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview#object_detection_for_images">Object detection for image data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Vertex dataset resource.</li>
<li>Train the model.</li>
<li>View the model evaluation.</li>
<li>Make a batch prediction.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_image_object_detection_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_image_object_detection_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_image_object_detection_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/sdk_automl_image_object_detection_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Forecasting with AutoML<br />
</td>
<td><strong>AutoML tabular forecasting model for batch prediction</strong> .<br />
Learn how to create an AutoML tabular forecasting model from a Python script, and then generate batch prediction using the Agent Platform SDK. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/overview">Forecasting with AutoML</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform dataset resource.</li>
<li>Train an AutoML tabular forecasting model resource.</li>
<li>Obtain the evaluation metrics for the model resource.</li>
<li>Make a batch prediction.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_forecasting_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_forecasting_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_forecasting_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/sdk_automl_tabular_forecasting_batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Regression for tabular data<br />
</td>
<td><strong>AutoML training tabular regression model for batch prediction using BigQuery</strong> .<br />
Learn how to create an AutoML tabular regression model and deploy it for batch prediction using the Agent Platform SDK for Python. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/overview">Regression for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform dataset resource.</li>
<li>Train an AutoML tabular regression model resource.</li>
<li>Obtain the evaluation metrics for the model resource.</li>
<li>Make a batch prediction.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_batch_bq.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_regression_batch_bq.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_batch_bq.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/sdk_automl_tabular_regression_batch_bq.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Regression for tabular data<br />
</td>
<td><strong>AutoML training tabular regression model for online prediction using BigQuery</strong> .<br />
Learn how to create an AutoML tabular regression model and deploy for online prediction from a Python script using the Agent Platform SDK. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/overview">Regression for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Vertex dataset resource.</li>
<li>Train the model.</li>
<li>View the model evaluation.</li>
<li>Deploy the model resource to a serving Endpoint resource.</li>
<li>Make a prediction.</li>
<li>Undeploy the model.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_online_bq.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_regression_online_bq.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_online_bq.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/automl/sdk_automl_tabular_regression_online_bq.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>BigQuery ML<br />
</td>
<td><strong>Get started with BigQuery ML Training</strong> .<br />
Learn how to use BigQuery ML for training with Gemini Enterprise Agent Platform. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/beginner/bqml">BigQuery ML</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a local BigQuery table in your project</li>
<li>Train a BigQuery ML model</li>
<li>Evaluate the BigQuery ML model</li>
<li>Export the BigQuery ML model as a cloud model</li>
<li>Upload the exported model as a Gemini Enterprise Agent Platform model resource</li>
<li>Hyperparameter tune a BigQuery ML model with Agent Platform Vizier</li>
<li>Automatically register a BigQuery ML model to Model Registry</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/bigquery_ml/get_started_with_bqml_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fbigquery_ml%2Fget_started_with_bqml_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/bigquery_ml/get_started_with_bqml_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/bigquery_ml/get_started_with_bqml_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Custom training<br />
Vertex AI Inference<br />
</td>
<td><strong>Deploying Iris-detection model using FastAPI and Gemini Enterprise Agent Platform custom container serving</strong> .<br />
Learn how to create, deploy and serve a custom classification model on Gemini Enterprise Agent Platform. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-predictions">Vertex AI Inference</a> .
<p>Tutorial steps</p>
<ul>
<li>Train a model that uses flower's measurements as input to predict the class of iris.</li>
<li>Save the model and its serialized preprocessor.</li>
<li>Build a FastAPI server to handle predictions and health checks.</li>
<li>Build a custom container with model artifacts.</li>
<li>Upload and deploy custom container to Gemini Enterprise Agent Platform Endpoints.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/SDK_Custom_Container_Prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2FSDK_Custom_Container_Prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/SDK_Custom_Container_Prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/custom/SDK_Custom_Container_Prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex AI Training<br />
</td>
<td><strong>Training a TensorFlow model on BigQuery data</strong> .<br />
Learn how to create a custom-trained model from a Python script in a Docker container using the Agent Platform SDK for Python, and then get a prediction from the deployed model by sending data. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Vertex AI Training</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform custom <code dir="ltr" translate="no">TrainingPipeline</code> for training a model.</li>
<li>Train a TensorFlow model.</li>
<li>Deploy the <code dir="ltr" translate="no">Model</code> resource to a serving <code dir="ltr" translate="no">Endpoint</code> resource.</li>
<li>Make a prediction.</li>
<li>Undeploy the <code dir="ltr" translate="no">Model</code> resource.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/custom-tabular-bq-managed-dataset.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fcustom-tabular-bq-managed-dataset.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/custom-tabular-bq-managed-dataset.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/custom/custom-tabular-bq-managed-dataset.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Custom training<br />
</td>
<td><strong>Custom training with custom container image and automatic model upload to Model Registry</strong> .<br />
In this tutorial, you train a machine learning model custom container image approach for custom training in Gemini Enterprise Agent Platform. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform custom job for training a model.</li>
<li>Train and register a TensorFlow model using a custom container.</li>
<li>List the registered model in the Model Registry.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/custom_training_container_and_model_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fcustom_training_container_and_model_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/custom_training_container_and_model_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/custom/custom_training_container_and_model_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Cloud Profiler<br />
</td>
<td><strong>Profile model training performance using Cloud Profiler</strong> .<br />
Learn how to enable Cloud Profiler for custom training jobs. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler">Cloud Profiler</a> .
<p>Tutorial steps</p>
<ul>
<li>Setup a service account and a Cloud Storage bucket</li>
<li>Create a Vertex AI TensorBoard instance</li>
<li>Create and run a custom training job</li>
<li>View the Cloud Profiler dashboard</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/custom_training_tensorboard_profiler.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fcustom_training_tensorboard_profiler.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/custom_training_tensorboard_profiler.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/custom/custom_training_tensorboard_profiler.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Custom training<br />
</td>
<td><strong>Get started with Vertex AI Training for XGBoost</strong> .<br />
Learn how to use Vertex AI Training for training a XGBoost custom model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Training using a Python package.</li>
<li>Report accuracy when hyperparameter tuning.</li>
<li>Save the model artifacts to Cloud Storage using Cloud StorageFuse.</li>
<li>Create a Gemini Enterprise Agent Platform model resource.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/get_started_vertex_training_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fget_started_vertex_training_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/get_started_vertex_training_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/custom/get_started_vertex_training_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Shared resources across deployments<br />
</td>
<td><strong>Get started with Endpoint and shared VM</strong> .<br />
Learn how to use deployment resource pools for deploying models. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/model-co-hosting">Shared resources across deployments</a> .
<p>Tutorial steps</p>
<ul>
<li>Upload a pretrained image classification model as a <code dir="ltr" translate="no">Model</code> resource (model A).</li>
<li>Upload a pretrained text sentence encoder model as a <code dir="ltr" translate="no">Model</code> resource (model B).</li>
<li>Create a shared VM deployment resource pool.</li>
<li>List shared VM deployment resource pools.</li>
<li>Create two <code dir="ltr" translate="no">Endpoint</code> resources.</li>
<li>Deploy first model (model A) to first <code dir="ltr" translate="no">Endpoint</code> resource using deployment resource pool.</li>
<li>Deploy second model (model B) to second <code dir="ltr" translate="no">Endpoint</code> resource using deployment resource pool.</li>
<li>Make a prediction request with first deployed model (model A).</li>
<li>Make a prediction request with second deployed model (model B).</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/get_started_with_vertex_endpoint_and_shared_vm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2F%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fget_started_with_vertex_endpoint_and_shared_vm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/get_started_with_vertex_endpoint_and_shared_vm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/custom/get_started_with_vertex_endpoint_and_shared_vm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Custom training<br />
Gemini Enterprise Agent Platform Batch Prediction<br />
</td>
<td><strong>Custom training and batch prediction</strong> .<br />
Learn to use Vertex AI Training to create a custom trained model and use Gemini Enterprise Agent Platform Batch Prediction to do a batch prediction on the trained model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions">Gemini Enterprise Agent Platform Batch Prediction</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform custom job for training a TensorFlow model.</li>
<li>Upload the trained model artifacts as a model resource.</li>
<li>Make a batch prediction.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/custom/sdk-custom-image-classification-batch.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Custom training<br />
Vertex AI Inference<br />
</td>
<td><strong>Custom training and online prediction</strong> .<br />
Learn to use <code dir="ltr" translate="no">Vertex AI Training</code> to create a custom-trained model from a Python script in a Docker container, and learn to use <code dir="ltr" translate="no">Vertex AI Inference</code> to do a prediction on the deployed model by sending data. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-predictions">Vertex AI Inference</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a <code dir="ltr" translate="no">Gemini Enterprise Agent Platform</code> custom job for training a TensorFlow model.</li>
<li>Upload the trained model artifacts to a <code dir="ltr" translate="no">Model</code> resource.</li>
<li>Create a serving <code dir="ltr" translate="no">Endpoint</code> resource.</li>
<li>Deploy the <code dir="ltr" translate="no">Model</code> resource to a serving <code dir="ltr" translate="no">Endpoint</code> resource.</li>
<li>Make a prediction.</li>
<li>Undeploy the <code dir="ltr" translate="no">Model</code> resource.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>BigQuery datasets<br />
Gemini Enterprise Agent Platform for BigQuery users<br />
</td>
<td><strong>Get started with BigQuery datasets</strong> .<br />
Learn how to use BigQuery as a dataset for training with Gemini Enterprise Agent Platform. Learn more about <a href="https://cloud.google.com/bigquery/docs/datasets-intro">BigQuery datasets</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/beginner/bqml">Gemini Enterprise Agent Platform for BigQuery users</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform dataset resource from BigQuery table compatible for AutoML training.</li>
<li>Extract a copy of the dataset from BigQuery to a CSV file in Cloud Storage compatible for AutoML or custom training.</li>
<li>Select rows from a BigQuery dataset into a pandas dataframe compatible for custom training.</li>
<li>Select rows from a BigQuery dataset into a <code dir="ltr" translate="no">tf.data.Dataset</code> compatible for custom training TensorFlow models.</li>
<li>Select rows from extracted CSV files into a <code dir="ltr" translate="no">tf.data.Dataset</code> compatible for custom training TensorFlow models.</li>
<li>Create a BigQuery dataset from CSV files.</li>
<li>Extract data from BigQuery table into a DMatrix compatible for custom training XGBoost models.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/datasets/get_started_bq_datasets.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fdatasets%2Fget_started_bq_datasets.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/datasets/get_started_bq_datasets.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/datasets/get_started_bq_datasets.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex AI Experiments<br />
Vertex ML Metadata<br />
</td>
<td><strong>Build Gemini Enterprise Agent Platform Experiment lineage for custom training</strong> .<br />
Learn how to integrate preprocessing code in a Gemini Enterprise Agent Platform experiments. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/intro-vertex-ai-experiments">Vertex AI Experiments</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction">Vertex ML Metadata</a> .
<p>Tutorial steps</p>
<ul>
<li>Execute module for preprocessing data</li>
<li>Create a dataset artifact</li>
<li>Log parameters</li>
<li>Execute module for training the model</li>
<li>Log parameters</li>
<li>Create model artifact</li>
<li>Assign tracking lineage to dataset, model and parameters</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/build_model_experimentation_lineage_with_prebuild_code.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fbuild_model_experimentation_lineage_with_prebuild_code.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/build_model_experimentation_lineage_with_prebuild_code.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/experiments/build_model_experimentation_lineage_with_prebuild_code.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Vertex AI Experiments<br />
</td>
<td><strong>Track parameters and metrics for locally trained models</strong> .<br />
Learn how to use Vertex AI Experiments to compare and evaluate model experiments. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/intro-vertex-ai-experiments">Vertex AI Experiments</a> .
<p>Tutorial steps</p>
<ul>
<li>log the model parameters</li>
<li>log the loss and metrics on every epoch to Vertex AI TensorBoard</li>
<li>log the evaluation metrics</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/comparing_local_trained_models.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fcomparing_local_trained_models.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/comparing_local_trained_models.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/experiments/comparing_local_trained_models.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex AI Experiments<br />
Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Compare pipeline runs with Vertex AI Experiments</strong> .<br />
Learn how to use Vertex AI Experiments to log a pipeline job and then compare different pipeline jobs. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/intro-vertex-ai-experiments">Vertex AI Experiments</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> .
<p>Tutorial steps</p>
<ul>
<li>Formalize a training component</li>
<li>Build a training pipeline</li>
<li>Run several pipeline jobs and log their results</li>
<li>Compare different pipeline jobs</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/comparing_pipeline_runs.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fcomparing_pipeline_runs.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/comparing_pipeline_runs.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/experiments/comparing_pipeline_runs.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Vertex AI TensorBoard<br />
</td>
<td><strong>Delete Outdated Experiments in Vertex AI TensorBoard</strong> .<br />
Learn how to delete outdated Vertex AI TensorBoard Experiments to avoid unnecessary storage costs. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction">Vertex AI TensorBoard</a> .
<p>Tutorial steps</p>
<ul>
<li>How to delete the TB Experiment with a predefined keyvalue label pair <code dir="ltr" translate="no"></code></li>
<li></li>
<li>How to delete the TB Experiments created before the <code dir="ltr" translate="no">create_time</code></li>
<li></li>
<li>How to delete the TB Experiments created before the <code dir="ltr" translate="no">update_time</code></li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/delete_outdated_tensorboard_experiments.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fdelete_outdated_tensorboard_experiments.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/delete_outdated_tensorboard_experiments.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/vertex-ai-samples/main/notebooks/official/experiments/delete_outdated_tensorboard_experiments.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex AI Experiments<br />
</td>
<td><strong>Custom training autologging - Local script</strong> .<br />
Learn how to autolog parameters and metrics of an ML experiment running on Vertex AI Training by leveraging the integration with Vertex AI Experiments.
<p>Tutorial steps</p>
<ul>
<li>Formalize model experiment in a script</li>
<li>Run model traning using local script on Vertex AI Training</li>
<li>Check out ML experiment parameters and metrics in Vertex AI Experiments</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_custom_training_autologging_local_script.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_custom_training_autologging_local_script.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_custom_training_autologging_local_script.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/experiments/get_started_with_custom_training_autologging_local_script.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Vertex AI Experiments<br />
Vertex ML Metadata<br />
Custom training<br />
</td>
<td><strong>Get started with Vertex AI Experiments</strong> .<br />
Learn how to use Vertex AI Experiments when training with Gemini Enterprise Agent Platform. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/intro-vertex-ai-experiments">Vertex AI Experiments</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction">Vertex ML Metadata</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Local (notebook) training</li>
<li>Create an experiment.</li>
<li>Create a first run in the experiment.</li>
<li>Log parameters and metrics.</li>
<li>Create artifact lineage.</li>
<li>Visualize the experiment results.</li>
<li>Execute a second run.</li>
<li>Compare the two runs in the experiment.</li>
<li>Cloud (Gemini Enterprise Agent Platform) training</li>
<li>Within the training script</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_vertex_experiments.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/experiments/get_started_with_vertex_experiments.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex AI Experiments<br />
</td>
<td><strong>Autologging</strong> .<br />
Learn how to use Gemini Enterprise Agent Platform Autologging.
<p>Tutorial steps</p>
<ul>
<li>Enable autologging in the Agent Platform SDK.</li>
<li>Train scikitlearn model and see the resulting experiment run with metrics and parameters autologged to Vertex AI Experiments without setting an experiment run.</li>
<li>Train Tensorflow model, check autologged metrics and parameters to Vertex AI Experiments by manually setting an experiment run with <code dir="ltr" translate="no">aiplatform.start_run()</code> and <code dir="ltr" translate="no">aiplatform.end_run()</code> .</li>
<li>Disable autologging in the Agent Platform SDK, train a PyTorch model and check that none of the parameters or metrics are logged.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments_autologging.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_vertex_experiments_autologging.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments_autologging.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/experiments/get_started_with_vertex_experiments_autologging.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Agent Platform Feature Store<br />
</td>
<td><strong>Online feature serving and fetching of BigQuery data with Agent Platform Feature Store</strong> .<br />
Learn how to create and use an online feature store instance to host and serve data in BigQuery with Agent Platform Feature Store in an end to end workflow of feature values serving and fetching user journey. Learn more about <a href="https://cloud.google.com/vertex-ai/docs/featurestore/overview">Agent Platform Feature Store</a> .
<p>Tutorial steps</p>
<ul>
<li>Provision an online feature store instance to host and serve data.</li>
<li>Register a BigQuery view with the online feature store instance and set up the sync job.</li>
<li>Use the online server to fetch feature values for online prediction.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/online_feature_serving_and_fetching_bigquery_data_with_feature_store_bigtable.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ffeature_store%2Fonline_feature_serving_and_fetching_bigquery_data_with_feature_store_bigtable.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/online_feature_serving_and_fetching_bigquery_data_with_feature_store_bigtable.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/feature_store/online_feature_serving_and_fetching_bigquery_data_with_feature_store_bigtable.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Agent Platform Feature Store<br />
</td>
<td><strong>Online feature serving and fetching of BigQuery data with Agent Platform Feature Store Optimized Serving</strong> .<br />
Learn how to create and use an online feature store instance to host and serve data in BigQuery with Agent Platform Feature Store in an end-to-end workflow of serving and fetching feature values. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/overview">Agent Platform Feature Store</a> .
<p>Tutorial steps</p>
<ul>
<li>Provision an online feature store instance to host and serve data using Optimized online serving with Public or Private endpoint.</li>
<li>Register a BigQuery view with the online feature store instance and set up the sync job.</li>
<li>Use the online server to fetch feature values for online prediction.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/online_feature_serving_and_fetching_bigquery_data_with_feature_store_optimized.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ffeature_store%2Fonline_feature_serving_and_fetching_bigquery_data_with_feature_store_optimized.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/online_feature_serving_and_fetching_bigquery_data_with_feature_store_optimized.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/feature_store/online_feature_serving_and_fetching_bigquery_data_with_feature_store_optimized.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Agent Platform Feature Store<br />
</td>
<td><strong>Online feature serving and vector retrieval of BigQuery data with Agent Platform Feature Store</strong> .<br />
Learn how to create and use an online feature store instance to host and serve data in BigQuery with Agent Platform Feature Store in an end to end workflow of features serving and vector retrieval user journey. Learn more about <a href="https://cloud.google.com/vertex-ai/docs/featurestore/overview">Agent Platform Feature Store</a> .
<p>Tutorial steps</p>
<ul>
<li>Provision an online feature store instance to host and serve data.</li>
<li>Create an online feature store instance to serve a BigQuery table.</li>
<li>Use the online server to search nearest neighbors.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/online_feature_serving_and_vector_retrieval_bigquery_data_with_feature_store.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ffeature_store%2Fonline_feature_serving_and_vector_retrieval_bigquery_data_with_feature_store.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/online_feature_serving_and_vector_retrieval_bigquery_data_with_feature_store.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/feature_store/online_feature_serving_and_vector_retrieval_bigquery_data_with_feature_store.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Agent Platform Feature Store<br />
</td>
<td><strong>Agent Platform Feature Store Based LLM Grounding tutorial</strong> .<br />
Learn how to create and use an online feature store instance to host and serve data in BigQuery with Agent Platform Feature Store in an end to end workflow of features serving and vector retrieval user journey. Learn more about <a href="https://cloud.google.com/vertex-ai/docs/featurestore/overview">Agent Platform Feature Store</a> .
<p>Tutorial steps</p>
<ul>
<li>Provision an online feature store instance to host and serve data.</li>
<li>Create an online feature store instance to serve a BigQuery table.</li>
<li>Use the online server to search nearest neighbors.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/vertex_ai_feature_store_based_llm_grounding_tutorial.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ffeature_store%2Fvertex_ai_feature_store_based_llm_grounding_tutorial.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/vertex_ai_feature_store_based_llm_grounding_tutorial.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/feature_store/vertex_ai_feature_store_based_llm_grounding_tutorial.ipynb.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Agent Platform Feature Store<br />
</td>
<td><strong>Agent Platform Feature Store Feature View Service Agents Tutorial</strong> .<br />
Learn how to use a dedicated service agent for a feature view in Agent Platform Feature Store. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/overview">Agent Platform Feature Store</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a feature view configured to use a dedicated service account.</li>
<li>A service account is created for each feature view. Such service account is used to sync data from BigQuery.</li>
<li>Get/List feature view API returns the autocreated service account. Users need to call <code dir="ltr" translate="no">bq addiampolicybinding</code> command to grant <code dir="ltr" translate="no">roles/bigquery.dataViewer</code> to the service account.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/vertex_ai_feature_store_feature_view_service_agents.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ffeature_store%2Fvertex_ai_feature_store_feature_view_service_agents.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/vertex_ai_feature_store_feature_view_service_agents.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/feature_store/vertex_ai_feature_store_feature_view_service_agents.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Agent Platform Feature Store<br />
</td>
<td><strong>Streaming import SDK in Agent Platform Feature Store (Legacy)</strong> .<br />
Learn how to import features from a <code dir="ltr" translate="no">Pandas DataFrame</code> into Agent Platform Feature Store using <code dir="ltr" translate="no">write_feature_values</code> method from the Agent Platform SDK. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore">Agent Platform Feature Store</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a featurestore.</li>
<li>Create a new entity type for your featurestore.</li>
<li>Import feature values from <code dir="ltr" translate="no">Pandas DataFrame</code> into the entity type in the featurestore.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store_legacy/feature_store_streaming_ingestion_sdk.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ffeature_store_legacy%2Ffeature_store_streaming_ingestion_sdk.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store_legacy/feature_store_streaming_ingestion_sdk.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/feature_store_legacy/feature_store_streaming_ingestion_sdk.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Agent Platform Feature Store<br />
</td>
<td><strong>Using Agent Platform Feature Store (Legacy) with Pandas Dataframe</strong> .<br />
Learn how to use <code dir="ltr" translate="no">Agent Platform Feature Store</code> with pandas Dataframe. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore">Agent Platform Feature Store</a> .
<p>Tutorial steps</p>
<ul>
<li>Create <code dir="ltr" translate="no">Featurestore</code> , <code dir="ltr" translate="no">EntityType</code> , and <code dir="ltr" translate="no">Feature</code> resources.</li>
<li>Import feature values from Pandas DataFrame into the entity type.</li>
<li>Read entity feature values from the online feature store into Pandas DataFrame.</li>
<li>Batch serve feature values from your featurestore into Pandas DataFrame.</li>
<li></li>
<li></li>
<li>Online serving with updated feature values.</li>
<li>Pointintime correctness to fetch feature values for training.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store_legacy/sdk-feature-store-pandas.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ffeature_store_legacy%2Fsdk-feature-store-pandas.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store_legacy/sdk-feature-store-pandas.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/feature_store_legacy/sdk-feature-store-pandas.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Agent Platform Feature Store<br />
</td>
<td><strong>Online and Batch predictions using Agent Platform Feature Store (Legacy)</strong> .<br />
Learn how to use <code dir="ltr" translate="no">Agent Platform Feature Store</code> to import feature data, and to access the feature data for both online serving and offline tasks, such as training. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore">Agent Platform Feature Store</a> .
<p>Tutorial steps</p>
<ul>
<li>Create <code dir="ltr" translate="no">Featurestore</code> , <code dir="ltr" translate="no">EntityType</code> , and <code dir="ltr" translate="no">Feature</code> resources.</li>
<li>Import feature data into the <code dir="ltr" translate="no">Featurestore</code> resource.</li>
<li>Serve online prediction requests using the imported features.</li>
<li>Access imported features in offline jobs, such as training jobs.</li>
<li>Use streaming import to import small amount of data.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store_legacy/sdk-feature-store.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ffeature_store_legacy%2Fsdk-feature-store.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store_legacy/sdk-feature-store.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/feature_store_legacy/sdk-feature-store.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Overview of Generative AI support on Gemini Enterprise Agent Platform<br />
</td>
<td><strong>Gemini Enterprise Agent Platform LLM Batch Inference with RLHF-tuned Models</strong> .<br />
In this tutorial, you use Gemini Enterprise Agent Platform to get predictions from an RLHF-tuned large-language model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/models/">Overview of Generative AI support on Gemini Enterprise Agent Platform</a> .
<p>Tutorial steps</p>
<ul>
<li>Create Gemini Enterprise Agent Platform Pipeline job using a predefined template for bulk inference.</li>
<li>Execute the pipeline using Gemini Enterprise Agent Platform Pipelines.</li>
<li>Produce prediction results against a model for a given dataset.</li>
</ul></td>
<td><a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Fbatch_eval_llm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/batch_eval_llm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/generative_ai/batch_eval_llm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>generative_ai<br />
</td>
<td><strong>Distill a large language model</strong> .<br />
Learn how to distill and deploy a large language model using Gemini Enterprise Agent Platform LLM.
<p>Tutorial steps</p>
<ul>
<li>Get the Gemini Enterprise Agent Platform LLM model.</li>
<li>Distill the model(this automatically creates a Gemini Enterprise Agent Platform endpoint and deploys the model to the endpoint).</li>
<li>Make a prediction using Gemini Enterprise Agent Platform LLM.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/distillation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Fdistillation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/distillation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/generative_ai/distillation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>text embedding<br />
</td>
<td><strong>Semantic Search using Embeddings</strong> .<br />
In this tutorial, we demonstrate how to create an embedding generated from text and perform a semantic search. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-text-embeddings">text embedding</a> .
<p>Tutorial steps</p>
<ul>
<li>Installation and imports</li>
<li>Create embedding dataset</li>
<li>Create an index</li>
<li>Query the index</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/text_embedding_api_semantic_search_with_scann.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Ftext_embedding_api_semantic_search_with_scann.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/text_embedding_api_semantic_search_with_scann.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/generative_ai/text_embedding_api_semantic_search_with_scann.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>generative_ai<br />
</td>
<td><strong>Getting Text Embeddings on Gemini Enterprise Agent Platform</strong> .<br />
Learn how to get a text embedding given a text-embedding model and a text.
<p>Tutorial steps</p>
<ul>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/text_embedding_new_api.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Ftext_embedding_new_api.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/text_embedding_new_api.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/generative_ai/text_embedding_new_api.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>generative_ai<br />
</td>
<td><strong>Getting Text Embeddings on Gemini Enterprise Agent Platform</strong> .<br />
Learn how to get a text embedding given a text-embedding model and a text.
<p>Tutorial steps</p>
<ul>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/text_embedding_new_api.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Ftext_embedding_new_api.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/text_embedding_new_api.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/generative_ai/text_embedding_new_api.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Tune text models by using supervised tuning<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Tuning a PEFT model</strong> .<br />
Learn to use Gemini Enterprise Agent Platform LLM to tune and deploy a PEFT large language model. Learn more about <a href="https://cloud.google.com/vertex-ai/generative-ai/docs/models/tune-text-models-supervised">Tune text models by using supervised tuning</a> .
<p>Tutorial steps</p>
<ul>
<li>Get the Gemini Enterprise Agent Platform LLM model.</li>
<li>Tune the model.</li>
<li>This automatically creates a Gemini Enterprise Agent Platform endpoint and deploy the model to it.</li>
<li>Make a prediction using Gemini Enterprise Agent Platform LLM.</li>
<li>Make a prediction using Vertex AI Inference.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/tune_peft.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Ftune_peft.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/tune_peft.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/generative_ai/tune_peft.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>generative_ai<br />
</td>
<td><strong>Getting Tuned Text-Embeddings on Gemini Enterprise Agent Platform</strong> .<br />
Learn how to tune a text-embedding model.
<p>Tutorial steps</p>
<ul>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/tuned_text-embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/tuned_text-embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/generative_ai/tuned_text-embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>PaLM API<br />
</td>
<td><strong>Using the Agent Platform SDK with Large Language Models</strong> .<br />
Learn how to provide text input to Large Language Models available on Gemini Enterprise Agent Platform to test, tune, and deploy generative AI language models. Learn more about <a href="https://ai.google/discover/palm2/">PaLM API</a> .
<p>Tutorial steps</p>
<ul>
<li>Use the predict endpoints of Gemini Enterprise Agent Platform PaLM API to receive generative AI responses to a message.</li>
<li>Use the text embedding endpoint to receive a vector representation of a message.</li>
<li>Perform prompt tuning of an LLM, based on input/output training data.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/vertex_sdk_llm_snippets.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Fvertex_sdk_llm_snippets.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/vertex_sdk_llm_snippets.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/generative_ai/vertex_sdk_llm_snippets.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Migrate to Gemini Enterprise Agent Platform<br />
Classification for image data<br />
</td>
<td><strong>AutoML Image Classification</strong> .<br />
Learn to use <code dir="ltr" translate="no">AutoML</code> to train an image model and use <code dir="ltr" translate="no">Vertex AI Inference</code> and <code dir="ltr" translate="no">Gemini Enterprise Agent Platform batch inference</code> to do online and batch predictions. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/overview">Migrate to Gemini Enterprise Agent Platform</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview#classification_for_images">Classification for image data</a> .
<p>Tutorial steps</p>
<ul>
<li>Train an AutoML image classification model.</li>
<li>Make a batch prediction.</li>
<li>Deploy model to a endpoint</li>
<li>Make a online prediction</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-automl-image-classification-batch-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmigration%2Fsdk-automl-image-classification-batch-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-automl-image-classification-batch-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/migration/sdk-automl-image-classification-batch-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Migrate to Gemini Enterprise Agent Platform<br />
Object detection for image data<br />
</td>
<td><strong>AutoML image object detection</strong> .<br />
Learn to use <code dir="ltr" translate="no">AutoML</code> to train an image model and use <code dir="ltr" translate="no">Vertex AI Inference</code> and <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Batch Prediction</code> to do online and batch predictions. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/overview">Migrate to Gemini Enterprise Agent Platform</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview#object_detection_for_images">Object detection for image data</a> .
<p>Tutorial steps</p>
<ul>
<li>Train an AutoML object detection model.</li>
<li>Make a batch prediction.</li>
<li>Deploy model to a endpoint</li>
<li>Make a online prediction</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-automl-image-object-detection-batch-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmigration%2Fsdk-automl-image-object-detection-batch-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-automl-image-object-detection-batch-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/migration/sdk-automl-image-object-detection-batch-online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Migrate to Gemini Enterprise Agent Platform<br />
Classification for tabular data<br />
</td>
<td><strong>AutoML tabular binary classification</strong> .<br />
In this tutorial, you create an AutoML tabular binary classification model and deploy for online prediction from a Python script using the Agent Platform SDK. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/overview">Migrate to Gemini Enterprise Agent Platform</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/overview">Classification for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform dataset resource.</li>
<li>Train the model.</li>
<li>View the model evaluation.</li>
<li>Deploy the model resource to a serving endpoint resource.</li>
<li>Make a prediction.</li>
<li>Undeploy the model</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-automl-tabular-binary-classification-online-prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmigration%2Fsdk-automl-tabular-binary-classification-online-prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-automl-tabular-binary-classification-online-prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/migration/sdk-automl-tabular-binary-classification-online-prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Migrate to Gemini Enterprise Agent Platform<br />
Custom training<br />
</td>
<td><strong>Custom image classification with a custom training container</strong> .<br />
Learn how to train a tensorflow image classification model using a custom container and Gemini Enterprise Agent Platform training. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/overview">Migrate to Gemini Enterprise Agent Platform</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Package the training code into a python application.</li>
<li>Containerize the training application using Cloud Build and Artifact Registry.</li>
<li>Create a custom container training job in Gemini Enterprise Agent Platform and run it.</li>
<li>Evaluate the model generated from the training job.</li>
<li>Create a model resource for the trained model in Model Registry.</li>
<li>Run a Gemini Enterprise Agent Platform batch inference job.</li>
<li>Deploy the model resource to a Gemini Enterprise Agent Platform endpoint.</li>
<li>Run a online prediction job on the model resource.</li>
<li>Clean up the resources created.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-custom-image-classification-custom-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmigration%2Fsdk-custom-image-classification-custom-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-custom-image-classification-custom-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/migration/sdk-custom-image-classification-custom-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Migrate to Gemini Enterprise Agent Platform<br />
Custom training overview<br />
</td>
<td><strong>Custom image classification with a pre-built training container</strong> .<br />
Learn how to train a tensorflow image classification model using a prebuilt container and Gemini Enterprise Agent Platform training. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/overview">Migrate to Gemini Enterprise Agent Platform</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training overview</a> .
<p>Tutorial steps</p>
<ul>
<li>Package the training code into a python application.</li>
<li>Containerize the training application using Cloud Build and Artifact Registry.</li>
<li>Create a custom container training job in Gemini Enterprise Agent Platform and run it.</li>
<li>Evaluate the model generated from the training job.</li>
<li>Create a model resource for the trained model in Model Registry.</li>
<li>Run a Gemini Enterprise Agent Platform batch inference job.</li>
<li>Deploy the model resource to a Gemini Enterprise Agent Platform endpoint.</li>
<li>Run a online prediction job on the model resource.</li>
<li>Clean up the resources created.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-custom-image-classification-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmigration%2Fsdk-custom-image-classification-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-custom-image-classification-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/migration/sdk-custom-image-classification-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Migrate to Gemini Enterprise Agent Platform<br />
Custom training overview<br />
</td>
<td><strong>Custom Scikit-Learn model with pre-built training container</strong> .<br />
Learn how to use Vertex AI Training to create a custom trained model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/overview">Migrate to Gemini Enterprise Agent Platform</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training overview</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform custom job for training a scikitlearn model.</li>
<li>Upload the trained model artifacts as a model resource.</li>
<li>Generate batch predictions.</li>
<li>Deploy the model resource to a serving endpoint resource.</li>
<li>Generate online predictions.</li>
<li>Undeploy the model resource.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-custom-scikit-learn-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmigration%2Fsdk-custom-scikit-learn-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-custom-scikit-learn-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/migration/sdk-custom-scikit-learn-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Migrate to Gemini Enterprise Agent Platform<br />
Custom training overview<br />
</td>
<td><strong>Custom XGBoost model with pre-built training container</strong> .<br />
Learn to use Vertex AI Training to create a custom trained model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/overview">Migrate to Gemini Enterprise Agent Platform</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training overview</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform custom job for training a xgboost model.</li>
<li>Upload the trained model artifacts as a model resource.</li>
<li>Generate batch predictions.</li>
<li>Deploy the model resource to a serving endpoint resource.</li>
<li>Generate online predictions.</li>
<li>Undeploy the model resource.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-custom-xgboost-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmigration%2Fsdk-custom-xgboost-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-custom-xgboost-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/migration/sdk-custom-xgboost-prebuilt-container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform hyperparameter tuning<br />
Custom training<br />
</td>
<td><strong>Hyperparameter Tuning</strong> .<br />
Learn to use Gemini Enterprise Agent Platform hyperparameter to create and tune a custom trained model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview">Gemini Enterprise Agent Platform hyperparameter tuning</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform hyperparameter tuning job for training a TensorFlow model.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-hyperparameter-tuning.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmigration%2Fsdk-hyperparameter-tuning.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-hyperparameter-tuning.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/migration/sdk-hyperparameter-tuning.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Google Artifact Registry documentation<br />
</td>
<td><strong>Get started with Google Artifact Registry</strong> .<br />
Learn how to use Google Artifact Registry. Learn more about <a href="https://cloud.google.com/artifact-registry/docs">Google Artifact Registry documentation</a> .
<p>Tutorial steps</p>
<ul>
<li>Creating a private Docker repository.</li>
<li>Tagging a container image, specific to the private Docker repository.</li>
<li>Pushing a container image to the private Docker repository.</li>
<li>Pulling a container image from the private Docker repository.</li>
<li>Deleting a private Docker repository.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/get_started_with_google_artifact_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fml_metadata%2Fget_started_with_google_artifact_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/get_started_with_google_artifact_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/ml_metadata/get_started_with_google_artifact_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex ML Metadata<br />
</td>
<td><strong>Track parameters and metrics for custom training jobs</strong> .<br />
Learn how to use Agent Platform SDK for Python to:
<p>Tutorial steps</p>
<ul>
<li>Track training parameters and prediction metrics for a custom training job.</li>
<li>Extract and perform analysis for all parameters and metrics within an Experiment.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/sdk-metric-parameter-tracking-for-custom-jobs.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fml_metadata%2Fsdk-metric-parameter-tracking-for-custom-jobs.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/sdk-metric-parameter-tracking-for-custom-jobs.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/ml_metadata/sdk-metric-parameter-tracking-for-custom-jobs.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Vertex ML Metadata<br />
</td>
<td><strong>Track parameters and metrics for locally trained models</strong> .<br />
Learn how to use Vertex ML Metadata to track training parameters and evaluation metrics. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction">Vertex ML Metadata</a> .
<p>Tutorial steps</p>
<ul>
<li>Track parameters and metrics for a locally trained model.</li>
<li>Extract and perform analysis for all parameters and metrics within an experiment.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/sdk-metric-parameter-tracking-for-locally-trained-models.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fml_metadata%2Fsdk-metric-parameter-tracking-for-locally-trained-models.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/sdk-metric-parameter-tracking-for-locally-trained-models.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/ml_metadata/sdk-metric-parameter-tracking-for-locally-trained-models.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex ML Metadata<br />
Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Track artifacts and metrics across Gemini Enterprise Agent Platform Pipelines runs using Vertex ML Metadata</strong> .<br />
Learn how to track artifacts and metrics with Vertex ML Metadata in Gemini Enterprise Agent Platform Pipeline runs. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction">Vertex ML Metadata</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> .
<p>Tutorial steps</p>
<ul>
<li>Use the Kubeflow Pipelines SDK to build an ML pipeline that runs on Gemini Enterprise Agent Platform.</li>
<li>The pipeline creates a dataset, trains a scikitlearn model, and deploys the model to an endpoint.</li>
<li>Write custom pipeline components that generate artifacts and metadata.</li>
<li>Compare Gemini Enterprise Agent Platform Pipeline runs, both in the Google Cloud console and programmatically.</li>
<li>Trace the lineage for pipelinegenerated artifacts.</li>
<li>Query your pipeline run metadata.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/vertex-pipelines-ml-metadata.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fml_metadata%2Fvertex-pipelines-ml-metadata.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/vertex-pipelines-ml-metadata.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/ml_metadata/vertex-pipelines-ml-metadata.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Model Evaluation<br />
Classification for tabular data<br />
</td>
<td><strong>Evaluating batch prediction results from an AutoML Tabular classification model</strong> .<br />
Learn how to train a Gemini Enterprise Agent Platform AutoML Tabular classification model and learn how to evaluate it through a Gemini Enterprise Agent Platform pipeline job using <code dir="ltr" translate="no">google_cloud_pipeline_components</code> : Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/introduction">Gemini Enterprise Agent Platform Model Evaluation</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/overview">Classification for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform <code dir="ltr" translate="no">Dataset</code> .</li>
<li>Train an Automl Tabular classification model on the <code dir="ltr" translate="no">Dataset</code> resource.</li>
<li>Import the trained <code dir="ltr" translate="no">AutoML model resource</code> into the pipeline.</li>
<li>Run a <code dir="ltr" translate="no">Batch Prediction</code> job.</li>
<li>Evaluate the AutoML model using the <code dir="ltr" translate="no">Classification Evaluation component</code> .</li>
<li>Import the classification metrics to the AutoML model resource.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_classification_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fautoml_tabular_classification_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_classification_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_evaluation/automl_tabular_classification_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Model Evaluation<br />
Regression for tabular data<br />
</td>
<td><strong>Evaluating batch prediction results from AutoML tabular regression model</strong> .<br />
Learn how to evaluate a Gemini Enterprise Agent Platform model resource through a Gemini Enterprise Agent Platform pipeline job using <code dir="ltr" translate="no">google_cloud_pipeline_components</code> : Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/introduction">Gemini Enterprise Agent Platform Model Evaluation</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/overview">Regression for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform dataset.</li>
<li>Configure an <code dir="ltr" translate="no">AutoMLTabularTrainingJob</code> class.</li>
<li>Run the <code dir="ltr" translate="no">AutoMLTabularTrainingJob</code> which returns a model.</li>
<li>Import a pretrained <code dir="ltr" translate="no">AutoML model resource</code> into the pipeline.</li>
<li>Run a <code dir="ltr" translate="no">batch prediction</code> job in the pipeline.</li>
<li>Evaluate the AutoML model using the <code dir="ltr" translate="no">regression evaluation component</code> .</li>
<li>Import the generated regression metrics into the AutoML model resource.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_regression_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fautoml_tabular_regression_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/automl_tabular_regression_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_evaluation/automl_tabular_regression_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform custom training<br />
Gemini Enterprise Agent Platform model evaluation<br />
</td>
<td><strong>Evaluating BatchPrediction results from a custom tabular classification model</strong> .<br />
In this tutorial, you train a scikit-learn RandomForest model, save the model in Model Registry and learn how to evaluate the model through a Gemini Enterprise Agent Platform pipeline job using Google Cloud Pipeline Components Python SDK. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Gemini Enterprise Agent Platform custom training</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/introduction">Gemini Enterprise Agent Platform model evaluation</a> .
<p>Tutorial steps</p>
<ul>
<li>Fetch the dataset from the public source.</li>
<li>Preprocess the data locally and save test data in BigQuery.</li>
<li>Train a RandomForest classification model locally using scikitlearn Python package.</li>
<li>Create a custom container in Artifact Registry for predictions.</li>
<li>Upload the model in Model Registry.</li>
<li>Create and run a Gemini Enterprise Agent Platform Pipeline that</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_classification_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fcustom_tabular_classification_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_classification_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_evaluation/custom_tabular_classification_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Model Evaluation<br />
Custom training<br />
</td>
<td><strong>Evaluating batch prediction results from custom tabular regression model</strong> .<br />
Learn how to evaluate a Gemini Enterprise Agent Platform model resource through a Gemini Enterprise Agent Platform pipeline job using google cloud pipeline components. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/introduction">Gemini Enterprise Agent Platform Model Evaluation</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform Custom Training Job to train a TensorFlow model.</li>
<li>Run the custom training job.</li>
<li>Retrieve and load the model artifacts.</li>
<li>View the model evaluation.</li>
<li>Upload the model as a Gemini Enterprise Agent Platform model resource.</li>
<li>Import a pretrained Gemini Enterprise Agent Platform model resource into the pipeline.</li>
<li>Run a batch prediction job in the pipeline.</li>
<li>Evaluate the model using the regression evaluation component.</li>
<li>Import the Regression Metrics to the Gemini Enterprise Agent Platform model resource.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_regression_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fcustom_tabular_regression_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/custom_tabular_regression_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_evaluation/custom_tabular_regression_model_evaluation.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform AutoSxS Model Evaluation<br />
</td>
<td><strong>Check autorater alignment against a human-preference dataset</strong> .<br />
Learn how to use <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Pipelines</code> and <code dir="ltr" translate="no">google_cloud_pipeline_components</code> to check autorater alignment using human-preference data: Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/models/side-by-side-eval#autosxs">Gemini Enterprise Agent Platform AutoSxS Model Evaluation</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a evaluation dataset with predictions and human preference data.</li>
<li>Preprocess the data locally and save it in Cloud Storage.</li>
<li>Create and run a Gemini Enterprise Agent Platform AutoSxS Pipeline that generates the judgments and a set of AutoSxS metrics using the generated judgments.</li>
<li>Print the judgments and AutoSxS metrics.</li>
<li>Clean up the resources created in this notebook.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/model_based_llm_evaluation/autosxs_check_alignment_against_human_preference_data.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fmodel_based_llm_evaluation%2Fautosxs_check_alignment_against_human_preference_data.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/model_based_llm_evaluation/autosxs_check_alignment_against_human_preference_data.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_evaluation/model_based_llm_evaluation/autosxs_check_alignment_against_human_preference_data.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform AutoSxS Model Evaluation<br />
</td>
<td><strong>Evaluate a LLM in Model Registry against a third-party model</strong> .<br />
Learn how to use <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Pipelines</code> and <code dir="ltr" translate="no">google_cloud_pipeline_components</code> to evaluate the performance between two LLM models: Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/models/side-by-side-eval#autosxs">Gemini Enterprise Agent Platform AutoSxS Model Evaluation</a> .
<p>Tutorial steps</p>
<ul>
<li>Fetch the dataset from the public source.</li>
<li>Preprocess the data locally and save test data in Cloud Storage.</li>
<li>Create and run a Gemini Enterprise Agent Platform AutoSxS Pipeline that generates the judgments and evaluates the two candidate models using the generated judgments.</li>
<li>Print the judgments and evaluation metrics.</li>
<li>Clean up the resources created in this notebook.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/model_based_llm_evaluation/autosxs_llm_evaluation_for_summarization_task.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_evaluation%2Fmodel_based_llm_evaluation%2Fautosxs_llm_evaluation_for_summarization_task.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/model_based_llm_evaluation/autosxs_llm_evaluation_for_summarization_task.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_evaluation/model_based_llm_evaluation/autosxs_llm_evaluation_for_summarization_task.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Model Monitoring for batch predictions<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Batch Prediction with Model Monitoring</strong> .<br />
Learn to use the Gemini Enterprise Agent Platform model monitoring service to detect drift and anomalies in batch prediction. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/model-monitoring-batch-predictions">Gemini Enterprise Agent Platform Model Monitoring for batch predictions</a> .
<p>Tutorial steps</p>
<ul>
<li>Upload a pretrained model as a Gemini Enterprise Agent Platform model resource.</li>
<li>Generate batch prediction requests.</li>
<li>Interpret the statistics, visualizations, other data reported by the model monitoring feature.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/batch_prediction_model_monitoring.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring%2Fbatch_prediction_model_monitoring.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/batch_prediction_model_monitoring.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_monitoring/batch_prediction_model_monitoring.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Model Monitoring<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Model Monitoring for AutoML tabular models</strong> .<br />
Learn to use the Gemini Enterprise Agent Platform Model Monitoring service to detect feature skew and drift in the input predict requests, for AutoML tabular models. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview">Gemini Enterprise Agent Platform Model Monitoring</a> .
<p>Tutorial steps</p>
<ul>
<li>Train an AutoML model.</li>
<li>Deploy the model resource to a Gemini Enterprise Agent Platform endpoint resource.</li>
<li>Configure the endpoint resource for model monitoring.</li>
<li>Generate synthetic prediction requests for skew.</li>
<li>Generate synthetic prediction requests for drift.</li>
<li>Wait for email alert notification.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_automl.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring%2Fget_started_with_model_monitoring_automl.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_automl.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_automl.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Model Monitoring<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Model Monitoring for online prediction in AutoML image models</strong> .<br />
Learn how to use <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Model Monitoring</code> with <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Online Prediction</code> with an AutoML image classification model to detect an out of distribution image. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview">Gemini Enterprise Agent Platform Model Monitoring</a> .
<p>Tutorial steps</p>
<ul>
<li>1. Train an AutoML image classification model.</li>
<li>2. Create an endpoint.</li>
<li>3. Deploy the model to the endpoint, and configure for model monitoring.</li>
<li>4. Submit a online prediction containing both in and out of distribution images.</li>
<li>5. Use Model Monitoring to calculate anomaly score on each image.</li>
<li>6. Identify the images in the online prediction request that are out of distribution.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_automl_image_online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring%2Fget_started_with_model_monitoring_automl_image_online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_automl_image_online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_automl_image_online.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Model Monitoring<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Model Monitoring for custom tabular models</strong> .<br />
Learn to use the Gemini Enterprise Agent Platform Model Monitoring service to detect feature skewness and drift in the input predict requests, for custom tabular models. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview">Gemini Enterprise Agent Platform Model Monitoring</a> .
<p>Tutorial steps</p>
<ul>
<li>Download a pretrained custom tabular model.</li>
<li>Upload the pretrained model to Model Registry.</li>
<li>Deploy the model resource to a Gemini Enterprise Agent Platform endpoint resource.</li>
<li>Configure the endpoint resource for model monitoring.</li>
<li>Generate synthetic prediction requests to simulate skewness.</li>
<li>Wait for email alert notifications.</li>
<li>Generate synthetic prediction requests to simulate drift.</li>
<li>Wait for email alert notifications.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_custom.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring%2Fget_started_with_model_monitoring_custom.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_custom.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_custom.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Model Monitoring<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Model Monitoring for custom tabular models with TensorFlow Serving container</strong> .<br />
Learn to use the Gemini Enterprise Agent Platform Model Monitoring service to detect feature skew and drift in the input predict requests, for custom tabular models, using a custom deployment container. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview">Gemini Enterprise Agent Platform Model Monitoring</a> .
<p>Tutorial steps</p>
<ul>
<li>Download a pretrained custom tabular model.</li>
<li>Upload the pretrained model as a model resource.</li>
<li>Deploying the model resource to an endpoint resource with "TensorFlow Serving" serving binary.</li>
<li>Configure the Endpoint resource for model monitoring.</li>
<li>Generate synthetic prediction requests for skew.</li>
<li>Wait for email alert notification.</li>
<li>Generate synthetic prediction requests for drift.</li>
<li>Wait for email alert notification.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_custom_tf_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring%2Fget_started_with_model_monitoring_custom_tf_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_custom_tf_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_custom_tf_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Model Monitoring<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Model Monitoring for setup for tabular models</strong> .<br />
Learn to setup the Gemini Enterprise Agent Platform Model Monitoring service to detect feature skew and drift in the input predict requests. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview">Gemini Enterprise Agent Platform Model Monitoring</a> .
<p>Tutorial steps</p>
<ul>
<li>Download a pretrained custom tabular model.</li>
<li>Upload the pretrained model as a model resource.</li>
<li>Deploy the model resource to the endpoint resource.</li>
<li>Configure the endpoint resource for model monitoring.</li>
<li>Skew and drift detection for feature inputs.</li>
<li>Skew and drift detection for feature attributions.</li>
<li>Automatic generation of the input schema by sending 1000 prediction request.</li>
<li>List, pause, resume and delete monitoring jobs.</li>
<li>Restart monitoring job with predefined input schema.</li>
<li>View logged monitored data.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_setup.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring%2Fget_started_with_model_monitoring_setup.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_setup.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_setup.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Model Monitoring<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Model Monitoring for XGBoost models</strong> .<br />
Learn to use the Gemini Enterprise Agent Platform Model Monitoring service to detect feature skew and drift in the input predict requests for XGBoost models. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview">Gemini Enterprise Agent Platform Model Monitoring</a> .
<p>Tutorial steps</p>
<ul>
<li>Download a pretrained XGBoost model.</li>
<li>Upload the pretrained model to Model Registry.</li>
<li>Deploy the model resource to a Gemini Enterprise Agent Platform endpoint resource.</li>
<li>Configure the endpoint resource for model monitoring</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring%2Fget_started_with_model_monitoring_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Model Monitoring<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Model Monitoring with Vertex Explainable AI Feature Attributions</strong> .<br />
Learn to use the Gemini Enterprise Agent Platform Model Monitoring service to detect drift and anomalies in prediction requests from a deployed Gemini Enterprise Agent Platform model resource. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview">Gemini Enterprise Agent Platform Model Monitoring</a> .
<p>Tutorial steps</p>
<ul>
<li>Upload a pretrained model as a Gemini Enterprise Agent Platform model resource.</li>
<li>Create a Gemini Enterprise Agent Platform endpoint resource.</li>
<li>Deploy the model resource to the endpoint resource.</li>
<li>Configure the endpoint resource for model monitoring.</li>
<li>Initialize the baseline distribution for model monitoring.</li>
<li>Generate synthetic prediction requests.</li>
<li>Understand how to interpret the statistics, visualizations, other data reported by the model monitoring feature.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring%2Fmodel_monitoring.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/model_monitoring/model_monitoring.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>model_monitoring_v2<br />
</td>
<td><strong>Model Monitoring for Gemini Enterprise Agent Platform Custom Model Batch Prediction Job</strong> .<br />
In this tutorial, you'll complete the following steps:
<p>Tutorial steps</p>
<ul>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_custom_model_batch_prediction_job.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2model_monitoring_v2%2model_monitoring_for_custom_model_batch_prediction_job.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_custom_model_batch_prediction_job.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_custom_model_batch_prediction_job.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>model_monitoring_v2<br />
</td>
<td><strong>Model Monitoring for Gemini Enterprise Agent Platform Custom Model Online Prediction</strong> .<br />
In this tutorial, you'll complete the following steps:
<p>Tutorial steps</p>
<ul>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_custom_model_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2model_monitoring_v2%2model_monitoring_for_custom_model_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_custom_model_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring_v2/model_monitoring_for_custom_model_online_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Model Registry<br />
</td>
<td><strong>Get started with Model Registry</strong> .<br />
Learn how to use Model Registry to create and register multiple versions of a model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction">Model Registry</a> .
<p>Tutorial steps</p>
<ul>
<li>Create and register a first version of a model to Model Registry.</li>
<li>Create and register a second version of a model to Model Registry.</li>
<li>Updating the model version which is the default.</li>
<li>Deleting a model version.</li>
<li>Retraining the next model version.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_registry/get_started_with_model_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_registry%2Fget_started_with_model_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_registry/get_started_with_model_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_registry/get_started_with_model_registry.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Pipelines<br />
AutoML components<br />
Classification for tabular data<br />
</td>
<td><strong>AutoML Tabular pipelines using google-cloud-pipeline-components</strong> .<br />
Learn to use Gemini Enterprise Agent Platform Pipelines and Google Cloud Pipeline Components to build an AutoML tabular classification model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/vertex-automl-component">AutoML components</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/overview">Classification for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a KFP pipeline that creates a Gemini Enterprise Agent Platform Dataset.</li>
<li>Add a component to the pipeline that trains an AutoML tabular classification model resource.</li>
<li>Add a component that creates a Gemini Enterprise Agent Platform endpoint resource.</li>
<li>Add a component that deploys the model resource to the endpoint resource.</li>
<li>Compile the KFP pipeline.</li>
<li>Execute the KFP pipeline using Gemini Enterprise Agent Platform Pipelines.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/automl_tabular_classification_beans.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fautoml_tabular_classification_beans.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/automl_tabular_classification_beans.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/automl_tabular_classification_beans.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Challenger vs Blessed methodology for model deployment into production</strong> .<br />
Learn how to construct a Gemini Enterprise Agent Platform pipeline, which trains a new challenger version of a model, evaluates the model and compares the evaluation to the existing blessed model in production.
<p>Tutorial steps</p>
<ul>
<li>Import a pretrained (blessed) model to the Model Registry.</li>
<li>Import synthetic model evaluation metrics to the corresponding (blessed) model.</li>
<li>Create a Gemini Enterprise Agent Platform endpoint resource</li>
<li>Deploy the blessed model to the endpoint resource.</li>
<li>Create a Gemini Enterprise Agent Platform Pipeline that runs the following steps</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/challenger_vs_blessed_deployment_method.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fchallenger_vs_blessed_deployment_method.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/challenger_vs_blessed_deployment_method.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/challenger_vs_blessed_deployment_method.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Pipeline control structures using the KFP SDK</strong> .<br />
Learn how to use the KFP SDK, which uses loops and conditionals including nested examples, to build pipelines. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a KFP pipeline using control flow components</li>
<li>Compile the KFP pipeline</li>
<li>Execute the KFP pipeline using Gemini Enterprise Agent Platform Pipelines</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/control_flow_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fcontrol_flow_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/control_flow_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/control_flow_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Pipelines<br />
Custom training components<br />
</td>
<td><strong>Custom training with pre-built Google Cloud Pipeline Components</strong> .<br />
Learn to use Gemini Enterprise Agent Platform Pipelines and Google Cloud Pipeline Components to build a custom model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline">Custom training components</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a KFP pipeline</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/custom_model_training_and_batch_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fcustom_model_training_and_batch_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/custom_model_training_and_batch_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/custom_model_training_and_batch_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Pipelines<br />
Gemini Enterprise Agent Platform Batch Prediction components<br />
</td>
<td><strong>Training and batch prediction with BigQuery source and destination for a custom tabular classification model</strong> .<br />
In this tutorial, you train a scikit-learn tabular classification model and create a batch prediction job for it through a Gemini Enterprise Agent Platform pipeline using google_cloud_pipeline_components. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/batchprediction-component">Gemini Enterprise Agent Platform Batch Prediction components</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a dataset in BigQuery.</li>
<li>Set some data aside from the source dataset for batch prediction.</li>
<li>Create a custom python package for training application.</li>
<li>Upload the python package to Cloud Storage.</li>
<li>Create a Gemini Enterprise Agent Platform Pipeline that</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/custom_tabular_train_batch_pred_bq_pipeline.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fcustom_tabular_train_batch_pred_bq_pipeline.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/custom_tabular_train_batch_pred_bq_pipeline.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/custom_tabular_train_batch_pred_bq_pipeline.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Pipelines<br />
Gemini Enterprise Agent Platform hyperparameter tuning<br />
</td>
<td><strong>Get started with Gemini Enterprise Agent Platform hyperparameter tuning pipeline components</strong> .<br />
Learn how to use prebuilt Google Cloud Pipeline Components for Gemini Enterprise Agent Platform hyperparameter tuning. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview">Gemini Enterprise Agent Platform hyperparameter tuning</a> .
<p>Tutorial steps</p>
<ul>
<li>Construct a pipeline for</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/get_started_with_hpt_pipeline_components.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fget_started_with_hpt_pipeline_components.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/get_started_with_hpt_pipeline_components.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/get_started_with_hpt_pipeline_components.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Get started with machine management for Gemini Enterprise Agent Platform Pipelines</strong> .<br />
Learn how to convert a self-contained custom training component into a <code dir="ltr" translate="no">Gemini Enterprise Agent Platform CustomJob</code> , whereby:
<p>Tutorial steps</p>
<ul>
<li>Create a custom component with a selfcontained training job.</li>
<li>Execute pipeline using componentlevel settings for machine resources</li>
<li>Convert the selfcontained training component into a <code dir="ltr" translate="no">Gemini Enterprise Agent Platform CustomJob</code> .</li>
<li>Execute pipeline using customjoblevel settings for machine resources</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/get_started_with_machine_management.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/get_started_with_machine_management.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/get_started_with_machine_management.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Pipelines<br />
AutoML components<br />
</td>
<td><strong>AutoML image classification pipelines using google-cloud-pipeline-components</strong> .<br />
Learn how to use Gemini Enterprise Agent Platform Pipelines and Google Cloud pipeline components to build an AutoML image classification model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/vertex-automl-component">AutoML components</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a KFP pipeline</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_automl_images.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fgoogle_cloud_pipeline_components_automl_images.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_automl_images.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/google_cloud_pipeline_components_automl_images.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Pipelines<br />
AutoML components<br />
Regression for tabular data<br />
</td>
<td><strong>AutoML tabular regression pipelines using google-cloud-pipeline-components</strong> .<br />
Learn to use <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Pipelines</code> and <code dir="ltr" translate="no">Google Cloud Pipeline Components</code> to build an <code dir="ltr" translate="no">AutoML</code> tabular regression model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/vertex-automl-component">AutoML components</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/overview">Regression for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a KFP pipeline that creates a <code dir="ltr" translate="no">Dataset</code> resource.</li>
<li>Add a component to the pipeline that trains an AutoML tabular regression <code dir="ltr" translate="no">Model</code> resource.</li>
<li>Add a component that creates an <code dir="ltr" translate="no">Endpoint</code> resource.</li>
<li>Add a component that deploys the <code dir="ltr" translate="no">Model</code> resource to the <code dir="ltr" translate="no">Endpoint</code> resource.</li>
<li>Compile the KFP pipeline.</li>
<li>Execute the KFP pipeline using <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Pipelines</code> .</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_automl_tabular.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fgoogle_cloud_pipeline_components_automl_tabular.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_automl_tabular.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/google_cloud_pipeline_components_automl_tabular.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Pipelines<br />
BigQuery ML components<br />
</td>
<td><strong>Training an acquisition-prediction model using Swivel, BigQuery ML and Gemini Enterprise Agent Platform Pipelines</strong> .<br />
Learn how to build a simple BigQuery ML pipeline using Agent Platform Pipelines in order to calculate text embeddings of content from articles and classify them into the *corporate acquisitions* category. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/bigqueryml-component">BigQuery ML components</a> .
<p>Tutorial steps</p>
<ul>
<li>Creating a component for Dataflow job that ingests data to BigQuery.</li>
<li>Creating a component for preprocessing steps to run on the data in BigQuery.</li>
<li>Creating a component for training a logistic regression model using BigQuery ML.</li>
<li>Building and configuring a Kubeflow DSL pipeline with all the created components.</li>
<li>Compiling and running the pipeline in Gemini Enterprise Agent Platform Pipelines.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_bqml_text.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fgoogle_cloud_pipeline_components_bqml_text.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_bqml_text.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/google_cloud_pipeline_components_bqml_text.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Pipelines<br />
Custom training components<br />
</td>
<td><strong>Model train, upload, and deploy using Google Cloud Pipeline Components</strong> .<br />
Learn how to use Gemini Enterprise Agent Platform Pipelines and Google Cloud pipeline component to build and deploy a custom model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/customjob-component">Custom training components</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a KFP pipeline</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_model_train_upload_deploy.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fgoogle_cloud_pipeline_components_model_train_upload_deploy.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_model_train_upload_deploy.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/google_cloud_pipeline_components_model_train_upload_deploy.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Pipelines with KFP 2.x</strong> .<br />
Learn to use <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Pipelines</code> and KFP 2.
<p>Tutorial steps</p>
<ul>
<li>Create a KFP pipeline</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/kfp2_pipeline.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fkfp2_pipeline.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/kfp2_pipeline.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/kfp2_pipeline.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Lightweight Python function-based components, and component I/O</strong> .<br />
Learn to use the KFP SDK to build lightweight Python function-based components, and then you learn to use Gemini Enterprise Agent Platform Pipelines to execute the pipeline. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> .
<p>Tutorial steps</p>
<ul>
<li>Build Python functionbased KFP components.</li>
<li>Construct a KFP pipeline.</li>
<li>Pass Artifacts and parameters between components, both by path reference and by value.</li>
<li>Use the kfp.dsl.importer method.</li>
<li>Compile the KFP pipeline.</li>
<li>Execute the KFP pipeline using Gemini Enterprise Agent Platform Pipelines</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/lightweight_functions_component_io_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Flightweight_functions_component_io_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/lightweight_functions_component_io_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/lightweight_functions_component_io_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Metrics visualization and run comparison using the KFP SDK</strong> .<br />
Learn how to use the KFP SDK for Python to build pipelines that generate evaluation metrics. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> .
<p>Tutorial steps</p>
<ul>
<li>Create KFP components</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/metrics_viz_run_compare_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fmetrics_viz_run_compare_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/metrics_viz_run_compare_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/metrics_viz_run_compare_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Multicontender vs Champion methodology for model deployment into production</strong> .<br />
Learn how to construct a Gemini Enterprise Agent Platform pipeline, which evaluates new production data from a deployed model against other versions of the model, to determine if a contender model becomes the champion model for replacement in production.
<p>Tutorial steps</p>
<ul>
<li>Import a pretrained (champion) model to the Model Registry.</li>
<li>Import synthetic model training evaluation metrics to the corresponding (champion) model.</li>
<li>Create a Gemini Enterprise Agent Platform endpoint resource.</li>
<li>Deploy the champion model to the endpoint resource.</li>
<li>Import additional (contender) versions of the deployed model.</li>
<li>Import synthetic model training evaluation metrics to the corresponding (contender) models.</li>
<li>Create a Gemini Enterprise Agent Platform Pipeline that runs the following steps</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/multicontender_vs_champion_deployment_method.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fmulticontender_vs_champion_deployment_method.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/multicontender_vs_champion_deployment_method.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/multicontender_vs_champion_deployment_method.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Pipelines introduction for KFP</strong> .<br />
Learn how to use the KFP SDK for Python to build pipelines that generate evaluation metrics. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> .
<p>Tutorial steps</p>
<ul>
<li>Define and compile a Gemini Enterprise Agent Platform pipeline.</li>
<li>Specify which service account to use for a pipeline run.</li>
<li>Run the pipeline using Agent Platform SDK for Python and REST API.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/pipelines_intro_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fpipelines_intro_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/pipelines_intro_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/pipelines_intro_kfp.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>AutoML components<br />
BigQuery ML components<br />
</td>
<td><strong>BigQuery ML and AutoML - Rapid Prototyping with Gemini Enterprise Agent Platform</strong> .<br />
Learn how to use Gemini Enterprise Agent Platform Pipelines for rapid prototyping a model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/vertex-automl-component">AutoML components</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/bigqueryml-component">BigQuery ML components</a> .
<p>Tutorial steps</p>
<ul>
<li>Creating a BigQuery and Gemini Enterprise Agent Platform training dataset.</li>
<li>Training a BigQuery ML and AutoML model.</li>
<li>Extracting evaluation metrics from the BigQueryML and AutoML models.</li>
<li>Selecting the best trained model.</li>
<li>Deploying the best trained model.</li>
<li>Testing the deployed model infrastructure.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/rapid_prototyping_bqml_automl.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Frapid_prototyping_bqml_automl.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/rapid_prototyping_bqml_automl.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/pipelines/rapid_prototyping_bqml_automl.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Batch Inference<br />
</td>
<td><strong>Custom model batch inference with feature filtering</strong> .<br />
Learn how to create a custom-trained model from a Python script in a Docker container using the Agent Platform SDK for Python, and then run a batch inference job by including or excluding a list of features. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions">Gemini Enterprise Agent Platform Batch Inference</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a Gemini Enterprise Agent Platform custom <code dir="ltr" translate="no">TrainingPipeline</code> for training a model.</li>
<li>Train a TensorFlow model.</li>
<li>Send batch prediction job.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/custom_batch_prediction_feature_filter.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fcustom_batch_prediction_feature_filter.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/custom_batch_prediction_feature_filter.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/prediction/custom_batch_prediction_feature_filter.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex AI Inference<br />
</td>
<td><strong>Get started with NVIDIA Triton server</strong> .<br />
Learn how to deploy a container running Nvidia Triton Server with a Gemini Enterprise Agent Platform model resource to a Gemini Enterprise Agent Platform endpoint for making online predictions. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions">Vertex AI Inference</a> .
<p>Tutorial steps</p>
<ul>
<li>Download the model artifacts from TensorFlow Hub.</li>
<li>Create Triton serving configuration file for the model.</li>
<li>Construct a custom container, with Triton serving image, for model deployment.</li>
<li>Upload the model as a Gemini Enterprise Agent Platform model resource.</li>
<li>Deploy the Gemini Enterprise Agent Platform model resource to a Gemini Enterprise Agent Platform endpoint resource.</li>
<li>Make a prediction request.</li>
<li>Undeploy the model resource and delete the endpoint.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/get_started_with_nvidia_triton_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2F%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fget_started_with_nvidia_triton_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/get_started_with_nvidia_triton_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/prediction/get_started_with_nvidia_triton_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Raw Predict<br />
</td>
<td><strong>Get started with TensorFlow serving functions with Gemini Enterprise Agent Platform Raw Prediction</strong> .<br />
Learn how to use <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Raw Prediction</code> on a <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Endpoint</code> resource. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/rawPredict">Raw Predict</a> .
<p>Tutorial steps</p>
<ul>
<li>Download pretrained tabular classification model artifacts for a TensorFlow 1.x estimator.</li>
<li>Upload the TensorFlow estimator model as a <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Model</code> resource.</li>
<li>Create an <code dir="ltr" translate="no">Endpoint</code> resource.</li>
<li>Deploy the <code dir="ltr" translate="no">Model</code> resource to an <code dir="ltr" translate="no">Endpoint</code> resource.</li>
<li>Make an online raw prediction to the <code dir="ltr" translate="no">Model</code> resource instance deployed to the <code dir="ltr" translate="no">Endpoint</code> resource.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/get_started_with_raw_predict.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fget_started_with_raw_predict.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/get_started_with_raw_predict.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/prediction/get_started_with_raw_predict.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>getting predictions from a custom trained model<br />
</td>
<td><strong>Get started with TensorFlow Serving with Vertex AI Inference</strong> .<br />
Learn how to use <code dir="ltr" translate="no">Vertex AI Inference</code> on a <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Endpoint</code> resource with <code dir="ltr" translate="no">TensorFlow Serving</code> serving binary. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-predictions">getting predictions from a custom trained model</a> .
<p>Tutorial steps</p>
<ul>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/get_started_with_tf_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fget_started_with_tf_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/get_started_with_tf_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/prediction/get_started_with_tf_serving.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Private Endpoints<br />
</td>
<td><strong>Get started with Gemini Enterprise Agent Platform Private Endpoints</strong> .<br />
Learn how to use <code dir="ltr" translate="no">Gemini Enterprise Agent Platform Private Endpoint</code> resources. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-private-endpoints">Private Endpoints</a> .
<p>Tutorial steps</p>
<ul>
<li>Creating a <code dir="ltr" translate="no">Private Endpoint</code> resource.</li>
<li>Configure a VPC peering connection.</li>
<li>Configuring the serving binary of a <code dir="ltr" translate="no">Model</code> resource for deployment to a <code dir="ltr" translate="no">Private Endpoint</code> resource.</li>
<li>Deploying a <code dir="ltr" translate="no">Model</code> resource to a <code dir="ltr" translate="no">Private Endpoint</code> resource.</li>
<li>Send a prediction request to a <code dir="ltr" translate="no">Private Endpoint</code></li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/get_started_with_vertex_private_endpoints.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fget_started_with_vertex_private_endpoints.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/get_started_with_vertex_private_endpoints.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/prediction/get_started_with_vertex_private_endpoints.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Language Models<br />
</td>
<td><strong>Gemini Enterprise Agent Platform LLM and streaming prediction</strong> .<br />
Learn how to use Gemini Enterprise Agent Platform LLM to download pretrained LLM model, make predictions and finetuning the model. Learn more about <a href="https://cloud.google.com/python/docs/reference/aiplatform/latest/vertexai.language_models.TextGenerationModel#vertexai_language_models_TextGenerationModel_predict_streaming">Gemini Enterprise Agent Platform Language Models</a> .
<p>Tutorial steps</p>
<ul>
<li>Load a pretrained text generation model.</li>
<li>Make a nonstreaming prediction</li>
<li>Load a pretrained text generation model, which supports streaming.</li>
<li>Make a streaming prediction</li>
<li>Load a pretrained chat model.</li>
<li>Do a local interactive chat session.</li>
<li>Do a batch prediction with a text generation model.</li>
<li>Do a batch prediction with a text embedding model.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official//prediction/llm_streaming_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fllm_streaming_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/llm_streaming_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/prediction/llm_streaming_prediction.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Pre-built containers for prediction<br />
</td>
<td><strong>Serving PyTorch image models with prebuilt containers on Gemini Enterprise Agent Platform</strong> .<br />
Learn how to package and deploy a PyTorch image classification model using a prebuilt Gemini Enterprise Agent Platform container with TorchServe for serving online and batch predictions. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/pre-built-containers">Pre-built containers for prediction</a> .
<p>Tutorial steps</p>
<ul>
<li>Download a pretrained image model from PyTorch</li>
<li>Create a custom model handler</li>
<li>Package model artifacts in a model archive file</li>
<li>Upload model for deployment</li>
<li>Deploy model for prediction</li>
<li>Make online predictions</li>
<li>Make batch predictions</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/pytorch_image_classification_with_prebuilt_serving_containers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fpytorch_image_classification_with_prebuilt_serving_containers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/pytorch_image_classification_with_prebuilt_serving_containers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/prediction/pytorch_image_classification_with_prebuilt_serving_containers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Inference<br />
</td>
<td><strong>Train and deploy PyTorch models with prebuilt containers on Gemini Enterprise Agent Platform</strong> .<br />
Learn how to build, train and deploy a PyTorch image classification model using prebuilt containers for custom training and prediction.
<p>Tutorial steps</p>
<ul>
<li>Package training application into a Python source distribution</li>
<li>Configure and run training job in a prebuilt container</li>
<li>Package model artifacts in a model archive file</li>
<li>Upload model for deployment</li>
<li>Deploy model using a prebuilt container for prediction</li>
<li>Make online predictions</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/pytorch_train_deploy_models_with_prebuilt_containers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fpytorch_train_deploy_models_with_prebuilt_containers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/pytorch_train_deploy_models_with_prebuilt_containers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/prediction/pytorch_train_deploy_models_with_prebuilt_containers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Ray on Gemini Enterprise Agent Platform overview<br />
</td>
<td><strong>Get started with PyTorch on Ray on Gemini Enterprise Agent Platform</strong> .<br />
Learn how to efficiently distribute the training process of a PyTorch image classification model by leveraging Ray on Gemini Enterprise Agent Platform. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/">Ray on Gemini Enterprise Agent Platform overview</a> .
<p>Tutorial steps</p>
<ul>
<li>Prepare the training script</li>
<li>Submit a Ray job using the Ray Jobs API</li>
<li>Download a trained image model from PyTorch</li>
<li>Create a custom model handler</li>
<li>Package model artifacts in a model archive file</li>
<li>Register model in Model Registry</li>
<li>Deploy model in Gemini Enterprise Agent Platform Endpoint</li>
<li>Make online predictions</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/get_started_with_pytorch_rov.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fget_started_with_pytorch_rov.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/get_started_with_pytorch_rov.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/get_started_with_pytorch_rov.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Ray on Gemini Enterprise Agent Platform overview<br />
</td>
<td><strong>Ray on Gemini Enterprise Agent Platform cluster management</strong> .<br />
Learn how to create a cluster, list existing clusters, get a cluster, update a cluster, and delete a cluster. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/">Ray on Gemini Enterprise Agent Platform overview</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a cluster.</li>
<li>List existing clusters.</li>
<li>Get a cluster.</li>
<li>Manually scale up the cluster, then scale down the cluster.</li>
<li>Autoscaling a cluster.</li>
<li>Delete existing clusters.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/ray_cluster_management.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fray_cluster_management.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/ray_cluster_management.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/ray_on_vertex_ai/ray_cluster_management.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Ray on Gemini Enterprise Agent Platform<br />
Spark on Ray on Gemini Enterprise Agent Platform<br />
</td>
<td><strong>Spark on Ray on Gemini Enterprise Agent Platform</strong> .<br />
Learn how to use RayDP to run Spark applications on a Ray cluster on Gemini Enterprise Agent Platform. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/">Ray on Gemini Enterprise Agent Platform</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/run-spark-on-ray">Spark on Ray on Gemini Enterprise Agent Platform</a> .
<p>Tutorial steps</p>
<ul>
<li>Create custom Ray on Gemini Enterprise Agent Platform container image</li>
<li>Create a Ray cluster on Gemini Enterprise Agent Platform using custom container image</li>
<li>Run Spark interactively on the cluster using RayDP</li>
<li>Run Spark application on cluster via Ray Job API</li>
<li>Read files from Google Cloud Storage in Spark application</li>
<li>Pandas UDF in Spark application on Ray on Gemini Enterprise Agent Platform</li>
<li>Delete the Ray cluster on Gemini Enterprise Agent Platform</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/spark_on_ray_on_vertex_ai.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fspark_on_ray_on_vertex_ai.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/spark_on_ray_on_vertex_ai.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/ray_on_vertex_ai/spark_on_ray_on_vertex_ai.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex AI Training<br />
Gemini Enterprise Agent Platform Reduction Server<br />
</td>
<td><strong>PyTorch distributed training with Gemini Enterprise Agent Platform Reduction Server</strong> .<br />
Learn how to create a PyTorch distributed training job that uses PyTorch distributed training framework and tools, and run the training job on the Vertex AI Training service with Reduction Server. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Vertex AI Training</a> . Learn more about <a href="https://cloud.google.com/blog/topics/developers-practitioners/optimize-training-performance-reduction-server-vertex-ai">Gemini Enterprise Agent Platform Reduction Server</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a PyTorch distributed training application</li>
<li>Package the training application with prebuilt containers</li>
<li>Create a custom job on Gemini Enterprise Agent Platform with Reduction Server</li>
<li>Submit and monitor the job</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/reduction_server/pytorch_distributed_training_reduction_server.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Freduction_server%2Fpytorch_distributed_training_reduction_server.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/reduction_server/pytorch_distributed_training_reduction_server.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/reduction_server/pytorch_distributed_training_reduction_server.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Custom training<br />
</td>
<td><strong>Custom training using Python package, managed text dataset, and TF Serving container</strong> .<br />
Learn how to create a custom model using Custom Python Package Training and you learn how to serve the model using TensorFlow-Serving Container for online prediction. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Create utility functions to download data and prepare csv files for creating Gemini Enterprise Agent Platform managed dataset</li>
<li>Download Data</li>
<li>Prepare CSV Files for creating managed dataset</li>
<li>Create custom training Python package</li>
<li>Create TensorFlow Serving container</li>
<li>Run custom Python package training with managed text dataset</li>
<li>Deploy a model and create an endpoint on Gemini Enterprise Agent Platform</li>
<li>Predict on the endpoint</li>
<li>Create a Batch Prediction job on the model</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/sdk/SDK_Custom_Training_Python_Package_Managed_Text_Dataset_Tensorflow_Serving_Container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fsdk%2FSDK_Custom_Training_Python_Package_Managed_Text_Dataset_Tensorflow_Serving_Container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/sdk/SDK_Custom_Training_Python_Package_Managed_Text_Dataset_Tensorflow_Serving_Container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/sdk/SDK_Custom_Training_Python_Package_Managed_Text_Dataset_Tensorflow_Serving_Container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>BigQuery ML ARIMA+ forecasting for tabular data<br />
</td>
<td><strong>Train a BigQuery ML ARIMA_PLUS Model using Gemini Enterprise Agent Platform tabular workflows</strong> .<br />
Learn how to create the BigQuery ML ARIMA_PLUS model using a training Gemini Enterprise Agent Platform Pipeline from Google Cloud Pipeline Components , and then do a batch prediction using the corresponding prediction pipeline. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-arima/overview">BigQuery ML ARIMA+ forecasting for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>Train the BigQuery ML ARIMA_PLUS model.</li>
<li>View BigQuery ML model evaluation.</li>
<li>Make a batch prediction with the BigQuery ML model.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tabular_workflows/bqml_arima_plus.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftabular_workflows%2Fbqml_arima_plus.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tabular_workflows/bqml_arima_plus.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/tabular_workflows/bqml_arima_plus.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Google Cloud Pipeline Components<br />
Prophet for tabular data<br />
</td>
<td><strong>Train a Prophet Model using Gemini Enterprise Agent Platform Tabular Workflows</strong> .<br />
Learn how to create several Prophet models using a training Gemini Enterprise Agent Platform Pipeline from Google Cloud Pipeline Components , and then do a batch prediction using the corresponding prediction pipeline. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-introduction">Google Cloud Pipeline Components</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-prophet">Prophet for tabular data</a> .
<p>Tutorial steps</p>
<ul>
<li>1. Train the Prophet models.</li>
<li>1. View the evaluation metrics.</li>
<li>1. Make a batch prediction with the Prophet models.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tabular_workflows/prophet_on_vertex_pipelines.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftabular_workflows%2Fprophet_on_vertex_pipelines.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tabular_workflows/prophet_on_vertex_pipelines.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/tabular_workflows/prophet_on_vertex_pipelines.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex AI TensorBoard<br />
Custom training<br />
</td>
<td><strong>Vertex AI TensorBoard custom training with custom container</strong> .<br />
Learn how to create a custom training job using custom containers, and monitor your training process on Vertex AI TensorBoard in near real time. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction">Vertex AI TensorBoard</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Create docker repository &amp; config.</li>
<li>Create a custom container image with your customized training code.</li>
<li>Setup service account and Google Cloud Storage buckets.</li>
<li>Create &amp; launch your custom training job with your custom container.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_custom_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/tensorboard/tensorboard_custom_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Vertex AI TensorBoard<br />
Custom training<br />
</td>
<td><strong>Vertex AI TensorBoard custom training with prebuilt container</strong> .<br />
Learn how to create a custom training job using prebuilt containers, and monitor your training process on Vertex AI TensorBoard in near real time. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction">Vertex AI TensorBoard</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Setup service account and Cloud Storage buckets.</li>
<li>Write your customized training code.</li>
<li>Package and upload your training code to Cloud Storage.</li>
<li>Create &amp; launch your custom training job with Vertex AI TensorBoard enabled for near real time monitoring.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_prebuilt_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_custom_training_with_prebuilt_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_prebuilt_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/tensorboard/tensorboard_custom_training_with_prebuilt_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex AI TensorBoard<br />
</td>
<td><strong>Vertex AI TensorBoard hyperparameter tuning with the HParams Dashboard</strong> .<br />
In this notebook, you train a model and perform hyperparameter tuning using tensorflow.
<p>Tutorial steps</p>
<ul>
<li>Adapt TensorFlow runs to log hyperparameters and metrics.</li>
<li>Start runs and log them all under one parent directory.</li>
<li>Visualize the results in Vertex AI TensorBoard's HParams dashboard.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_hyperparameter_tuning_with_hparams.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_hyperparameter_tuning_with_hparams.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_hyperparameter_tuning_with_hparams.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/tensorboard/tensorboard_hyperparameter_tuning_with_hparams.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Profiler<br />
Vertex AI TensorBoard<br />
</td>
<td><strong>Profile model training performance using Cloud Profiler</strong> .<br />
Learn how to enable Profiler for custom training jobs. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler">Profiler</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction">Vertex AI TensorBoard</a> .
<p>Tutorial steps</p>
<ul>
<li>Setup a service account and a Cloud Storage bucket</li>
<li>Create a Vertex AI TensorBoard instance</li>
<li>Create and run a custom training job that enables Profiler</li>
<li>View the Profiler dashboard to debug your model training performance</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Profiler<br />
Vertex AI TensorBoard<br />
</td>
<td><strong>Profile model training performance using Cloud Profiler in custom training with prebuilt container</strong> .<br />
Learn how to enable Profiler in Gemini Enterprise Agent Platform for custom training jobs with a prebuilt container. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler">Profiler</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction">Vertex AI TensorBoard</a> .
<p>Tutorial steps</p>
<ul>
<li>Prepare your custom training code and load your training code as a Python package to a prebuilt container</li>
<li>Create and run a custom training job that enables Profiler</li>
<li>View the Profiler dashboard to debug your model training performance</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training_with_prebuilt_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training_with_prebuilt_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training_with_prebuilt_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training_with_prebuilt_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Vertex AI TensorBoard<br />
Gemini Enterprise Agent Platform Pipelines<br />
</td>
<td><strong>Vertex AI TensorBoard integration with Gemini Enterprise Agent Platform Pipelines</strong> .<br />
Learn how to create a training pipeline using the KFP SDK, execute the pipeline in Gemini Enterprise Agent Platform Pipelines, and monitor the training process on Vertex AI TensorBoard in near real time. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction">Vertex AI TensorBoard</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction">Gemini Enterprise Agent Platform Pipelines</a> .
<p>Tutorial steps</p>
<ul>
<li>Setup a service account and Google Cloud Storage buckets.</li>
<li>Construct a KFP pipeline with your custom training code.</li>
<li>Compile and execute the KFP pipeline in Gemini Enterprise Agent Platform Pipelines with Vertex AI TensorBoard enabled for near real time monitoring.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_vertex_ai_pipelines_integration.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_vertex_ai_pipelines_integration.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_vertex_ai_pipelines_integration.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/tensorboard/tensorboard_vertex_ai_pipelines_integration.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Hyperparameter Tuning<br />
</td>
<td><strong>Distributed Gemini Enterprise Agent Platform Hyperparameter Tuning</strong> .<br />
In this notebook, you create a custom trained model from a Python script in a Docker container. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview">Gemini Enterprise Agent Platform Hyperparameter Tuning</a> .
<p>Tutorial steps</p>
<ul>
<li>Training using a Python package.</li>
<li>Report accuracy when hyperparameter tuning.</li>
<li>Save the model artifacts to Cloud Storage using Cloud StorageFuse.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/distributed_hyperparameter_tuning.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fdistributed_hyperparameter_tuning.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/distributed_hyperparameter_tuning.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/distributed_hyperparameter_tuning.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Vertex AI Training<br />
</td>
<td><strong>Get started with Vertex AI Training for LightGBM</strong> .<br />
Learn how to train a LightGBM custom model using the custom container method for Vertex AI Training.
<p>Tutorial steps</p>
<ul>
<li>Training using a Python package.</li>
<li>Save the model artifacts to Cloud Storage using Cloud StorageFuse.</li>
<li>Construct a FastAPI prediction server.</li>
<li>Construct a Dockerfile deployment image for the server.</li>
<li>Test the deployment image locally (optional and not for Colab users).</li>
<li>Create a Gemini Enterprise Agent Platform model resource.</li>
<li>Run a batch prediction job.</li>
<li>Deploy the model to an endpoint and send online prediction requests.</li>
<li>Clean up the created resources.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/get_started_vertex_training_lightgbm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fget_started_vertex_training_lightgbm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/get_started_vertex_training_lightgbm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/get_started_vertex_training_lightgbm.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform distributed training<br />
</td>
<td><strong>Get started with Gemini Enterprise Agent Platform distributed training</strong> .<br />
Learn how to use Gemini Enterprise Agent Platform distributed training when training with <code dir="ltr" translate="no">Gemini Enterprise Agent Platform</code> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training">Gemini Enterprise Agent Platform distributed training</a> .
<p>Tutorial steps</p>
<ul>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/get_started_with_vertex_distributed_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fget_started_with_vertex_distributed_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/get_started_with_vertex_distributed_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/get_started_with_vertex_distributed_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Hyperparameter Tuning<br />
</td>
<td><strong>Run hyperparameter tuning for a TensorFlow model</strong> .<br />
Learn how to run a Gemini Enterprise Agent Platform hyperparameter tuning job for a TensorFlow model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview">Gemini Enterprise Agent Platform Hyperparameter Tuning</a> .
<p>Tutorial steps</p>
<ul>
<li>Modify training application code for automated hyperparameter tuning.</li>
<li>Containerize training application code.</li>
<li>Configure and launch a hyperparameter tuning job with the Gemini Enterprise Agent Platform Python SDK.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/hyperparameter_tuning_tensorflow.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fhyperparameter_tuning_tensorflow.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/hyperparameter_tuning_tensorflow.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/hyperparameter_tuning_tensorflow.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform hyperparameter tuning<br />
</td>
<td><strong>Gemini Enterprise Agent Platform Hyperparameter Tuning for XGBoost</strong> .<br />
Learn how to use the Gemini Enterprise Agent Platform hyperparameter tuning service for training an XGBoost model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview">Gemini Enterprise Agent Platform hyperparameter tuning</a> .
<p>Tutorial steps</p>
<ul>
<li>Train using a Python training application package.</li>
<li>Report accuracy during hyperparameter tuning.</li>
<li>Save the model artifacts to Cloud Storage using Cloud StorageFuse.</li>
<li>List the best model.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/hyperparameter_tuning_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fhyperparameter_tuning_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/hyperparameter_tuning_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/hyperparameter_tuning_xgboost.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Vertex AI Training<br />
</td>
<td><strong>PyTorch image classification multi-node distributed data parallel training on cpu using Gemini Enterprise Agent Platform training with custom container</strong> .<br />
Learn how to create a distributed PyTorch training job using Agent Platform SDK for Python and custom containers. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Vertex AI Training</a> .
<p>Tutorial steps</p>
<ul>
<li>Setting up your Google Cloud project</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/multi_node_ddp_gloo_vertex_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fmulti_node_ddp_gloo_vertex_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/multi_node_ddp_gloo_vertex_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/multi_node_ddp_gloo_vertex_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Vertex AI Training<br />
</td>
<td><strong>PyTorch image classification using multi-node NCCL distributed data parallel training on CPU and Gemini Enterprise Agent Platform</strong> .<br />
Learn how to create a distributed PyTorch training job using Agent Platform SDK for Python and custom containers. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Vertex AI Training</a> .
<p>Tutorial steps</p>
<ul>
<li>Building a custom container using Artifact Registry and Docker.</li>
<li>Creating a Gemini Enterprise Agent Platform tensorboard instance to store your Gemini Enterprise Agent Platform experiment.</li>
<li>Run a Gemini Enterprise Agent Platform training job using Agent Platform SDK for Python.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/multi_node_ddp_nccl_vertex_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fmulti_node_ddp_nccl_vertex_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/multi_node_ddp_nccl_vertex_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/multi_node_ddp_nccl_vertex_training_with_custom_container.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Custom training<br />
</td>
<td><strong>Training, tuning and deploying a PyTorch text sentiment classification model on Gemini Enterprise Agent Platform</strong> .<br />
Learn to build, train, tune and deploy a PyTorch model on Gemini Enterprise Agent Platform. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Create training package for the text classification model.</li>
<li>Train the model with custom training on Gemini Enterprise Agent Platform.</li>
<li>Check the created model artifacts.</li>
<li>Create a custom container for predictions.</li>
<li>Deploy the trained model to a Gemini Enterprise Agent Platform Endpoint using the custom container for predictions.</li>
<li>Send online prediction requests to the deployed model and validate.</li>
<li>Clean up the resources created in this notebook.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_evaluation/model_based_llm_evaluation/autosxs_check_alignment_against_human_preference_data.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fpytorch-text-sentiment-classification-custom-train-deploy.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/pytorch-text-sentiment-classification-custom-train-deploy.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/pytorch-text-sentiment-classification-custom-train-deploy.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>PyTorch integration in Gemini Enterprise Agent Platform<br />
</td>
<td><strong>Train PyTorch model on Gemini Enterprise Agent Platform with data from Cloud Storage</strong> .<br />
Learn how to create a training job using PyTorch and a dataset stored on Cloud Storage. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/pytorch">PyTorch integration in Gemini Enterprise Agent Platform</a> .
<p>Tutorial steps</p>
<ul>
<li>Writing a custom training script that creates your train &amp; test datasets and trains the model.</li>
<li>Running a <code dir="ltr" translate="no">CustomTrainingJob</code> using Agent Platform SDK for Python.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/pytorch_gcs_data_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fpytorch_gcs_data_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/pytorch_gcs_data_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/pytorch_gcs_data_training.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Distributed training<br />
</td>
<td><strong>Using PyTorch torchrun to simplify multi-node training with custom containers</strong> .<br />
Learn how to train an Imagenet model using PyTorch's Torchrun on multiple nodes. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training">Distributed training</a> .
<p>Tutorial steps</p>
<ul>
<li>Create a shell script to start an ETCD cluster on the master node</li>
<li>Create a training script using code from PyTorch Elastic's GitHub repository</li>
<li>Create containers that download the data, and start an ETCD cluster on the host</li>
<li>Train the model using multiple nodes with GPUs</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/sdk_pytorch_torchrun_custom_container_training_imagenet.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fsdk_pytorch_torchrun_custom_container_training_imagenet.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/sdk_pytorch_torchrun_custom_container_training_imagenet.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/sdk_pytorch_torchrun_custom_container_training_imagenet.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Custom training<br />
</td>
<td><strong>Distributed XGBoost training with Dask</strong> .<br />
Learn how to create a distributed training job using XGBoost with Dask. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Configure the <code dir="ltr" translate="no">PROJECT_ID</code> and <code dir="ltr" translate="no">LOCATION</code> variables for your Google Cloud project.</li>
<li>Create a Cloud Storage bucket to store your model artifacts.</li>
<li>Build a custom Docker container that hosts your training code and push the container image to Artifact Registry.</li>
<li>Run a Agent Platform SDK CustomContainerTrainingJob</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/xgboost_data_parallel_training_on_cpu_using_dask.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fxgboost_data_parallel_training_on_cpu_using_dask.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/xgboost_data_parallel_training_on_cpu_using_dask.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/training/xgboost_data_parallel_training_on_cpu_using_dask.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>vector_search<br />
</td>
<td><strong>Using Gemini Enterprise Agent Platform Multimodal Embeddings and Vector Search</strong> .<br />
Learn how to encode custom text embeddings, create an Approximate Nearest Neighbor index, and query against indexes.
<p>Tutorial steps</p>
<ul>
<li>Convert an image dataset to embeddings.</li>
<li>Create an index.</li>
<li>Upload embeddings to the index.</li>
<li>Create an index endpoint.</li>
<li>Deploy the index to the index endpoint.</li>
<li>Perform an online query.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vector_search/sdk_vector_search_create_multimodal_embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2fvector_search%2fsdk_vector_search_create_multimodal_embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vector_search/sdk_vector_search_create_multimodal_embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/vector_search/sdk_vector_search_create_multimodal_embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Vector Search<br />
</td>
<td><strong>Using Gemini Enterprise Agent Platform Vector Search for StackOverflow Questions</strong> .<br />
Learn how to encode custom text embeddings, create an Approximate Nearest Neighbor index, and query against indexes. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview">Gemini Enterprise Agent Platform Vector Search</a> .
<p>Tutorial steps</p>
<ul>
<li>Create ANN index.</li>
<li>Create an index endpoint with VPC Network.</li>
<li>Deploy ANN index.</li>
<li>Perform online query.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vector_search/sdk_vector_search_create_stack_overflow_embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fvector_search%2Fsdk_vector_search_create_stack_overflow_embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vector_search/sdk_vector_search_create_stack_overflow_embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/vector_search/sdk_vector_search_create_stack_overflow_embeddings.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Vector Search<br />
Gemini Enterprise Agent Platform embeddings for text<br />
</td>
<td><strong>Using Gemini Enterprise Agent Platform Vector Search and Gemini Enterprise Agent Platform embeddings for text for StackOverflow Questions</strong> .<br />
Learn how to encode text embeddings, create an Approximate Nearest Neighbor index, and query against indexes. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview">Gemini Enterprise Agent Platform Vector Search</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-text-embeddings">Gemini Enterprise Agent Platform embeddings for text</a> .
<p>Tutorial steps</p>
<ul>
<li>Convert a BigQuery dataset to embeddings.</li>
<li>Create an index.</li>
<li>Upload embeddings to the index.</li>
<li>Create an index endpoint.</li>
<li>Deploy the index to the index endpoint.</li>
<li>Perform an online query.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vector_search/sdk_vector_search_create_stack_overflow_embeddings_vertex.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fvector_search%2Fsdk_vector_search_create_stack_overflow_embeddings_vertex.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vector_search/sdk_vector_search_create_stack_overflow_embeddings_vertex.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/vector_search/sdk_vector_search_create_stack_overflow_embeddings_vertex"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Vector Search<br />
</td>
<td><strong>Create Gemini Enterprise Agent Platform Vector Search index</strong> .<br />
Learn how to create Approximate Nearest Neighbor Index, query against indexes, and validate the performance of the index. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview">Gemini Enterprise Agent Platform Vector Search</a> .
<p>Tutorial steps</p>
<ul>
<li>Create ANN Index and Brute Force Index.</li>
<li>Create an IndexEndpoint with VPC Network.</li>
<li>Deploy ANN Index and Brute Force Index.</li>
<li>Perform online query.</li>
<li>Compute recall.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vector_search/sdk_vector_search_for_indexing.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fvector_search%2Fsdk_vector_search_for_indexing.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vector_search/sdk_vector_search_for_indexing.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/vector_search/sdk_vector_search_for_indexing.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Agent Platform Vizier<br />
</td>
<td><strong>Optimizing multiple objectives with Agent Platform Vizier</strong> .<br />
Learn how to use Agent Platform Vizier to optimize a multi-objective study. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/vizier/overview">Agent Platform Vizier</a> .
<p>Tutorial steps</p>
<ul>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vizier/gapic-vizier-multi-objective-optimization.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fvizier%2Fgapic-vizier-multi-objective-optimization.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vizier/gapic-vizier-multi-objective-optimization.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/vizier/gapic-vizier-multi-objective-optimization.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Agent Platform Vizier<br />
</td>
<td><strong>Get started with Agent Platform Vizier</strong> .<br />
Learn how to use Agent Platform Vizier when training with Gemini Enterprise Agent Platform. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/vizier/overview">Agent Platform Vizier</a> .
<p>Tutorial steps</p>
<ul>
<li>Hyperparameter tuning with Random algorithm.</li>
<li>Hyperparameter tuning with Agent Platform Vizier (Bayesian) algorithm.</li>
<li>Suggesting trials and updating results for Agent Platform Vizier study</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vizier/get_started_vertex_vizier.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fvizier%2Fget_started_vertex_vizier.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/vizier/get_started_vertex_vizier.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/vizier/get_started_vertex_vizier.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Workbench<br />
Vertex AI Training<br />
</td>
<td><strong>Train a multi-class classification model for ads-targeting</strong> .<br />
Learn how to collect data from BigQuery, preprocess it, and train a multi-class classification model on an e-commerce dataset. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction">Gemini Enterprise Agent Platform Workbench</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Vertex AI Training</a> .
<p>Tutorial steps</p>
<ul>
<li>Fetch the required data from BigQuery</li>
<li>Preprocess the data</li>
<li>Train a TensorFlow (&gt;=2.4) classification model</li>
<li>Evaluate the loss for the trained model</li>
<li>Automate the notebook execution using the executor feature</li>
<li>Save the model to a Cloud Storage path</li>
<li>Clean up the created resources</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/ads_targetting/training-multi-class-classification-model-for-ads-targeting-usecase.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fads_targetting%2Ftraining-multi-class-classification-model-for-ads-targeting-usecase.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/ads_targetting/training-multi-class-classification-model-for-ads-targeting-usecase.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/workbench/ads_targetting/training-multi-class-classification-model-for-ads-targeting-usecase.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Workbench<br />
BigQuery ML<br />
</td>
<td><strong>Forecasting retail demand with Gemini Enterprise Agent Platform and BigQuery ML</strong> .<br />
Learn how to build ARIMA (Autoregressive integrated moving average) model from BigQuery ML on retail data Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction">Gemini Enterprise Agent Platform Workbench</a> . Learn more about <a href="https://cloud.google.com/bigquery-ml/docs/managing-models-vertex">BigQuery ML</a> .
<p>Tutorial steps</p>
<ul>
<li>Explore data</li>
<li>Model with BigQuery and the ARIMA model</li>
<li>Evaluate the model</li>
<li>Evaluate the model results using BigQuery ML (on training data)</li>
<li>Evaluate the model results MAE, MAPE, MSE, RMSE (on test data)</li>
<li>Use the executor feature</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/demand_forecasting/forecasting-retail-demand.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fdemand_forecasting%2Fforecasting-retail-demand.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/demand_forecasting/forecasting-retail-demand.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/workbench/demand_forecasting/forecasting-retail-demand.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Workbench<br />
BigQuery ML<br />
</td>
<td><strong>Interactive exploratory analysis of BigQuery data in a notebook</strong> .<br />
Learn about various ways to explore and gain insights from BigQuery data in a Jupyter notebook environment. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/visualize-data-bigquery">Gemini Enterprise Agent Platform Workbench</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/beginner/bqml">BigQuery ML</a> .
<p>Tutorial steps</p>
<ul>
<li>Using Python &amp; SQL to query public data in BigQuery</li>
<li>Exploring the dataset using BigQuery INFORMATION_SCHEMA</li>
<li>Creating interactive elements to help explore interesting parts of the data</li>
<li>Doing some exploratory correlation and time series analysis</li>
<li>Creating static and interactive outputs (data tables and plots) in the notebook</li>
<li>Saving some outputs to Cloud Storage</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/exploratory_data_analysis/explore_data_in_bigquery_with_workbench.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fexploratory_data_analysis%2Fexplore_data_in_bigquery_with_workbench.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/exploratory_data_analysis/explore_data_in_bigquery_with_workbench.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/workbench/exploratory_data_analysis/explore_data_in_bigquery_with_workbench.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Workbench<br />
Custom training<br />
</td>
<td><strong>Build a fraud detection model on Gemini Enterprise Agent Platform</strong> .<br />
This tutorial demonstrates data analysis and model-building using a synthetic financial dataset. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction">Gemini Enterprise Agent Platform Workbench</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Custom training</a> .
<p>Tutorial steps</p>
<ul>
<li>Installation of required libraries</li>
<li>Reading the dataset from a Cloud Storage bucket</li>
<li>Performing exploratory analysis on the dataset</li>
<li>Preprocessing the dataset</li>
<li>Training a random forest model using scikitlearn</li>
<li>Saving the model to a Cloud Storage bucket</li>
<li>Creating a Gemini Enterprise Agent Platform model resource and deploying to an endpoint</li>
<li>Running the WhatIf Tool on test data</li>
<li>Undeploying the model and cleaning up the model resources</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/fraud_detection/fraud-detection-model.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/fraud_detection/fraud-detection-model.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/workbench/fraud_detection/fraud-detection-model.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Workbench<br />
BigQuery ML<br />
</td>
<td><strong>Churn prediction for game developers using Google Analytics 4 and BigQuery ML</strong> .<br />
Learn how to train, evaluate a propensity model in BigQuery ML. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction">Gemini Enterprise Agent Platform Workbench</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/beginner/bqml#machine_learning_directly_in">BigQuery ML</a> .
<p>Tutorial steps</p>
<ul>
<li>Explore the data exported from Google Analytics 4 in BigQuery.</li>
<li>Prepare the training data using demographic, behavioral data, and labels (churn/notchurn).</li>
<li>Train an XGBoost model using BigQuery ML.</li>
<li>Evaluate the model using BigQuery ML.</li>
<li>Use BigQuery ML to predict which users are likely to churn.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/gaming_churn_prediction/churn_prediction_for_game_developers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fgaming_churn_predictionchurn_prediction_for_game_developers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/gaming_churn_prediction/churn_prediction_for_game_developers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/workbench/gaming_churn_prediction/churn_prediction_for_game_developers.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Workbench<br />
Gemini Enterprise Agent Platform training<br />
</td>
<td><strong>Predictive maintenance using Gemini Enterprise Agent Platform</strong> .<br />
Learn how to use the executor feature of Gemini Enterprise Agent Platform Workbench to automate a workflow to train and deploy a model. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction">Gemini Enterprise Agent Platform Workbench</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview">Gemini Enterprise Agent Platform training</a> .
<p>Tutorial steps</p>
<ul>
<li>Loading the required dataset from a Cloud Storage bucket.</li>
<li>Analyzing the fields present in the dataset.</li>
<li>Selecting the required data for the predictive maintenance model.</li>
<li>Training an XGBoost regression model for predicting the remaining useful life.</li>
<li>Evaluating the model.</li>
<li>Running the notebook endtoend as a training job using Executor.</li>
<li>Deploying the model on Gemini Enterprise Agent Platform.</li>
<li>Clean up.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/predictive_maintainance/predictive_maintenance_usecase.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fpredictive_maintainance%2Fpredictive_maintenance_usecase.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/predictive_maintainance/predictive_maintenance_usecase.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/workbench/predictive_maintainance/predictive_maintenance_usecase.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Workbench<br />
BigQuery ML<br />
</td>
<td><strong>Analysis of pricing optimization on CDM Pricing Data</strong> .<br />
The objective of this notebook is to build a pricing optimization model using BigQuery ML. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction">Gemini Enterprise Agent Platform Workbench</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/beginner/bqml#machine_learning_directly_in">BigQuery ML</a> .
<p>Tutorial steps</p>
<ul>
<li>Load the required dataset from a Cloud Storage bucket.</li>
<li>Analyze the fields present in the dataset.</li>
<li>Process the data to build a model.</li>
<li>Build a BigQuery ML forecast model on the processed data.</li>
<li>Get forecasted values from the BigQuery ML model.</li>
<li>Interpret the forecasts to identify the best prices.</li>
<li>Clean up.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/pricing_optimization/pricing-optimization.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fpricing_optimization%2Fpricing-optimization.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/pricing_optimization/pricing-optimization.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/workbench/pricing_optimization/pricing-optimization.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="odd">
<td>Gemini Enterprise Agent Platform Workbench<br />
Dataproc Serverless for Spark<br />
</td>
<td><strong>Digest and analyze data from BigQuery with Dataproc</strong> .<br />
This notebook tutorial runs an Apache Spark job that fetches data from the BigQuery "GitHub Activity Data" dataset, queries the data, and then writes the results back to BigQuery. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction">Gemini Enterprise Agent Platform Workbench</a> . Learn more about <a href="https://cloud.google.com/dataproc-serverless/docs/guides/bigquery-connector-spark-example">Dataproc Serverless for Spark</a> .
<p>Tutorial steps</p>
<ul>
<li>Setting up a Google Cloud project and Dataproc cluster.</li>
<li>Configuring the sparkbigqueryconnector.</li>
<li>Ingesting data from BigQuery into a Spark DataFrame.</li>
<li>Preprocessing ingested data.</li>
<li>Querying the most frequently used programming language in monoglot repos.</li>
<li>Querying the average size (MB) of code in each language stored in monoglot repos.</li>
<li>Querying the languages files most frequently found together in polyglot repos.</li>
<li>Writing the query results back into BigQuery.</li>
<li>Deleting the resources created for this notebook tutorial.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/spark/spark_bigquery.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fspark%2Fspark_bigquery.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/spark/spark_bigquery.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/workbench/spark/spark_bigquery.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
<tr class="even">
<td>Gemini Enterprise Agent Platform Workbench<br />
Dataproc<br />
</td>
<td><strong>SparkML with Dataproc and BigQuery</strong> .<br />
This tutorial runs an Apache SparkML job that fetches data from the BigQuery dataset, performs exploratory data analysis, cleans the data, executes feature engineering, trains the model, evaluates the model, outputs results, and saves the model to a Cloud Storage bucket. Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction">Gemini Enterprise Agent Platform Workbench</a> . Learn more about <a href="https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/dataproc-component">Dataproc</a> .
<p>Tutorial steps</p>
<ul>
<li>Sets up a Google Cloud project and Dataproc cluster.</li>
<li>Creates a Cloud Storage bucket and a BigQuery dataset.</li>
<li>Configures the sparkbigqueryconnector.</li>
<li>Ingests BigQuery data into a Spark DataFrame.</li>
<li>Performa Exploratory Data Analysis (EDA).</li>
<li>Visualizes the data with samples.</li>
<li>Cleans the data.</li>
<li>Selects features.</li>
<li>Trains the model.</li>
<li>Outputs results.</li>
<li>Saves the model to a Cloud Storage bucket.</li>
<li>Deletes the resources created for the tutorial.</li>
</ul></td>
<td><a href="https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/spark/spark_ml.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png" width="24" height="24" alt="Colab logo" /> Colab</a><br />
<a href="https://console.cloud.google.com/agent-platform/colab/import/https:%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fworkbench%2Fspark%2Fspark_ml.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png" width="24" height="24" alt="Colab Enterprise logo" /> Colab Enterprise</a><br />
<a href="https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/spark/spark_ml.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png" width="24" height="24" alt="GitHub logo" /> GitHub</a><br />
<a href="https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https://raw.githubusercontent.com/GoogleCloudPlatform/vertex-ai-samples/main/notebooks/official/workbench/spark/spark_ml.ipynb"><img src="https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png" width="24" height="24" alt="Gemini Enterprise Agent Platform Workbench logo" /> Gemini Enterprise Agent Platform Workbench</a><br />
</td>
</tr>
</tbody>
</table>
