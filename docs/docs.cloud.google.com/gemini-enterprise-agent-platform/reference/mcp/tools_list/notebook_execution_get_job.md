---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_get_job
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_get_job
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `notebook_execution_get_job`

Describes a Colab Enterprise notebook execution job. Use this to retrieve details and status for a specific execution. Format: 'projects/{project_id}/locations/{region}/notebookExecutionJobs/{notebook_execution_job_id}'. CRITICAL: For {region}, use the region specified in the current context. If no region is specified, prompt the user for one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `notebook_execution_get_job` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "notebook_execution_get_job",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for \[NotebookService.GetNotebookExecutionJob\]

### GetNotebookExecutionJobRequest

**JSON representation**

```
{
  "name": string,
  "view": enum (NotebookExecutionJobView)
}
```

| Fields |                                                                                                                                                                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. The name of the NotebookExecutionJob resource.                                                                                                                                                                                               |
| `view` | `enum ( `[`NotebookExecutionJobView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_get_job#Input.Schema.NotebookExecutionJobView)` )` Optional. The NotebookExecutionJob view. Defaults to BASIC. |

### NotebookExecutionJobView

Views for Get/List NotebookExecutionJob

| Enums                                     |                                                        |
|-------------------------------------------|--------------------------------------------------------|
| `NOTEBOOK_EXECUTION_JOB_VIEW_UNSPECIFIED` | When unspecified, the API defaults to the BASIC view.  |
| `NOTEBOOK_EXECUTION_JOB_VIEW_BASIC`       | Includes all fields except for direct notebook inputs. |
| `NOTEBOOK_EXECUTION_JOB_VIEW_FULL`        | Includes all fields.                                   |

## Output Schema

NotebookExecutionJob represents an instance of a notebook execution.

### NotebookExecutionJob

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "executionTimeout": string,
  "scheduleResourceName": string,
  "jobState": enum (JobState),
  "status": {
    object (Status)
  },
  "createTime": string,
  "updateTime": string,
  "labels": {
    string: string,
    ...
  },
  "kernelName": string,
  "encryptionSpec": {
    object (EncryptionSpec)
  },

  // Union field notebook_source can be only one of the following:
  "dataformRepositorySource": {
    object (DataformRepositorySource)
  },
  "gcsNotebookSource": {
    object (GcsNotebookSource)
  },
  "directNotebookSource": {
    object (DirectNotebookSource)
  }
  // End of list of possible types for union field notebook_source.

  // Union field environment_spec can be only one of the following:
  "notebookRuntimeTemplateResourceName": string,
  "customEnvironmentSpec": {
    object (CustomEnvironmentSpec)
  }
  // End of list of possible types for union field environment_spec.

  // Union field execution_sink can be only one of the following:
  "gcsOutputUri": string
  // End of list of possible types for union field execution_sink.

  // Union field execution_identity can be only one of the following:
  "executionUser": string,
  "serviceAccount": string
  // End of list of possible types for union field execution_identity.

  // Union field runtime_environment can be only one of the following:
  "workbenchRuntime": {
    object (WorkbenchRuntime)
  }
  // End of list of possible types for union field runtime_environment.
}
```

