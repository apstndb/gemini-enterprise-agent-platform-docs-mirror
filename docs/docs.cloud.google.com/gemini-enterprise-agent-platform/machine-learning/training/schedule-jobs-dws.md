---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/schedule-jobs-dws
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/schedule-jobs-dws
title: Schedule training jobs based on resource availability
description: Use Dynamic Workload Scheduler to schedule Gemini Enterprise Agent Platform serverless training jobs based on GPU resource availability.
data_source: docs.cloud.google.com
---

For Gemini Enterprise Agent Platform serverless training jobs that request GPU resources, Dynamic Workload Scheduler lets you schedule the jobs based on when the requested GPU resources become available. This page shows you how to schedule serverless training jobs by using Dynamic Workload Scheduler, and how to customize the scheduling behavior on Gemini Enterprise Agent Platform.

## Recommended use cases

We recommend using Dynamic Workload Scheduler to schedule serverless training jobs in the following situations:

  - The serverless training job requests L4, A100, H100, H200, or B200 GPUs and you want to run the job as soon as the requested resources become available. For example, when Gemini Enterprise Agent Platform allocates the GPU resources outside of peak hours.
  - Your workload requires multiple nodes and can't start running until all GPU nodes are provisioned and ready at the same time. For example, you're creating a distributed training job.

## Requirements

To use Dynamic Workload Scheduler, your serverless training job must meet the following requirements:

  - Your serverless training job requests L4, A100, H100, H200, or B200 GPUs.
  - Your serverless training job has a maximum `timeout` of 7 days or less.
  - Your serverless training job uses the same machine configuration for all worker pools.

### Supported job types

All serverless training job types are supported, including `CustomJob` , `HyperparameterTuningjob` , and `TrainingPipeline` .

## Enable Dynamic Workload Scheduler in your serverless training job

To enable Dynamic Workload Scheduler in your serverless training job, set the `scheduling.strategy` API field to `FLEX_START` when you create the job.

For details on how to create a serverless training job, see the following links.

  - [Create a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job)
  - [Create a `HyperparameterTuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview)
  - [Create a `TrainingPipeline`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline)

### Configure the duration to wait for resource availability

You can configure how long your job can wait for resources in the `scheduling.maxWaitDuration` field. A value of `0` means that the job waits indefinitely until the requested resources become available. The default value is **1 day** .

### Examples

The following examples show you how to enable Dynamic Workload Scheduler for a `customJob` . Select the tab for the interface that you want to use.

### gcloud

When submitting a job using the Google Cloud CLI, add the `scheduling.strategy` field in the [`config.yaml`](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/create#--config) file.

Example YAML configuration file:

    workerPoolSpecs:
      machineSpec:
        machineType: a2-highgpu-1g
        acceleratorType: NVIDIA_TESLA_A100
        acceleratorCount: 1
      replicaCount: 1
      containerSpec:
        imageUri: gcr.io/ucaip-test/ucaip-training-test
        args:
        - port=8500
        command:
        - start
    scheduling:
      strategy: FLEX_START
      maxWaitDuration: 7200s

### Python

When submitting a job using the Agent Platform SDK for Python, set the `scheduling_strategy` field in the relevant `CustomJob` creation method.

    from google.cloud.aiplatform_v1.types import custom_job as gca_custom_job_compat
    
    def create_custom_job_with_dws_sample(
        project: str,
        location: str,
        staging_bucket: str,
        display_name: str,
        script_path: str,
        container_uri: str,
        service_account: str,
        experiment: str,
        experiment_run: Optional[str] = None,
    ) -> None:
        aiplatform.init(project=project, location=location, staging_bucket=staging_bucket, experiment=experiment)
    
        job = aiplatform.CustomJob.from_local_script(
            display_name=display_name,
            script_path=script_path,
            container_uri=container_uri,
            enable_autolog=True,
            machine_type="a2-highgpu-1g",
            accelerator_type="NVIDIA_TESLA_A100",
            accelerator_count=1,
        )
    
        job.run(
            service_account=service_account,
            experiment=experiment,
            experiment_run=experiment_run,
            max_wait_duration=1800,
            scheduling_strategy=gca_custom_job_compat.Scheduling.Strategy.FLEX_START
        )

### REST

When submitting a job using the Gemini Enterprise Agent Platform REST API, set the fields `scheduling.strategy` and `scheduling.maxWaitDuration` when creating your serverless training job.

Example request JSON body:

    {
      "displayName": "MyDwsJob",
      "jobSpec": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": "a2-highgpu-1g",
              "acceleratorType": "NVIDIA_TESLA_A100",
              "acceleratorCount": 1
            },
            "replicaCount": 1,
            "diskSpec": {
              "bootDiskType": "pd-ssd",
              "bootDiskSizeGb": 100
            },
            "containerSpec": {
              "imageUri": "python:3.10",
              "command": [
                "sleep"
              ],
              "args": [
                "100"
              ]
            }
          }
        ],
        "scheduling": {
          "maxWaitDuration": "1800s",
          "strategy": "FLEX_START"
        }
      }
    }

## Quota

When you submit a job using Dynamic Workload Scheduler, instead of consuming on-demand Gemini Enterprise Agent Platform quota, Gemini Enterprise Agent Platform consumes *preemptible* quota. For example, for Nvidia H100 GPUs, instead of consuming:

`aiplatform.googleapis.com/custom_model_training_nvidia_h100_gpus` ,

Gemini Enterprise Agent Platform consumes:

`aiplatform.googleapis.com/custom_model_training_preemptible_nvidia_h100_gpus` .

However, *preemptible* quota is used only in name. Your resources aren't preemptible and behave like standard resources.

Before submitting a job using Dynamic Workload Scheduler, ensure that your preemptible quotas have been increased to a sufficient amount. For details on Gemini Enterprise Agent Platform quotas and instructions for making quota increase requests, see [Gemini Enterprise Agent Platform quotas and limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas) .

## Billing

When using DWS flex start, you're billed according to [Dynamic Workload Scheduler pricing](https://cloud.google.com/products/dws/pricing) . There are serverless training management fees in addition to your infrastructure usage.

## What's Next

  - Learn more about [configuring compute resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) for serverless training jobs.
  - Learn more about [using distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) for serverless training jobs.
  - Learn more about [other scheduling options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#scheduling) .
