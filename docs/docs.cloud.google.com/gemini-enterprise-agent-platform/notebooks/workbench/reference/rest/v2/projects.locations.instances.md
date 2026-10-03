---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances
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
  "proxyUri": string,
  "instanceOwners": [
    string
  ],
  "creator": string,
  "state": enum (State),
  "upgradeHistory": [
    {
      object (UpgradeHistoryEntry)
    }
  ],
  "id": string,
  "healthState": enum (HealthState),
  "healthInfo": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "disableProxyAccess": boolean,
  "labels": {
    string: string,
    ...
  },
  "thirdPartyProxyUrl": string,
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean,
  "enableThirdPartyIdentity": boolean,
  "enableManagedEuc": boolean,
  "enableDeletionProtection": boolean,

  // Union field infrastructure can be only one of the following:
  "gceSetup": {
    object (GceSetup)
  }
  // End of list of possible types for union field infrastructure.
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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Output only. Identifier. The name of this notebook instance. Format: <code>projects/{projectId}/locations/{location}/instances/{instanceId}</code></p></td>
</tr>
<tr class="even">
<td><code>proxyUri</code></td>
<td><p><code>string</code></p>
<p>Output only. The proxy endpoint that is used to access the Jupyter notebook.</p></td>
</tr>
<tr class="odd">
<td><code>instanceOwners[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The owner of this instance after creation. Format: <code>alias@example.com</code></p>
<p>Currently supports one owner only. If not specified, all of the service account users of your VM instance's service account can use the instance.</p></td>
</tr>
<tr class="even">
<td><code>creator</code></td>
<td><p><code>string</code></p>
<p>Output only. Email address of entity that sent original instances.create request.</p></td>
</tr>
<tr class="odd">
<td><code>state</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#State"><code>State</code></a><code> )</code></p>
<p>Output only. The state of this instance.</p></td>
</tr>
<tr class="even">
<td><code>upgradeHistory[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#UpgradeHistoryEntry"><code>UpgradeHistoryEntry</code></a><code> )</code></p>
<p>Output only. The upgrade history of this instance.</p></td>
</tr>
<tr class="odd">
<td><code>id</code></td>
<td><p><code>string</code></p>
<p>Output only. Unique ID of the resource.</p></td>
</tr>
<tr class="even">
<td><code>healthState</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#HealthState"><code>HealthState</code></a><code> )</code></p>
<p>Output only. Instance healthState.</p></td>
</tr>
<tr class="odd">
<td><code>healthInfo</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Output only. Additional information about instance health. Example:</p>
<pre data-fenced=""><code>healthInfo&quot;: {
  &quot;docker_proxy_agent_status&quot;: &quot;1&quot;,
  &quot;docker_status&quot;: &quot;1&quot;,
  &quot;jupyterlab_api_status&quot;: &quot;-1&quot;,
  &quot;jupyterlab_status&quot;: &quot;-1&quot;,
  &quot;updated&quot;: &quot;2020-10-18 09:40:03.573409&quot;
}</code></pre>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Instance creation time.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>updateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Instance update time.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>disableProxyAccess</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If true, the notebook instance will not register with the proxy.</p></td>
</tr>
<tr class="odd">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Optional. Labels to apply to this instance. These can be later modified by the instances.patch method.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>thirdPartyProxyUrl</code></td>
<td><p><code>string</code></p>
<p>Output only. The workforce pools proxy endpoint that is used to access the Jupyter notebook.</p></td>
</tr>
<tr class="odd">
<td><code>satisfiesPzs</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Reserved for future use for Zone Separation.</p></td>
</tr>
<tr class="even">
<td><code>satisfiesPzi</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Reserved for future use for Zone Isolation.</p></td>
</tr>
<tr class="odd">
<td><code>enableThirdPartyIdentity</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Flag that specifies that a notebook can be accessed with third party identity provider.</p></td>
</tr>
<tr class="even">
<td><code>enableManagedEuc</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Flag to enable managed end user credentials for the instance.</p></td>
</tr>
<tr class="odd">
<td><code>enableDeletionProtection</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If true, deletion protection will be enabled for this Workbench Instance. If false, deletion protection will be disabled for this Workbench Instance.</p></td>
</tr>
<tr class="even">
<td>Union field <code>infrastructure</code> . Setup for the Notebook instance. <code>infrastructure</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>gceSetup</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#GceSetup"><code>GceSetup</code></a><code> )</code></p>
<p>Optional. Compute Engine setup for the notebook. Uses notebook-defined fields.</p></td>
</tr>
</tbody>
</table>

## GceSetup

The definition of how to configure a VM instance outside of Resources and Identity.

**JSON representation**

```
{
  "machineType": string,
  "minCpuPlatform": string,
  "acceleratorConfigs": [
    {
      object (AcceleratorConfig)
    }
  ],
  "serviceAccounts": [
    {
      object (ServiceAccount)
    }
  ],
  "bootDisk": {
    object (BootDisk)
  },
  "dataDisks": [
    {
      object (DataDisk)
    }
  ],
  "shieldedInstanceConfig": {
    object (ShieldedInstanceConfig)
  },
  "networkInterfaces": [
    {
      object (NetworkInterface)
    }
  ],
  "disablePublicIp": boolean,
  "tags": [
    string
  ],
  "metadata": {
    string: string,
    ...
  },
  "enableIpForwarding": boolean,
  "gpuDriverConfig": {
    object (GPUDriverConfig)
  },
  "confidentialInstanceConfig": {
    object (ConfidentialInstanceConfig)
  },
  "instanceId": string,

  // Union field image can be only one of the following:
  "vmImage": {
    object (VmImage)
  },
  "containerImage": {
    object (ContainerImage)
  }
  // End of list of possible types for union field image.
}
```

| Fields                                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineType`                                                                                                                  | `string` Optional. The machine type of the VM instance. <https://cloud.google.com/compute/docs/machine-resource>                                                                                                                                                                                                                                                                                                                                                                                             |
| `minCpuPlatform`                                                                                                               | `string` Optional. The minimum CPU platform to use for this instance. The list of valid values can be found in <https://cloud.google.com/compute/docs/instances/specify-min-cpu-platform#availablezones>                                                                                                                                                                                                                                                                                                     |
| `acceleratorConfigs[]`                                                                                                         | `object ( `[`AcceleratorConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#AcceleratorConfig)` )` Optional. The hardware accelerators used on this instance. If you use accelerators, make sure that your configuration has [enough vCPUs and memory to support the `machineType` you have selected](https://cloud.google.com/compute/docs/gpus/#gpus-list) . Currently supports only one accelerator configuration. |
| `serviceAccounts[]`                                                                                                            | `object ( `[`ServiceAccount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#ServiceAccount)` )` Optional. The service account that serves as an identity for the VM instance. Currently supports only one service account.                                                                                                                                                                                               |
| `bootDisk`                                                                                                                     | `object ( `[`BootDisk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#BootDisk)` )` Optional. The boot disk for the VM.                                                                                                                                                                                                                                                                                                  |
| `dataDisks[]`                                                                                                                  | `object ( `[`DataDisk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#DataDisk)` )` Optional. Data disks attached to the VM instance. Currently supports only one data disk.                                                                                                                                                                                                                                             |
| `shieldedInstanceConfig`                                                                                                       | `object ( `[`ShieldedInstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#ShieldedInstanceConfig)` )` Optional. Shielded VM configuration. [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) .                                                                                                                                              |
| `networkInterfaces[]`                                                                                                          | `object ( `[`NetworkInterface`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#NetworkInterface)` )` Optional. The network interfaces for the VM. Supports only one interface.                                                                                                                                                                                                                                            |
| `disablePublicIp`                                                                                                              | `boolean` Optional. If true, no external IP will be assigned to this VM instance.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `tags[]`                                                                                                                       | `string` Optional. The Compute Engine network tags to add to runtime (see [Add network tags](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).                                                                                                                                                                                                                                                                                                                                                   |
| `metadata`                                                                                                                     | `map (key: string, value: string)` Optional. Custom metadata to apply to this instance. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                                                                                                |
| `enableIpForwarding`                                                                                                           | `boolean` Optional. Flag to enable ip forwarding or not, default false/off. <https://cloud.google.com/vpc/docs/using-routes#canipforward>                                                                                                                                                                                                                                                                                                                                                                    |
| `gpuDriverConfig`                                                                                                              | `object ( `[`GPUDriverConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#GPUDriverConfig)` )` Optional. Configuration for GPU drivers.                                                                                                                                                                                                                                                                               |
| `confidentialInstanceConfig`                                                                                                   | `object ( `[`ConfidentialInstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#ConfidentialInstanceConfig)` )` Optional. Confidential instance configuration.                                                                                                                                                                                                                                                   |
| `instanceId`                                                                                                                   | `string` Output only. The unique ID of the Compute Engine instance resource.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Union field `image` . Type of the image; can be one of VM image, or container image. `image` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `vmImage`                                                                                                                      | `object ( `[`VmImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#VmImage)` )` Optional. Use a Compute Engine VM image to start the notebook instance.                                                                                                                                                                                                                                                                |
| `containerImage`                                                                                                               | `object ( `[`ContainerImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#ContainerImage)` )` Optional. Use a container image to start the notebook instance.                                                                                                                                                                                                                                                          |

## AcceleratorConfig

An accelerator configuration for a VM instance Definition of a hardware accelerator. Note that there is no check on `type` and `coreCount` combinations. TPUs are not supported. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus/#gpus-list) to find a valid combination.

**JSON representation**

```
{
  "type": enum (AcceleratorType),
  "coreCount": string
}
```

| Fields      |                                                                                                                                                                                                                         |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`      | `enum ( `[`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#AcceleratorType)` )` Optional. Type of this accelerator. |
| `coreCount` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Count of cores of this accelerator.                                                                                    |

## AcceleratorType

Definition of the types of hardware accelerators that can be used on this instance.

| Enums                          |                                                             |
|--------------------------------|-------------------------------------------------------------|
| `ACCELERATOR_TYPE_UNSPECIFIED` | Accelerator type is not specified.                          |
| `NVIDIA_TESLA_P100`            | Accelerator type is Nvidia Tesla P100.                      |
| `NVIDIA_TESLA_V100`            | Accelerator type is Nvidia Tesla V100.                      |
| `NVIDIA_TESLA_P4`              | Accelerator type is Nvidia Tesla P4.                        |
| `NVIDIA_TESLA_T4`              | Accelerator type is Nvidia Tesla T4.                        |
| `NVIDIA_TESLA_A100`            | Accelerator type is Nvidia Tesla A100 - 40GB.               |
| `NVIDIA_A100_80GB`             | Accelerator type is Nvidia Tesla A100 - 80GB.               |
| `NVIDIA_L4`                    | Accelerator type is Nvidia Tesla L4.                        |
| `NVIDIA_H100_80GB`             | Accelerator type is Nvidia Tesla H100 - 80GB.               |
| `NVIDIA_H100_MEGA_80GB`        | Accelerator type is Nvidia Tesla H100 - MEGA 80GB.          |
| `NVIDIA_H200_141GB`            | Accelerator type is Nvidia Tesla H200 - 141GB.              |
| `NVIDIA_TESLA_T4_VWS`          | Accelerator type is NVIDIA Tesla T4 Virtual Workstations.   |
| `NVIDIA_TESLA_P100_VWS`        | Accelerator type is NVIDIA Tesla P100 Virtual Workstations. |
| `NVIDIA_TESLA_P4_VWS`          | Accelerator type is NVIDIA Tesla P4 Virtual Workstations.   |
| `NVIDIA_B200`                  | Accelerator type is NVIDIA B200.                            |

## ServiceAccount

A service account that acts as an identity.

**JSON representation**

```
{
  "email": string,
  "scopes": [
    string
  ]
}
```

| Fields     |                                                                                                                                                            |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `email`    | `string` Optional. Email address of the service account.                                                                                                   |
| `scopes[]` | `string` Output only. The list of scopes to be made available for this service account. Set by the CLH to <https://www.googleapis.com/auth/cloud-platform> |

## VmImage

Definition of a custom Compute Engine virtual machine image for starting a notebook instance with the environment installed directly on the VM.

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

| Fields                                                                                                                |                                                                                                              |
|-----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| `project`                                                                                                             | `string` Required. The name of the Google Cloud project that this VM image belongs to. Format: `{projectId}` |
| Union field `image` . The reference to an external Compute Engine VM image. `image` can be only one of the following: |                                                                                                              |
| `name`                                                                                                                | `string` Optional. Use VM image name to find the image.                                                      |
| `family`                                                                                                              | `string` Optional. Use this VM image family to find the image; the newest image in this family will be used. |

## ContainerImage

Definition of a container image for starting a notebook instance with the environment installed in a container.

**JSON representation**

```
{
  "repository": string,
  "tag": string
}
```

| Fields       |                                                                                                              |
|--------------|--------------------------------------------------------------------------------------------------------------|
| `repository` | `string` Required. The path to the container image repository. For example: `gcr.io/{projectId}/{imageName}` |
| `tag`        | `string` Optional. The tag of the container image. If not specified, this defaults to the latest tag.        |

## BootDisk

The definition of a boot disk.

**JSON representation**

```
{
  "diskSizeGb": string,
  "diskType": enum (DiskType),
  "diskEncryption": enum (DiskEncryption),
  "kmsKey": string
}
```

| Fields           |                                                                                                                                                                                                                                                                                   |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `diskSizeGb`     | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. The size of the boot disk in GB attached to this instance, up to a maximum of 64000 GB (64 TB). If not specified, this defaults to the recommended value of 150GB.               |
| `diskType`       | `enum ( `[`DiskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#DiskType)` )` Optional. Indicates the type of the disk.                                                                   |
| `diskEncryption` | `enum ( `[`DiskEncryption`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#DiskEncryption)` )` Optional. Input only. Disk encryption method used on the boot and data disks, defaults to GMEK. |
| `kmsKey`         | `string` Optional. Input only. The KMS key used to encrypt the disks, only applicable if diskEncryption is CMEK. Format: `projects/{projectId}/locations/{location}/keyRings/{key_ring_id}/cryptoKeys/{key_id}` Learn more about using your own encryption keys.                  |

## DiskType

Possible disk types.

| Enums                                  |                                                                                                                    |
|----------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| `DISK_TYPE_UNSPECIFIED`                | Disk type not set.                                                                                                 |
| `PD_STANDARD`                          | Standard persistent disk type.                                                                                     |
| `PD_SSD`                               | SSD persistent disk type.                                                                                          |
| `PD_BALANCED`                          | Balanced persistent disk type.                                                                                     |
| `PD_EXTREME`                           | Extreme persistent disk type.                                                                                      |
| `HYPERDISK_BALANCED`                   | Represents the Hyperdisk Balanced persistent disk type. Can be used as a boot disk or data disk.                   |
| `HYPERDISK_EXTREME`                    | Represents the Hyperdisk Extreme persistent disk type. Can only be used as a data disk.                            |
| `HYPERDISK_THROUGHPUT`                 | Represents the Hyperdisk Throughput persistent disk type. Can only be used as a data disk.                         |
| `HYPERDISK_BALANCED_HIGH_AVAILABILITY` | Represents the Hyperdisk Balanced High Availability persistent disk type. Can be used as a boot disk or data disk. |
| `HYPERDISK_ML`                         | Represents the Hyperdisk ML persistent disk type. Can be used as a boot disk or data disk.                         |

## DiskEncryption

Definition of the disk encryption options.

| Enums                         |                                                                |
|-------------------------------|----------------------------------------------------------------|
| `DISK_ENCRYPTION_UNSPECIFIED` | Disk encryption is not specified.                              |
| `GMEK`                        | Use Google managed encryption keys to encrypt the boot disk.   |
| `CMEK`                        | Use customer managed encryption keys to encrypt the boot disk. |

## DataDisk

An instance-attached disk resource.

**JSON representation**

```
{
  "diskSizeGb": string,
  "diskType": enum (DiskType),
  "diskEncryption": enum (DiskEncryption),
  "kmsKey": string,
  "resourcePolicies": [
    string
  ]
}
```

| Fields               |                                                                                                                                                                                                                                                                                   |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `diskSizeGb`         | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. The size of the disk in GB attached to this VM instance, up to a maximum of 64000 GB (64 TB). If not specified, this defaults to 100.                                            |
| `diskType`           | `enum ( `[`DiskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#DiskType)` )` Optional. Input only. Indicates the type of the disk.                                                       |
| `diskEncryption`     | `enum ( `[`DiskEncryption`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#DiskEncryption)` )` Optional. Input only. Disk encryption method used on the boot and data disks, defaults to GMEK. |
| `kmsKey`             | `string` Optional. Input only. The KMS key used to encrypt the disks, only applicable if diskEncryption is CMEK. Format: `projects/{projectId}/locations/{location}/keyRings/{key_ring_id}/cryptoKeys/{key_id}` Learn more about using your own encryption keys.                  |
| `resourcePolicies[]` | `string` Optional. The resource policies to apply to the data disk.                                                                                                                                                                                                               |

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

| Fields                      |                                                                                                                                                                                                                                                                                                                                                   |
|-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableSecureBoot`          | `boolean` Optional. Defines whether the VM instance has Secure Boot enabled. Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails. Disabled by default.                                                  |
| `enableVtpm`                | `boolean` Optional. Defines whether the VM instance has the vTPM enabled.                                                                                                                                                                                                                                                                         |
| `enableIntegrityMonitoring` | `boolean` Optional. Defines whether the VM instance has integrity monitoring enabled. Enables monitoring and attestation of the boot integrity of the VM instance. The attestation is performed against the integrity policy baseline. This baseline is initially derived from the implicitly trusted boot image when the VM instance is created. |

## NetworkInterface

The definition of a network interface resource attached to a VM.

**JSON representation**

```
{
  "network": string,
  "subnet": string,
  "nicType": enum (NicType),
  "accessConfigs": [
    {
      object (AccessConfig)
    }
  ]
}
```

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `network`         | `string` Optional. The name of the VPC that this VM instance is in. Format: `projects/{projectId}/global/networks/{network_id}`                                                                                                                                                                                                                                                                                                       |
| `subnet`          | `string` Optional. The name of the subnet that this VM instance is in. Format: `projects/{projectId}/regions/{region}/subnetworks/{subnetwork_id}`                                                                                                                                                                                                                                                                                    |
| `nicType`         | `enum ( `[`NicType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#NicType)` )` Optional. The type of vNIC to be used on this interface. This may be gVNIC or VirtioNet.                                                                                                                                                                          |
| `accessConfigs[]` | `object ( `[`AccessConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#AccessConfig)` )` Optional. An array of configurations for this interface. Currently, only one access config, ONE_TO_ONE_NAT, is supported. If no accessConfigs specified, the instance will have an external internet access through an ephemeral external IP address. |

## NicType

The type of vNIC driver. Default should be NIC_TYPE_UNSPECIFIED.

| Enums                  |                    |
|------------------------|--------------------|
| `NIC_TYPE_UNSPECIFIED` | No type specified. |
| `VIRTIO_NET`           | VIRTIO             |
| `GVNIC`                | GVNIC              |

## AccessConfig

An access configuration attached to an instance's network interface.

**JSON representation**

```
{
  "externalIp": string
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                    |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `externalIp` | `string` An external IP address associated with this instance. Specify an unused static external IP address available to the project or leave this field undefined to use an IP from a shared ephemeral IP address pool. If you specify a static external IP address, it must live in the same region as the zone of the instance. |

## GPUDriverConfig

A GPU driver configuration

**JSON representation**

```
{
  "enableGpuDriver": boolean,
  "customGpuDriverPath": string
}
```

| Fields                |                                                                                                                                                                                                                                |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableGpuDriver`     | `boolean` Optional. Whether the end user authorizes Google Cloud to install GPU driver on this VM instance. If this field is empty or set to false, the GPU driver won't be installed. Only applicable to instances with GPUs. |
| `customGpuDriverPath` | `string` Optional. Specify a custom Cloud Storage path where the GPU driver is stored. If not specified, we'll automatically choose from official GPU drivers.                                                                 |

## ConfidentialInstanceConfig

A set of Confidential Instance options.

**JSON representation**

```
{
  "confidentialInstanceType": enum (ConfidentialInstanceType)
}
```

| Fields                     |                                                                                                                                                                                                                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `confidentialInstanceType` | `enum ( `[`ConfidentialInstanceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#ConfidentialInstanceType)` )` Optional. Defines the type of technology used by the confidential instance. |

## ConfidentialInstanceType

The type of confidential instance.

| Enums                                    |                                           |
|------------------------------------------|-------------------------------------------|
| `CONFIDENTIAL_INSTANCE_TYPE_UNSPECIFIED` | No type specified. Do not use this value. |
| `SEV`                                    | AMD Secure Encrypted Virtualization.      |

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
| `SUSPENDING`        | The instance is suspending.                                                                          |
| `SUSPENDED`         | The instance is suspended.                                                                           |

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
  "action": enum (Action),
  "targetVersion": string
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `snapshot`       | `string` Optional. The snapshot of the boot disk of this notebook instance before upgrade.                                                                                                                                                                                                                                                                                                                                                     |
| `vmImage`        | `string` Optional. The VM image before this instance upgrade.                                                                                                                                                                                                                                                                                                                                                                                  |
| `containerImage` | `string` Optional. The container image before this instance upgrade.                                                                                                                                                                                                                                                                                                                                                                           |
| `framework`      | `string` Optional. The framework of this notebook instance.                                                                                                                                                                                                                                                                                                                                                                                    |
| `version`        | `string` Optional. The version of the notebook instance before this upgrade.                                                                                                                                                                                                                                                                                                                                                                   |
| `state`          | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#State_1)` )` Output only. The state of this instance upgrade history entry.                                                                                                                                                                                                               |
| `createTime`     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Immutable. The time that this instance upgrade history entry is created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `action`         | `enum ( `[`Action`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#Action)` )` Optional. Action. Rolloback or Upgrade.                                                                                                                                                                                                                                      |
| `targetVersion`  | `string` Optional. Target VM Version, like m63.                                                                                                                                                                                                                                                                                                                                                                                                |

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

## HealthState

The instance health state.

| Enums                      |                                                                                                                            |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------|
| `HEALTH_STATE_UNSPECIFIED` | The instance substate is unknown.                                                                                          |
| `HEALTHY`                  | The instance is known to be in an healthy state (for example, critical daemons are running) Applies to ACTIVE state.       |
| `UNHEALTHY`                | The instance is known to be in an unhealthy state (for example, critical daemons are not running) Applies to ACTIVE state. |
| `AGENT_NOT_INSTALLED`      | The instance has not installed health monitoring agent. Applies to ACTIVE state.                                           |
| `AGENT_NOT_RUNNING`        | The instance health monitoring agent is not running. Applies to ACTIVE state.                                              |

| Methods                                                                                                                                                                      |                                                                       |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| [`checkUpgradability`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/checkUpgradability) | Checks whether a notebook instance is upgradable.                     |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/create)                         | Creates a new Instance in a given project and location.               |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/delete)                         | Deletes a single Instance.                                            |
| [`diagnose`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/diagnose)                     | Creates a Diagnostic File and runs Diagnostic Tool given an Instance. |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/get)                               | Gets details of a single Instance.                                    |
| [`getConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/getConfig)                   | Returns various configuration parameters.                             |
| [`getIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/getIamPolicy)             | Gets the access control policy for a resource.                        |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/list)                             | Lists instances in a given project and location.                      |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch)                           | UpdateInstance updates an Instance.                                   |
| [`reset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/reset)                           | Resets a notebook instance.                                           |
| [`resizeDisk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/resizeDisk)                 | Resize a notebook instance disk to a higher capacity.                 |
| [`restore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/restore)                       | RestoreInstance restores an Instance from a BackupSource.             |
| [`rollback`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/rollback)                     | Rollbacks a notebook instance to the previous version.                |
| [`setIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/setIamPolicy)             | Sets the access control policy on the specified resource.             |
| [`start`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/start)                           | Starts a notebook instance.                                           |
| [`stop`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/stop)                             | Stops a notebook instance.                                            |
| [`testIamPermissions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/testIamPermissions) | Returns permissions that a caller has on the specified resource.      |
| [`upgrade`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/upgrade)                       | Upgrades a notebook instance to the latest version.                   |
