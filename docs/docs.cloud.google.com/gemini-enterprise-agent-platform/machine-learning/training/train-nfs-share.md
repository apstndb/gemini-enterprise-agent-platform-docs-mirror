---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/train-nfs-share
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/train-nfs-share
title: Mount a Network File System share
description: How to mount a Network File System share when running a Vertex AI serverless training job.
data_source: docs.cloud.google.com
---

You can configure your Vertex AI serverless training jobs to mount Network File System (NFS) shares to the container where your code is running. This lets your jobs access remote files as if they were local, enabling high throughput and low latency.

This guide shows how to mount a Network File System share when running a serverless training job.

## Before you begin

1.  Create an NFS share in a [Virtual Private Cloud (VPC)](https://docs.cloud.google.com/vpc/docs/vpc-peering) . Your share must be accessible without authentication.
    
    You can use a first-party managed NFS service like [Filestore](https://docs.cloud.google.com/filestore) or [Google Cloud NetApp Volumes](https://docs.cloud.google.com/netapp/volumes/docs/discover/overview) as your NFS share. If you are using Filestore and plan to use VPC peering for Vertex AI in the next step, select **private service access** as the connect mode when you create an instance. For an example, see [Create instances](https://docs.cloud.google.com/filestore/docs/creating-instances) in the Filestore documentation.

2.  To connect Vertex AI with the VPC that hosts your NFS share, follow the instructions in [Use Private Service Connect interface for Vertex AI](https://docs.cloud.google.com/vertex-ai/machine-learning/training/psc-i-egress) (recommended), or [Set up VPC Network Peering](https://docs.cloud.google.com/vertex-ai/docs/general/vpc-peering) .

## Network File System information for serverless training

When you create a serverless training job that mounts an NFS share, you must specify the following:

  - The name of the network for Vertex AI to access. The way that you specify the network name differs depending on the type of serverless training job. For details, see [Perform serverless training](https://docs.cloud.google.com/vertex-ai/machine-learning/training/using-private-ip#perform-serverless-training) .

  - Your NFS configuration in the [WorkerPoolSpec field](https://docs.cloud.google.com/vertex-ai/reference/rest/v1/CustomJobSpec#workerpoolspec) . Include the following fields:
    
    | Field                  | Description                                                                                                                                                                                          |
    | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `nfsMounts.server`     | The IP address of your NFS server. This must be a private address in your VPC.                                                                                                                       |
    | `nfsMounts.path`       | The NFS share path. This must be an absolute path that begins with `/` .                                                                                                                             |
    | `nfsMounts.mountPoint` | The local mount point. This must be a valid UNIX directory name. For example, if the local mount point is `sourceData` , then specify the path `/mnt/nfs/sourceData` from your training VM instance. |
    

    For more information, see [Where to specify compute resources](https://docs.cloud.google.com/vertex-ai/machine-learning/training/configure-compute#where_to_specify_compute_resources) .

## Example: create a custom job using the gcloud CLI

1.  Follow the steps in [Create a Python training application for a prebuilt container](https://docs.cloud.google.com/vertex-ai/machine-learning/training/create-python-pre-built-container) to build a training application to run on Vertex AI.

2.  Create a file named `config.yaml` that describes the PSA or Private Service Connect interface config mount settings for your training job. Use one of the following formats:

### Private Service Connect interface

> **Preview — Private Service Connect interface**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

1.  To use Private Service Connect interface:
    
        pscInterfaceConfig:
             network_attachment: NETWORK_ATTACHMENT_NAME
        workerPoolSpecs:
            - machineSpec:
                machineType: MACHINE_TYPE
            replicaCount: 1
            pythonPackageSpec:
               executorImageUri: PYTHON_PACKAGE_EXECUTOR_IMAGE_URI or PRE_BUILT_CONTAINER_IMAGE_URI
               packageUris:
               -  PYTHON_PACKAGE_URIS
               pythonModule: PYTHON_MODULE
            nfsMounts:
              - server: NFS_SERVER_IP
              path: NFS_SHARE_NAME
              mountPoint: LOCAL_FOLDER
    
    Replace the following:
    
      - NETWORK\_ATTACHMENT\_NAME : The name of your network attachment.
    
      - MACHINE\_TYPE : The identifier of your virtual machine type.
    
      - PYTHON\_PACKAGE\_EXECUTOR\_IMAGE\_URI or PRE\_BUILT\_CONTAINER\_IMAGE\_URI : The URI of a container image in Artifact Registry that will run the provided Python package. Vertex AI provides a [wide range of executor images with pre-installed packages](https://docs.cloud.google.com/vertex-ai/machine-learning/training/pre-built-containers) to meet users' various use cases.
    
      - PYTHON\_PACKAGE\_URIS : A comma-separated list of Cloud Storage URIs that specify the Python package files that make up the training program and its dependent packages. The maximum number of package URIs is 100.
    
      - PYTHON\_MODULE : The Python module name to run after installing the packages.
    
      - NFS\_SERVER\_IP : The IP address of your NFS server.
    
      - NFS\_SHARE\_NAME : The NFS share path, which is an absolute path that begins with `/` .
    
      - LOCAL\_FOLDER : The local mount point (UNIX directory name).
    
    Make sure that your network name is formatted correctly and that your NFS share exists in the specified network.

2.  Create your custom job and pass your `config.yaml` file to the `--config` parameter.
    
        gcloud ai custom-jobs create \
          --region=LOCATION \
          --display-name=JOB_NAME \
          --config=config.yaml
    
    Replace the following:
    
      - LOCATION : Specify the region to create the job in.
    
      - JOB\_NAME : A name for the custom job.

### VPC peering

1.  Use VPC Peering if you want the job to use VPC Peering/PSA on the job or not.
    
        network: projects/PROJECT_NUMBER/global/networks/NETWORK_NAME
        workerPoolSpecs:
            - machineSpec:
                machineType: MACHINE_TYPE
              replicaCount: 1
              pythonPackageSpec:
                executorImageUri: PYTHON_PACKAGE_EXECUTOR_IMAGE_URI or 
                      PRE_BUILT_CONTAINER_IMAGE_URI
                packageUris:
                  -  PYTHON_PACKAGE_URIS
                pythonModule: PYTHON_MODULE
              nfsMounts:
                - server: NFS_SERVER_IP
                  path: NFS_SHARE_NAME
                  mountPoint: LOCAL_FOLDER
    
    Replace the following:
    
      - PROJECT\_NUMBER : The project ID of your Google Cloud project.
    
      - NETWORK\_NAME : The name of your private or Shared VPC.
    
      - MACHINE\_TYPE : The identifier of your virtual machine type.
    
      - PYTHON\_PACKAGE\_EXECUTOR\_IMAGE\_URI or PRE\_BUILT\_CONTAINER\_IMAGE\_URI : The URI of a container image in Artifact Registry that will run the provided Python package. Vertex AI provides a [wide range of executor images with pre-installed packages](https://docs.cloud.google.com/vertex-ai/machine-learning/training/pre-built-containers) to meet users' various use cases.
    
      - PYTHON\_PACKAGE\_URIS : A comma-separated list of Cloud Storage URIs that specify the Python package files that make up the training program and its dependent packages. The maximum number of package URIs is 100.
    
      - PYTHON\_MODULE : The Python module name to run after installing the packages.
    
      - NFS\_SERVER\_IP : The IP address of your NFS server.
    
      - NFS\_SHARE\_NAME : The NFS share path, which is an absolute path that begins with `/` .
    
      - LOCAL\_FOLDER : The local mount point (UNIX directory name).
    
    Make sure that your network name is formatted correctly and that your NFS share exists in the specified network.

2.  Create your custom job and pass your `config.yaml` file to the `--config` parameter.
    
        gcloud ai custom-jobs create \
          --region=LOCATION \
          --display-name=JOB_NAME \
          --config=config.yaml

Replace the following:

  - LOCATION : Specify the region to create the job in.

  - JOB\_NAME : A name for the custom job.

## Limitations

  - You must mount your NFS share using an IP address that is internal to your VPC; using public URLs isn't allowed.

  - Training jobs mount NFS shares without authentication, and will fail if a username and password are required.
    
    To secure your data, set permissions on your NFS share. If you are using Filestore, see [access control](https://docs.cloud.google.com/filestore/docs/access-control) in the Filestore documentation.

  - You can't run two training jobs that mount NFS shares from different VPC networks at the same time. This is due to the [network peering restriction](https://docs.cloud.google.com/vertex-ai/machine-learning/training/using-private-ip#run_jobs_on_different_networks) .
