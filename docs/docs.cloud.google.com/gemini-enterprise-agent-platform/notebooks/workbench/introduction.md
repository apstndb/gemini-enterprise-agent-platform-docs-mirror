---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction
title: Introduction to Vertex AI Workbench
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Vertex AI Workbench instances are Jupyter notebook-based development environments for the entire data science workflow. You can interact with Gemini Enterprise Agent Platform and other Google Cloud services from within a Vertex AI Workbench instance's Jupyter notebook.

Vertex AI Workbench integrations and features can make it easier to access your data, process data faster, schedule notebook runs, and more.

Vertex AI Workbench instances are prepackaged with [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html) and have a preinstalled suite of deep learning packages, including support for the TensorFlow and PyTorch frameworks. You can configure either CPU-only or GPU-enabled instances.

Vertex AI Workbench instances support the ability to sync with a [GitHub](https://github.com/) repository.

Vertex AI Workbench instances are protected by Google Cloud authentication and authorization.

## Access to data

You can access your data without leaving the JupyterLab user interface.

In JupyterLab's navigation menu on a Vertex AI Workbench instance, you can use the Cloud Storage integration to browse data and other files that you have access to. See [Access Cloud Storage buckets and files from within JupyterLab](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cloud-storage) .

You can also use the BigQuery integration to browse tables that you have access to, write queries, preview results, and load data into your notebook. See [Query data in BigQuery tables from within JupyterLab](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/bigquery) .

## Execute notebook runs

Use the executor to run a notebook file as a one-time execution or on a schedule. Choose the specific environment and hardware that you want your execution to run on. Your notebook's code will run on Agent Platform custom training, which can make it easier to do distributed training, optimize hyperparameters, or schedule continuous training jobs.

You can use parameters in your execution to make specific changes to each run. For example, you might specify a different dataset to use, change the learning rate on your model, or change the version of the model.

You can also set a notebook to run on a recurring schedule. Even while your instance is shut down, Vertex AI Workbench will run your notebook file and save the results for you to look at and share with others. See [Schedule a notebook run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/schedule-notebook-run-quickstart) .

## Share insights

Executed notebook runs are stored in a Cloud Storage bucket, so you can share your insights with others by granting access to the results. See the [previous section on executing notebook runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction#executor) .

## Secure your instance

The following sections describe supported capabilities that can help you secure your Vertex AI Workbench instance.

### VPC

You can deploy your Vertex AI Workbench instance with the default Google-managed network, which uses a default VPC network and subnet. Instead of the default network, you can specify a VPC network to use with your instance.

To use Vertex AI Workbench within a service perimeter, see [Use a Vertex AI Workbench instance within a service perimeter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/service-perimeter) .

### Customer-managed encryption keys (CMEK)

By default, Google Cloud automatically [encrypts data when it is at rest](https://docs.cloud.google.com/docs/security/encryption/default-encryption) using encryption keys managed by Google. If you have specific compliance or regulatory requirements related to the keys that protect your data, you can use customer-managed encryption keys (CMEK) with your Vertex AI Workbench instances. For more information, see [Customer-managed encryption keys](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cmek) .

### Confidential Computing

You can encrypt your data-in-use by using Confidential Computing. To use Confidential Computing, you enable the Confidential VM service when you create a Vertex AI Workbench instance. To get started, see [Create an instance with Confidential Computing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-confidential-computing) .

## Automated shutdown for idle instances

To help manage costs, Vertex AI Workbench instances shut down after being idle for a specific time period by default. You can change the amount of time or turn this feature off. For more information, see [Idle shutdown](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/idle-shutdown) .

## Add conda environments

Vertex AI Workbench instances use [kernels](https://jupyterlab.readthedocs.io/en/stable/user/documents_kernels.html) based on conda environments. You can add a conda environment to your Vertex AI Workbench instance, and the environment appears as a kernel in your instance's JupyterLab interface.

Adding conda environments lets you use kernels that aren't available in the default Vertex AI Workbench instance. For example, you can add conda environments for R and Apache Beam. Or you can add conda environments for specific earlier versions of the available frameworks, such as TensorFlow, PyTorch, or Python.

For more information, see [Add a conda environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/add-environment) .

## Custom containers

You can create a Vertex AI Workbench instance based on a custom container. Start with a Google-provided base container image, and modify it for your needs. Then create an instance based on your custom container.

For more information, see [Create an instance using a custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container) .

## Managed Service for Apache Spark integration

You can process data quickly by running a notebook on a Managed Service for Apache Spark cluster. After your cluster is set up, you can run a notebook file on it without leaving the JupyterLab user interface. For more information, see [Create a Managed Service for Apache Spark-enabled instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-dataproc-enabled) .

## Reserve VM resources

Use [Compute Engine reservations](https://docs.cloud.google.com/compute/docs/instances/reservations-overview) to gain a high level of assurance that your Vertex AI Workbench instances have enough virtual machine (VM) resources to run.

Reservations are a Compute Engine feature. They help make sure that you have the resources available to create VMs with the same hardware (memory and vCPUs) and optional resources (GPUs and Local SSD disks) whenever you need them.

For more information, see [Use reservations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/reservations) .

## Create instances with third party credentials

You can create and manage Vertex AI Workbench instances with third party credentials provided by Workforce Identity Federation. Workforce Identity Federation uses your external identity provider (IdP) to grant a group of users access to Vertex AI Workbench instances through a proxy.

Access to a Vertex AI Workbench instance is granted by assigning a [workforce pool principal](https://docs.cloud.google.com/iam/docs/workforce-identity-federation#representing-workforce-users) to the Vertex AI Workbench instance's service account.

For more information, see [Create an instance with third party credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-third-party-instance) .

## Tags for Vertex AI Workbench instances

The underlying VM of a Vertex AI Workbench instance is a Compute Engine VM. You can add and manage resource tags to your Vertex AI Workbench instance through its Compute Engine VM.

When you create a Vertex AI Workbench instance, Vertex AI Workbench attaches the Compute Engine resource tag `vertex-workbench-instances:prod=READ_ONLY` . This resource tag is only used for internal purposes.

To learn more about managing tags for Compute Engine instances, see [Manage tags for resources](https://docs.cloud.google.com/compute/docs/tag-resources) .

## Limitations

Consider the following limitations of Vertex AI Workbench instances when planning your project:

  - Third party JupyterLab extensions aren't supported.

  - When you use [Access Context Manager](https://docs.cloud.google.com/access-context-manager/docs/create-basic-access-level#corporate-network-example) and [Chrome Enterprise Premium](https://docs.cloud.google.com/chrome-enterprise-premium/docs/access-levels) to protect Vertex AI Workbench instances with context-aware access controls, access is evaluated each time the user authenticates to the instance. For example, access is evaluated the first time the user accesses JupyterLab and whenever they access it thereafter if their web browser's cookie has expired.

  - Using a custom container that isn't derived from the Google-provided base container ( `gcr.io/deeplearning-platform-release/workbench-container:latest` ) increases the risks of compatibility issues with our services and isn't supported. Instead, modify the base container to create a custom container that meets your needs, and then [create an instance using the custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container) .

  - Vertex AI Workbench instances expect images from the `cloud-notebooks-managed` project. The list of image names is available at the creation page in the Google Cloud console. Although the use of custom virtual machine (VM) images or [Deep Learning VM](https://docs.cloud.google.com/deep-learning-vm/docs/introduction) images with Vertex AI Workbench instances can be possible, Vertex AI Workbench doesn't provide any support for unexpected behaviors or malfunctions when using those images.

  - You can't edit the underlying VM of a Vertex AI Workbench instance by using the Google Cloud console or the Compute Engine API. To edit a Vertex AI Workbench instance's underlying VM, use the [`projects.locations.instances.patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch) method in the Notebooks API or the [`gcloud workbench instances update`](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/update) command in the Agent Platform SDK.

  - In instances that use VPC Service Controls, use of the [executor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/schedule-notebook-run-quickstart) isn't supported.

  - To use accelerators with Vertex AI Workbench instances, the accelerator type that you want must be available in your instance's zone. To learn about accelerator availability by zone, see [GPU regions and zones availability](https://docs.cloud.google.com/compute/docs/gpus/gpu-regions-zones) .

## What's next

  - [Create a Vertex AI Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) .

  - [Compare Gemini Enterprise Agent Platform's notebook solutions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/notebook-solution) .