| Fields                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                                                | `string` Output only. The resource name of this NotebookExecutionJob. Format: `projects/{project_id}/locations/{location}/notebookExecutionJobs/{job_id}`                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `displayName`                                                                                                                                                                                         | `string` The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `executionTimeout`                                                                                                                                                                                    | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Max running time of the execution job in seconds (default 86400s / 24 hrs). A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .                                                                                                                                                                                                                                                                                                                            |
| `scheduleResourceName`                                                                                                                                                                                | `string` The Schedule resource name if this job is triggered by one. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `jobState`                                                                                                                                                                                            | `enum ( `[`JobState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.JobState)` )` Output only. The state of the NotebookExecutionJob.                                                                                                                                                                                                                                                                                                                                                                                                |
| `status`                                                                                                                                                                                              | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated.                                                                                                                                                                                                                                                                                                 |
| `createTime`                                                                                                                                                                                          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this NotebookExecutionJob was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                      |
| `updateTime`                                                                                                                                                                                          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this NotebookExecutionJob was most recently updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                        |
| `labels`                                                                                                                                                                                              | `map (key: string, value: string)` The labels with user-defined metadata to organize NotebookExecutionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `kernelName`                                                                                                                                                                                          | `string` The name of the kernel to use during notebook execution. If unset, the default kernel is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `encryptionSpec`                                                                                                                                                                                      | `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec)` )` Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the [`NotebookRuntimeTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookRuntimeTemplate) has an encryption spec.                                                                                              |
| Union field `notebook_source` . The input notebook. `notebook_source` can be only one of the following:                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `dataformRepositorySource`                                                                                                                                                                            | `object ( `[`DataformRepositorySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.DataformRepositorySource)` )` The Dataform Repository pointing to a single file notebook repository.                                                                                                                                                                                                                                                                                                                               |
| `gcsNotebookSource`                                                                                                                                                                                   | `object ( `[`GcsNotebookSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.GcsNotebookSource)` )` The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`                                                                                                                                                                                                                                                                                                                        |
| `directNotebookSource`                                                                                                                                                                                | `object ( `[`DirectNotebookSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.DirectNotebookSource)` )` The contents of an input notebook file.                                                                                                                                                                                                                                                                                                                                                                      |
| Union field `environment_spec` . The compute config to use for an execution job. `environment_spec` can be only one of the following:                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `notebookRuntimeTemplateResourceName`                                                                                                                                                                 | `string` The NotebookRuntimeTemplate to source compute configuration from.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `customEnvironmentSpec`                                                                                                                                                                               | `object ( `[`CustomEnvironmentSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.CustomEnvironmentSpec)` )` The custom compute configuration for an execution job.                                                                                                                                                                                                                                                                                                                                                     |
| Union field `execution_sink` . The location to store the notebook execution result. `execution_sink` can be only one of the following:                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `gcsOutputUri`                                                                                                                                                                                        | `string` The Cloud Storage location to upload the result to. Format: `gs://bucket-name`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `execution_identity` . The identity to run the execution as. `execution_identity` can be only one of the following:                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `executionUser`                                                                                                                                                                                       | `string` The user email to run the execution as. Only supported by Colab runtimes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `serviceAccount`                                                                                                                                                                                      | `string` The service account to run the execution as.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Union field `runtime_environment` . Runtime environment for the notebook execution job. If unspecified, the default runtime of Colab is used. `runtime_environment` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `workbenchRuntime`                                                                                                                                                                                    | `object ( `[`WorkbenchRuntime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.WorkbenchRuntime)` )` The Workbench runtime configuration to use for the notebook execution.                                                                                                                                                                                                                                                                                                                                               |

### DataformRepositorySource

**JSON representation**

```
{
  "dataformRepositoryResourceName": string,
  "commitSha": string
}
```

| Fields                           |                                                                                                                                          |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| `dataformRepositoryResourceName` | `string` The resource name of the Dataform Repository. Format: `projects/{project_id}/locations/{location}/repositories/{repository_id}` |
| `commitSha`                      | `string` The commit SHA to read repository with. If unset, the file will be read at HEAD.                                                |

### GcsNotebookSource

**JSON representation**

```
{
  "uri": string,
  "generation": string
}
```

| Fields       |                                                                                                                                                                                         |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uri`        | `string` The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`                                                                                    |
| `generation` | `string` The version of the Cloud Storage object to read. If unset, the current version of the object is read. See <https://cloud.google.com/storage/docs/metadata#generation-number> . |

### DirectNotebookSource

**JSON representation**

```
{
  "content": string
}
```

| Fields    |                                                                                                                                                                         |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `content` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The base64-encoded contents of the input notebook file. A base64-encoded string. |

### CustomEnvironmentSpec

**JSON representation**

```
{
  "machineSpec": {
    object (MachineSpec)
  },
  "persistentDiskSpec": {
    object (PersistentDiskSpec)
  },
  "networkSpec": {
    object (NetworkSpec)
  },
  "shieldedInstanceConfig": {
    object (ShieldedInstanceConfig)
  }
}
```

| Fields                   |                                                                                                                                                                                                                                                                                           |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineSpec`            | `object ( `[`MachineSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.MachineSpec)` )` The specification of a single machine for the execution job.                           |
| `persistentDiskSpec`     | `object ( `[`PersistentDiskSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.PersistentDiskSpec)` )` The specification of a persistent disk to attach for the execution job.  |
| `networkSpec`            | `object ( `[`NetworkSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NetworkSpec)` )` The network configuration to use for the execution job.                                |
| `shieldedInstanceConfig` | `object ( `[`ShieldedInstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.ShieldedInstanceConfig)` )` Optional. Shielded VM configuration (for example, Secure Boot) for the execution VM. |

### MachineSpec

**JSON representation**

```
{
  "machineType": string,
  "acceleratorType": enum (AcceleratorType),
  "acceleratorCount": integer,
  "gpuPartitionSize": string,
  "tpuTopology": string,
  "reservationAffinity": {
    object (ReservationAffinity)
  }
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineType`         | `string` Immutable. The type of the machine. See the [list of machine types supported for prediction](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#machine-types) See the [list of machine types supported for custom training](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . For `DeployedModel` this field is optional, and the default value is `n1-standard-2` . For `BatchPredictionJob` or as part of `WorkerPoolSpec` this field is required.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `acceleratorType`     | `enum ( `[`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.AcceleratorType)` )` Immutable. The type of accelerator(s) that may be attached to the machine as per `accelerator_count` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `acceleratorCount`    | `integer` The number of accelerators to attach to the machine. For [accelerator optimized machine types](https://cloud.google.com/compute/docs/accelerator-optimized-machines) , One may set the accelerator_count from 1 to N for machine with N GPUs. If accelerator_count is less than or equal to N / 2, Agent Platform co-schedules the replicas of the model into the same VM to save cost. For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set accelerator_count to 1 to 8. If accelerator_count is 1, 2, 3, or 4, Agent Platform co-schedules 8, 4, 2, or 2 replicas of the model into the same VM to save cost. When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM. Note that the feature is not compatible with \[multihost_gpu_node_count\]\[\]. When multihost_gpu_node_count is set, the co-scheduling will not be enabled. |
| `gpuPartitionSize`    | `string` Optional. Immutable. The Nvidia GPU partition size. When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu_partition_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances. The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes. If set, the accelerator_count should be set to 1.                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `tpuTopology`         | `string` Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu_topology: "2x2x1").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `reservationAffinity` | `object ( `[`ReservationAffinity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.ReservationAffinity)` )` Optional. Immutable. Configuration controlling how this resource pool consumes reservation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### ReservationAffinity

**JSON representation**

```
{
  "reservationAffinityType": enum (Type),
  "key": string,
  "values": [
    string
  ]
}
```

| Fields                    |                                                                                                                                                                                                                                       |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservationAffinityType` | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.Type)` )` Required. Specifies the reservation affinity type. |
| `key`                     | `string` Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.  |
| `values[]`                | `string` Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.                                                                            |

