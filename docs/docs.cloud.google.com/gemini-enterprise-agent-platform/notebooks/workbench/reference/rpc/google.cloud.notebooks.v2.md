---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v2
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v2
title: Package google.cloud.notebooks.v2
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  NotebookService  ` (interface)
  - `  AcceleratorConfig  ` (message)
  - `  AcceleratorConfig.AcceleratorType  ` (enum)
  - `  AccessConfig  ` (message)
  - `  BootDisk  ` (message)
  - `  CheckInstanceUpgradabilityRequest  ` (message)
  - `  CheckInstanceUpgradabilityResponse  ` (message)
  - `  ConfidentialInstanceConfig  ` (message)
  - `  ConfidentialInstanceConfig.ConfidentialInstanceType  ` (enum)
  - `  Config  ` (message)
  - `  ContainerImage  ` (message)
  - `  CreateInstanceRequest  ` (message)
  - `  DataDisk  ` (message)
  - `  DefaultValues  ` (message)
  - `  DeleteInstanceRequest  ` (message)
  - `  DiagnoseInstanceRequest  ` (message)
  - `  DiagnosticConfig  ` (message)
  - `  DiskEncryption  ` (enum)
  - `  DiskType  ` (enum)
  - `  GPUDriverConfig  ` (message)
  - `  GceSetup  ` (message)
  - `  GetConfigRequest  ` (message)
  - `  GetInstanceRequest  ` (message)
  - `  HealthState  ` (enum)
  - `  ImageRelease  ` (message)
  - `  Instance  ` (message)
  - `  ListInstancesRequest  ` (message)
  - `  ListInstancesResponse  ` (message)
  - `  NetworkInterface  ` (message)
  - `  NetworkInterface.NicType  ` (enum)
  - `  OperationMetadata  ` (message)
  - `  ResetInstanceRequest  ` (message)
  - `  ResizeDiskRequest  ` (message)
  - `  RestoreInstanceRequest  ` (message)
  - `  RollbackInstanceRequest  ` (message)
  - `  ServiceAccount  ` (message)
  - `  ShieldedInstanceConfig  ` (message)
  - `  Snapshot  ` (message)
  - `  StartInstanceRequest  ` (message)
  - `  State  ` (enum)
  - `  StopInstanceRequest  ` (message)
  - `  SupportedValues  ` (message)
  - `  UpdateInstanceRequest  ` (message)
  - `  UpgradeHistoryEntry  ` (message)
  - `  UpgradeHistoryEntry.Action  ` (enum)
  - `  UpgradeHistoryEntry.State  ` (enum)
  - `  UpgradeInstanceRequest  ` (message)
  - `  VmImage  ` (message)

## NotebookService

API v2 service for Workbench Notebooks Instances.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CheckInstanceUpgradability</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CheckInstanceUpgradability(              CheckInstanceUpgradabilityRequest            </code> ) returns ( <code dir="ltr" translate="no">             CheckInstanceUpgradabilityResponse            </code> )</p>
<p>Checks whether a notebook instance is upgradable.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CreateInstance(              CreateInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Creates a new Instance in a given project and location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc DeleteInstance(              DeleteInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Deletes a single Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DiagnoseInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc DiagnoseInstance(              DiagnoseInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Creates a Diagnostic File and runs Diagnostic Tool given an Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetConfig</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetConfig(              GetConfigRequest            </code> ) returns ( <code dir="ltr" translate="no">             Config            </code> )</p>
<p>Returns various configuration parameters.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetInstance(              GetInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Instance            </code> )</p>
<p>Gets details of a single Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListInstances</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ListInstances(              ListInstancesRequest            </code> ) returns ( <code dir="ltr" translate="no">             ListInstancesResponse            </code> )</p>
<p>Lists instances in a given project and location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ResetInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ResetInstance(              ResetInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Resets a notebook instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ResizeDisk</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ResizeDisk(              ResizeDiskRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Resize a notebook instance disk to a higher capacity.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>RestoreInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc RestoreInstance(              RestoreInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>RestoreInstance restores an Instance from a BackupSource.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>RollbackInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc RollbackInstance(              RollbackInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Rollbacks a notebook instance to the previous version.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>StartInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc StartInstance(              StartInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Starts a notebook instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>StopInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc StopInstance(              StopInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Stops a notebook instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpdateInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc UpdateInstance(              UpdateInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>UpdateInstance updates an Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpgradeInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc UpgradeInstance(              UpgradeInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Upgrades a notebook instance to the latest version.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## AcceleratorConfig

An accelerator configuration for a VM instance Definition of a hardware accelerator. Note that there is no check on `type` and `core_count` combinations. TPUs are not supported. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus/#gpus-list) to find a valid combination.

Fields

`type`

`  AcceleratorType  `

Optional. Type of this accelerator.

`core_count`

`int64`

Optional. Count of cores of this accelerator.

## AcceleratorType

Definition of the types of hardware accelerators that can be used on this instance.

Enums

`ACCELERATOR_TYPE_UNSPECIFIED`

Accelerator type is not specified.

`NVIDIA_TESLA_P100`

Accelerator type is Nvidia Tesla P100.

`NVIDIA_TESLA_V100`

Accelerator type is Nvidia Tesla V100.

`NVIDIA_TESLA_P4`

Accelerator type is Nvidia Tesla P4.

`NVIDIA_TESLA_T4`

Accelerator type is Nvidia Tesla T4.

`NVIDIA_TESLA_A100`

Accelerator type is Nvidia Tesla A100 - 40GB.

`NVIDIA_A100_80GB`

Accelerator type is Nvidia Tesla A100 - 80GB.

`NVIDIA_L4`

Accelerator type is Nvidia Tesla L4.

`NVIDIA_H100_80GB`

Accelerator type is Nvidia Tesla H100 - 80GB.

`NVIDIA_H100_MEGA_80GB`

Accelerator type is Nvidia Tesla H100 - MEGA 80GB.

`NVIDIA_H200_141GB`

Accelerator type is Nvidia Tesla H200 - 141GB.

`NVIDIA_TESLA_T4_VWS`

Accelerator type is NVIDIA Tesla T4 Virtual Workstations.

`NVIDIA_TESLA_P100_VWS`

Accelerator type is NVIDIA Tesla P100 Virtual Workstations.

`NVIDIA_TESLA_P4_VWS`

Accelerator type is NVIDIA Tesla P4 Virtual Workstations.

`NVIDIA_B200`

Accelerator type is NVIDIA B200.

## AccessConfig

An access configuration attached to an instance's network interface.

Fields

`external_ip`

`string`

An external IP address associated with this instance. Specify an unused static external IP address available to the project or leave this field undefined to use an IP from a shared ephemeral IP address pool. If you specify a static external IP address, it must live in the same region as the zone of the instance.

## BootDisk

The definition of a boot disk.

Fields

`disk_size_gb`

`int64`

Optional. The size of the boot disk in GB attached to this instance, up to a maximum of 64000 GB (64 TB). If not specified, this defaults to the recommended value of 150GB.

`disk_type`

`  DiskType  `

Optional. Indicates the type of the disk.

`disk_encryption`

`  DiskEncryption  `

Optional. Input only. Disk encryption method used on the boot and data disks, defaults to GMEK.

`kms_key`

`string`

Optional. Input only. The KMS key used to encrypt the disks, only applicable if disk\_encryption is CMEK. Format: `projects/{project_id}/locations/{location}/keyRings/{key_ring_id}/cryptoKeys/{key_id}`

Learn more about using your own encryption keys.

## CheckInstanceUpgradabilityRequest

Request for checking if a notebook instance is upgradeable.

Fields

`notebook_instance`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `notebookInstance` :

  - `notebooks.instances.checkUpgradability`

## CheckInstanceUpgradabilityResponse

Response for checking if a notebook instance is upgradeable.

Fields

`upgradeable`

`bool`

If an instance is upgradeable.

`upgrade_version`

`string`

The version this instance will be upgraded to if calling the upgrade endpoint. This field will only be populated if field upgradeable is true.

`upgrade_info`

`string`

Additional information about upgrade.

`upgrade_image`

`string`

The new image self link this instance will be upgraded to if calling the upgrade endpoint. This field will only be populated if field upgradeable is true.

## ConfidentialInstanceConfig

A set of Confidential Instance options.

Fields

`confidential_instance_type`

`  ConfidentialInstanceType  `

Optional. Defines the type of technology used by the confidential instance.

## ConfidentialInstanceType

The type of confidential instance.

Enums

`CONFIDENTIAL_INSTANCE_TYPE_UNSPECIFIED`

No type specified. Do not use this value.

`SEV`

AMD Secure Encrypted Virtualization.

## Config

Response for getting WbI configurations in a location

Fields

`default_values`

`  DefaultValues  `

Output only. The default values for configuration.

`supported_values`

`  SupportedValues  `

Output only. The supported values for configuration.

`available_images[]`

`  ImageRelease  `

Output only. The list of available images to create a WbI.

`disable_workbench_legacy_creation`

`bool`

Output only. Flag to disable the creation of legacy Workbench notebooks (User-managed notebooks and Google-managed notebooks).

## ContainerImage

Definition of a container image for starting a notebook instance with the environment installed in a container.

Fields

`repository`

`string`

Required. The path to the container image repository. For example: `gcr.io/{project_id}/{image_name}`

`tag`

`string`

Optional. The tag of the container image. If not specified, this defaults to the latest tag.

## CreateInstanceRequest

Request for creating a notebook instance.

Fields

`parent`

`string`

Required. Format: `parent=projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.instances.create`

`instance_id`

`string`

Required. User-defined unique ID of this instance.

`instance`

`  Instance  `

Required. The instance to be created.

`request_id`

`string`

Optional. Idempotent request UUID.

## DataDisk

An instance-attached disk resource.

Fields

`disk_size_gb`

`int64`

Optional. The size of the disk in GB attached to this VM instance, up to a maximum of 64000 GB (64 TB). If not specified, this defaults to 100.

`disk_type`

`  DiskType  `

Optional. Input only. Indicates the type of the disk.

`disk_encryption`

`  DiskEncryption  `

Optional. Input only. Disk encryption method used on the boot and data disks, defaults to GMEK.

`kms_key`

`string`

Optional. Input only. The KMS key used to encrypt the disks, only applicable if disk\_encryption is CMEK. Format: `projects/{project_id}/locations/{location}/keyRings/{key_ring_id}/cryptoKeys/{key_id}`

Learn more about using your own encryption keys.

`resource_policies[]`

`string`

Optional. The resource policies to apply to the data disk.

## DefaultValues

DefaultValues represents the default configuration values.

Fields

`machine_type`

`string`

Output only. The default machine type used by the backend if not provided by the user.

## DeleteInstanceRequest

Request for deleting a notebook instance.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.delete`

