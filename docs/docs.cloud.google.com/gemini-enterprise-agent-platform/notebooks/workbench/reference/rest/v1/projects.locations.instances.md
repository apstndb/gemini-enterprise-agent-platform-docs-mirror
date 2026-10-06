---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances
title: 'REST Resource: projects.locations.instances'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Instance

The definition of a notebook instance.

**JSON representation**

```
{
  "name": string,
  "postStartupScript": string,
  "proxyUri": string,
  "instanceOwners": [
    string
  ],
  "serviceAccount": string,
  "serviceAccountScopes": [
    string
  ],
  "machineType": string,
  "acceleratorConfig": {
    object (AcceleratorConfig)
  },
  "state": enum (State),
  "installGpuDriver": boolean,
  "customGpuDriverPath": string,
  "bootDiskType": enum (DiskType),
  "bootDiskSizeGb": string,
  "dataDiskType": enum (DiskType),
  "dataDiskSizeGb": string,
  "noRemoveDataDisk": boolean,
  "diskEncryption": enum (DiskEncryption),
  "kmsKey": string,
  "disks": [
    {
      object (Disk)
    }
  ],
  "shieldedInstanceConfig": {
    object (ShieldedInstanceConfig)
  },
  "noPublicIp": boolean,
  "noProxyAccess": boolean,
  "network": string,
  "subnet": string,
  "labels": {
    string: string,
    ...
  },
  "metadata": {
    string: string,
    ...
  },
  "tags": [
    string
  ],
  "upgradeHistory": [
    {
      object (UpgradeHistoryEntry)
    }
  ],
  "nicType": enum (NicType),
  "reservationAffinity": {
    object (ReservationAffinity)
  },
  "creator": string,
  "canIpForward": boolean,
  "createTime": string,
  "updateTime": string,
  "instanceMigrationEligibility": {
    object (InstanceMigrationEligibility)
  },

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "vmImage": {
    object (VmImage)
  },
  "containerImage": {
    object (ContainerImage)
  }
  // End of mutually exclusive fields.
  "migrated": boolean
}
```