### PersistentDiskSpec

**JSON representation**

```
{
  "diskType": string,
  "diskSizeGb": string
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `diskType`   | `string` Type of the disk (default is "pd-standard"). Valid values: "pd-ssd" (Persistent Disk Solid State Drive) "pd-standard" (Persistent Disk Hard Disk Drive) "pd-balanced" (Balanced Persistent Disk) "pd-extreme" (Extreme Persistent Disk) "hyperdisk-balanced" (Hyperdisk Balanced) "hyperdisk-extreme" (Hyperdisk Extreme) "hyperdisk-balanced-high-availability" (Hyperdisk Balanced High Availability) "hyperdisk-ml" (Hyperdisk ML) "hyperdisk-throughput" (Hyperdisk Throughput) |
| `diskSizeGb` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Size in GB of the disk (default is 100GB).                                                                                                                                                                                                                                                                                                                                                            |

### NetworkSpec

**JSON representation**

```
{
  "enableInternetAccess": boolean,
  "network": string,
  "subnetwork": string
}
```

| Fields                 |                                                                                                                                                  |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableInternetAccess` | `boolean` Whether to enable public internet access. Default false.                                                                               |
| `network`              | `string` The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks)            |
| `subnetwork`           | `string` The name of the subnet that this instance is in. Format: `projects/{project_id_or_number}/regions/{region}/subnetworks/{subnetwork_id}` |

