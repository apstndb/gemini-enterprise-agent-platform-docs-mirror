---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/storage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/storage
title: Storage
description: Deploy Filestore as shared storage for Gemini Enterprise Agent Platform. Configure home directories, VPC peering, and select service tiers.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters, contact your sales representative for access.

Choosing the right storage configuration is critical for the performance and stability of your training cluster. The service integrates with two distinct, high-performance storage solutions:

  - Filestore: A required managed file service that provides the shared `/home` directories for all nodes in the cluster.
  - Google Cloud Managed Lustre: An optional parallel file system designed for extreme I/O performance, ideal for training on massive datasets.

This page provides an overview of their key uses and outlines the specific networking and deployment requirements for a successful integration with your cluster.

## Storage integration for training clusters

Gemini Enterprise Agent Platform training clusters relies on specific, networked storage solutions for its operation. Filestore is required to provide the shared `/home` directories for the cluster, while Managed Lustre is an optional high-performance file system for demanding workloads.

It's critical to configure the networking for these storage services correctly before deploying your cluster.

### Filestore for home directories

This service uses a Filestore instance to provide the shared `/home` directory for the cluster. To ensure proper connectivity, you must create your cloud resources in this specific order:

1.  Create the VPC Network: First, deploy a VPC network configured with the recommended MTU (for example, 8896).
2.  Create the Filestore instance: Next, deploy the Filestore instance *into the VPC you just created* .
3.  Create the training cluster: Finally, deploy the cluster, which will then be able to connect to the Filestore instance within the same network.

### Google Cloud Managed Lustre for high-performance workloads

For workloads that require maximum I/O performance, you can attach a Managed Lustre file system. This service connects to your VPC using Private Service Access.

### Critical networking limitation: No transitive peering

A critical limitation for both Filestore and Google Cloud Managed Lustre is that they don't support transitive peering. This means only resources within the directly connected VPC can access the storage service. For example, if your cluster's VPC (N1) is peered with the storage service, another VPC (N2) that is peered with N1 won't have access.

### Storage integration for training clusters

Gemini Enterprise Agent Platform training clusters relies on specific, networked storage solutions for its operation. Filestore is required to provide the shared `/home` directories for the cluster, while Google Cloud Managed Lustre is an optional high-performance file system for demanding workloads. It's critical to configure the networking for these storage services correctly before deploying your cluster.

### Filestore

### Key uses of Filestore with training clusters

Beyond its role as the mandatory home directory, Filestore provides a flexible way to share data with your cluster.  
**Additional shared storage** : You can attach one or more additional Filestore instances to any node pool. This is useful for providing shared datasets, application binaries, or other common files to your training jobs. When specified in the node pool configuration, training clusters automatically mounts these instances to the `/mnt/filestore` directory on each node.

### Filestore Requirements

A successful Filestore integration with training clusters requires the following configuration:

  - **Enable the API** : The Filestore API must be enabled in your Google Cloud project before you can create the cluster.
  - **Mandatory `/home` Directory** : Every training cluster requires a dedicated Filestore instance to serve as the shared `/home` directory. This instance has specific configuration requirements:
      - **Network** : It must reside in the same VPC network as the cluster's compute and login nodes.
      - **Location** : It must be located in the same region or zone as the cluster.
      - **Configuration** : You must specify the full resource name of this instance in the `orchestrator_spec.slurm_spec.home_directory_storage` field when creating the cluster via the API.

### Configure Filestore storage

Create a zonal or regional Filestore instance in the zone where you want to create the cluster. Vertex AI API requires a Filestore to be attached to the cluster to serve as the `/home` directory. This Filestore has to be in the same zone or region and in the same network as all the compute nodes and login nodes. In the example below, 172.16.10.0/24 is used for the Filestore deployment.

``` 
    SERVICE_TIER=ZONAL # Can use BASIC_SSD

    # Create reserved IP address range
    gcloud compute addresses create CLUSTER_IDfs-ip-range \
        --project=PROJECT_ID \
        --global \
        --purpose=VPC_PEERING \
        --addresses=172.16.10.0 \
        --prefix-length=24 \
        --description="Filestore instance reserved IP range" \
        --network=NETWORK

    # Get the CIDR range
    FS_IP_RANGE=$(
      gcloud compute addresses describe CLUSTER_IDfs-ip-range \
        --global  \
        --format="value[separator=/](address, prefixLength)"
    )

    # Create the Filestore instance
    gcloud filestore instances create FS_INSTANCE_ID \
        --project=PROJECT_ID \
        --location=ZONE \
        --tier=ZONAL \
        --file-share=name="nfsshare",capacity=1024 \
    --network=name=NETWORK,connect-mode=DIRECT_PEERING,reserved-ip-range="${FS_IP_RANGE}"
  
```

### Lustre

Google Cloud Managed Lustre delivers a high-performance, fully managed parallel file system optimized for AI and HPC applications. With multi-petabyte-scale capacity and up to 1 TBps throughput, Managed Lustre facilitates the migration of demanding workloads to the cloud.