`request_id`

`string`

Optional. Idempotent request UUID.

## DiagnoseInstanceRequest

Request for creating a notebook instance diagnostic file.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.diagnose`

`diagnostic_config`

`  DiagnosticConfig  `

Required. Defines flags that are used to run the diagnostic tool

`timeout_minutes`

`int32`

Optional. Maximum amount of time in minutes before the operation times out.

## DiagnosticConfig

Defines flags that are used to run the diagnostic tool

Fields

`gcs_bucket`

`string`

Required. User Cloud Storage bucket location (REQUIRED). Must be formatted with path prefix ( `gs://$GCS_BUCKET` ).

Permissions: User Managed Notebooks: - storage.buckets.writer: Must be given to the project's service account attached to VM. Google Managed Notebooks: - storage.buckets.writer: Must be given to the project's service account or user credentials attached to VM depending on authentication mode.

Cloud Storage bucket Log file will be written to `gs://$GCS_BUCKET/$RELATIVE_PATH/$VM_DATE_$TIME.tar.gz`

`relative_path`

`string`

Optional. Defines the relative storage path in the Cloud Storage bucket where the diagnostic logs will be written: Default path will be the root directory of the Cloud Storage bucket ( `gs://$GCS_BUCKET/$DATE_$TIME.tar.gz` ) Example of full path where Log file will be written: `gs://$GCS_BUCKET/$RELATIVE_PATH/`

