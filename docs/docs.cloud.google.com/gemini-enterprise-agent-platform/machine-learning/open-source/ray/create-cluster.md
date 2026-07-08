---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster
title: Create a Ray cluster on Gemini Enterprise Agent Platform
description: Create a Ray cluster on Gemini Enterprise Agent Platform using either the {{dynamic_data.site_values.cloud_name_short}} console or the Agent Platform SDK for Python.
data_source: docs.cloud.google.com
---

> To see an example of getting started with Gemma on Ray on , run the "Get started with Gemma on Ray on " notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/model_garden/model_garden_gemma_fine_tuning_batch_deployment_on_rov.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fcommunity%2Fmodel_garden%2Fmodel_garden_gemma_fine_tuning_batch_deployment_on_rov.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fcommunity%2Fmodel_garden%2Fmodel_garden_gemma_fine_tuning_batch_deployment_on_rov.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/model_garden/model_garden_gemma_fine_tuning_batch_deployment_on_rov.ipynb)

This document provides instructions for setting up a Ray cluster on Gemini Enterprise Agent Platform to meet various needs. For example, to build your image, see [Custom image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#custom-image) . Some enterprises can use private networking. This document covers [Private Service Connect interface for Ray on Vertex AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#use-psc-i-egress) . Another use case involves accessing remote files as if they were local (see [Ray on Agent Platform Network File System](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#rov-on-nfs) ).

## Overview

Topics covered here include:

  - [creating a Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#create-ray-cluster)
  - [managing the lifecycle of a Ray cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#lifecycle-management)
  - [creating a custom image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#custom-image)
  - [setting up Private and public connectivity (VPC)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#private-and-public-connectivity)
  - [using Private Service Connect interface for Ray on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#use-psc-i-egress)
  - [setting up Ray on Agent Platform Network File System (NFS)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#rov-on-nfs)
  - [setting up a Ray Dashboard and Interactive Shell with VPC-SC + VPC Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#workaround)

## Create a Ray cluster

You can use the Google Cloud console or the Agent Platform SDK for Python to create a Ray cluster. A cluster can have up to 2,000 nodes. An upper limit of 1,000 nodes exists within one worker pool . No limit exists on the number of worker pools, but a large number of worker pools, such as 1,000 worker pools with one node each, can negatively affect cluster performance.

Before you begin, read the [Ray on Gemini Enterprise Agent Platform overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray) and [set up](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/set-up) all the prerequisite tools you need.

A Ray cluster on Agent Platform might take 10-20 minutes to start up after you create the cluster.

### Console

In accordance with the [OSS Ray best practice](https://docs.ray.io/en/latest/cluster/vms/user-guides/large-cluster-best-practices.html#configuring-the-head-node) recommendation, setting the logical CPU count to 0 on the Ray head node is enforced in order to avoid running any workload on the head node.

1.  In the Google Cloud console, go to the Ray on Agent Platform page.

2.  Click **Create Cluster** to open the **Create Cluster** panel.

3.  For each step in the **Create Cluster** panel, review or replace the default cluster information. Click **Continue** to complete each step:
    
    1.  For **Name and region** , specify a **Name** and choose a **Location** for your cluster.
    
    2.  For **Compute settings** , specify the configuration of the Ray cluster on the Gemini Enterprise Agent Platform's head node, including its machine type, accelerator type and count, disk type and size, and replica count. Optionally, add a custom image URI to specify a custom container image to add Python dependencies not provided by the default container image. See [Custom image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#custom-image) .
        
        Under **Advanced options** , you can:
        
          - Specify your own encryption key.
          - Specify a [custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) .
          - Disable metrics collection, if you don't need to monitor the resource stats of your workload during training.
    
    3.  (Optional) To deploy a private endpoint for your cluster, the recommended method is to use Private Service Connect. For further details, see [Private Service Connect interface for Ray on Vertex AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#use-psc-i-egress) .

4.  Click **Create** .

### Ray on Agent Platform SDK

In accordance with the [OSS Ray best practice](https://docs.ray.io/en/latest/cluster/vms/user-guides/large-cluster-best-practices.html#configuring-the-head-node) recommendation, setting the logical CPU count to 0 on the Ray head node is enforced in order to avoid running any workload on the head node.

> **Note:** Configuring the head node as a GPU node and using it for running the actual training workload is not recommended. Instead, create the head node as a CPU node with a recommended machine type n1-standard-16 (or larger), and use worker nodes as GPU nodes for training and running their code.

From an interactive Python environment, use the following to create the Ray cluster on Gemini Enterprise Agent Platform:

    import ray
    import vertex_ray
    from google.cloud import aiplatform
    from vertex_ray import Resources
    from vertex_ray.util.resources import NfsMount
    
    # Define a default CPU cluster, machine_type is n1-standard-16, 1 head node and 1 worker node
    head_node_type = Resources()
    worker_node_types = [Resources()]
    
    # Or define a GPU cluster.
    head_node_type = Resources(
      machine_type="n1-standard-16",
      node_count=1,
      custom_image="us-docker.pkg.dev/my-project/ray-custom.2-9.py310:latest",  # Optional. When not specified, a prebuilt image is used.
    )
    
    worker_node_types = [Resources(
      machine_type="n1-standard-16",
      node_count=2,  # Must be >= 1
      accelerator_type="NVIDIA_TESLA_T4",
      accelerator_count=1,
      custom_image="us-docker.pkg.dev/my-project/ray-custom.2-9.py310:latest",  # When not specified, a prebuilt image is used.
    )]
    # Optional. Create cluster with Network File System (NFS) setup.
    nfs_mount = NfsMount(
        server="10.10.10.10",
        path="nfs_path",
        mount_point="nfs_mount_point",
    )
    aiplatform.init()
    # Initialize Agent Platform to retrieve projects for downstream operations.
    # Create the Ray cluster on Agent Platform
    CLUSTER_RESOURCE_NAME = vertex_ray.create_ray_cluster(
      head_node_type=head_node_type,
      network=NETWORK, #Optional
      worker_node_types=worker_node_types,
      python_version="3.10",  # Optional
      ray_version="2.47",  # Optional
      cluster_name=CLUSTER_NAME, # Optional
      service_account=SERVICE_ACCOUNT,  # Optional
      enable_metrics_collection=True,  # Optional. Enable metrics collection for monitoring.
      labels=LABELS,  # Optional.
      nfs_mounts=[nfs_mount],  # Optional.
    
    )

Where:

  - CLUSTER\_NAME : A name for the Ray cluster on Gemini Enterprise Agent Platform that must be unique across your project.

  - NETWORK : (Optional) The full name of your VPC network, in the format of ` projects/ PROJECT_ID /global/networks/ VPC_NAME  ` . To set a private endpoint instead of a public endpoint for your cluster, specify a VPC network to use with Ray on Agent Platform. For more information, see [Private and public connectivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#private-and-public-connectivity) .

  - **VPC\_NAME** : Optional: The VPC on which the VM operates.

  - **PROJECT\_ID** : Your Google Cloud project ID. You can find the project ID on the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.

  - **SERVICE\_ACCOUNT** : Optional: The service account to run Ray applications on the cluster. Grant [required roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-create#required_roles) .

  - **LABELS** : (Optional) The labels with user-defined metadata used to organize Ray clusters. Label keys and values can be no longer than 64 characters (Unicode codepoints), and can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See <https://goo.gl/xmQnxf> for more information and examples of labels.

> **Note:** Unlike when using open source Ray, you don't need to use `ray start` or `ray up` to create a Ray cluster on Gemini Enterprise Agent Platform. Gemini Enterprise Agent Platform manages the provisioning of the machines and Ray cluster.

You should see the following output until the status changes to `RUNNING` :

    [Ray on Agent Platform]: Cluster State = State.PROVISIONING
    Waiting for cluster provisioning; attempt 1; sleeping for 0:02:30 seconds
    ...
    [Ray on Agent Platform]: Cluster State = State.RUNNING

Note the following:

  - The first node is the head node.

  - TPU machine types aren't supported.

## Lifecycle management

During the lifecycle of a Ray cluster on Gemini Enterprise Agent Platform, each action associates with a state. The following table summarizes the billing status and management option for each state. The [reference documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.persistentResources#state) provides a definition for each of these states.

| Action                              | State              | Billed?                     | Delete action available? | Cancel action available?          |
| ----------------------------------- | ------------------ | --------------------------- | ------------------------ | --------------------------------- |
| The user creates a cluster          | PROVISIONING       | No                          | No                       | No                                |
| The user manually scales up or down | UPDATING           | Yes, per the real-time size | Yes                      | No                                |
| The cluster runs                    | RUNNING            | Yes                         | Yes                      | Not applicable - you can delete   |
| The cluster autoscales up or down   | UPDATING           | Yes, per the real-time size | Yes                      | No                                |
| The user deletes the cluster        | STOPPING           | No                          | No                       | Not applicable - already stopping |
| The cluster enters an Error state   | ERROR              | No                          | Yes                      | Not applicable - you can delete   |
| Not applicable                      | STATE\_UNSPECIFIED | No                          | Yes                      | Not applicable                    |

## Custom Image (Optional)

[Prebuilt images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#ray) align with most use cases. If you want to build your image, use the Ray on Gemini Enterprise Agent Platform prebuilt images as a base image. See the [Docker documentation](https://docs.cloud.google.com/build/docs/building/build-containers) for how to build your images from a base image.

> **Note:** For details about the available Ray on Agent Platform prebuilt container images, see [Supported versions of Ray on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#ray) .

These base images include an installation of Python, Ubuntu, and Ray. They also include dependencies such as:

  - python-json-logger
  - google-cloud-resource-manager
  - ca-certificates-java
  - libatlas-base-dev
  - liblapack-dev
  - g++, libio-all-perl
  - libyaml-0-2.

> **Note:** If you use an [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/overview) image from the same Google Cloud project in which you used Gemini Enterprise Agent Platform, then no further configuration of permissions is necessary. You can immediately create a Ray cluster Gemini Enterprise Agent Platform that uses your container image.

## Private and public connectivity

By default, Ray on Agent Platform creates a public, secure endpoint for interactive development with the *Ray Client* on Ray clusters on Gemini Enterprise Agent Platform. Use public connectivity for development or ephemeral use cases. This public endpoint is accessible through the internet. Only authorized users who have, at a minimum, [Gemini Enterprise Agent Platform user role permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.user) on the Ray cluster's user project can access the cluster.

If you require a private connection to your cluster or if you use VPC Service Controls, VPC peering is supported for Ray clusters on Gemini Enterprise Agent Platform. Clusters with a private endpoint are only accessible from a client within a VPC network that is peered with Gemini Enterprise Agent Platform.

To set up private connectivity with VPC Peering for Ray on Agent Platform, select a VPC network when you create your cluster. The VPC network requires a [private services connection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering#set-up-psa) between your VPC network and Gemini Enterprise Agent Platform. If you use Ray on Agent Platform in the console, you can set up your private services access connection when [creating the cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#create-ray-cluster) .

If you want to use VPC Service Controls and VPC peering with Ray clusters on Agent Platform, extra set up is required to use the Ray dashboard and interactive shell. Follow the instructions covered in [Ray Dashboard and Interactive Shell with VPC-SC + VPC Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#workaround) to configure the interactive shell setup with VPC-SC and VPC Peering in your user project.

After you create your Ray cluster on Gemini Enterprise Agent Platform, you can connect to the head node using the Agent Platform SDK for Python . The connecting environment, such as a Compute Engine VM or Vertex AI Workbench instance, must be in the VPC network that is peered with Gemini Enterprise Agent Platform. Note that a private services connection has a limited number of IP addresses, which could result in IP address exhaustion . Therefore, we recommend using private connections for long-running clusters.

## Private Service Connect interface for Ray on Gemini Enterprise Agent Platform

Private Service Connect interface egress and Private Service Connect interface ingress are supported on Ray clusters on Gemini Enterprise Agent Platform.

To use Private Service Connect interface egress, follow the instructions in the following section. If VPC Service Controls is not enabled, clusters with Private Service Connect interface egress use the secure public endpoint for ingress with Ray Client.

If VPC Service Controls is enabled, Private Service Connect interface ingress is used by default with Private Service Connect interface egress. To connect with the Ray Client or submit jobs from a notebook for a cluster with Private Service Connect interface ingress, make sure that the notebook is within the user project VPC and subnetwork. For more details on how to set up VPC Service Controls, see [VPC Service Controls with Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls) .

![Diagram of enabling Private Service Connect interface](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/images/psc-i-egress.png)

### Enable Private Service Connect interface

Follow the [setting up your resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup) guide to set up your Private Service Connect interface. After setting up your resources, you're ready to enable Private Service Connect interface on your Ray cluster on Gemini Enterprise Agent Platform.

### Console

1.  While creating your cluster and after specifying **Name and region** and **Compute settings** , the **Networking** option appears.
    
    ![Console specify network](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/images/networking-optional.png)

2.  Set up a network attachment by doing one of the following:
    
      - Use the NETWORK\_ATTACHMENT\_NAME name that you specified when setting up your resources for Private Service Connect.
      - Create a new network attachment by clicking the **Create network attachment** button that appears in the drop-down.
    
    ![Console create new network](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/images/networking-optional-2.png)

3.  Click **Create network attachment** .

4.  In the subtask that appears, specify a name, network, and subnetwork for the new network attachment.
    
    ![Network attachment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/images/network-attachment-new.png)

5.  Click **Create** .

### Ray on Agent Platform SDK

The Ray on Agent Platform SDK is a part of the Agent Platform SDK for Python. To learn how to install or update the Agent Platform SDK for Python, see [Install the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk) . For more information, see the [Agent Platform SDK for Python API reference](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) documentation.

    from google.cloud import aiplatform
    import vertex_ray
    
    # Initialization
    aiplatform.init()
    
    # Create a default cluster with network attachment configuration
    
    psc_config = vertex_ray.PscIConfig(network_attachment=NETWORK_ATTACHMENT_NAME)
    cluster_resource_name = vertex_ray.create_ray_cluster(
       psc_interface_config=psc_config,
    )

Where:

  - NETWORK\_ATTACHMENT\_NAME : The name you specified when setting up your resources for Private Service Connect on your user project.

## Ray on Agent Platform Network File System (NFS)

To make remote files available to your cluster, mount Network File System (NFS) shares. Your jobs can then access remote files as if they were local, which enables high throughput and low latency.

### VPC setup

Two options exist for setting up VPC:

1.  [Create a Private Service Connect interface Network Attachment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup) . (Recommended)
2.  [Set up VPC Network Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering) .

### Set up your NFS instance

> **Note:** If you use a [third-party NFS solution](https://docs.cloud.google.com/architecture/filers-on-compute-engine#filer_solutions_in_marketplace) you can skip this step.

For more details on how to create a Filestore instance, see [Create an instance](https://docs.cloud.google.com/filestore/docs/creating-instances#gcloud) . If you use the Private Service Connect interface method, you don't have to select private service access mode when creating the filestore.

### Use the Network File System (NFS)

To use the Network File System, specify either a **network** or a **network attachment** (recommended).

### Console

1.  In the Networking step of the create page, after specifying either a **network** or a **network attachment** . To do this, click **Add NFS mount** under the Network File System (NFS) section and specify an NFS mount (server, path and mount point).
    
    | Field        | Description                                                                                                                                                                                           |
    | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `server`     | The IP address of your NFS server. This must be a private address in your VPC.                                                                                                                        |
    | `path`       | The NFS share path. This must be an absolute path that begins with `/` .                                                                                                                              |
    | `mountPoint` | The local mount point. This must be a valid UNIX directory name. For example, if the local mount point is `sourceData` , then specify the path `/mnt/nfs/ sourceData` from your training VM instance. |
    

    For more information, see [Where to specify compute resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) .

2.  Specify a server, path, and mount point. ![NFS file system](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/images/network-file-system-mount.png)
    
    > **Note:** You can mount more than one NFS share. Click **Add NFS mount** to specify another NFS share.

3.  Click **Create** . This creates the Ray cluster.

## Ray Dashboard and Interactive Shell with VPC-SC + VPC Peering

1.  Configure `peered-dns-domains` .
    
    ``` 
    {
      VPC_NAME=NETWORK_NAME
      REGION=LOCATION
      gcloud services peered-dns-domains create training-cloud \
      --network=$VPC_NAME \
      --dns-suffix=$REGION.aiplatform-training.cloud.google.com.
    
      # Verify
      gcloud beta services peered-dns-domains list --network $VPC_NAME;
    }
        
    ```
    
      - NETWORK\_NAME : Change to peered network.
    
      - LOCATION : Desired location (for example, `us-central1` ).

2.  Configure `DNS managed zone` .
    
    ``` 
    {
      PROJECT_ID=PROJECT_ID
      ZONE_NAME=$PROJECT_ID-aiplatform-training-cloud-google-com
      DNS_NAME=aiplatform-training.cloud.google.com
      DESCRIPTION=aiplatform-training.cloud.google.com
    
      gcloud dns managed-zones create $ZONE_NAME  \
      --visibility=private  \
      --networks=https://www.googleapis.com/compute/v1/projects/$PROJECT_ID/global/networks/$VPC_NAME  \
      --dns-name=$DNS_NAME  \
      --description="Training $DESCRIPTION"
    }
        
    ```
    
      - PROJECT\_ID : Your project ID. You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.

3.  Record DNS transaction.
    
    ``` 
    {
      gcloud dns record-sets transaction start --zone=$ZONE_NAME
    
      gcloud dns record-sets transaction add \
      --name=$DNS_NAME. \
      --type=A 199.36.153.4 199.36.153.5 199.36.153.6 199.36.153.7 \
      --zone=$ZONE_NAME \
      --ttl=300
    
      gcloud dns record-sets transaction add \
      --name=*.$DNS_NAME. \
      --type=CNAME $DNS_NAME. \
      --zone=$ZONE_NAME \
      --ttl=300
    
      gcloud dns record-sets transaction execute --zone=$ZONE_NAME
    }
        
    ```

4.  Submit a training job with the interactive shell + VPC-SC + VPC Peering enabled.

## Shared Responsibility

Securing your workloads on Gemini Enterprise Agent Platform is a shared responsibility. While Gemini Enterprise Agent Platform regularly upgrades infrastructure configurations to address security vulnerabilities, Gemini Enterprise Agent Platform doesn't automatically upgrade your existing Ray on Vertex AI clusters and persistent resources to avoid preempting running workloads. Therefore, you're responsible for tasks such as the following:

1.  Periodically delete and recreate your Ray on Vertex AI clusters and persistent resources to use the latest infrastructure versions. Gemini Enterprise Agent Platform recommends recreating your clusters and persistent resources at least once every 30 days.
2.  Properly configure any custom images you use.

For more information, see [Shared responsibility](https://docs.cloud.google.com/gemini-enterprise-agent-platform/shared-responsibility) .

## What's next

  - [Develop a Ray application on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/develop-application)