Managed Lustre instances live in [zones within regions](https://docs.cloud.google.com/managed-lustre/docs/locations) . A region is a specific geographical location where you can run your resources. Each region is subdivided into several zones. For example, the `us-central1` region in the central United States has zones `us-central1-a` , `us-central1-b` , `us-central1-c` , and `us-central1-f` . For more information, see [Geography and regions](https://docs.cloud.google.com/docs/geography-and-regions) .

To decrease network latency, we recommend creating a Managed Lustre instance in a region and zone that's close to where you plan to use it.

When creating a Managed Lustre instance, you must define the following properties:

  - The name of the instance used by Google Cloud.
  - The file system name used by client-side tools, for example `lfs` .
  - The storage capacity in gibibytes (GiB). Capacity can range from 9,000 GiB to \~8 PiB (7,632,000 GiB). The maximum size of an instance depends on its performance tier.
  - Managed Lustre offers **performance tiers** ranging from 125 MBps per TiB to 1000 MBps per TiB.
  - For best performance, create your instance in the same zone as your training cluster.
  - The VPC network for this instance must be the same one your training cluster uses.

Managed Lustre offers [4 performance tiers](https://docs.cloud.google.com/managed-lustre/docs/performance) , each with a different maximum throughput speed per TiB. Performance tiers also affect the minimum and maximum instance size, and the step size between acceptable capacity values. You cannot change an instance's performance tier after it's been created.

Deploying Managed Lustre requires Private Service Access, which establishes VPC peering between the training cluster's VPC and the VPC hosting Managed Lustre, using a dedicated /20 subnet.

### Configure Managed Lustre instance (optional)

Use Google Cloud Managed Lustre only if you want to use the Managed Lustre in Model Development Service.

Google Cloud Managed Lustre is a fully managed, high-performance parallel file system service on Google Cloud. It's specifically designed to accelerate demanding workloads in AI/Machine Learning and High-Performance Computing (HPC).

For optimal performance when using training clusters, Google Cloud Managed Lustre should be deployed from the same VPC and zone as your training cluster using VPC peering to [services networking](https://docs.cloud.google.com/managed-lustre/docs/vpc#create_and_configure_the_vpc) .

### Create Lustre instance

``` 
    gcloud lustre instances create LUSTRE_INSTANCE_ID \
    --project=PROJECT_ID \
    --location=ZONE \
    --filesystem=lustrefs \
    --per-unit-storage-throughput=500 \
    --capacity-gib=36000 \
    --network=NETWORK_NAME

  
```

## Cloud Storage mounting

As a prerequisite, make sure that the VM service account has the Storage Object User role.

### Default mount

Vertex AI training clusters uses Cloud Storage FUSE to dynamically mount your Cloud Storage buckets on all login and compute nodes, making them accessible under the `/gcs` directory. Dynamically mounted buckets can't be listed from the root mount point `/gcs` . You can access the dynamically mounted buckets as subdirectories:

> **Note:** Dynamically mounted buckets can't be listed from the root mount point `/gcs` . The bucket name must be specified as part of the operation.

    user@testcluster:$ ls /gcs/your-bucket-name
    user@testcluster:$ cd /gcs/your-bucket-name

### Custom mount

To mount a specific Cloud Storage bucket to a local directory with custom options, use the following command structure by either passing it as part of the startup script on cluster creation, or directly running on the node after the cluster is created.

    sudo mkdir -p $MOUNT_DIR
    echo "$GCS_BUCKET $MOUNT_DIR gcsfuse $OPTION_1,$OPTION_2,..." | sudo tee -a /etc/fstab
    sudo mount -a

For example, to mount the bucket `mtdata` to the `/data` directory, use the following command:

    sudo mkdir -p /data
    echo "mtdata /data gcsfuse defaults,_netdev,implicit_dirs,allow_other,dir_mode=777,file-mode=777,metadata_cache_negative_ttl_secs=0,metadata_cache_ttl_secs=-1,stat_cache_max_size_mb=-1,type_cache_max_size_mb=-1,enable_streaming_writes=true" | sudo tee -a /etc/fstab
    sudo mount -a

For a fully automated and consistent setup, include your custom mount scripts within the cluster's startup scripts. This practice ensures that your Cloud Storage buckets are automatically mounted across all nodes on startup, eliminating the need for manual configuration.

For additional configuration recommendations tailored to AI/ML workloads, see the [Performance tuning best practices guide](https://docs.cloud.google.com/storage/docs/cloud-storage-fuse/performance) . It provides specific guidance for optimizing Cloud Storage FUSE for training, inference, and checkpointing.

## What's next

The next steps focus on using your cluster effectively for large-scale training.

  - Adapt your code for distributed training: To take full advantage of a multi-node cluster and high-performance storage, adapt your training code for a distributed environment.
      - [Learn about distributed training on Vertex AI](https://docs.cloud.google.com/vertex-ai/machine-learning/training/distributed-training)
  - Orchestrate your jobs with Gemini Enterprise Agent Platform Pipelines: For production workflows, automate the process of data preparation, job submission, and model registration using Agent Platform Pipelines.
      - [Run a custom training job in a pipeline](https://docs.cloud.google.com/vertex-ai/docs/pipelines/run-pipeline#run_a_custom_training_job_in_a_pipeline)
  - Monitor and debug your training jobs: Track the progress and resource utilization of your distributed training jobs to identify and resolve issues.
      - [Monitor training jobs on Vertex AI](https://docs.cloud.google.com/vertex-ai/docs/general/monitoring-metrics)
