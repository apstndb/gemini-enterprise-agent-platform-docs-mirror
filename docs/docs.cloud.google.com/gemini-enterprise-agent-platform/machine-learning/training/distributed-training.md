---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training
title: Distributed training
description: Run distributed training jobs on Agent Platform.
data_source: docs.cloud.google.com
---

[Video](https://www.youtube.com/watch?v=rAGauhXYgw4)

This page describes how to run distributed training jobs on Agent Platform.

## Code requirements

Use an ML framework that supports distributed training. In your training code, you can use the [`CLUSTER_SPEC` or `TF_CONFIG` environment variables](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training#cluster-variables) to reference specific parts of your training cluster.

## Structure of the training cluster

If you run a distributed training job with Agent Platform, you specify multiple machines (nodes) in a *training cluster* . The training service allocates the resources for the machine types you specify. Your running job on a given node is called a *replica* . A group of replicas with the same configuration is called a *worker pool* .

Each replica in the training cluster is given a single role or task in distributed training. For example:

  - **Primary replica** : Exactly one replica is designated the *primary replica* . This task manages the others and reports status for the job as a whole.

  - **Worker(s)** : One or more replicas may be designated as *workers* . These replicas do their portion of the work as you designate in your job configuration.

  - **Parameter server(s)** : If supported by your ML framework, one or more replicas may be designated as *parameter servers* . These replicas store model parameters and coordinate shared model state between the workers.

  - **Evaluator(s)** : If supported by your ML framework, one or more replicas may be designated as *evaluators* . These replicas can be used to evaluate your model. If you are using TensorFlow, note that TensorFlow generally expects that you use no more than one evaluator.

## Configure a distributed training job

You can configure any Gemini Enterprise Agent Platform serverless training job as a distributed training job by defining multiple worker pools. You can also run distributed training within a training pipeline or a hyperparameter tuning job.

<span id="worker-pool-types"></span>

To configure a distributed training job, define your list of worker pools ( [`workerPoolSpecs[]`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#FIELDS.worker_pool_specs) ), designating one `WorkerPoolSpec` for each type of task:

| Position in `workerPoolSpecs[]` | Task performed in cluster              |
| ------------------------------- | -------------------------------------- |
| First ( `workerPoolSpecs[0]` )  | Primary, chief, scheduler, or "master" |
| Second ( `workerPoolSpecs[1]` ) | Secondary, replicas, workers           |
| Third ( `workerPoolSpecs[2]` )  | Parameter servers, Reduction Server    |
| Fourth ( `workerPoolSpecs[3]` ) | Evaluators                             |

You must specify a primary replica, which coordinates the work done by all the other replicas. Use the first worker pool specification only for your primary replica, and set its [`replicaCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#WorkerPoolSpec.FIELDS.replica_count) to `1` :

    {
      "workerPoolSpecs": [
         // `WorkerPoolSpec` for worker pool 0, primary replica, required
         {
           "machineSpec": {...},
           "replicaCount": 1,
           "diskSpec": {...},
           ...
         },
         // `WorkerPoolSpec` for worker pool 1, optional
         {},
         // `WorkerPoolSpec` for worker pool 2, optional
         {},
         // `WorkerPoolSpec` for worker pool 3, optional
         {}
       ]
       ...
    }

### Specify additional worker pools

Depending on your ML framework, you may specify additional worker pools for other purposes. For example, if you are using TensorFlow, you could specify worker pools to configure worker replicas, parameter server replicas, and evaluator replicas.

The order of the worker pools you specify in the `workerPoolSpecs[]` list determines the [type of worker pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training#worker-pool-types) . Set empty values for worker pools that you don't want to use, so that you can skip them in the `workerPoolSpecs[]` list in order to specify worker pools that you do want to use. For example:

If you want to specify a job that has only a primary replica and a parameter server worker pool, you must set an empty value for worker pool 1:

    {
      "workerPoolSpecs": [
         // `WorkerPoolSpec` for worker pool 0, required
         {
           "machineSpec": {...},
           "replicaCount": 1,
           "diskSpec": {...},
           ...
         },
         // `WorkerPoolSpec` for worker pool 1, optional
         {},
         // `WorkerPoolSpec` for worker pool 2, optional
         {
           "machineSpec": {...},
           "replicaCount": 1,
           "diskSpec": {...},
           ...
         },
         // `WorkerPoolSpec` for worker pool 3, optional
         {}
       ]
       ...
    }

### Reduce training time with Reduction Server

When you train a large ML model using multiple nodes, communicating gradients between nodes can contribute significant latency. *Reduction Server* is an all-reduce algorithm that can increase throughput and reduce latency for distributed training. Agent Platform makes Reduction Server available in a Docker container image that you can use for one of your worker pools during distributed training.

To learn about how Reduction Server works, see [Faster distributed GPU training with Reduction Server on Agent Platform](https://cloud.google.com/blog/products/ai-machine-learning/faster-distributed-training-with-google-clouds-reduction-server) .

#### Prerequisites

You can use Reduction Server if you meet the following requirements:

  - You are performing distributed training with GPU workers.

  - Your training code uses TensorFlow or PyTorch and is configured for multi-host data-parallel training with GPUs using [NCCL](https://developer.nvidia.com/nccl) all-reduce. (You might also be able to use other ML frameworks that use NCCL.)

  - The containers running on your primary node ( `workerPoolSpecs[0]` ) and workers ( `workerPoolSpecs[1]` ) support Reduction Server. Specifically, each container is one of the following:
    
      - A [prebuilt TensorFlow training container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers#tensorflow) , version 2.3 or later.
    
      - A [prebuilt Pytorch training container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers#pytorch) , version 1.4 or later.
    
      - A [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containers-overview) with NCCL 2.7 or later and the `google-reduction-server` package installed. You can install this package on a custom container image by adding the following line to your Dockerfile:
        
            RUN echo "deb https://packages.cloud.google.com/apt google-fast-socket main" | tee /etc/apt/sources.list.d/google-fast-socket.list && \
                curl -s -L https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
                apt update && apt install -y google-reduction-server

#### Train using Reduction Server

To use Reduction Server, do the following when you create a serverless training resource:

1.  Specify one of the following URIs in the [`containerSpec.imageUri` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#ContainerSpec) of the third worker pool ( `workerPoolSpecs[2]` ):
    
      - `us-docker.pkg.dev/vertex-ai-restricted/training/reductionserver:latest`
      - `europe-docker.pkg.dev/vertex-ai-restricted/training/reductionserver:latest`
      - `asia-docker.pkg.dev/vertex-ai-restricted/training/reductionserver:latest`
    
    Choosing the multi-region closest to where you are performing serverless training might reduce latency.

2.  When selecting the [machine type and number of nodes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) for the third worker pool, make sure that the total network bandwidth of the third worker pool matches or exceeds the total network bandwidth of the first and second worker pools.
    
    To learn about the maximum available bandwidth of each node in the second worker pool, see [Network bandwidth and GPUs](https://docs.cloud.google.com/compute/docs/gpus/gpu-network-bandwidth) .
    
    You do not use GPUs for the Reduction Server nodes. To learn about the maximum available bandwidth of each node in the third worker pool, see the "Maximum egress bandwidth (Gbps)" columns in [General-purpose machine family](https://docs.cloud.google.com/compute/docs/general-purpose-machines) .
    
    For example, if you configure the first and second worker pools to use 5 `n1-highmem-96` nodes, each with 8 `NVIDIA_TESLA_V100` GPUs, then each node has a maximum available bandwidth of 100 Gbps, for a total bandwidth of 500 Gbps. In order to match this bandwidth in the third worker pool, you might use 16 `n1-highcpu-16` nodes, each with a maximum bandwidth of 32 Gbps, for a total bandwidth of 512 Gbps.
    
    We recommend that you use the `n1-highcpu-16` machine type for Reduction Server nodes, because this machine type offers relatively high bandwidth for its resources.

The following command provides an example of how to create a `CustomJob` resource that uses Reduction Server:

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --worker-pool-spec=machine-type=n1-highmem-96,replica-count=1,accelerator-type=NVIDIA_TESLA_V100,accelerator-count=8,container-image-uri=CUSTOM_CONTAINER_IMAGE_URI \
      --worker-pool-spec=machine-type=n1-highmem-96,replica-count=4,accelerator-type=NVIDIA_TESLA_V100,accelerator-count=8,container-image-uri=CUSTOM_CONTAINER_IMAGE_URI \
      --worker-pool-spec=machine-type=n1-highcpu-16,replica-count=16,container-image-uri=us-docker.pkg.dev/vertex-ai-restricted/training/reductionserver:latest

For more context, see the [guide to creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

> To see an example of how to perform distributed training in PyTorch by using Reduction Server, run the "PyTorch distributed training with Reduction Server" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/reduction_server/pytorch_distributed_training_reduction_server.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Freduction_server%2Fpytorch_distributed_training_reduction_server.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Freduction_server%2Fpytorch_distributed_training_reduction_server.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/reduction_server/pytorch_distributed_training_reduction_server.ipynb)

> To see an example of how to perform parallel training in XGBoost by using Dask, run the "Distributed XGBoost training with Dask" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/xgboost_data_parallel_training_on_cpu_using_dask.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fxgboost_data_parallel_training_on_cpu_using_dask.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fxgboost_data_parallel_training_on_cpu_using_dask.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/xgboost_data_parallel_training_on_cpu_using_dask.ipynb)

### Best practices for training using Reduction Server

To optimize the performance and efficiency of your Reduction Server training jobs, consider the following best practices for configuring your cluster.

#### Machine type and count

In Reduction Server training, each worker needs to connect to all of the reducer hosts. To minimize the number of connections on the worker host, use a machine type with the highest network bandwidth for your reducer host.

A good choice for reducer hosts is a general purpose N1/N2 VM with at least 16 vCPU that provides [32 Gbps egress bandwidth](https://docs.cloud.google.com/compute/docs/networking/configure-vm-with-high-bandwidth-configuration#bandwidth-tiers) , such as `n1-highcpu-16` and `n2-highcpu-16` . Tier 1 VM bandwidth for N1/N2 VMs increases the maximum egress bandwidth ranging from 50 Gbps and 100 Gbps, making these a good choice for reducer VM nodes.

The total egress bandwidth of workers and reducers should be the same. For example, if you use 8 `a2-megagpu-16g` VMs as workers, you should use at least 25 `n1-highcpu-16` VMs as reducers.

    `(8 worker VMs * 100&nbsp;Gbps) / 32&nbsp;Gbps egress = 25 reducer VMs`.

#### Batch small messages together

Reduction Server works best if the messages to be aggregated are sufficiently large. Most ML frameworks already provide techniques under different terminology for batching small gradient tensors before performing all-reduce.

##### Horovod

Horovod supports [Tensor Fusion](https://horovod.readthedocs.io/en/stable/tensor-fusion_include.html) to batch small tensors for all-reduce. Tensors are filled in a fusion buffer until the buffer is fully filled and the all-reduce operation on the buffer executes. You can adjust the size of the fusion buffer by setting the `HOROVOD_FUSION_THRESHOLD` environment variable.

The recommended value for the `HOROVOD_FUSION_THRESHOLD` environment variable is at least 128 MB. In this case, set the `HOROVOD_FUSION_THRESHOLD` environment variable to 134217728 (128 \* 1024 \* 1024).

##### PyTorch

PyTorch [DistributedDataParallel](https://pytorch.org/docs/stable/notes/ddp.html) supports batch messages as "gradient bucketing". Set the `bucket_cap_mb` parameter in the `DistributedDataParallel` constructor to control the size of your batch buckets. The default size is 25 MB.

BEST PRACTICE: The recommended value of bucket\_cap\_mb is 64 (64 MB).

## Environment variables for your cluster

Agent Platform populates an environment variable, `CLUSTER_SPEC` , on every replica to describe how the overall cluster is set up. Like [TensorFlow's `TF_CONFIG`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training#tf-config) , `CLUSTER_SPEC` describes every replica in the cluster, including its index and role (primary replica, worker, parameter server, or evaluator).

When you run distributed training with TensorFlow, `TF_CONFIG` is parsed to build [`tf.train.ClusterSpec`](https://www.tensorflow.org/api_docs/python/tf/train/ClusterSpec) . Similarly, when you run distributed training with other ML frameworks, you must parse `CLUSTER_SPEC` to populate any environment variables or settings required by the framework.

### The format of `CLUSTER_SPEC`

The `CLUSTER_SPEC` environment variable is a JSON string with the following format:

Key

Description

`"cluster"`

The cluster description for your custom container. As with `TF_CONFIG` , this object is formatted as a TensorFlow cluster specification, and can be passed to the constructor of [tf.train.ClusterSpec](https://www.tensorflow.org/api_docs/python/tf/train/ClusterSpec) .

The cluster description contains a list of replica names for each worker pool you specify.

`"workerpool0"`

All distributed training jobs have one primary replica in the first worker pool.

`"workerpool1"`

This worker pool contains worker replicas, if you specified them when creating your job.

`"workerpool2"`

This worker pool contains parameter servers, if you specified them when creating your job.

`"workerpool3"`

This worker pool contains evaluators, if you specified them when creating your job.

`"environment"`

The string `cloud` .

`"task"`

Describes the task of the particular node on which your code is running. You can use this information to write code for specific workers in a distributed job. This entry is a dictionary with the following keys:

`"type"`

The type of worker pool this task is running in. For example, `"workerpool0"` refers to the primary replica.

`"index"`

The zero-based index of the task. For example, if your training job includes two workers, this value is set to `0` on one of them and `1` on the other.

`"trial"`

The identifier of the hyperparameter tuning trial currently running. When you configure hyperparameter tuning for your job, you set a number of trials to train. This value gives you a way to differentiate in your code between trials that are running. The identifier is a string value containing the trial number, starting at 1.

`job`

The [`CustomJobSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec) that you provided to create the current training job, represented as a dictionary.

#### `CLUSTER_SPEC` example

Here is an example value:

    {
       "cluster":{
          "workerpool0":[
             "cmle-training-workerpool0-ab-0:2222"
          ],
          "workerpool1":[
             "cmle-training-workerpool1-ab-0:2222",
             "cmle-training-workerpool1-ab-1:2222"
          ],
          "workerpool2":[
             "cmle-training-workerpool2-ab-0:2222",
             "cmle-training-workerpool2-ab-1:2222"
          ],
          "workerpool3":[
             "cmle-training-workerpool3-ab-0:2222",
             "cmle-training-workerpool3-ab-1:2222",
             "cmle-training-workerpool3-ab-2:2222"
          ]
       },
       "environment":"cloud",
       "task":{
          "type":"workerpool0",
          "index":0,
          "trial":"TRIAL_ID"
       },
       "job": {
          ...
       }
    }

### The format of `TF_CONFIG`

In addition to `CLUSTER_SPEC` , Agent Platform sets the [`TF_CONFIG`](https://www.tensorflow.org/guide/distributed_training#setting_up_tf_config_environment_variable) environment variable on each replica of all distributed training jobs. Agent Platform does *not* set `TF_CONFIG` for single-replica training jobs.

`CLUSTER_SPEC` and `TF_CONFIG` share some values, but they have different formats. Both environment variables include additional fields beyond what TensorFlow requires.

Distributed training with TensorFlow works the same way when you use custom containers as when you use a prebuilt container.

The `TF_CONFIG` environment variable is a JSON string with the following format:

`TF_CONFIG` fields

`cluster`

The TensorFlow cluster description. A dictionary mapping one or more task names ( `chief` , `worker` , `ps` , or `master` ) to lists of network addresses where these tasks are running. For a given training job, this dictionary is the same on every VM.

This is a valid first argument for the [`tf.train.ClusterSpec`](https://www.tensorflow.org/api_docs/python/tf/train/ClusterSpec) constructor. Note that this dictionary never contains `evaluator` as a key, since evaluators are not considered part of the training cluster even if you use them for your job.

`task`

The task description of the VM where this environment variable is set. For a given training job, this dictionary is different on every VM. You can use this information to customize what code runs on each VM in a distributed training job. You can also use it to change the behavior of your training code for different trials of a hyperparameter tuning job.

This dictionary includes the following key-value pairs:

`task` fields

`type`

The type of task that this VM is performing. This value is set to `worker` on workers, `ps` on parameter servers, and `evaluator` on evaluators. On your job's master worker, the value is set to either `chief` or `master` .

`index`

The zero-based index of the task. For example, if your training job includes two workers, this value is set to `0` on one of them and `1` on the other.

`trial`

The ID of the hyperparameter tuning trial currently running on this VM. This field is only set if the current training job is a hyperparameter tuning job.

For hyperparameter tuning jobs, Agent Platform runs your training code repeatedly in many trials with different hyperparameters each time. This field contains the current trial number, starting at `1` for the first trial.

`cloud`

An ID used internally by Agent Platform. You can ignore this field.

`job`

The [`CustomJobSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec) that you provided to create the current training job, represented as a dictionary.

`environment`

The string `cloud` .

#### `TF_CONFIG` example

The following example code prints the `TF_CONFIG` environment variable to your training logs:

    import json
    import os
    
    tf_config_str = os.environ.get('TF_CONFIG')
    tf_config_dict  = json.loads(tf_config_str)
    
    # Convert back to string just for pretty printing
    print(json.dumps(tf_config_dict, indent=2))

In a hyperparameter tuning job that runs in runtime version 2.1 or later and uses a master worker, two workers, and a parameter server, this code produces the following log for one of the workers during the first hyperparameter tuning trial. The example output hides the `job` field for conciseness and replaces some IDs with generic values.

    {
      "cluster": {
        "chief": [
          "training-workerpool0-[ID_STRING_1]-0:2222"
        ],
        "ps": [
          "training-workerpool2-[ID_STRING_1]-0:2222"
        ],
        "worker": [
          "training-workerpool1-[ID_STRING_1]-0:2222",
          "training-workerpool1-[ID_STRING_1]-1:2222"
        ]
      },
      "environment": "cloud",
      "job": {
        ...
      },
      "task": {
        "cloud": "[ID_STRING_2]",
        "index": 0,
        "trial": "1",
        "type": "worker"
      }
    }

## When to use `TF_CONFIG`

`TF_CONFIG` is set only for distributed training jobs.

You likely don't need to interact with the `TF_CONFIG` environment variable directly in your training code. Only access the the `TF_CONFIG` environment variable if TensorFlow's distribution strategies and Agent Platform's standard hyperparameter tuning workflow, both described in the next sections, don't work for your job.

### Distributed training

Agent Platform sets the `TF_CONFIG` environment variable to extend the [specifications that TensorFlow requires for distributed training](https://www.tensorflow.org/guide/distributed_training#setting_up_tf_config_environment_variable) .

To perform distributed training with TensorFlow, use the [`tf.distribute.Strategy` API](https://www.tensorflow.org/guide/distributed_training) . In particular, we recommend that you use the Keras API together with the [`MultiWorkerMirroredStrategy`](https://www.tensorflow.org/guide/distributed_training#multiworkermirroredstrategy) or, if you [specify parameter servers for your job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) , the [`ParameterServerStrategy`](https://www.tensorflow.org/guide/distributed_training#parameterserverstrategy) . However, note that TensorFlow only provides experimental support for these strategies.

These distribution strategies use the `TF_CONFIG` environment variable to assign roles to each VM in your training job and to facilitate communication between the VMs. You don't need to access the `TF_CONFIG` environment variable directly in your training code, because TensorFlow handles it for you.

Only parse the `TF_CONFIG` environment variable directly if you want to customize how the different VMs running your training job behave.

### Hyperparameter tuning

When you run a [hyperparameter tuning job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) , Agent Platform provides different arguments to your training code for each trial. Your training code does not necessarily need to be aware of what trial is currently running. In addition, you can monitor the progress of hyperparameter tuning jobs in Google Cloud console.

If needed, your code can read the current trial number from [the `trial` field of the `task` field of the `TF_CONFIG` environment variable](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training#tf-config) .

## What's next

  - Create a [training pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) .
