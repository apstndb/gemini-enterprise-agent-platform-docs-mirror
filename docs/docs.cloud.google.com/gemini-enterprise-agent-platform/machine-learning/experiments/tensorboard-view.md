---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-view
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-view
title: View Vertex AI TensorBoard data
description: Use the Vertex AI TensorBoard web app to visualize logs and use the {{dynamic_data.site_values.cloud_name_short}} console to access web app visualizations.
data_source: docs.cloud.google.com
---

The Vertex AI TensorBoard web app provides a visualization of logs associated with a Vertex AI TensorBoard experiment. This web application offers several tools and dashboards to visualize and compare data across experiment runs, and to [profile model training performance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler) .

    Note: If you are having trouble viewing results, make sure your user account
    has the [Agent Platform Viewer](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.viewer) (or higher) role associated with it.

![TensorBoard view appear](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/tb-view-appears.png)

To learn more about each dashboard, see the [README](https://github.com/tensorflow/tensorboard/blob/master/README.md#the-visualizations) for "The Visualization".

## Access a Vertex AI TensorBoard web app

The Vertex AI TensorBoard web app is accessed using the following address format:

` https:// REGION .tensorboard.googleusercontent.com/experiment/projects+ PROJECT_NAME_OR_ID +locations+ REGION +tensorboards+ TENSORBOARD_ID +experiments+ EXPERIMENT_NAME  `

  - `  REGION  ` : the region your TensorBoard is located in
  - `  PROJECT_ID  ` : the project your TensorBoard was created in
  - `  TENSORBOARD_ID  ` : the [TensorBoard ID](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-setup#tensorboard_id)
  - `  EXPERIMENT_NAME  ` : the name of the TensorBoard experiment

This link can be shared and used by anyone who has permission.

You can navigate here directly by inserting the appropriate values, or by following a link available in the following ways.

### gcloud CLI and Agent Platform SDK for Python

When creating or uploading logs to a Vertex AI TensorBoard, the gcloud CLI and SDK output a link to the Vertex AI TensorBoard instance.

### Google Cloud console

You can access the TensorBoard web app using the Google Cloud console.

### Experiments

If your Vertex AI TensorBoard is associated with a Gemini Enterprise Agent Platform Experiment, which is automatic when a [default instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-setup#use_default_instance) is involved, you can access the TensorBoard web app directly from the Experiments page. ![tensorboard view](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/experiments-tb-view.png)

### Custom training

If you used Vertex AI TensorBoard with [custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-training) you can access the TensorBoard web app directly from the custom training job.

1.  In the Gemini Enterprise Agent Platform section of the Google Cloud console, go to the **Training** page.
2.  Click **Custom Jobs** tab.
3.  Select your training job from the list of training runs. The details page appears
4.  Click the **Open TensorBoard** button.  
    ![open tensorboard button](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/custom-job-link.png)

### Gemini Enterprise Agent Platform Pipelines

If you used Vertex AI TensorBoard with [Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-with-pipelines) , the TensorBoard web app can be accessed directly from the component information display.

1.  In the Gemini Enterprise Agent Platform section of the Google Cloud console, go to the **Pipelines** page.
2.  From the pipelines tab, scroll or filter the pipeline list to find your pipeline.
3.  On the pipeline display select the component where TensorBoard metrics are captured, typically the training component.
4.  Select the **Open TensorBoard** button in the upper right.  
    ![tensorboard view for classification](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/image-classification-pipeline.png)

## Visualize Vertex AI TensorBoard metrics in the Google Cloud console

If your TensorBoard instance is associated with a Vertex AI Experiments, which is automatic when using a [default TensorBoard instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-setup#use_default_instance) , certain metrics can be visualized directly in the Google Cloud console, without using the web application.

The [Compare and analyze runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/compare-analyze-runs#console-compare-analyze-runs) document describes how to view details of your experiment runs and compare the experiment runs to each other in the Google Cloud console. TensorBoard timeseries metrics appear under the **Charts** tab in the navigation bar of the Gemini Enterprise Agent Platform Experiments console.

![Agent Platform navigation bar with timeseries data charts](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/compare-runs-single-run-details.png)