| Fields                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                          | `string` Output only. The name of this notebook instance. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}`                                                                                                                                                                                                                                                                                                       |
| `postStartupScript`                                                                                                                                                             | `string` Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path ( `gs://path-to-file/file-name` ).                                                                                                                                                                                                                                                           |
| `proxyUri`                                                                                                                                                                      | `string` Output only. The proxy endpoint that is used to access the Jupyter notebook.                                                                                                                                                                                                                                                                                                                                                      |
| `instanceOwners[]`                                                                                                                                                              | `string` Input only. The owner of this instance after creation. Format: `alias@example.com` Currently supports one owner only. If not specified, all of the service account users of your VM instance's service account can use the instance.                                                                                                                                                                                              |
| `serviceAccount`                                                                                                                                                                | `string` The service account on this instance, giving access to other Google Cloud services. You can use any service account within the same project, but you must have the service account user permission to use the instance. If not specified, the [Compute Engine default service account](https://cloud.google.com/compute/docs/access/service-accounts#default_service_account) is used.                                            |
| `serviceAccountScopes[]`                                                                                                                                                        | `string` Optional. The URIs of service account scopes to be included in Compute Engine instances. If not specified, the following [scopes](https://cloud.google.com/compute/docs/access/service-accounts#accesscopesiam) are defined: - <https://www.googleapis.com/auth/cloud-platform> - <https://www.googleapis.com/auth/userinfo.email> If not using default scopes, you need at least: <https://www.googleapis.com/auth/compute>      |
| `machineType`                                                                                                                                                                   | `string` Required. The [Compute Engine machine type](https://cloud.google.com/compute/docs/machine-resource) of this instance.                                                                                                                                                                                                                                                                                                             |
| `acceleratorConfig`                                                                                                                                                             | `object ( `[`AcceleratorConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#AcceleratorConfig)` )` The hardware accelerator used on this instance. If you use accelerators, make sure that your configuration has [enough vCPUs and memory to support the `machineType` you have selected](https://cloud.google.com/compute/docs/gpus/#gpus-list) . |
| `state`                                                                                                                                                                         | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#State)` )` Output only. The state of this instance.                                                                                                                                                                                                                                   |
| `installGpuDriver`                                                                                                                                                              | `boolean` Whether the end user authorizes Google Cloud to install GPU driver on this instance. If this field is empty or set to false, the GPU driver won't be installed. Only applicable to instances with GPUs.                                                                                                                                                                                                                          |
| `customGpuDriverPath`                                                                                                                                                           | `string` Specify a custom Cloud Storage path where the GPU driver is stored. If not specified, we'll automatically choose from official GPU drivers.                                                                                                                                                                                                                                                                                       |
| `bootDiskType`                                                                                                                                                                  | `enum ( `[`DiskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#DiskType)` )` Input only. The type of the boot disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).                                                                                                                                             |
| `bootDiskSizeGb`                                                                                                                                                                | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Input only. The size of the boot disk in GB attached to this instance, up to a maximum of 64000 GB (64 TB). The minimum recommended value is 100 GB. If not specified, this defaults to 100.                                                                                                                                                        |
| `dataDiskType`                                                                                                                                                                  | `enum ( `[`DiskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#DiskType)` )` Input only. The type of the data disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).                                                                                                                                             |
| `dataDiskSizeGb`                                                                                                                                                                | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Input only. The size of the data disk in GB attached to this instance, up to a maximum of 64000 GB (64 TB). You can choose the size of the data disk based on how big your notebooks and data are. If not specified, this defaults to 100.                                                                                                          |
| `noRemoveDataDisk`                                                                                                                                                              | `boolean` Input only. If true, the data disk will not be auto deleted when deleting the instance.                                                                                                                                                                                                                                                                                                                                          |
| `diskEncryption`                                                                                                                                                                | `enum ( `[`DiskEncryption`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#DiskEncryption)` )` Input only. Disk encryption method used on the boot and data disks, defaults to GMEK.                                                                                                                                                                    |
| `kmsKey`                                                                                                                                                                        | `string` Input only. The KMS key used to encrypt the disks, only applicable if diskEncryption is CMEK. Format: `projects/{projectId}/locations/{location}/keyRings/{key_ring_id}/cryptoKeys/{key_id}` Learn more about [using your own encryption keys](https://docs.cloud.google.com/kms/docs/quickstart) .                                                                                                                               |
| `disks[]`                                                                                                                                                                       | `object ( `[`Disk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#Disk)` )` Output only. Attached disks to notebook instance.                                                                                                                                                                                                                          |
| `shieldedInstanceConfig`                                                                                                                                                        | `object ( `[`ShieldedInstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#ShieldedInstanceConfig)` )` Optional. Shielded VM configuration. [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) .                                                                            |
| `noPublicIp`                                                                                                                                                                    | `boolean` If true, no external IP will be assigned to this instance.                                                                                                                                                                                                                                                                                                                                                                       |
| `noProxyAccess`                                                                                                                                                                 | `boolean` If true, the notebook instance will not register with the proxy.                                                                                                                                                                                                                                                                                                                                                                 |
| `network`                                                                                                                                                                       | `string` The name of the VPC that this instance is in. Format: `projects/{projectId}/global/networks/{network_id}`                                                                                                                                                                                                                                                                                                                         |
| `subnet`                                                                                                                                                                        | `string` The name of the subnet that this instance is in. Format: `projects/{projectId}/regions/{region}/subnetworks/{subnetwork_id}`                                                                                                                                                                                                                                                                                                      |
| `labels`                                                                                                                                                                        | `map (key: string, value: string)` Labels to apply to this instance. These can be later modified by the setLabels method. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                            |
| `metadata`                                                                                                                                                                      | `map (key: string, value: string)` Custom metadata to apply to this instance. For example, to specify a Cloud Storage bucket for automatic backup, you can use the `gcs-data-bucket` metadata tag. Format: `"--metadata=gcs-data-bucket=BUCKET"` . An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                   |
| `tags[]`                                                                                                                                                                        | `string` Optional. The Compute Engine network tags to add to runtime (see [Add network tags](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).                                                                                                                                                                                                                                                                                 |
| `upgradeHistory[]`                                                                                                                                                              | `object ( `[`UpgradeHistoryEntry`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#UpgradeHistoryEntry)` )` The upgrade history of this instance.                                                                                                                                                                                                        |
| `nicType`                                                                                                                                                                       | `enum ( `[`NicType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#NicType)` )` Optional. The type of vNIC to be used on this interface. This may be gVNIC or VirtioNet.                                                                                                                                                                               |
| `reservationAffinity`                                                                                                                                                           | `object ( `[`ReservationAffinity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#ReservationAffinity)` )` Optional. The optional reservation affinity. Setting this field will apply the specified [Zonal Compute Reservation](https://cloud.google.com/compute/docs/instances/reserving-zonal-resources) to this notebook instance.                   |
| `creator`                                                                                                                                                                       | `string` Output only. Email address of entity that sent original instances.create request.                                                                                                                                                                                                                                                                                                                                                 |
| `canIpForward`                                                                                                                                                                  | `boolean` Optional. Flag to enable ip forwarding or not, default false/off. <https://cloud.google.com/vpc/docs/using-routes#canipforward>                                                                                                                                                                                                                                                                                                  |
| `createTime`                                                                                                                                                                    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Instance creation time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                 |
| `updateTime`                                                                                                                                                                    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Instance update time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                   |
| `instanceMigrationEligibility`                                                                                                                                                  | `object ( `[`InstanceMigrationEligibility`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#InstanceMigrationEligibility)` )` Output only. Checks how feasible a migration from UmN to WbI is.                                                                                                                                                           |
| Type of the environment; can be one of VM image, or container image. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `vmImage`                                                                                                                                                                       | `object ( `[`VmImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/VmImage)` )` Use a Compute Engine VM image to start the notebook instance.                                                                                                                                                                                                                                     |
| `containerImage`                                                                                                                                                                | `object ( `[`ContainerImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ContainerImage)` )` Use a container image to start the notebook instance.                                                                                                                                                                                                                               |
| End of mutually exclusive fields.                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `migrated`                                                                                                                                                                      | `boolean` Output only. Bool indicating whether this notebook has been migrated to a Workbench Instance                                                                                                                                                                                                                                                                                                                                     |

## AcceleratorConfig

Definition of a hardware accelerator. Note that not all combinations of `type` and `coreCount` are valid. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus/#gpus-list) to find a valid combination. TPUs are not supported.

**JSON representation**

```
{
  "type": enum (AcceleratorType),
  "coreCount": string
}
```

| Fields      |                                                                                                                                                                                                               |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`      | `enum ( `[`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#AcceleratorType)` )` Type of this accelerator. |
| `coreCount` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Count of cores of this accelerator.                                                                                    |

## AcceleratorType

Definition of the types of hardware accelerators that can be used on this instance.

| Enums                          |                                                             |
|--------------------------------|-------------------------------------------------------------|
| `ACCELERATOR_TYPE_UNSPECIFIED` | Accelerator type is not specified.                          |
| `NVIDIA_TESLA_K80`             | Accelerator type is Nvidia Tesla K80.                       |
| `NVIDIA_TESLA_P100`            | Accelerator type is Nvidia Tesla P100.                      |
| `NVIDIA_TESLA_V100`            | Accelerator type is Nvidia Tesla V100.                      |
| `NVIDIA_TESLA_P4`              | Accelerator type is Nvidia Tesla P4.                        |
| `NVIDIA_TESLA_T4`              | Accelerator type is Nvidia Tesla T4.                        |
| `NVIDIA_TESLA_A100`            | Accelerator type is Nvidia Tesla A100.                      |
| `NVIDIA_L4`                    | Accelerator type is Nvidia Tesla L4.                        |
| `NVIDIA_A100_80GB`             | Accelerator type is Nvidia Tesla A100 80GB.                 |
| `NVIDIA_TESLA_T4_VWS`          | Accelerator type is NVIDIA Tesla T4 Virtual Workstations.   |
| `NVIDIA_TESLA_P100_VWS`        | Accelerator type is NVIDIA Tesla P100 Virtual Workstations. |
| `NVIDIA_TESLA_P4_VWS`          | Accelerator type is NVIDIA Tesla P4 Virtual Workstations.   |
| `NVIDIA_H100_80GB`             | Accelerator type is NVIDIA H100 80GB.                       |
| `NVIDIA_H100_MEGA_80GB`        | Accelerator type is NVIDIA H100 Mega 80GB.                  |
| `TPU_V2`                       | (Coming soon) Accelerator type is TPU V2.                   |
| `TPU_V3`                       | (Coming soon) Accelerator type is TPU V3.                   |

## State

The definition of the states of this instance.

| Enums               |                                                                                                      |
|---------------------|------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | State is not specified.                                                                              |
| `STARTING`          | The control logic is starting the instance.                                                          |
| `PROVISIONING`      | The control logic is installing required frameworks and registering the instance with notebook proxy |
| `ACTIVE`            | The instance is running.                                                                             |
| `STOPPING`          | The control logic is stopping the instance.                                                          |
| `STOPPED`           | The instance is stopped.                                                                             |
| `DELETED`           | The instance is deleted.                                                                             |
| `UPGRADING`         | The instance is upgrading.                                                                           |
| `INITIALIZING`      | The instance is being created.                                                                       |
| `REGISTERING`       | The instance is getting registered.                                                                  |
| `SUSPENDING`        | The instance is suspending.                                                                          |
| `SUSPENDED`         | The instance is suspended.                                                                           |

## DiskType

Possible disk types for notebook instances.

| Enums                   |                                |
|-------------------------|--------------------------------|
| `DISK_TYPE_UNSPECIFIED` | Disk type not set.             |
| `PD_STANDARD`           | Standard persistent disk type. |
| `PD_SSD`                | SSD persistent disk type.      |
| `PD_BALANCED`           | Balanced persistent disk type. |
| `PD_EXTREME`            | Extreme persistent disk type.  |

## DiskEncryption

Definition of the disk encryption options.

| Enums                         |                                                                |
|-------------------------------|----------------------------------------------------------------|
| `DISK_ENCRYPTION_UNSPECIFIED` | Disk encryption is not specified.                              |
| `GMEK`                        | Use Google managed encryption keys to encrypt the boot disk.   |
| `CMEK`                        | Use customer managed encryption keys to encrypt the boot disk. |

## Disk

An instance-attached disk resource.

**JSON representation**

```
{
  "autoDelete": boolean,
  "boot": boolean,
  "deviceName": string,
  "diskSizeGb": string,
  "guestOsFeatures": [
    {
      object (GuestOsFeature)
    }
  ],
  "index": string,
  "interface": string,
  "kind": string,
  "licenses": [
    string
  ],
  "mode": string,
  "source": string,
  "type": string
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>autoDelete</code></td>
<td><p><code>boolean</code></p>
<p>Indicates whether the disk will be auto-deleted when the instance is deleted (but not when the disk is detached from the instance).</p></td>
</tr>
<tr class="even">
<td><code>boot</code></td>
<td><p><code>boolean</code></p>
<p>Indicates that this is a boot disk. The virtual machine will use the first partition of the disk for its root filesystem.</p></td>
</tr>
<tr class="odd">
<td><code>deviceName</code></td>
<td><p><code>string</code></p>
<p>Indicates a unique device name of your choice that is reflected into the <code>/dev/disk/by-id/google-*</code> tree of a Linux operating system running within the instance. This name can be used to reference the device for mounting, resizing, and so on, from within the instance.</p>
<p>If not specified, the server chooses a default device name to apply to this disk, in the form persistent-disk-x, where x is a number assigned by Google Compute Engine.This field is only applicable for persistent disks.</p></td>
</tr>
<tr class="even">
<td><code>diskSizeGb</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Indicates the size of the disk in base-2 GB.</p></td>
</tr>
<tr class="odd">
<td><code>guestOsFeatures[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#GuestOsFeature"><code>GuestOsFeature</code></a><code> )</code></p>
<p>Indicates a list of features to enable on the guest operating system. Applicable only for bootable images. Read Enabling guest operating system features to see a list of available options.</p></td>
</tr>
<tr class="even">
<td><code>index</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>A zero-based index to this disk, where 0 is reserved for the boot disk. If you have many disks attached to an instance, each disk would have a unique index number.</p></td>
</tr>
<tr class="odd">
<td><code>interface</code></td>
<td><p><code>string</code></p>
<p>Indicates the disk interface to use for attaching this disk, which is either SCSI or NVME. The default is SCSI. Persistent disks must always use SCSI and the request will fail if you attempt to attach a persistent disk in any other format than SCSI. Local SSDs can use either NVME or SCSI. For performance characteristics of SCSI over NVMe, see Local SSD performance. Valid values:</p>
<ul>
<li><code>NVME</code></li>
<li><code>SCSI</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>kind</code></td>
<td><p><code>string</code></p>
<p>Type of the resource. Always compute#attachedDisk for attached disks.</p></td>
</tr>
<tr class="odd">
<td><code>licenses[]</code></td>
<td><p><code>string</code></p>
<p>A list of publicly visible licenses. Reserved for Google's use. A License represents billing and aggregate usage data for public and marketplace images.</p></td>
</tr>
<tr class="even">
<td><code>mode</code></td>
<td><p><code>string</code></p>
<p>The mode in which to attach this disk, either <code>READ_WRITE</code> or <code>READ_ONLY</code> . If not specified, the default is to attach the disk in <code>READ_WRITE</code> mode. Valid values:</p>
<ul>
<li><code>READ_ONLY</code></li>
<li><code>READ_WRITE</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>source</code></td>
<td><p><code>string</code></p>
<p>Indicates a valid partial or full URL to an existing Persistent Disk resource.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Indicates the type of the disk, either <code>SCRATCH</code> or <code>PERSISTENT</code> . Valid values:</p>
<ul>
<li><code>PERSISTENT</code></li>
<li><code>SCRATCH</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GuestOsFeature

Guest OS features for boot disk.

**JSON representation**

```
{
  "type": string
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>The ID of a supported feature. Read Enabling guest operating system features to see a list of available options. Valid values:</p>
<ul>
<li><code>FEATURE_TYPE_UNSPECIFIED</code></li>
<li><code>MULTI_IP_SUBNET</code></li>
<li><code>SECURE_BOOT</code></li>
<li><code>UEFI_COMPATIBLE</code></li>
<li><code>VIRTIO_SCSI_MULTIQUEUE</code></li>
<li><code>WINDOWS</code></li>
</ul></td>
</tr>
</tbody>
</table>

## ShieldedInstanceConfig

A set of Shielded Instance options. See [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) . Not all combinations are valid.

**JSON representation**

```
{
  "enableSecureBoot": boolean,
  "enableVtpm": boolean,
  "enableIntegrityMonitoring": boolean
}
```

| Fields                      |                                                                                                                                                                                                                                                                                                                                                    |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableSecureBoot`          | `boolean` Defines whether the instance has Secure Boot enabled. Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails. Disabled by default.                                                                |
| `enableVtpm`                | `boolean` Defines whether the instance has the vTPM enabled. Enabled by default.                                                                                                                                                                                                                                                                   |
| `enableIntegrityMonitoring` | `boolean` Defines whether the instance has integrity monitoring enabled. Enables monitoring and attestation of the boot integrity of the instance. The attestation is performed against the integrity policy baseline. This baseline is initially derived from the implicitly trusted boot image when the instance is created. Enabled by default. |

## UpgradeHistoryEntry

The entry of VM image upgrade history.

**JSON representation**

```
{
  "snapshot": string,
  "vmImage": string,
  "containerImage": string,
  "framework": string,
  "version": string,
  "state": enum (State),
  "createTime": string,
  "targetImage": string,
  "action": enum (Action),
  "targetVersion": string
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>snapshot</code></td>
<td><p><code>string</code></p>
<p>The snapshot of the boot disk of this notebook instance before upgrade.</p></td>
</tr>
<tr class="even">
<td><code>vmImage</code></td>
<td><p><code>string</code></p>
<p>The VM image before this instance upgrade.</p></td>
</tr>
<tr class="odd">
<td><code>containerImage</code></td>
<td><p><code>string</code></p>
<p>The container image before this instance upgrade.</p></td>
</tr>
<tr class="even">
<td><code>framework</code></td>
<td><p><code>string</code></p>
<p>The framework of this notebook instance.</p></td>
</tr>
<tr class="odd">
<td><code>version</code></td>
<td><p><code>string</code></p>
<p>The version of the notebook instance before this upgrade.</p></td>
</tr>
<tr class="even">
<td><code>state</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#State_1"><code>State</code></a><code> )</code></p>
<p>The state of this instance upgrade history entry.</p></td>
</tr>
<tr class="odd">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>The time that this instance upgrade history entry is created.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>targetImage </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Target VM Image. Format: <code>ainotebooks-vm/project/image-name/name</code> .</p></td>
</tr>
<tr class="odd">
<td><code>action</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#Action"><code>Action</code></a><code> )</code></p>
<p>Action. Rolloback or Upgrade.</p></td>
</tr>
<tr class="even">
<td><code>targetVersion</code></td>
<td><p><code>string</code></p>
<p>Target VM Version, like m63.</p></td>
</tr>
</tbody>
</table>

## State

The definition of the states of this upgrade history entry.

| Enums               |                                    |
|---------------------|------------------------------------|
| `STATE_UNSPECIFIED` | State is not specified.            |
| `STARTED`           | The instance upgrade is started.   |
| `SUCCEEDED`         | The instance upgrade is succeeded. |
| `FAILED`            | The instance upgrade is failed.    |

## Action

The definition of operations of this upgrade history entry.

| Enums                |                             |
|----------------------|-----------------------------|
| `ACTION_UNSPECIFIED` | Operation is not specified. |
| `UPGRADE`            | Upgrade.                    |
| `ROLLBACK`           | Rollback.                   |

## NicType

The type of vNIC driver. Default should be UNSPECIFIED_NIC_TYPE.

| Enums                  |                    |
|------------------------|--------------------|
| `UNSPECIFIED_NIC_TYPE` | No type specified. |
| `VIRTIO_NET`           | VIRTIO             |
| `GVNIC`                | GVNIC              |

## ReservationAffinity

Reservation Affinity for consuming Zonal reservation.

**JSON representation**

```
{
  "consumeReservationType": enum (Type),
  "key": string,
  "values": [
    string
  ]
}
```

| Fields                   |                                                                                                                                                                                                        |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `consumeReservationType` | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#Type)` )` Optional. Type of reservation to consume |
| `key`                    | `string` Optional. Corresponds to the label key of reservation resource.                                                                                                                               |
| `values[]`               | `string` Optional. Corresponds to the label values of reservation resource.                                                                                                                            |

## Type

Indicates whether to consume capacity from an reservation or not.

| Enums                  |                                                                                                          |
|------------------------|----------------------------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED`     | Default type.                                                                                            |
| `NO_RESERVATION`       | Do not consume from any allocated capacity.                                                              |
| `ANY_RESERVATION`      | Consume any reservation available.                                                                       |
| `SPECIFIC_RESERVATION` | Must consume from a specific reservation. Must specify key value fields for specifying the reservations. |

## InstanceMigrationEligibility

InstanceMigrationEligibility represents the feasibility information of a migration from UmN to WbI.

**JSON representation**

```
{
  "warnings": [
    enum (Warning)
  ],
  "errors": [
    enum (Error)
  ]
}
```

| Fields       |                                                                                                                                                                                                                                                                                         |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `warnings[]` | `enum ( `[`Warning`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#Warning)` )` Output only. Certain configurations will be defaulted during the migration.                                         |
| `errors[]`   | `enum ( `[`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances#Error)` )` Output only. Certain configurations make the UmN ineligible for an automatic migration. A manual migration is required. |

## Warning

A migration warning message means certain configurations will be defaulted during the migration.

| Enums                          |                                                                                                                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `WARNING_UNSPECIFIED`          | Default type.                                                                                                                                                                   |
| `UNSUPPORTED_MACHINE_TYPE`     | The UmN uses an machine type that's unsupported in WbI. It will be migrated with the default machine type e2-standard-4. Users can change the machine type after the migration. |
| `UNSUPPORTED_ACCELERATOR_TYPE` | The UmN uses an accelerator type that's unsupported in WbI. It will be migrated without an accelerator. User can attach an accelerator after the migration.                     |
| `UNSUPPORTED_OS`               | The UmN uses an operating system that's unsupported in WbI (e.g. Debian 10, Ubuntu). It will be replaced with Debian 11 in WbI.                                                 |
| `NO_REMOVE_DATA_DISK`          | This UmN is configured with noRemoveDataDisk, which is no longer available in WbI.                                                                                              |
| `GCS_BACKUP`                   | This UmN is configured with the Cloud Storage backup feature, which is no longer available in WbI.                                                                              |
| `POST_STARTUP_SCRIPT`          | This UmN is configured with a post startup script. Please optionally provide the `postStartupScriptOption` for the migration.                                                   |

## Error

A migration error message means certain configurations make the UmN ineligible for an automatic migration. A manual migration is required.

| Enums               |                                                   |
|---------------------|---------------------------------------------------|
| `ERROR_UNSPECIFIED` | Default type.                                     |
| `DATAPROC_HUB`      | The UmN uses Dataproc Hub and cannot be migrated. |

| Methods                                                                                                                                                                                          |                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/create)                                             | Creates a new Instance in a given project and location.                                            |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/delete)                                             | Deletes a single Instance.                                                                         |
| [`diagnose`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/diagnose)                                         | Creates a Diagnostic File and runs Diagnostic Tool given an Instance.                              |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/get)                                                   | Gets details of a single Instance.                                                                 |
| [`getIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/getIamPolicy)                                 | Gets the access control policy for a resource.                                                     |
| [`getInstanceHealth`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/getInstanceHealth)                       | Checks whether a notebook instance is healthy.                                                     |
| [`isUpgradeable`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/isUpgradeable)                               | Checks whether a notebook instance is upgradable.                                                  |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/list)                                                 | Lists instances in a given project and location.                                                   |
| [`migrate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/migrate)                                           | Migrates an existing User-Managed Notebook to Workbench Instances.                                 |
| [`register`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/register)                                         | Registers an existing legacy notebook instance to the Notebooks API server.                        |
| [`report`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/report)                                             | Allows notebook instances to report their latest instance information to the Notebooks API server. |
| [`reset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/reset)                                               | Resets a notebook instance.                                                                        |
| [`rollback`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/rollback)                                         | Rollbacks a notebook instance to the previous version.                                             |
| [`setAccelerator`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/setAccelerator)                             | Updates the guest accelerators of a single Instance.                                               |
| [`setIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/setIamPolicy)                                 | Sets the access control policy on the specified resource.                                          |
| [`setLabels`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/setLabels)                                       | Replaces all the labels of an Instance.                                                            |
| [`setMachineType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/setMachineType)                             | Updates the machine type of a single Instance.                                                     |
| [`start`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/start)                                               | Starts a notebook instance.                                                                        |
| [`stop`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/stop)                                                 | Stops a notebook instance.                                                                         |
| [`testIamPermissions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/testIamPermissions)                     | Returns permissions that a caller has on the specified resource.                                   |
| [`updateConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/updateConfig)                                 | Update Notebook Instance configurations.                                                           |
| [`updateMetadataItems`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/updateMetadataItems)                   | Add/update metadata items for an instance.                                                         |
| [`updateShieldedInstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/updateShieldedInstanceConfig) | Updates the Shielded instance configuration of a single Instance.                                  |
| [`upgrade`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/upgrade)                                           | Upgrades a notebook instance to the latest version.                                                |
