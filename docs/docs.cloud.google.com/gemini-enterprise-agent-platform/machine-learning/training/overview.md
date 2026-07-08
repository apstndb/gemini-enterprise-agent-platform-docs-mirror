---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview
title: Gemini Enterprise Agent Platform serverless training overview
description: Provides a managed training service that helps you operationalize large scale model training
data_source: docs.cloud.google.com
---

[Video](https://www.youtube.com/watch?v=VRQXIiNLdAk)

Gemini Enterprise Agent Platform provides a managed training service that helps you operationalize large scale model training. You can use Gemini Enterprise Agent Platform to run training applications based on any machine learning (ML) framework on Google Cloud infrastructure. For the following popular ML frameworks, Gemini Enterprise Agent Platform also has integrated support that simplifies the preparation process for model training and serving:

  - [PyTorch](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/pytorch)
  - [TensorFlow](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/tensorflow)
  - [scikit-learn](https://scikit-learn.org/stable/)
  - [XGBoost](https://xgboost.readthedocs.io/en/stable/)

This page explains the benefits of serverless training on Gemini Enterprise Agent Platform, the workflow involved, and the various training options that are available.

### Gemini Enterprise Agent Platform operationalizes training at scale

There are several challenges to operationalizing model training. These challenges include the time and cost needed to train models, the depth of skills required to manage the compute infrastructure, and the need to provide enterprise-level security. Gemini Enterprise Agent Platform addresses these challenges while providing a host of other benefits.

#### Fully managed compute infrastructure

|                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Managed infrastructure](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/images/icons/managed.svg) | Model training on Gemini Enterprise Agent Platform is a fully managed service that requires no administration of physical infrastructure. You can train ML models without the need to provision or manage servers. You only pay for the compute resources that you consume. Gemini Enterprise Agent Platform also handles job logging, queuing, and monitoring. |

#### High-performance

|                                                                                                                                                   |                                                                                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![High-performance](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/images/icons/performance.svg) | Gemini Enterprise Agent Platform training jobs are optimized for ML model training, which can provide faster performance than directly running your training application on a Google Kubernetes Engine (GKE) cluster. You can also identify and debug performance bottlenecks in your training job by using Cloud Profiler. |

#### Distributed training

|                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Distributed training](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/images/icons/distributed.svg) | [Reduction Server](https://cloud.google.com/blog/topics/developers-practitioners/optimize-training-performance-reduction-server-vertex-ai) is an all-reduce algorithm in Gemini Enterprise Agent Platform that can increase throughput and reduce latency of multi-node distributed training on NVIDIA graphics processing units (GPUs). This optimization helps reduce the time and cost of completing large training jobs. |

#### Hyperparameter optimization

|                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Hyperparameter tuning](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/images/icons/hptuning.svg) | [Hyperparameter tuning jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) run multiple trials of your training application using different hyperparameter values. You specify a range of values to test, and Gemini Enterprise Agent Platform discovers the optimal values for your model within that range. |

#### Enterprise security

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/images/icons/security.svg" class="invert-hue" alt="Enterprise security" /></td>
<td><p>Gemini Enterprise Agent Platform provides the following enterprise security features:</p>
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering">VPC peering</a> to limit network access.</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls">VPC Service Controls</a> to mitigate the risks of data exfiltration.</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek">Customer-managed encryption keys</a> to help you meet specific compliance or regulatory requirements related to data protection.</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control">Identity and Access Management</a> for fine-grained control over service account access.</li>
<li>Data isolation with single-tenant project boundaries.</li>
</ul></td>
</tr>
</tbody>
</table>

#### ML operations (MLOps) integrations

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><img src="https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/images/icons/mlops.svg" class="invert-hue" alt="MLOps" /></td>
<td><p>Gemini Enterprise Agent Platform provides a suite of <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/introduction-mlops">integrated MLOps tools</a> and features that you can use for the following purposes:</p>
<ul>
<li>Orchestrate end-to-end ML workflows.</li>
<li>Perform feature engineering.</li>
<li>Run experiments.</li>
<li>Manage and iterate your models.</li>
<li>Track ML metadata.</li>
<li>Monitor and evaluate model quality.</li>
</ul></td>
</tr>
</tbody>
</table>

## Workflow for serverless training

The following diagram shows a high-level overview of the serverless training workflow on Gemini Enterprise Agent Platform. The sections that follow describe each step in detail.

![Workflow for custom training](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/images/custom-training-workflow.png)

### Load and prepare training data

For the best performance and support, use one of the following Google Cloud services as your data source:

  - [Cloud Storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/cloud-storage-file-system)
  - [BigQuery](https://docs.cloud.google.com/bigquery/docs/introduction)
  - High-performance file systems, such as [NFS shares on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/train-nfs-share) using services like [Google Cloud NetApp Volumes](https://docs.cloud.google.com/netapp/volumes/docs/discover/overview) or [Filestore](https://docs.cloud.google.com/filestore/docs/overview) .

For a comparison of these services, see [Data preparation overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/data-preparation-overview) .

You can also specify a [Gemini Enterprise Agent Platform managed dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-managed-datasets) as the data source when using a training pipeline to train your model. Training a custom model and an AutoML model using the same dataset lets you compare the performance of the two models.

### Prepare your training application

To prepare your training application for use on Gemini Enterprise Agent Platform, do the following:

  - Implement training code best practices for Gemini Enterprise Agent Platform.
  - Determine a type of container image to use.
  - Package your training application into a supported format based on the selected container image type.

#### Implement training code best practices

Your training application should implement the [training code best practices for Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#requirements_for_all_custom_training_code) . These best practices relate to the ability of your training application to do the following:

  - Access Google Cloud services.
  - Load input data.
  - Enable autologging for experiment tracking.
  - Export model artifacts.
  - Use the environment variables of Gemini Enterprise Agent Platform.
  - Ensure resilience to VM restarts.

#### Select a container type

Gemini Enterprise Agent Platform runs your training application in a [Docker container image](https://www.docker.com/resources/what-container/) . A Docker container image is a self-contained software package that includes code and all dependencies, which can run in almost any computing environment. You can either specify the URI of a [prebuilt container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) to use, or create and upload a [custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containers-overview) that has your training application and dependencies pre-installed.

The following table shows the differences between prebuilt and custom container images:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Specifications</th>
<th>Prebuilt container images</th>
<th>Custom container images</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>ML framework</strong></td>
<td>Each container image is specific to an ML framework.</td>
<td>Use any ML framework or use none.</td>
</tr>
<tr class="even">
<td><strong>ML framework version</strong></td>
<td>Each container image is specific to an ML framework version.</td>
<td>Use any ML framework version, including minor versions and nightly builds.</td>
</tr>
<tr class="odd">
<td><strong>Application dependencies</strong></td>
<td>Common dependencies for the ML framework are pre-installed. You can specify additional dependencies to install in your training application.</td>
<td>Pre-install the dependencies that your training application needs.</td>
</tr>
<tr class="even">
<td><strong>Application delivery format</strong></td>
<td><ul>
<li>Python source distribution.</li>
<li>Single Python file.</li>
</ul></td>
<td>Pre-install the training application in the custom container image.</td>
</tr>
<tr class="odd">
<td><strong>Effort to set up</strong></td>
<td>Low</td>
<td>High</td>
</tr>
<tr class="even">
<td><strong>Recommended for</strong></td>
<td>Python training applications based on an ML framework and framework version that has a prebuilt container image available.</td>
<td><ul>
<li>Greater customization and control.</li>
<li>Non-Python training applications.</li>
<li>Private or custom dependencies.</li>
<li>Training applications that use an ML framework or framework version that has no prebuilt container image available.</li>
</ul></td>
</tr>
</tbody>
</table>

#### Package your training application

After you've determined the type of container image to use, package your training application into one of the following formats based on the container image type:

  - **Single Python file for use in a prebuilt container**
    
    Write your training application as a single Python file and use the [Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) to create a `CustomJob` or `CustomTrainingJob` class. The Python file is packaged into a Python source distribution and installed to a prebuilt container image. Delivering your training application as a single Python file is suitable for prototyping. For production training applications, you'll likely have your training application arranged into more than one file.

  - **Python source distribution for use in a prebuilt container**
    
    [Package your training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) into one or more Python source distributions and upload them to a Cloud Storage bucket. Gemini Enterprise Agent Platform installs the source distributions to a prebuilt container image when you create a training job.

  - **Custom container image**
    
    [Create your own Docker container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) that has your training application and dependencies pre-installed, and upload it to Artifact Registry. If your training application is written in Python, you can [perform these steps by using one Google Cloud CLI command](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#create_custom_job-gcloud) .

### Configure training job

A Gemini Enterprise Agent Platform training job performs the following tasks:

  - Provisions one (single node training) or more (distributed training) virtual machines (VMs).
  - Runs your containerized training application on the provisioned VMs.
  - Deletes the VMs after the training job completes.

Gemini Enterprise Agent Platform offers [three types of training jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-training-methods) for running your training application:

  - **[Custom job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job)**
    
    A custom job ( [`CustomJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob) ) runs your training application. If you're using a prebuilt container image, model artifacts are output to the specified Cloud Storage bucket. For custom container images, your training application can also output model artifacts to other locations.

  - **[Hyperparameter tuning job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview)**
    
    A hyperparameter tuning job ( [`HyperparameterTuningJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob) ) runs multiple trials of your training application using different hyperparameter values until it produces model artifacts with the optimal performing hyperparameter values. You specify the range of hyperparameter values to test and the metrics to optimize for.

  - **[Training pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline)**
    
    A training pipeline ( [`CustomTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob) ) runs a custom job or hyperparameter tuning job and optionally exports the model artifacts to Gemini Enterprise Agent Platform to create a model resource. You can specify a Gemini Enterprise Agent Platform managed dataset as your data source.

When creating a training job, specify the compute resources to use for running your training application and configure your container settings.

#### Compute configurations

[Specify the compute resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) to use for a training job. Gemini Enterprise Agent Platform supports single-node training, where the training job runs on one VM, and [distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) , where the training job runs on multiple VMs.

The compute resources that you can specify for your training job are as follows:

  - **VM machine type**
    
    Different machine types offer different CPUs, memory size, and bandwidth.

  - **Graphics processing units (GPUs)**
    
    You can add one or more GPUs to A2 or N1 type VMs. If your training application is designed to use GPUs, adding GPUs can significantly improve performance.

  - **Tensor Processing Units (TPUs)**
    
    TPUs are designed specifically for accelerating machine learning workloads. When using a TPU VM for training, you can specify only one worker pool. That worker pool can have only one replica.

  - **Boot disks**
    
    You can use SSDs (default) or HDDs for your boot disk. If your training application reads and writes to disk, using SSDs can improve performance. You can also specify the size of your boot disk based on the amount of temporary data that your training application writes to disk. Boot disks can have between 100 GiB (default) and 64,000 GiB. All VMs in a worker pool must use the same type and size of boot disk.

#### Container configurations

The [container configurations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings) that you need to make depend on whether you're using a prebuilt or custom container image.

  - **Prebuilt container configurations:**
    
      - Specify the URI of the prebuilt container image that you want to use.
      - If your training application is packaged as a Python source distribution, specify the Cloud Storage URI where the package is located.
      - Specify the entry point module of your training application.
      - Optional: Specify a list of command-line arguments to pass to the entry point module of your training application.

  - **Custom container configurations:**
    
      - Specify the URI of your custom container image, which can be a URI from Artifact Registry or Docker Hub.
      - **Optional** : Override the `ENTRYPOINT` or `CMD` instructions in your container image.

### Create a training job

After your data and training application are prepared, run your training application by creating one of the following training jobs:

  - [Create a custom job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .
  - [Create a hyperparameter tuning job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) .
  - [Create a training pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) .

To create the training job, you can use the Google Cloud console, Google Cloud CLI, Agent Platform SDK for Python, or the Agent Platform API.

### (Optional) Import model artifacts into Gemini Enterprise Agent Platform

Your training application likely outputs one or more model artifacts to a specified location, usually a Cloud Storage bucket. Before you can get inferences in Gemini Enterprise Agent Platform from your model artifacts, first [import the model artifacts into Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts) .

Like container images for training, Gemini Enterprise Agent Platform gives you the choice of using [prebuilt](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/pre-built-containers) or [custom](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements) container images for inferences. If a prebuilt container image for inferences is available for your ML framework and framework version, we recommend using a prebuilt container image.

## What's next

  - [Get inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-predictions) from your model.
  - [Evaluate your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/evaluation/introduction) .
  - Try the [Hello serverless training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom) tutorial for step-by-step instructions on training a TensorFlow Keras image classification model on Gemini Enterprise Agent Platform.
