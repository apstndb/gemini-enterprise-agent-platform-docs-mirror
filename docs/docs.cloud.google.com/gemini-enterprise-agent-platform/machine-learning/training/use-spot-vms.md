---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-spot-vms
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-spot-vms
title: Use Spot VMs with training
description: Use Spot VMs with with Gemini Enterprise Agent Platform serverless training.
data_source: docs.cloud.google.com
---

## Overview

You can reduce the cost of running your serverless training jobs by using Spot VMs. Spot VMs are virtual machine (VM) instances that are excess Compute Engine capacity. Spot VMs have significant discounts, but Compute Engine might preemptively stop or delete (preempt) Spot VMs to reclaim the capacity at any time.

To learn more, see [Spot VMs](https://docs.cloud.google.com/compute/docs/instances/spot) .

## Limitations and requirements

Consider the following limitations and requirements when using Spot VMs with Agent Platform:

  - All [Spot VMs limitations](https://docs.cloud.google.com/compute/docs/instances/spot#limitations) apply when using Spot VMs with Agent Platform.
  - Using Spot VMs with Agent Platform is supported only for serverless training and inference.
  - Using Spot VMs with TPU Pods isn't supported.
  - Submitting your job through the Google Cloud console is not supported.

## Billing

If your workloads are fault-tolerant and can withstand possible VM preemption, Spot VMs can reduce your compute costs significantly. If some of your VMs stop during processing, the job slows but does not completely stop. Spot VMs complete your batch processing tasks without placing additional load on your existing VMs and without requiring you to pay full price for additional standard VMs. See [Preemption handling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-spot-vms#preemption-handling) .

When you use Spot VMs, you're billed by job duration and machine type. You don't pay for the time that the job is in a queue or preempted.

## Preemption handling

Spot VMs can be reclaimed by Compute Engine at any time. Therefore, your serverless training job must be fault tolerant to get the most benefit from Spot VMs. When Spot VMs are preempted, the serverless training job fails with a `STOCKOUT` error and Compute Engine tries to restart the job up to six times. To learn how to get the most out of your Spot VMs, see [Spot VM best practices](https://docs.cloud.google.com/compute/docs/instances/create-use-spot#best-practices) .

The following are some of the methods that you can use to make your serverless training job fault tolerant:

  - Create checkpoints to save progress. By periodically storing the progress of your model, you can ensure that a terminated serverless training job can resume from the last stored checkpoint, instead of starting over from the beginning.
  - Use Elastic Horovod. Elastic training enables Horovod to scale your compute resources without requiring a restart or resuming from checkpoints. To learn more, see [Elastic Horovod](https://horovod.readthedocs.io/en/latest/elastic_include.html) .
  - Use a shutdown script. When Compute Engine preempts a Spot VM, you can use a [shutdown script](https://docs.cloud.google.com/compute/docs/shutdownscript) that tries to perform cleanup actions before the VM is preempted. To learn more, see [Handle preemption with a shutdown script](https://docs.cloud.google.com/compute/docs/instances/create-use-spot#handle-preemption) .

## Before you begin

Prepare your serverless training application:

  - To use a prebuilt container, see [Create a Python training application for a prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) .
  - To use a custom container, see [Create a custom container image for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .

## Configure your training job to use Spot VMs

You can configure your serverless training job to use Spot VMs by specifying a `SPOT` strategy in your scheduling configuration.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the container or Python package will be run.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - JOB\_NAME : Required. A display name for the `CustomJob` .
  - Define the custom training job:
      - MACHINE\_TYPE : The type of the machine. Refer to [available machine types for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) .
      - REPLICA\_COUNT : The number of worker replicas to use. In most cases, set this to `1` for your [first worker pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#configure_distributed_training) .
      - If your training application runs in a custom container, specify the following:
          - CUSTOM\_CONTAINER\_IMAGE\_URI : the URI of a Docker container image with your training code. Learn how to [create a custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .
          - CUSTOM\_CONTAINER\_COMMAND : Optional. The command to be invoked when the container is started. This command overrides the container's default entrypoint.
          - CUSTOM\_CONTAINER\_ARGS : Optional. The arguments to be passed when starting the container.
      - If your training application is a Python package that runs in a prebuilt container, specify the following:
          - EXECUTOR\_IMAGE\_URI : The URI of the container image that runs the provided code. Refer to the [available prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) .
          - PYTHON\_PACKAGE\_URIS : Comma-separated list of Cloud Storage URIs specifying the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100.
          - PYTHON\_MODULE : The Python module name to run after installing the packages.
          - PYTHON\_PACKAGE\_ARGS : Optional. Command-line arguments to be passed to the Python module.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs

Request JSON body:

    {
      "displayName": "JOB_NAME",
      "jobSpec": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": "MACHINE_TYPE"
              }
            },
            "replicaCount": REPLICA_COUNT,
    
            // Union field task can be only one of the following:
            "containerSpec": {
              "imageUri": CUSTOM_CONTAINER_IMAGE_URI,
              "command": [
                CUSTOM_CONTAINER_COMMAND
              ],
              "args": [
                CUSTOM_CONTAINER_ARGS
              ]
            },
            "pythonPackageSpec": {
              "executorImageUri": EXECUTOR_IMAGE_URI,
              "packageUris": [
                PYTHON_PACKAGE_URIS
              ],
              "pythonModule": PYTHON_MODULE,
              "args": [
                PYTHON_PACKAGE_ARGS
              ]
            }
            // End of list of possible types for union field task.
          }
          // Specify one workerPoolSpec for single replica training, or multiple workerPoolSpecs
          // for distributed training.
        ],
        "scheduling": {
          "strategy": "SPOT"
        }
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs" | Select-Object -Expand Content

The response contains information about specifications as well as the JOB\_ID .

#### Response

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/customJobs/JOB_ID",
      "displayName": "JOB_NAME",
      "trainingTaskInputs": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": "MACHINE_TYPE"
            },
            "replicaCount": "1",
            "pythonPackageSpec": {
              "executorImageUri": "us-docker.pkg.dev/vertex-ai/training/training-tf-cpu.2-1:latest",
              "packageUris": [
                "gs://BUCKET_NAME/training/hello-custom-training-1.0.tar.gz"
              ],
              "pythonModule": "trainer.task",
              "args": [
                "--model-dir=gs://BUCKET_NAME/output/"
              ]
            }
          }
        ]
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "2020-09-15T19:09:54.342080Z",
      "startTime": "2020-09-15T19:13:42.991045Z",
    }

### Python

To learn how to install or update the Agent Platform SDK for Python, see [Install the Agent Platform SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/install-sdk) . For more information, see the [Agent Platform SDK for Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

```python
customJob = aiplatform.CustomJob(
    display_name=TEST_CASE_NAME,
    worker_pool_specs=worker_pool_spec,
    staging_bucket=OUTPUT_DIRECTORY
)
customJob.run(
    scheduling_strategy=aiplatform.compat.types.custom_job.Scheduling.Strategy.SPOT
)
```

## What's next

  - Learn more about [Spot VMs](https://docs.cloud.google.com/compute/docs/instances/spot) .
  - To learn more about Compute Engine VMs in general, read the [Virtual machine instances](https://docs.cloud.google.com/compute/docs/instances) documentation.
  - To learn how to create Spot VMs, read [Create and use Spot VMs](https://docs.cloud.google.com/compute/docs/instances/create-use-spot) .
  - [Use Spot VMs with Vertex AI Inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-spot-vms) .