`enable_repair_flag`

`bool`

Optional. Enables flag to repair service for instance

`enable_packet_capture_flag`

`bool`

Optional. Enables flag to capture packets from the instance for 30 seconds

`enable_copy_home_files_flag`

`bool`

Optional. Enables flag to copy all `/home/jupyter` folder contents

## DiskEncryption

Definition of the disk encryption options.

Enums

`DISK_ENCRYPTION_UNSPECIFIED`

Disk encryption is not specified.

`GMEK`

Use Google managed encryption keys to encrypt the boot disk.

`CMEK`

Use customer managed encryption keys to encrypt the boot disk.

## DiskType

Possible disk types.

Enums

`DISK_TYPE_UNSPECIFIED`

Disk type not set.

`PD_STANDARD`

Standard persistent disk type.

`PD_SSD`

SSD persistent disk type.

`PD_BALANCED`

Balanced persistent disk type.

`PD_EXTREME`

Extreme persistent disk type.

`HYPERDISK_BALANCED`

Represents the Hyperdisk Balanced persistent disk type. Can be used as a boot disk or data disk.

`HYPERDISK_EXTREME`

Represents the Hyperdisk Extreme persistent disk type. Can only be used as a data disk.

`HYPERDISK_THROUGHPUT`

Represents the Hyperdisk Throughput persistent disk type. Can only be used as a data disk.

