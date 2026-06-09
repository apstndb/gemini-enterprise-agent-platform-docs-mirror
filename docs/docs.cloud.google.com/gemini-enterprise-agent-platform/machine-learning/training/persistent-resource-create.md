---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-create
title: Create a persistent resource
description: Create a persistent resource for running your Gemini Enterprise Agent Platform serverless training jobs by using the {{dynamic_data.site_values.cloud_name_short}} console, Google Cloud CLI, Agent Platform SDK for Python, or the REST API.
data_source: docs.cloud.google.com
---

When you create a persistent resource, the training service first finds resources from the Compute Engine resource pool based on the specifications you provided, and then provisions a long-running cluster for you. This page shows you how to create a persistent resource for running your serverless training jobs by using the Google Cloud console, Google Cloud CLI, and the REST API.

## Required roles

To get the permission that you need to create a persistent resource, ask your administrator to grant you the [Agent Platform Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.admin) ( `roles/aiplatform.admin` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `aiplatform.persistentResources.create` permission, which is required to create a persistent resource.

You might also be able to get this permission with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create a persistent resource

Select one of the following tabs for instructions on how to create a persistent resource.

### Console

To create a persistent resource by using the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Persistent resources** page.

2.  Click **Create cluster** .

3.  Configure the cluster as follows:
    
      - **Name:** Enter a name for the cluster.
      - **Description:** (Optional) Enter a description of the cluster.
      - **Region:** Select the region where you want to create the cluster.

4.  Click **Continue** .

5.  Configure the compute resources for the cluster as follows:
    
    1.  Click **Worker pool 1** .
    
    2.  Select the tab of the machine family that you want to use and configure the worker pool as follows:
        
        ### General purpose
        
        General purpose VMs offer the best price-performance ratio for a variety of workloads.
        
          - **Series:** Select a machine series.
          - **Machine type:** Select a machine type.
          - **Disk type:** Select **Standard disk** or **SSD disk** .
          - **Disk size:** Enter the size of the disk you want.
          - **Minimum replica count:** Enter the minimum number of replicas to have in the worker pool.
          - **Maximum replica count:** (Optional) Enter the maximum number of replicas allowed in the worker pool. If specified, the worker pool automatically scales the number of replicas up to the configured maximum replica count as needed.
        
        ### Compute optimized
        
        Compute-optimized VMs offer the highest performance per core and are optimized for compute-intensive workloads.
        
          - **Series:** Select a machine series.
          - **Machine type:** Select a machine type.
          - **Disk type:** Select **Standard disk** or **SSD disk** .
          - **Disk size:** Enter the size of the disk you want.
          - **Minimum replica count:** Enter the minimum number of replicas to have in the worker pool.
          - **Maximum replica count:** (Optional) Enter the maximum number of replicas allowed in the worker pool. If specified, the worker pool automatically scales the number of replicas up to the configured maximum replica count as needed.
        
        ### Memory optimized
        
        Memory-optimized VMs are ideal for memory-intensive workloads, offering more memory per core than other machine families, with up to 12 TB of memory.
        
          - **Series:** Select a machine series.
          - **Machine type:** Select a machine type.
          - **Disk type:** Select **Standard disk** or **SSD disk** .
          - **Disk size:** Enter the size of the disk you want.
          - **Minimum replica count:** Enter the minimum number of replicas to have in the worker pool.
          - **Maximum replica count:** (Optional) Enter the maximum number of replicas allowed in the worker pool. If specified, the worker pool automatically scales the number of replicas up to the configured maximum replica count as needed.
        
        ### GPUs
        
        These accelerator-optimized VMs are ideal for massively parallelized Compute Unified Device Architecture (CUDA) compute workloads, such as machine learning (ML) and high performance computing (HPC). This family is the best option for workloads that require GPUs.
        
          - **GPU type:** Select the type of GPU that you want to use.
          - **Number of GPUs:** Enter the number of GPUs you want to use.
          - **Series:** Select a machine series.
          - **Machine type:** Select a machine type.
          - **Disk type:** Select **Standard disk** or **SSD disk** .
          - **Disk size:** Enter the size of the disk you want.
          - **Minimum replica count:** Enter the minimum number of replicas to have in the worker pool.
          - **Maximum replica count:** (Optional) Enter the maximum number of replicas allowed in the worker pool. If specified, the worker pool automatically scales the number of replicas up to the configured maximum replica count as needed.
    
    3.  Click **Done** .
    
    4.  (Optional) To add additional worker pools, click **Add worker pool** .

6.  Click **Create** .

### gcloud

A persistent resource can have one or more resource pools. To create multiple resource pools in a persistent resource, specify multiple `--resource-pool-spec` flags.

Each resource pool can have autoscaling either enabled or disabled. To enable autoscaling, specify `min_replica_count` and `max_replica_count` .

You can specify all resource pool configurations as part of the command-line or use the `--config` flag to specify the path to a YAML file that contains the configurations.

Before using any of the command data below, make the following replacements:

  - PROJECT\_ID : The Project ID of the Google Cloud project where you want to create the persistent resource.

  - LOCATION : The region where you want to create the persistent resource. For a list of supported regions, see [Feature availability](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .

  - PERSISTENT\_RESOURCE\_ID : The ID of the persistent resource.

  - DISPLAY\_NAME : (Optional) The display name of the persistent resource.

  - MACHINE\_TYPE : The type of VM to use. For a list of supported VMs, see [Machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . This field corresponds to the `machineSpec.machineType` field in the `ResourcePool` API message.

  - ACCELERATOR\_TYPE : (Optional) The type of GPU to attach to each VM in the resource pool. For a list of supported GPUs, see [GPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_gpus) . This field corresponds to the `machineSpec.acceleratorType` field in the `ResourcePool` API message.

  - ACCELERATOR\_COUNT : (Optional) The number of GPUs to attach to each VM in the resource pool. The default the value is `1` . This field corresponds to the `machineSpec.acceleratorCount` field in `ResourcePool` API message.

  - REPLICA\_COUNT : The number of replicas to create when creating this resource pool. This field corresponds to the `replicaCount` field in the `ResourcePool` API message. This field is required if you're not specifying MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT .

  - MIN\_REPLICA\_COUNT : (Optional) The minimum number of replicas that autoscaling can scale down to for this resource pool. Both MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT are required to enable autoscaling on this resource pool.

  - MAX\_REPLICA\_COUNT : (Optional) The maximum number of replicas that autoscaling can scale up to for this resource pool. Both MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT are required to enable autoscaling on this resource pool.

  - BOOT\_DISK\_TYPE : (Optional) The type of disk to use for as the boot disk of each VM in the resource pool. This field corresponds to the `diskSpec.bootDiskType` field in the `ResourcePool` API message. Acceptable values include the following:
    
      - `pd-standard` (default)
      - `pd-ssd`

  - BOOT\_DISK\_SIZE\_GB : (Optional) The disk size in GiB for the boot disk of each VM in the resource pool. Acceptable values are `100` (default) to `64000` . This field corresponds to the `diskSpec.bootDiskSizeGb` field in the `ResourcePool` API message.

  - CONFIG : Path to the persistent resource YAML configuration file. This file should contain a list of ResourcePool. If an option is specified in both the configuration file and the command-line arguments, the command-line arguments override the configuration file. Note that keys with underscores are invalid.
    
    Example YAML configuration file:
    
    ``` 
    resourcePoolSpecs:
      machineSpec:
        machineType: n1-standard-4
      replicaCount: 1
        
    ```

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources create \
        --persistent-resource-id=PERSISTENT_RESOURCE_ID \
        --display-name=DISPLAY_NAME \
        --project=PROJECT_ID \
        --region=LOCATION \
        --resource-pool-spec="replica-count=REPLICA_COUNT,min-replica-count=MIN_REPLICA_COUNT,max-replica-count=MAX_REPLICA_COUNT,machine-type=MACHINE_TYPE,accelerator-type=ACCELERATOR_TYPE,accelerator-count=ACCELERATOR_COUNT,disk-type=BOOT_DISK_TYPE,disk-size=BOOT_DISK_SIZE_GB"

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources create `
        --persistent-resource-id=PERSISTENT_RESOURCE_ID `
        --display-name=DISPLAY_NAME `
        --project=PROJECT_ID `
        --region=LOCATION `
        --resource-pool-spec="replica-count=REPLICA_COUNT,min-replica-count=MIN_REPLICA_COUNT,max-replica-count=MAX_REPLICA_COUNT,machine-type=MACHINE_TYPE,accelerator-type=ACCELERATOR_TYPE,accelerator-count=ACCELERATOR_COUNT,disk-type=BOOT_DISK_TYPE,disk-size=BOOT_DISK_SIZE_GB"

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources create ^
        --persistent-resource-id=PERSISTENT_RESOURCE_ID ^
        --display-name=DISPLAY_NAME ^
        --project=PROJECT_ID ^
        --region=LOCATION ^
        --resource-pool-spec="replica-count=REPLICA_COUNT,min-replica-count=MIN_REPLICA_COUNT,max-replica-count=MAX_REPLICA_COUNT,machine-type=MACHINE_TYPE,accelerator-type=ACCELERATOR_TYPE,accelerator-count=ACCELERATOR_COUNT,disk-type=BOOT_DISK_TYPE,disk-size=BOOT_DISK_SIZE_GB"

You should receive a response similar to the following:

    Using endpoint [https://us-central1-aiplatform.googleapis.com/]
    Operation to create PersistentResource [projects/123456789012/locations/us-central1/persistentResources/mypersistentresource/operations/1234567890123456789] is submitted successfully.
    
    You may view the status of your PersistentResource create operation with the command
    
      $ gcloud ai operations describe projects/sample-project/locations/us-central1/operations/1234567890123456789

Example `gcloud` command:

    gcloud ai persistent-resources create \
        --persistent-resource-id=my-persistent-resource \
        --region=us-central1 \
        --resource-pool-spec="min-replica-count=4,max-replica-count=12,machine-type=n1-highmem-2,accelerator-type=NVIDIA_TESLA_T4,accelerator-count=1,disk-type=pd-standard,disk-size=200" \
        --resource-pool-spec="replica-count=4,machine-type=n1-standard-4"

#### Advanced `gcloud` configurations

If you want to specify configuration options that are not available in the preceding examples, you can use the `--config` flag to specify the path to a `config.yaml` file in your local environment that contains the fields of [`persistentResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.persistentResources) . For example:

    gcloud ai persistent-resources create \
        --persistent-resource-id=PERSISTENT_RESOURCE_ID \
        --project=PROJECT_ID \
        --region=LOCATION \
        --config=CONFIG

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

To create a [persistent resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PersistentResource) that you can use with a pipeline run, set the `enable_custom_service_account` parameter to `True` in the `ResourceRuntimeSpec` object while creating the persistent resource.

    from google.cloud.aiplatform.preview import persistent_resource
    from google.cloud.aiplatform_v1beta1.types.persistent_resource import ResourcePool
    from google.cloud.aiplatform_v1beta1.types.machine_resources import MachineSpec
    
    # Create the persistent resource. This method returns the created resource.
    
    my_example_resource = persistent_resource.PersistentResource.create(
        persistent_resource_id='PERSISTENT_RESOURCE_ID',
        display_name='DISPLAY_NAME',
        resource_pools=[
            ResourcePool(
                machine_spec=MachineSpec(
                    machine_type='MACHINE_TYPE'
                ),
                replica_count=REPLICA_COUNT
            )
        ],
        enable_custom_service_account=True,
    )
    
    # Setting `sync` to `False` makes the method is non-blocking and the resource
    # object returned syncs when the method completes.
    
    SYNC=False
    
    if not SYNC:
        my_example_resource.wait()

Replace the following:

  - PERSISTENT\_RESOURCE\_ID : A unique, user-defined ID for the persistent resource. It must start with a letter, end with a letter or number, and contain only lowercase letters, numbers, and hyphens (-).
  - DISPLAY\_NAME : Optional. The display name of the persistent resource.
  - MACHINE\_TYPE : The type of virtual machine (VM) to use. For a list of supported VMs, see [Machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . This field corresponds to the `machineSpec.machineType` field in the
  - REPLICA\_COUNT : The number of replicas to create when creating this resource pool.

### REST

A persistent resource can have one or more resource pools ( `machine_spec` ), and each resource pool can have autoscaling either enabled or disabled.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : The Project ID of the Google Cloud project where you want to create the persistent resource.
  - LOCATION : The region where you want to create the persistent resource. For a list of supported regions, see [Feature availability](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .
  - PERSISTENT\_RESOURCE\_ID : The ID of the persistent resource.
  - DISPLAY\_NAME : (Optional) The display name of the persistent resource.
  - MACHINE\_TYPE : The type of VM to use. For a list of supported VMs, see [Machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . This field corresponds to the `machineSpec.machineType` field in the `ResourcePool` API message.
  - ACCELERATOR\_TYPE : (Optional) The type of GPU to attach to each VM in the resource pool. For a list of supported GPUs, see [GPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_gpus) . This field corresponds to the `machineSpec.acceleratorType` field in the `ResourcePool` API message.
  - ACCELERATOR\_COUNT : (Optional) The number of GPUs to attach to each VM in the resource pool. The default the value is `1` . This field corresponds to the `machineSpec.acceleratorCount` field in `ResourcePool` API message.
  - REPLICA\_COUNT : The number of replicas to create when creating this resource pool. This field corresponds to the `replicaCount` field in the `ResourcePool` API message. This field is required if you're not specifying MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT .
  - MIN\_REPLICA\_COUNT : (Optional) The minimum number of replicas that autoscaling can scale down to for this resource pool. Both MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT are required to enable autoscaling on this resource pool.
  - MAX\_REPLICA\_COUNT : (Optional) The maximum number of replicas that autoscaling can scale up to for this resource pool. Both MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT are required to enable autoscaling on this resource pool.
  - BOOT\_DISK\_TYPE : (Optional) The type of disk to use for as the boot disk of each VM in the resource pool. This field corresponds to the `diskSpec.bootDiskType` field in the `ResourcePool` API message. Acceptable values include the following:
      - `pd-standard` (default)
      - `pd-ssd`
  - BOOT\_DISK\_SIZE\_GB : (Optional) The disk size in GiB for the boot disk of each VM in the resource pool. Acceptable values are `100` (default) to `64000` . This field corresponds to the `diskSpec.bootDiskSizeGb` field in the `ResourcePool` API message.

HTTP method and URL:

    POST https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources?persistent_resource_id=PERSISTENT_RESOURCE_ID

Request JSON body:

    {
      "display_name": "DISPLAY_NAME",
      "resource_pools": [
        {
          "machine_spec": {
            "machine_type": "MACHINE_TYPE",
            "accelerator_type": "ACCELERATOR_TYPE",
            "accelerator_count": ACCELERATOR_COUNT
          },
          "replica_count": REPLICA_COUNT,
          "autoscaling_spec": {
            "min_replica_count": MIN_REPLICA_COUNT,
            "max_replica_count": MAX_REPLICA_COUNT
          },
          "disk_spec": {
            "boot_disk_type": "BOOT_DISK_TYPE",
            "boot_disk_size_gb": BOOT_DISK_SIZE_GB
          }
        }
      ]
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
      "display_name": "DISPLAY_NAME",
      "resource_pools": [
        {
          "machine_spec": {
            "machine_type": "MACHINE_TYPE",
            "accelerator_type": "ACCELERATOR_TYPE",
            "accelerator_count": ACCELERATOR_COUNT
          },
          "replica_count": REPLICA_COUNT,
          "autoscaling_spec": {
            "min_replica_count": MIN_REPLICA_COUNT,
            "max_replica_count": MAX_REPLICA_COUNT
          },
          "disk_spec": {
            "boot_disk_type": "BOOT_DISK_TYPE",
            "boot_disk_size_gb": BOOT_DISK_SIZE_GB
          }
        }
      ]
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources?persistent_resource_id=PERSISTENT_RESOURCE_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
      "display_name": "DISPLAY_NAME",
      "resource_pools": [
        {
          "machine_spec": {
            "machine_type": "MACHINE_TYPE",
            "accelerator_type": "ACCELERATOR_TYPE",
            "accelerator_count": ACCELERATOR_COUNT
          },
          "replica_count": REPLICA_COUNT,
          "autoscaling_spec": {
            "min_replica_count": MIN_REPLICA_COUNT,
            "max_replica_count": MAX_REPLICA_COUNT
          },
          "disk_spec": {
            "boot_disk_type": "BOOT_DISK_TYPE",
            "boot_disk_size_gb": BOOT_DISK_SIZE_GB
          }
        }
      ]
    }
    '@  | Out-File -FilePath request.json -Encoding utf8

Then execute the following command to send your REST request:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources?persistent_resource_id=PERSISTENT_RESOURCE_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/123456789012/locations/us-central1/persistentResources/mypersistentresource/operations/1234567890123456789",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreatePersistentResourceOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-02-08T21:17:15.009668Z",
          "updateTime": "2023-02-08T21:17:15.009668Z"
        }
      }
    }

### Resource stockout

There could be stockout for scarce resources like A100 GPUs, which can lead to persistent resource creation failure when no resource is available in the region you specified. In this case, you can try to reduce the number of replicas, change to different accelerator type, try again during non-peak hours, or try another region.

## Shared Responsibility

Securing your workloads on Vertex AI is a shared responsibility. While Vertex AI regularly upgrades infrastructure configurations to address security vulnerabilities, Vertex AI doesn't automatically upgrade your existing Ray on Vertex AI clusters and persistent resources to avoid preempting running workloads. Therefore, you're responsible for tasks such as the following:

1.  Periodically delete and recreate your Ray on Vertex AI clusters and persistent resources to use the latest infrastructure versions. Vertex AI recommends recreating your clusters and persistent resources at least once every 30 days.
2.  Properly configure any custom images you use.

For more information, see [Shared responsibility](https://docs.cloud.google.com/vertex-ai/docs/shared-responsibility) .

## What's next

  - [Run training jobs on a persistent resource](https://docs.cloud.google.com/vertex-ai/machine-learning/training/persistent-resource-train) .
  - [Learn about persistent resource](https://docs.cloud.google.com/vertex-ai/machine-learning/training/persistent-resource-overview) .
  - [Get information about a persistent resource](https://docs.cloud.google.com/vertex-ai/machine-learning/training/persistent-resource-get) .
  - [Reboot a persistent resource](https://docs.cloud.google.com/vertex-ai/machine-learning/training/persistent-resource-reboot) .
  - [Delete a persistent resource](https://docs.cloud.google.com/vertex-ai/machine-learning/training/persistent-resource-delete) .