### ShieldedInstanceConfig

**JSON representation**

```
{
  "enableSecureBoot": boolean,
  "enableVtpm": boolean,
  "enableIntegrityMonitoring": boolean
}
```

| Fields                      |                                                                                           |
|-----------------------------|-------------------------------------------------------------------------------------------|
| `enableSecureBoot`          | `boolean` Optional. Whether the VM instance has Secure Boot enabled. Disabled by default. |
| `enableVtpm`                | `boolean` Optional. Whether the VM instance has vTPM enabled.                             |
| `enableIntegrityMonitoring` | `boolean` Optional. Whether the VM instance has integrity monitoring enabled.             |

### WorkbenchRuntime

**JSON representation**

```
{

  // Union field image_environment can be only one of the following:
  "vmImage": {
    object (VmImage)
  },
  "customContainerImage": {
    object (ContainerImage)
  }
  // End of list of possible types for union field image_environment.
}
```

| Fields                                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                                                         |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `image_environment` . The image environment to run the notebook execution in. Optional: if unset, the service defaults to a managed `workbench-instances-2603` VM image (Python 3.12). `image_environment` can be only one of the following: |                                                                                                                                                                                                                                                                                                         |
| `vmImage`                                                                                                                                                                                                                                                | `object ( `[`VmImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.VmImage)` )` A specific Compute Engine VM image to run the notebook on.                                                                       |
| `customContainerImage`                                                                                                                                                                                                                                   | `object ( `[`ContainerImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.ContainerImage)` )` A user-provided container image. The notebook executes inside this container on a managed container-host (COS) VM. |

### VmImage

**JSON representation**

```
{
  "project": string,

  // Union field image can be only one of the following:
  "name": string,
  "family": string
  // End of list of possible types for union field image.
}
```

| Fields                                                                                                      |                                                                                                                 |
|-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| `project`                                                                                                   | `string` Required. The name of the Google Cloud project that this VM image belongs to. Format: `{project_id}` . |
| Union field `image` . The reference to a Compute Engine VM image. `image` can be only one of the following: |                                                                                                                 |
| `name`                                                                                                      | `string` Use this VM image name to find the image.                                                              |
| `family`                                                                                                    | `string` Use this VM image family to find the image; the newest image in this family is used.                   |

### ContainerImage

**JSON representation**

```
{
  "repository": string,
  "tag": string
}
```

| Fields       |                                                                                                                  |
|--------------|------------------------------------------------------------------------------------------------------------------|
| `repository` | `string` Required. The path to the container image repository. For example: `gcr.io/{project_id}/{image_name}` . |
| `tag`        | `string` Optional. The tag of the container image. If unset, defaults to `latest` .                              |

### Duration

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years                                                                                    |
| `nanos`   | `integer` Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive. |

### Status

**JSON representation**

```
{
  "code": integer,
  "message": string,
  "details": [
    {
      "@type": string,
      field1: ...,
      ...
    }
  ]
}
```

| Fields      |                                                                                                                                                                                                                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`      | `integer` The status code, which should be an enum value of `google.rpc.Code` .                                                                                                                                                                                                                              |
| `message`   | `string` A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.                                                                                                      |
| `details[]` | `object` A list of messages that carry the error details. There is a common set of message types for APIs to use. An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` . |

### Any

**JSON representation**