`HYPERDISK_BALANCED_HIGH_AVAILABILITY`

Represents the Hyperdisk Balanced High Availability persistent disk type. Can be used as a boot disk or data disk.

`HYPERDISK_ML`

Represents the Hyperdisk ML persistent disk type. Can be used as a boot disk or data disk.

## GPUDriverConfig

A GPU driver configuration

Fields

`enable_gpu_driver`

`bool`

Optional. Whether the end user authorizes Google Cloud to install GPU driver on this VM instance. If this field is empty or set to false, the GPU driver won't be installed. Only applicable to instances with GPUs.

`custom_gpu_driver_path`

`string`

Optional. Specify a custom Cloud Storage path where the GPU driver is stored. If not specified, we'll automatically choose from official GPU drivers.

## GceSetup

The definition of how to configure a VM instance outside of Resources and Identity.

Fields

`machine_type`

`string`

Optional. The machine type of the VM instance. <https://cloud.google.com/compute/docs/machine-resource>

`min_cpu_platform`

`string`

Optional. The minimum CPU platform to use for this instance. The list of valid values can be found in <https://cloud.google.com/compute/docs/instances/specify-min-cpu-platform#availablezones>

`accelerator_configs[]`

`  AcceleratorConfig  `

Optional. The hardware accelerators used on this instance. If you use accelerators, make sure that your configuration has [enough vCPUs and memory to support the `machine_type` you have selected](https://cloud.google.com/compute/docs/gpus/#gpus-list) . Currently supports only one accelerator configuration.

`service_accounts[]`

`  ServiceAccount  `

Optional. The service account that serves as an identity for the VM instance. Currently supports only one service account.

`boot_disk`

`  BootDisk  `

Optional. The boot disk for the VM.

`data_disks[]`

`  DataDisk  `

Optional. Data disks attached to the VM instance. Currently supports only one data disk.

`shielded_instance_config`

`  ShieldedInstanceConfig  `

Optional. Shielded VM configuration. [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) .

`network_interfaces[]`

`  NetworkInterface  `

Optional. The network interfaces for the VM. Supports only one interface.

`disable_public_ip`

`bool`

Optional. If true, no external IP will be assigned to this VM instance.

`tags[]`

`string`

Optional. The Compute Engine network tags to add to runtime (see [Add network tags](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).

`metadata`

`map<string, string>`

Optional. Custom metadata to apply to this instance.

`enable_ip_forwarding`

`bool`

Optional. Flag to enable ip forwarding or not, default false/off. <https://cloud.google.com/vpc/docs/using-routes#canipforward>

`gpu_driver_config`

`  GPUDriverConfig  `

Optional. Configuration for GPU drivers.

`confidential_instance_config`

`  ConfidentialInstanceConfig  `

Optional. Confidential instance configuration.

`instance_id`

`string`

Output only. The unique ID of the Compute Engine instance resource.

Union field `image` . Type of the image; can be one of VM image, or container image. `image` can be only one of the following:

`vm_image`

`  VmImage  `

Optional. Use a Compute Engine VM image to start the notebook instance.

`container_image`

`  ContainerImage  `

Optional. Use a container image to start the notebook instance.

## GetConfigRequest

Request for getting Workbench configuration parameters.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}`

## GetInstanceRequest

Request for getting a notebook instance.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.get`

## HealthState

The instance health state.

Enums

`HEALTH_STATE_UNSPECIFIED`

The instance substate is unknown.

`HEALTHY`

The instance is known to be in an healthy state (for example, critical daemons are running) Applies to ACTIVE state.

`UNHEALTHY`

The instance is known to be in an unhealthy state (for example, critical daemons are not running) Applies to ACTIVE state.

`AGENT_NOT_INSTALLED`

The instance has not installed health monitoring agent. Applies to ACTIVE state.

`AGENT_NOT_RUNNING`

The instance health monitoring agent is not running. Applies to ACTIVE state.

## ImageRelease

ConfigImage represents an image release available to create a WbI

Fields

`image_name`

`string`

Output only. The name of the image of the form workbench-instances-vYYYYmmdd- -

`release_name`

`string`

Output only. The release of the image of the form m123

## Instance

The definition of a notebook instance.

Fields

`name`

`string`

Output only. Identifier. The name of this notebook instance. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

`proxy_uri`

`string`

Output only. The proxy endpoint that is used to access the Jupyter notebook.

`instance_owners[]`

`string`

Optional. The owner of this instance after creation. Format: `alias@example.com`

Currently supports one owner only. If not specified, all of the service account users of your VM instance's service account can use the instance.

`creator`

`string`

Output only. Email address of entity that sent original CreateInstance request.

`state`

`  State  `

Output only. The state of this instance.

`upgrade_history[]`

`  UpgradeHistoryEntry  `

Output only. The upgrade history of this instance.

`id`

`string`

Output only. Unique ID of the resource.

`health_state`

`  HealthState  `

Output only. Instance health\_state.

`health_info`

`map<string, string>`

Output only. Additional information about instance health. Example:

    healthInfo": {
      "docker_proxy_agent_status": "1",
      "docker_status": "1",
      "jupyterlab_api_status": "-1",
      "jupyterlab_status": "-1",
      "updated": "2020-10-18 09:40:03.573409"
    }

