---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/rerun-pipeline-task
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/rerun-pipeline-task
title: Rerun a pipeline
description: Rerun a completed, failed, or cancelled pipeline with updated task-level or job-level parameters.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can rerun specific tasks from a completed, cancelled, or failed machine learning (ML) pipeline runs. When you initiate a rerun, you can modify task-level configurations, or choose to skip tasks, and then create a run based on the updated configuration. The new pipeline run maintains a reference to the original pipeline run for traceability. If a task succeeded in a prior run, Gemini Enterprise Agent Platform Pipelines reuses the cached outcomes for that task. Otherwise, if the step had failed, Agent Platform Pipelines runs the step during the pipeline rerun.

This lets you efficiently address ML pipeline failures by making adjustments to your ML pipeline without restarting the entire ML pipeline. You can adjust a failed task, compare outcomes with different sets of parameters, or skip a non-essential task that's failing.

Rerunning a pipeline is useful for MLOps practitioners managing complex ML pipelines in production. Examples of scenarios where it's useful include the following:

  - **Handling partial failures in parallel processes** : When one part of a large parallel process fails, you can skip the failed task and let the remainder of the pipeline run continue. For example, if a data pipeline for one out of 100 tasks fails, you can skip it.

  - **Rerunning a task with updated input data** : If a single task needs to be rerun with updated data, you can rerun that specific task.

  - **Debugging production issues without requiring code changes** : Rerun a specific task and all the tasks that depend on it without involving the author of the pipeline code.

## Rerun a pipeline

To rerun a pipeline, use the Agent Platform SDK for Python.

### Python

Use the following sample to rerun a pipeline by skipping a failed task and rerunning another task with updated parameters by using the `PipelineJob.rerun()` method:

    from google.cloud import aiplatform
    from google.cloud.aiplatform.preview.pipelinejob.pipeline_jobs import (
      _PipelineJob as PipelineJob
    )
    from google.cloud.aiplatform_v1beta1.types.ui_pipeline_spec import RuntimeArtifact
    from google.protobuf.struct_pb2 import Value
    from google.cloud.aiplatform_v1beta1.types import PipelineTaskRerunConfig
    aiplatform.init(project="PROJECT_ID", location="LOCATION")
    job = aiplatform.PipelineJob.get(resource_name="PIPELINE_RUN_RESOURCE_NAME")
    original_job_name = job.resource_name
    rerun_task_id = None
    skip_failed_task_id = None
    task_inputs_override = PipelineTaskRerunConfig.Inputs(
        parameter_values={
          "TASK_PARAMETER_1": Value(TASK_PARAMETER_1_VALUE),
          "TASK_PARAMETER_2": Value(TASK_PARAMETER_2_VALUE)
        }
    )
    for task in job.task_details:
        if task.task_name == RERUN_TASK_NAME:
            rerun_task_id = task.task_id
        if task.task_name == SKIP_FAILED_TASK_NAME:
            skip_failed_task_id = task.task_id
    pipeline_job.rerun(original_pipelinejob_name=original_job_name,
      pipeline_task_rerun_configs=[
        PipelineTaskRerunConfig(task_id = rerun_task_id,
          skip_task = False,
          inputs = PipelineTaskRerunConfig.Inputs(task_inputs_override)
        ),
        PipelineTaskRerunConfig(task_id = skip_failed_task_id,
          skip_task = True
        )
      ],
      parameter_values=PIPELINE_PARAMETER_VALUES,
      job_id=RERUN_PIPELINE_JOB_ID)

Replace the following:

  - PROJECT\_ID : The Google Cloud project containing the pipeline run.

  - LOCATION : The region where the pipeline run is located. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .

  - PIPELINE\_RUN\_RESOURCE\_NAME : The fully qualified resource name of the completed, failed, or cancelled pipeline run that you want to rerun. Enter the resource name in the format ` projects/ PROJECT_NUMBER /locations/ LOCATION /pipelineJobs/ PIPELINE_RUN_ID  ` , where:
    
      - PROJECT\_NUMBER : The project number for your project. You can locate this project number in the Google Cloud console. For more information, see [Find the project name, number, and ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
      - PIPELINE\_RUN\_ID with the unique ID of the pipeline run that you want to rerun. The ID is displayed in the **Runs** tab on the **Pipelines** page in the Google Cloud console.

  - RERUN\_TASK\_NAME : The name of the task to rerun with updated parameters.

  - SKIP\_FAILED\_TASK\_NAME : The name of the failed task to skip during the rerun.

  - TASK\_PARAMETER\_1 and TASK\_PARAMETER\_2 : The names of the parameters for the task that you want to override in the pipeline rerun.

  - TASK\_PARAMETER\_1\_VALUE and TASK\_PARAMETER\_2\_VALUE : The new values of TASK\_PARAMETER\_1 and TASK\_PARAMETER\_2 respectively in the pipeline rerun.

  - PIPELINE\_PARAMETER\_VALUES : Optional. The updated pipeline run-level parameter values to use for the pipeline rerun.

  - RERUN\_PIPELINE\_JOB\_ID : Optional. A unique ID to assign to the new pipeline rerun job.