```
{
  "typeUrl": string,
  "value": string
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `typeUrl` | `string` Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name. Example: type.googleapis.com/google.protobuf.StringValue This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them. The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests. All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected. In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs. |
| `value`   | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Holds a Protobuf serialization of the type described by type_url. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### EncryptionSpec

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Required. Resource name of the Cloud KMS key used to protect the resource. The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

### AcceleratorType

Represents a hardware accelerator type.

| Enums                          |                                                                                                                        |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------|
| `ACCELERATOR_TYPE_UNSPECIFIED` | Unspecified accelerator type, which means no accelerator.                                                              |
| `NVIDIA_TESLA_K80`             | Deprecated: Nvidia Tesla K80 GPU has reached end of support, see <https://cloud.google.com/compute/docs/eol/k80-eol> . |
| `NVIDIA_TESLA_P100`            | Nvidia Tesla P100 GPU.                                                                                                 |
| `NVIDIA_TESLA_V100`            | Nvidia Tesla V100 GPU.                                                                                                 |
| `NVIDIA_TESLA_P4`              | Nvidia Tesla P4 GPU.                                                                                                   |
| `NVIDIA_TESLA_T4`              | Nvidia Tesla T4 GPU.                                                                                                   |
| `NVIDIA_TESLA_A100`            | Nvidia Tesla A100 GPU.                                                                                                 |
| `NVIDIA_A100_80GB`             | Nvidia A100 80GB GPU.                                                                                                  |
| `NVIDIA_L4`                    | Nvidia L4 GPU.                                                                                                         |
| `NVIDIA_H100_80GB`             | Nvidia H100 80Gb GPU.                                                                                                  |
| `NVIDIA_H100_MEGA_80GB`        | Nvidia H100 Mega 80Gb GPU.                                                                                             |
| `NVIDIA_H200_141GB`            | Nvidia H200 141Gb GPU.                                                                                                 |
| `NVIDIA_B200`                  | Nvidia B200 GPU.                                                                                                       |
| `NVIDIA_GB200`                 | Nvidia GB200 GPU.                                                                                                      |
| `NVIDIA_RTX_PRO_6000`          | Nvidia RTX Pro 6000 GPU.                                                                                               |
| `TPU_V2`                       | TPU v2.                                                                                                                |
| `TPU_V3`                       | TPU v3.                                                                                                                |
| `TPU_V4_POD`                   | TPU v4.                                                                                                                |
| `TPU_V5_LITEPOD`               | TPU v5.                                                                                                                |

### Type

Identifies a type of reservation affinity.

| Enums                  |                                                                                                                         |
|------------------------|-------------------------------------------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED`     | Default value. This should not be used.                                                                                 |
| `NO_RESERVATION`       | Do not consume from any reserved capacity, only use on-demand.                                                          |
| `ANY_RESERVATION`      | Consume any reservation available, falling back to on-demand.                                                           |
| `SPECIFIC_RESERVATION` | Consume from a specific reservation. When chosen, the reservation must be identified via the `key` and `values` fields. |

### JobState

Describes the state of a job.

| Enums                           |                                                                                                                                                 |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `JOB_STATE_UNSPECIFIED`         | The job state is unspecified.                                                                                                                   |
| `JOB_STATE_QUEUED`              | The job has been just created or resumed and processing has not yet begun.                                                                      |
| `JOB_STATE_PENDING`             | The service is preparing to run the job.                                                                                                        |
| `JOB_STATE_RUNNING`             | The job is in progress.                                                                                                                         |
| `JOB_STATE_SUCCEEDED`           | The job completed successfully.                                                                                                                 |
| `JOB_STATE_FAILED`              | The job failed.                                                                                                                                 |
| `JOB_STATE_CANCELLING`          | The job is being cancelled. From this state the job may only go to either `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` . |
| `JOB_STATE_CANCELLED`           | The job has been cancelled.                                                                                                                     |
| `JOB_STATE_PAUSED`              | The job has been stopped, and can be resumed.                                                                                                   |
| `JOB_STATE_EXPIRED`             | The job has expired.                                                                                                                            |
| `JOB_STATE_UPDATING`            | The job is being updated. Only jobs in the `RUNNING` state can be updated. After updating, the job goes back to the `RUNNING` state.            |
| `JOB_STATE_PARTIALLY_SUCCEEDED` | The job is partially succeeded, some results may be missing due to errors.                                                                      |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