`create_time`

`  Timestamp  `

Output only. Instance creation time.

`update_time`

`  Timestamp  `

Output only. Instance update time.

`disable_proxy_access`

`bool`

Optional. If true, the notebook instance will not register with the proxy.

`labels`

`map<string, string>`

Optional. Labels to apply to this instance. These can be later modified by the UpdateInstance method.

`third_party_proxy_url`

`string`

Output only. The workforce pools proxy endpoint that is used to access the Jupyter notebook.

`satisfies_pzs`

`bool`

Output only. Reserved for future use for Zone Separation.

`satisfies_pzi`

`bool`

Output only. Reserved for future use for Zone Isolation.

`enable_third_party_identity`

`bool`

Optional. Flag that specifies that a notebook can be accessed with third party identity provider.

`enable_managed_euc`

`bool`

Optional. Flag to enable managed end user credentials for the instance.

`enable_deletion_protection`

`bool`

Optional. If true, deletion protection will be enabled for this Workbench Instance. If false, deletion protection will be disabled for this Workbench Instance.

Union field `infrastructure` . Setup for the Notebook instance. `infrastructure` can be only one of the following:

`gce_setup`

`  GceSetup  `

Optional. Compute Engine setup for the notebook. Uses notebook-defined fields.

## ListInstancesRequest

Request for listing notebook instances.

Fields

`parent`

`string`

