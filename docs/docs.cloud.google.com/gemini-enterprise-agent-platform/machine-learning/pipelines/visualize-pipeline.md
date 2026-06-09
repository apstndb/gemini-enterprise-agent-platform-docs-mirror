---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/visualize-pipeline
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/visualize-pipeline
title: Visualize and analyze pipeline results
description: Visualize and interpret your ML pipeline runs in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

> To learn more, run the "Build Pipelines that generate model metrics and visualizations, and compare pipeline runs" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/metrics_viz_run_compare_kfp.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fmetrics_viz_run_compare_kfp.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Fmetrics_viz_run_compare_kfp.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/metrics_viz_run_compare_kfp.ipynb)

Agent Platform Pipelines lets you run machine learning (ML) pipelines that were built using the Kubeflow Pipelines SDK or TensorFlow Extended in a serverless manner. This document describes how to use Agent Platform Pipelines to visualize, analyze, and compare pipeline runs.

To learn more about running and scheduling pipelines, read the guide to [running a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline) .

## Visualize pipeline runs using Google Cloud console

Use the following instructions to learn more about using Google Cloud console to visualize pipeline runs.

1.  Open Agent Platform Pipelines in Google Cloud console.

2.  In **Select a recent project** , click a project tile.

3.  Click the run name of the pipeline run that you want to analyze.
    
    The pipeline run page appears and displays the pipeline's runtime graph. The pipeline's summary appears in the **Pipeline run analysis** pane.
    
      - The pipeline graph shows the workflow steps in the pipeline.
      - The pipeline summary shows the basic information about the pipeline run and the parameters that were used in this pipeline run.

4.  To learn more about a pipeline step or artifact, click the step or artifact in the runtime graph.
    
    The **Pipeline run analysis** pane shows information about this pipeline step or artifact.
    
      - For pipeline steps, this information includes execution details, the input parameters that were passed to the step, and any output parameters that the step passed to the pipeline.
        
        To learn more about the selected pipeline step:
        
          - Click **View job** to see the job details.
            
            The job details page includes information like the machine type used to run this step, the container image that the step runs in, and the encryption key used by this step.
        
          - Click **View logs** to see the logs produced by this pipeline step.
            
            The logs pane appears. Use the logs to help debug the behavior of your pipeline.
    
      - For artifacts, this information includes the data type of the artifact, the location where the artifact is stored, and the artifact's metrics.
        
        To learn more about the selected artifact:
        
          - Click the artifact's **URI** to open that location in Cloud Storage.
        
          - Click **Open in ML Metadata** to view the lineage of the artifact in Vertex ML Metadata. For more information about pipeline artifact lineage, see [Track the lineage of pipeline artifacts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/lineage) . If you're new to Vertex ML Metadata, read the [introduction to Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction) .

## Compare pipeline runs using Google Cloud console

Use the following instructions to compare pipeline runs in Google Cloud console.

1.  Open Agent Platform Pipelines in Google Cloud console.

2.  Select the checkboxes of the pipeline runs that you want to compare.

3.  In the Agent Platform Pipelines menubar, click **compare\_arrows Compare** .
    
    The **Compare runs** pane appears.

4.  The **Compare runs** pane lists your pipeline's parameters and metrics.
    
    This information helps you to perform analysis, such as analyzing how different sets of hyperparameters affect a model's metrics.

## What's next

  - Read the [introduction to Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction) to learn more about orchestrating ML workflows.
  - Learn how to [build a machine learning pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline) .
