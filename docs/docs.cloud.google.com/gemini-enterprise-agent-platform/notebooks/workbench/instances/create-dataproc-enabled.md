---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-dataproc-enabled
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-dataproc-enabled
title: Create a Managed Service for Apache Spark Spark-enabled Agent Platform Workbench instance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Dataproc Serverless** is now **Managed Service for Apache Spark** . Until updated, the Google Cloud console and JupyterLab pages will refer to the previous name.

This page describes how to create a Managed Service for Apache Spark Spark-enabled Gemini Enterprise Agent Platform Workbench instance. This page also describes the benefits of the Managed Service for Apache Spark JupyterLab extension and provides an overview on how to use the extension with Managed Service for Apache Spark and Managed Service for Apache Spark on Compute Engine.

## Overview of the Managed Service for Apache Spark JupyterLab extension

Agent Platform Workbench instances have the Managed Service for Apache Spark JupyterLab extension preinstalled, as of version `M113` and later.

> **Note:** You can also [install and use the Managed Service for Apache Spark JupyterLab extension on your local machine or a Compute Engine VM instance](https://docs.cloud.google.com/dataproc-serverless/docs/quickstarts/jupyterlab-sessions) .

The Managed Service for Apache Spark JupyterLab extension provides two ways to run Apache Spark notebook jobs: Managed Service for Apache Spark clusters and Managed Service for Apache Spark.

  - **Managed Service for Apache Spark clusters** include a rich set of features with control over the infrastructure that Spark runs on. You choose the size and configuration of your Spark cluster, allowing for customization and control over your environment. This approach is ideal for complex workloads, long-running jobs, and fine-grained resource management.
  - **Managed Service for Apache Spark** eliminates infrastructure concerns. You submit your Spark jobs, and Google handles the provisioning, scaling, and optimization of resources behind the scenes. This serverless approach offers a cost-efficient option for data science and ML workloads.

With both options, you can use Spark for data processing and analysis. The choice between Managed Service for Apache Spark clusters and Managed Service for Apache Spark depends on your specific workload requirements, required level of control, and resource usage patterns.

Benefits of using Managed Service for Apache Spark for data science and ML workloads include:

  - **No cluster management** : You don't need to worry about provisioning, configuring, or managing Spark clusters. This saves you time and resources.
  - **Autoscaling** : Managed Service for Apache Spark automatically scales up and down based on the workload, so you only pay for the resources you use.
  - **High performance** : Managed Service for Apache Spark is optimized for performance and takes advantage of Google Cloud's infrastructure.
  - **Integration with other Google Cloud technologies** : Managed Service for Apache Spark integrates with other Google Cloud products, such as BigQuery and Knowledge Catalog.

For more information, see the [Managed Service for Apache Spark documentation](https://docs.cloud.google.com/dataproc-serverless/docs) .

## Before you begin

### Required roles

To ensure that the service account has the necessary permissions to run a notebook file on a Managed Service for Apache Spark cluster or a Managed Service for Apache Spark cluster, ask your administrator to grant the following IAM roles to the service account:

> **Important:** You must grant these roles to the service account, *not* to your user account. Failure to grant the roles to the correct principal might result in permission errors.

  - [Dataproc Worker](https://docs.cloud.google.com/iam/docs/roles-permissions/dataproc#dataproc.worker) ( `roles/dataproc.worker` ) on your project
  - [Dataproc Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/dataproc#dataproc.editor) ( `roles/dataproc.editor` ) on the cluster for the `dataproc.clusters.use` permission

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to run a notebook file on a Managed Service for Apache Spark cluster or a Managed Service for Apache Spark cluster. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to run a notebook file on a Managed Service for Apache Spark cluster or a Managed Service for Apache Spark cluster:

  - `dataproc.agents.create`
  - `dataproc.agents.delete`
  - `dataproc.agents.get`
  - `dataproc.agents.update`
  - `dataproc.tasks.lease`
  - `dataproc.tasks.listInvalidatedLeases`
  - `dataproc.tasks.reportStatus`
  - `dataproc.clusters.use`

Your administrator might also be able to give the service account these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create an instance with Managed Service for Apache Spark enabled

To create a Agent Platform Workbench instance with Managed Service for Apache Spark enabled, do the following:

1.  In the Google Cloud console, go to the **Instances** page.

2.  Click add\_box **Create new** .

3.  In the **New instance** dialog, click **Advanced options** .

4.  In the **Create instance** dialog, in the **Details** section, make sure **Enable Dataproc Serverless Interactive Sessions** is selected.

5.  Make sure **Workbench type** is set to **Instance** .

6.  In the **Environment** section, make sure you use the latest version or a version numbered `M113` or higher.

7.  Click **Create** .
    
    Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link.

> **Note:** Specific network configurations could affect your ability to use the Managed Service for Apache Spark extension. For more information on how to ensure that your network configuration is compatible, see [Network configuration options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create#network-options) .

## Open JupyterLab

Next to your instance's name, click **Open JupyterLab** .

The JupyterLab **Launcher** tab opens in your browser. By default it contains sections for **Managed Service for Apache Spark Notebooks** and **Managed Service for Apache Spark Jobs and Sessions** . If there are Jupyter-ready clusters in the selected project and region, there will be a section called **Managed Service for Apache Spark Cluster Notebooks** .

## Use the extension with Managed Service for Apache Spark

Managed Service for Apache Spark runtime templates that are in the same region and project as your Agent Platform Workbench instance appear in the **Managed Service for Apache Spark Notebooks** section of the JupyterLab **Launcher** tab.

To create a runtime template, see [Create a Managed Service for Apache Spark runtime template](https://docs.cloud.google.com/dataproc-serverless/docs/quickstarts/jupyterlab-sessions#create_a_serverless_runtime_template) .

To open a new serverless Spark notebook, click a runtime template. It takes about a minute for the remote Spark kernel to start. After the kernel starts, you can start coding.

## Use the extension with Managed Service for Apache Spark on Compute Engine

If you created a [Managed Service for Apache Spark on Compute Engine Jupyter cluster](https://docs.cloud.google.com/dataproc/docs/concepts/components/jupyter#install_jupyter) , the **Launcher** tab has a **Managed Service for Apache Spark Cluster Notebooks** section.

Four cards appear for each Jupyter-ready Managed Service for Apache Spark cluster that you have access to in that region and project.

To change the region and project, do the following:

1.  Select **Settings \> Cloud Managed Service for Apache Spark Settings** .

2.  On the **Setup Config** tab, under **Project Info** , change the **Project ID** and **Region** , and then click **Save** .
    
    These changes don't take effect until you restart JupyterLab.

3.  To restart JupyterLab, select **File \> Shut Down** , and then click **Open JupyterLab** on the **Agent Platform Workbench instances** page.

To create a new notebook, click a card. After the remote kernel on the Managed Service for Apache Spark cluster starts, you can start writing your code and then run it on your cluster.

## Manage Managed Service for Apache Spark on an instance using the gcloud CLI and the API

This section describes ways to manage Managed Service for Apache Spark on a Agent Platform Workbench instance.

### Change the region of your Managed Service for Apache Spark cluster

Your Agent Platform Workbench instance's default kernels, such as Python and TensorFlow, are local kernels that run in the instance's VM. On a Managed Service for Apache Spark Spark-enabled Agent Platform Workbench instance, your notebook runs on a Managed Service for Apache Spark cluster through a remote kernel. The remote kernel runs on a service outside of your instance's VM, which lets you access any Managed Service for Apache Spark cluster within the same project.

By default Agent Platform Workbench uses Managed Service for Apache Spark clusters within the same region as your instance, but you can [change the Managed Service for Apache Spark region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-dataproc-enabled#dataproc-compute) as long as the [Component Gateway](https://docs.cloud.google.com/dataproc/docs/concepts/accessing/dataproc-gateways) and the [optional Jupyter component](https://docs.cloud.google.com/dataproc/docs/concepts/components/jupyter) are enabled on the Managed Service for Apache Spark cluster.

### Test Access

The Managed Service for Apache Spark JupyterLab extension is enabled by default for Agent Platform Workbench instances. To test access to Managed Service for Apache Spark, you can check access to your instance's remote kernels by sending the following curl request to the `kernels.googleusercontent.com` domain:

```sh
curl --verbose -H "Authorization: Bearer $(gcloud auth print-access-token)" https://PROJECT_ID-dot-REGION.kernels.googleusercontent.com/api/kernelspecs | jq .
```

If the curl command fails, check to make sure that:

1.  Your DNS entries are configured correctly.

2.  There is a cluster available in the same project (or you will need to create one if it doesn't exist).

3.  Your cluster has both the [Component Gateway](https://docs.cloud.google.com/dataproc/docs/concepts/accessing/dataproc-gateways) and the [optional Jupyter component](https://docs.cloud.google.com/dataproc/docs/concepts/components/jupyter) enabled.

### Turn off Managed Service for Apache Spark

Agent Platform Workbench instances are created with Managed Service for Apache Spark enabled by default. You can create a Agent Platform Workbench instance with Managed Service for Apache Spark turned off by setting the `disable-mixer` `metadata` key to `true` .

    gcloud workbench instances create INSTANCE_NAME --metadata=disable-mixer=true

### Enable Managed Service for Apache Spark

You can enable Managed Service for Apache Spark on a stopped Agent Platform Workbench instance by updating the metadata value.

    gcloud workbench instances update INSTANCE_NAME --metadata=disable-mixer=false

## Manage Managed Service for Apache Spark using Terraform

Managed Service for Apache Spark for Agent Platform Workbench instances on Terraform is managed using the `disable-mixer` key in the metadata field. Turn on Managed Service for Apache Spark by setting the `disable-mixer` `metadata` key to `false` . Turn off Managed Service for Apache Spark by setting the `disable-mixer` metadata key to `true` .

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) .

```terraform
resource "google_workbench_instance" "default" {
  name     = "workbench-instance-example"
  location = "us-central1-a"

  gce_setup {
    machine_type = "n1-standard-1"
    vm_image {
      project = "cloud-notebooks-managed"
      family  = "workbench-instances"
    }
    metadata = {
      disable-mixer = "false"
    }
  }
}
```

## Troubleshoot

To diagnose and resolve issues related to creating a Managed Service for Apache Spark Spark-enabled instance, see [Troubleshooting Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/troubleshooting-workbench#dataproc-instances) .

## What's next

  - For more information about the Managed Service for Apache Spark JupyterLab extension, see [Use the JupyterLab extension to develop serverless Spark workloads](https://docs.cloud.google.com/dataproc-serverless/docs/quickstarts/jupyterlab-sessions) .

  - To learn more about Managed Service for Apache Spark, see the [Managed Service for Apache Spark documentation](https://docs.cloud.google.com/dataproc-serverless/docs)

  - [Learn how to run Managed Service for Apache Spark workloads without provisioning and managing clusters.](https://cloud.google.com/blog/products/data-analytics/serverless-spark-on-google-cloud-interactive-tutorial)

  - To learn more about using Spark with Google Cloud products and services, see [Spark on Google Cloud](https://docs.cloud.google.com/solutions/spark) .

  - Browse the available [Managed Service for Apache Spark templates on GitHub](https://github.com/GoogleCloudPlatform/dataproc-templates) .

  - Learn about Serverless Spark through the [`serverless-spark-workshop` on GitHub](https://github.com/GoogleCloudPlatform/serverless-spark-workshop) .

  - Read the [Apache Spark documentation](https://spark.apache.org/docs/latest/) .