Required. The parent of the instance. Formats: - `projects/{project_id}/locations/{location}` to list instances in a specific zone. - `projects/{project_id}/locations/-` to list instances in all locations.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.instances.list`

`page_size`

`int32`

Optional. Maximum return size of the list call.

`page_token`

`string`

Optional. A previous returned page token that can be used to continue listing from the last result.

`order_by`

`string`

Optional. Sort results. Supported values are "name", "name desc" or "" (unsorted).

`filter`

`string`

Optional. List filter.

## ListInstancesResponse

Response for listing notebook instances.

Fields

`instances[]`

`  Instance  `

A list of returned instances.

`next_page_token`

`string`

Page token that can be used to continue listing from the last result in the next list call.

`unreachable[]`

`string`

Unordered list. Locations that could not be reached. For example, \['projects/{project\_id}/locations/us-west1-a', 'projects/{project\_id}/locations/us-central1-b'\]. A ListInstancesResponse will only contain either instances or unreachables,

## NetworkInterface

The definition of a network interface resource attached to a VM.

Fields

`network`

`string`

Optional. The name of the VPC that this VM instance is in. Format: `projects/{project_id}/global/networks/{network_id}`

`subnet`

`string`

Optional. The name of the subnet that this VM instance is in. Format: `projects/{project_id}/regions/{region}/subnetworks/{subnetwork_id}`

`nic_type`

`  NicType  `

Optional. The type of vNIC to be used on this interface. This may be gVNIC or VirtioNet.

`access_configs[]`

`  AccessConfig  `

Optional. An array of configurations for this interface. Currently, only one access config, ONE\_TO\_ONE\_NAT, is supported. If no accessConfigs specified, the instance will have an external internet access through an ephemeral external IP address.

## NicType

The type of vNIC driver. Default should be NIC\_TYPE\_UNSPECIFIED.

Enums

`NIC_TYPE_UNSPECIFIED`

No type specified.

`VIRTIO_NET`

VIRTIO

`GVNIC`

GVNIC

## OperationMetadata

Represents the metadata of the long-running operation.

Fields

`create_time`

`  Timestamp  `

The time the operation was created.

`end_time`

`  Timestamp  `

The time the operation finished running.

`target`

`string`

Server-defined resource path for the target of the operation.

`verb`

`string`

Name of the verb executed by the operation.

`status_message`

`string`

Human-readable status of the operation, if any.

`requested_cancellation`

`bool`

Identifies whether the user has requested cancellation of the operation. Operations that have successfully been cancelled have `  google.longrunning.Operation.error  ` value with a `  google.rpc.Status.code  ` of `1` , corresponding to `Code.CANCELLED` .

`api_version`

`string`

API version used to start the operation.

`endpoint`

`string`

API endpoint name of this operation.

## ResetInstanceRequest

Request for resetting a notebook instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.reset`

## ResizeDiskRequest

Request for resizing the notebook instance disks

Fields

`notebook_instance`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `notebookInstance` :

  - `notebooks.instances.update`

Union field `Disk` . Type of the disk that can be resized: boot or data disk `Disk` can be only one of the following:

`boot_disk`

`  BootDisk  `

Required. The boot disk to be resized. Only disk\_size\_gb will be used.

`data_disk`

`  DataDisk  `

Required. The data disk to be resized. Only disk\_size\_gb will be used.

## RestoreInstanceRequest

Request for restoring the notebook instance from a BackupSource.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.update`

Union field `Source` . Source to be restored from. `Source` can be only one of the following:

`snapshot`

`  Snapshot  `

Snapshot to be used for restore.

## RollbackInstanceRequest

Request for rollbacking a notebook instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.rollback`

`target_snapshot`

`string`

Required. The snapshot for rollback. Example: "projects/test-project/global/snapshots/krwlzipynril".

`revision_id`

`string`

Required. Output only. Revision Id

## ServiceAccount

A service account that acts as an identity.

Fields

`email`

`string`

Optional. Email address of the service account.

`scopes[]`

`string`

Output only. The list of scopes to be made available for this service account. Set by the CLH to <https://www.googleapis.com/auth/cloud-platform>

## ShieldedInstanceConfig

A set of Shielded Instance options. See [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) . Not all combinations are valid.

Fields

`enable_secure_boot`

`bool`

Optional. Defines whether the VM instance has Secure Boot enabled.

Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails. Disabled by default.

`enable_vtpm`

`bool`

Optional. Defines whether the VM instance has the vTPM enabled.

`enable_integrity_monitoring`

`bool`

Optional. Defines whether the VM instance has integrity monitoring enabled.

Enables monitoring and attestation of the boot integrity of the VM instance. The attestation is performed against the integrity policy baseline. This baseline is initially derived from the implicitly trusted boot image when the VM instance is created.

## Snapshot

Snapshot represents the snapshot of the data disk used to restore the Workbench Instance from. Refers to: compute/v1/projects/{project\_id}/global/snapshots/{snapshot\_id}

Fields

`snapshot_id`

`string`

Required. The ID of the snapshot.

`project_id`

`string`

Required. The project ID of the snapshot.

## StartInstanceRequest

