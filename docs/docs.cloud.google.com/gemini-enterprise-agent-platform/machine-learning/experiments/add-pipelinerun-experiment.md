---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/add-pipelinerun-experiment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/add-pipelinerun-experiment
title: Add pipeline run to experiment
description: To add a pipeline run to an experiment or an experiment run, you can use either the {{dynamic_data.site_values.cloud_name_short}} console or the Agent Platform SDK for Python.
data_source: docs.cloud.google.com
---

You can use either the Google Cloud console or the Agent Platform SDK for Python to add a pipeline run to either an experiment or an experiment run .

### Google Cloud console

Use the following instructions to run an ML pipeline and associate the pipeline with an experiment and, optionally, an experiment run using Google Cloud console. Experiment runs can only be created through the Agent Platform SDK for Python (see [Create and manage experiment runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/create-manage-exp-run#vertex-ai-sdk-for-python) ).

In the Google Cloud console, in the Agent Platform section, go to the **Pipelines** page.  

In the **Region** drop-down list, select the region that you want to create a pipeline run in.

Click **add\_box Create run** to open the **Create pipeline run** pane.

Specify the following **Run** details.

  - In the **File** field, click **Choose** to open the file selector. Navigate to the compiled pipeline JSON file that you want to run, select the pipeline, and click **Open** .
  - The **Pipeline name** defaults to the name that you specified in the pipeline definition. Optionally, specify a different **Pipeline name** .
  - Specify a **Run name** to uniquely identify this pipeline run.

To specify that this pipeline run uses a custom service account, a customer-managed encryption key, or a peered VPC network, click **Advanced options** (Optional).  
Use the following instructions to configure advanced options such as a custom service account.

  - To specify a service account , select a service account from the **Service account** drop-down list.  
    If you do not specify a service account, Agent Platform Pipelines runs your pipeline using the default Compute Engine service account.  
    Learn more about [configuring a service account for use with Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-project#service-account) .
  - To use a customer managed encryption key (CMEK), select **Use a customer-managed encryption key** . The **Select a customer-managed key** drop-down list appears. In the **Select a customer-managed key** drop-down list, select the key that you want to use.
  - To use a peered VPC network in this pipeline run, enter the VPC network name in the **Peered VPC network** box.

Click **Continue** .  
The **Cloud Storage** location and **Pipeline parameters** pane appears.

  - Required: Enter the Cloud Storage output directory, for example: gs:// *location\_of\_directory* .
  - Optional: Specify the parameters that you want to use for this pipeline run.

Click **Submit** to create your pipeline run.

After the Pipeline is submitted, it appears in the Pipeline's Google Cloud console table.

In the row associated with your pipeline click more\_vert **View more \> Add to Experiment**

  - Select an existing Experiment or create a new one.
  - Optional: If Experiment runs are associated with the Experiment, they show up in the drop-down. Select an existing Experiment run.

Click **Save** .

#### Compare a pipeline run with experiment runs using the Google Cloud console

1.  In the Google Cloud console, go to the **Experiments** page.  
    .  
    A list of experiments appears in the **Experiments** page.
2.  Select the experiment you want to add your pipeline run to.  
    A list of runs appears.
3.  Select the runs you want to compare, then click **Compare**  
4.  Click the **Add run** button. A list of runs appears
5.  Select the pipeline run you want to add. The run is added.

### Agent Platform SDK for Python {:\#sdk-add-pipeline-run}

The following samples use the [PipelineJob](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob) API.

### Associate pipeline run with an experiment

This sample shows how to associate a pipeline run with an experiment. When you want to compare Pipeline runs, you should associate your pipeline run(s) to an experiment. See [`init`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_init) in the Agent Platform SDK for Python reference documentation.

### Python

    from typing import Any, Dict, Optional
    
    from google.cloud import aiplatform
    
    
    def log_pipeline_job_to_experiment_sample(
        experiment_name: str,
        pipeline_job_display_name: str,
        template_path: str,
        pipeline_root: str,
        project: str,
        location: str,
        parameter_values: Optional[Dict[str, Any]] = None,
    ):
        aiplatform.init(project=project, location=location)
    
        pipeline_job = aiplatform.PipelineJob(
            display_name=pipeline_job_display_name,
            template_path=template_path,
            pipeline_root=pipeline_root,
            parameter_values=parameter_values,
        )
    
        pipeline_job.submit(experiment=experiment_name)

  - `experiment_name` : Provide a name for your experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `pipeline_job_display_name` : The user-defined name of this Pipeline.
  - `template_path` : The path of PipelineJob or PipelineSpec JSON or YAML file. It can be a local path or a Cloud Storage URI. Example: "gs://project.name"
  - `pipeline_root` : The root of the pipeline outputs. Default to be staging bucket.
  - `parameter_values` : The mapping from runtime parameter names to its values that control the pipeline run.
  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations) .

### Associate pipeline run with experiment run

The sample provided includes associating a pipeline run with an experiment run .

Use cases:

  - When doing local model training and then running evaluation on that model (evaluation is done by using a pipeline). In this case you'd want to write the eval metrics from your pipeline run to an ExperimentRun
  - When re-running the same pipeline multiple times. For example, if you change the input parameters, or if one component fails and you need to run it again.

When associating a pipeline run to an experiment run, parameters and metrics are not automatically surfaced and need to be logged manually using the [logging APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data) .

Note: When the optional `resume` parameter is specified as `TRUE` , the previously started run resumes. When not specified, `resume` defaults to `FALSE` and a new run is created.

See [`init`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_init) , [`start_run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatformm#google_cloud_aiplatform_start_run) , and [`log`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_log) in the Agent Platform SDK for Python reference documentation.

### Python

    from google.cloud import aiplatform
    
    
    def log_pipeline_job_sample(
        experiment_name: str,
        run_name: str,
        pipeline_job: aiplatform.PipelineJob,
        project: str,
        location: str,
    ):
        aiplatform.init(experiment=experiment_name, project=project, location=location)
    
        aiplatform.start_run(run=run_name, resume=True)
    
        aiplatform.log(pipeline_job=pipeline_job)

  - `experiment_name` : Provide a name for your experiment. You can find your list of experiments in the Google Cloud console by selecting **Experiments** in the section nav.
  - `run_name` : Specify a run name.
  - `pipeline_job` : An Agent Platform PipelineJob
  - `project` : . You can find these in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.
  - `location` : See [List of available locations](https://docs.cloud.google.com/vertex-ai/docs/general/locations)

## View list of pipeline runs in Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Pipelines** page.

2.  Check to be sure you are in the correct project.

3.  A list of experiments and runs associated with your project's pipeline runs appears in the **Experiment** and **Experiment run** columns, respectively.  

![Agent PlatformList of experiments](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/pipeline-exp-run.png)

## Codelab

  - [Make the Most of Experimentation: Manage Machine Learning Experiments with Agent Platform](https://codelabs.developers.google.com/vertex_experiments_pipelines_intro#0)
    
    This codelab involves using Gemini Enterprise Agent Platform to build a pipeline that trains a custom Keras Model in TensorFlow. Vertex AI Experiments is used to track and compare experiment runs in order to identify which combination of hyperparameters results in the best performance.

## What's next

  - [Log data to an experiment run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data)

## Relevant notebook sample

  - [Compare pipeline runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-pipeline-runs)