Request for starting a notebook instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.start`

## State

The definition of the states of this instance.

Enums

`STATE_UNSPECIFIED`

State is not specified.

`STARTING`

The control logic is starting the instance.

`PROVISIONING`

The control logic is installing required frameworks and registering the instance with notebook proxy

`ACTIVE`

The instance is running.

`STOPPING`

The control logic is stopping the instance.

`STOPPED`

The instance is stopped.

`DELETED`

The instance is deleted.

`UPGRADING`

The instance is upgrading.

`INITIALIZING`

The instance is being created.

`SUSPENDING`

The instance is suspending.

`SUSPENDED`

The instance is suspended.

## StopInstanceRequest

Request for stopping a notebook instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.stop`

## SupportedValues

SupportedValues represents the values supported by the configuration.

Fields

`machine_types[]`

`string`

Output only. The machine types supported by WbI.

`accelerator_types[]`

`string`

Output only. The accelerator types supported by WbI.

## UpdateInstanceRequest

Request for updating a notebook instance.

Fields

`instance`

`  Instance  `

Required. A representation of an instance.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `instance` :

  - `iam.permissions.none`

`update_mask`

`  FieldMask  `

Required. Mask used to update an instance. Updatable fields:

  - `labels`
  - `gce_setup.min_cpu_platform`
  - `gce_setup.metadata`
  - `gce_setup.machine_type`
  - `gce_setup.accelerator_configs`
  - `gce_setup.accelerator_configs.type`
  - `gce_setup.accelerator_configs.core_count`
  - `gce_setup.gpu_driver_config`
  - `gce_setup.gpu_driver_config.enable_gpu_driver`
  - `gce_setup.gpu_driver_config.custom_gpu_driver_path`
  - `gce_setup.shielded_instance_config`
  - `gce_setup.shielded_instance_config.enable_secure_boot`
  - `gce_setup.shielded_instance_config.enable_vtpm`
  - `gce_setup.shielded_instance_config.enable_integrity_monitoring`
  - `gce_setup.reservation_affinity`
  - `gce_setup.reservation_affinity.consume_reservation_type`
  - `gce_setup.reservation_affinity.key`
  - `gce_setup.reservation_affinity.values`
  - `gce_setup.tags`
  - `gce_setup.container_image`
  - `gce_setup.container_image.repository`
  - `gce_setup.container_image.tag`
  - `gce_setup.disable_public_ip`
  - `disable_proxy_access`

`request_id`

`string`

Optional. Idempotent request UUID.

## UpgradeHistoryEntry

The entry of VM image upgrade history.

Fields

`snapshot`

`string`

Optional. The snapshot of the boot disk of this notebook instance before upgrade.

`vm_image`

`string`

Optional. The VM image before this instance upgrade.

`container_image`

`string`

Optional. The container image before this instance upgrade.

`framework`

`string`

Optional. The framework of this notebook instance.

`version`

`string`

Optional. The version of the notebook instance before this upgrade.

`state`

`  State  `

Output only. The state of this instance upgrade history entry.

`create_time`

`  Timestamp  `

Immutable. The time that this instance upgrade history entry is created.

`action`

`  Action  `

Optional. Action. Rolloback or Upgrade.

`target_version`

`string`

Optional. Target VM Version, like m63.

## Action

The definition of operations of this upgrade history entry.

Enums

`ACTION_UNSPECIFIED`

Operation is not specified.

`UPGRADE`

Upgrade.

`ROLLBACK`

Rollback.

## State

The definition of the states of this upgrade history entry.

Enums

`STATE_UNSPECIFIED`

State is not specified.

`STARTED`

The instance upgrade is started.

`SUCCEEDED`

The instance upgrade is succeeded.

`FAILED`

The instance upgrade is failed.

## UpgradeInstanceRequest

Request for upgrading a notebook instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.upgrade`

## VmImage

Definition of a custom Compute Engine virtual machine image for starting a notebook instance with the environment installed directly on the VM.

Fields

`project`

`string`

Required. The name of the Google Cloud project that this VM image belongs to. Format: `{project_id}`

Union field `image` . The reference to an external Compute Engine VM image. `image` can be only one of the following:

`name`

`string`

Optional. Use VM image name to find the image.

`family`

`string`

Optional. Use this VM image family to find the image; the newest image in this family will be used.
