---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes
title: 'REST Resource: projects.locations.runtimes'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Runtime

The definition of a Runtime for a managed notebook instance.

**JSON representation**

```
{
  "name": string,
  "state": enum (State),
  "healthState": enum (HealthState),
  "accessConfig": {
    object (RuntimeAccessConfig)
  },
  "softwareConfig": {
    object (RuntimeSoftwareConfig)
  },
  "metrics": {
    object (RuntimeMetrics)
  },
  "createTime": string,
  "updateTime": string,
  "labels": {
    string: string,
    ...
  },
  "runtimeMigrationEligibility": {
    object (RuntimeMigrationEligibility)
  },

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "virtualMachine": {
    object (VirtualMachine)
  }
  // End of mutually exclusive fields.
  "migrated": boolean
}
```

| Fields                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                     | `string` Output only. The resource name of the runtime. Format: `projects/{project}/locations/{location}/runtimes/{runtimeId}`                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `state`                                                                                                                                                                    | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#State)` )` Output only. Runtime state.                                                                                                                                                                                                                                                                                                                                                                                |
| `healthState`                                                                                                                                                              | `enum ( `[`HealthState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#HealthState)` )` Output only. Runtime healthState.                                                                                                                                                                                                                                                                                                                                                              |
| `accessConfig`                                                                                                                                                             | `object ( `[`RuntimeAccessConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#RuntimeAccessConfig)` )` The config settings for accessing runtime.                                                                                                                                                                                                                                                                                                                                   |
| `softwareConfig`                                                                                                                                                           | `object ( `[`RuntimeSoftwareConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#RuntimeSoftwareConfig)` )` The config settings for software inside the runtime.                                                                                                                                                                                                                                                                                                                     |
| `metrics`                                                                                                                                                                  | `object ( `[`RuntimeMetrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#RuntimeMetrics)` )` Output only. Contains Runtime daemon metrics such as Service status and JupyterLab stats.                                                                                                                                                                                                                                                                                              |
| `createTime`                                                                                                                                                               | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Runtime creation time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                 |
| `updateTime`                                                                                                                                                               | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Runtime update time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                   |
| `labels`                                                                                                                                                                   | `map (key: string, value: string)` Optional. The labels to associate with this Managed Notebook or Runtime. Label **keys** must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . Label **values** may be empty, but, if present, must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . No more than 32 labels can be associated with a cluster. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `runtimeMigrationEligibility`                                                                                                                                              | `object ( `[`RuntimeMigrationEligibility`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#RuntimeMigrationEligibility)` )` Output only. Checks how feasible a migration from GmN to WbI is.                                                                                                                                                                                                                                                                                             |
| Type of the runtime; currently only supports Compute Engine VM. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `virtualMachine`                                                                                                                                                           | `object ( `[`VirtualMachine`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#VirtualMachine)` )` Use a Compute Engine VM image to start the managed notebook instance.                                                                                                                                                                                                                                                                                                                  |
| End of mutually exclusive fields.                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `migrated`                                                                                                                                                                 | `boolean` Output only. Bool indicating whether this notebook has been migrated to a Workbench Instance                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

## VirtualMachine

Runtime using Virtual Machine for computing.

**JSON representation**

```
{
  "instanceName": string,
  "instanceId": string,
  "virtualMachineConfig": {
    object (VirtualMachineConfig)
  }
}
```

| Fields                 |                                                                                                                                                                                                                                        |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `instanceName`         | `string` Output only. The user-friendly name of the Managed Compute Engine instance.                                                                                                                                                   |
| `instanceId`           | `string` Output only. The unique identifier of the Managed Compute Engine instance.                                                                                                                                                    |
| `virtualMachineConfig` | `object ( `[`VirtualMachineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#VirtualMachineConfig)` )` Virtual Machine configuration settings. |

## VirtualMachineConfig

The config settings for virtual machine.

**JSON representation**

```
{
  "zone": string,
  "machineType": string,
  "containerImages": [
    {
      object (ContainerImage)
    }
  ],
  "dataDisk": {
    object (LocalDisk)
  },
  "encryptionConfig": {
    object (EncryptionConfig)
  },
  "shieldedInstanceConfig": {
    object (RuntimeShieldedInstanceConfig)
  },
  "acceleratorConfig": {
    object (RuntimeAcceleratorConfig)
  },
  "network": string,
  "subnet": string,
  "internalIpOnly": boolean,
  "tags": [
    string
  ],
  "guestAttributes": {
    string: string,
    ...
  },
  "metadata": {
    string: string,
    ...
  },
  "labels": {
    string: string,
    ...
  },
  "nicType": enum (NicType),
  "reservedIpRange": string,
  "bootImage": {
    object (BootImage)
  }
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
<td><code>zone</code></td>
<td><p><code>string</code></p>
<p>Output only. The zone where the virtual machine is located. If using regional request, the notebooks service will pick a location in the corresponding runtime region. On a get request, zone will always be present. Example: * <code>us-central1-b</code></p></td>
</tr>
<tr class="even">
<td><code>machineType</code></td>
<td><p><code>string</code></p>
<p>Required. The Compute Engine machine type used for runtimes. Short name is valid. Examples: * <code>n1-standard-2</code> * <code>e2-standard-8</code></p></td>
</tr>
<tr class="odd">
<td><code>containerImages[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ContainerImage"><code>ContainerImage</code></a><code> )</code></p>
<p>Optional. Use a list of container images to use as Kernels in the notebook instance.</p></td>
</tr>
<tr class="even">
<td><code>dataDisk</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#LocalDisk"><code>LocalDisk</code></a><code> )</code></p>
<p>Required. Data disk option configuration settings.</p></td>
</tr>
<tr class="odd">
<td><code>encryptionConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#EncryptionConfig"><code>EncryptionConfig</code></a><code> )</code></p>
<p>Optional. Encryption settings for virtual machine data disk.</p></td>
</tr>
<tr class="even">
<td><code>shieldedInstanceConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#RuntimeShieldedInstanceConfig"><code>RuntimeShieldedInstanceConfig</code></a><code> )</code></p>
<p>Optional. Shielded VM Instance configuration settings.</p></td>
</tr>
<tr class="odd">
<td><code>acceleratorConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#RuntimeAcceleratorConfig"><code>RuntimeAcceleratorConfig</code></a><code> )</code></p>
<p>Optional. The Compute Engine accelerator configuration for this runtime.</p></td>
</tr>
<tr class="even">
<td><code>network</code></td>
<td><p><code>string</code></p>
<p>Optional. The Compute Engine network to be used for machine communications. Cannot be specified with subnetwork. If neither <code>network</code> nor <code>subnet</code> is specified, the "default" network of the project is used, if it exists.</p>
<p>A full URL or partial URI. Examples:</p>
<ul>
<li><code>https://www.googleapis.com/compute/v1/projects/[projectId]/global/networks/default</code></li>
<li><code>projects/[projectId]/global/networks/default</code></li>
</ul>
<p>Runtimes are managed resources inside Google Infrastructure. Runtimes support the following network configurations:</p>
<ul>
<li>Google Managed Network (Network &amp; subnet are empty)</li>
<li>Consumer Project VPC (network &amp; subnet are required). Requires configuring Private Service Access.</li>
<li>Shared VPC (network &amp; subnet are required). Requires configuring Private Service Access.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>subnet</code></td>
<td><p><code>string</code></p>
<p>Optional. The Compute Engine subnetwork to be used for machine communications. Cannot be specified with network.</p>
<p>A full URL or partial URI are valid. Examples:</p>
<ul>
<li><code>https://www.googleapis.com/compute/v1/projects/[projectId]/regions/us-east1/subnetworks/sub0</code></li>
<li><code>projects/[projectId]/regions/us-east1/subnetworks/sub0</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>internalIpOnly</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If true, runtime will only have internal IP addresses. By default, runtimes are not restricted to internal IP addresses, and will have ephemeral external IP addresses assigned to each vm. This <code>internalIpOnly</code> restriction can only be enabled for subnetwork enabled networks, and all dependencies must be configured to be accessible without external IP addresses.</p></td>
</tr>
<tr class="odd">
<td><code>tags[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The Compute Engine network tags to add to runtime (see <a href="https://cloud.google.com/vpc/docs/add-remove-network-tags">Add network tags</a> ).</p></td>
</tr>
<tr class="even">
<td><code>guestAttributes</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Output only. The Compute Engine guest attributes. (see <a href="https://cloud.google.com/compute/docs/storing-retrieving-metadata#guestAttributes">Project and instance guest attributes</a> ).</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>metadata</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Optional. The Compute Engine metadata entries to add to virtual machine. (see <a href="https://cloud.google.com/compute/docs/storing-retrieving-metadata#project_and_instance_metadata">Project and instance metadata</a> ).</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Optional. The labels to associate with this runtime. Label <strong>keys</strong> must contain 1 to 63 characters, and must conform to <a href="https://www.ietf.org/rfc/rfc1035.txt">RFC 1035</a> . Label <strong>values</strong> may be empty, but, if present, must contain 1 to 63 characters, and must conform to <a href="https://www.ietf.org/rfc/rfc1035.txt">RFC 1035</a> . No more than 32 labels can be associated with a cluster.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>nicType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#NicType"><code>NicType</code></a><code> )</code></p>
<p>Optional. The type of vNIC to be used on this interface. This may be gVNIC or VirtioNet.</p></td>
</tr>
<tr class="even">
<td><code>reservedIpRange</code></td>
<td><p><code>string</code></p>
<p>Optional. Reserved IP Range name is used for VPC Peering. The subnetwork allocation will use the range <em>name</em> if it's assigned.</p>
<p>Example: managed-notebooks-range-c</p>
<pre data-fenced=""><code>PEERING_RANGE_NAME_3=managed-notebooks-range-c
gcloud compute addresses create $PEERING_RANGE_NAME_3 \
  --global \
  --prefix-length=24 \
  --description=&quot;Google Cloud Managed Notebooks Range 24 c&quot; \
  --network=$NETWORK \
  --addresses=192.168.0.0 \
  --purpose=VPC_PEERING</code></pre>
<p>Field value will be: <code>managed-notebooks-range-c</code></p></td>
</tr>
<tr class="odd">
<td><code>bootImage</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#BootImage"><code>BootImage</code></a><code> )</code></p>
<p>Optional. Boot image metadata used for runtime upgradeability.</p></td>
</tr>
</tbody>
</table>

## LocalDisk

A Local attached disk resource.

**JSON representation**

```
{
  "autoDelete": boolean,
  "boot": boolean,
  "deviceName": string,
  "guestOsFeatures": [
    {
      object (RuntimeGuestOsFeature)
    }
  ],
  "index": integer,
  "initializeParams": {
    object (LocalDiskInitializeParams)
  },
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
<p>Optional. Output only. Specifies whether the disk will be auto-deleted when the instance is deleted (but not when the disk is detached from the instance).</p></td>
</tr>
<tr class="even">
<td><code>boot</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Output only. Indicates that this is a boot disk. The virtual machine will use the first partition of the disk for its root filesystem.</p></td>
</tr>
<tr class="odd">
<td><code>deviceName</code></td>
<td><p><code>string</code></p>
<p>Optional. Output only. Specifies a unique device name of your choice that is reflected into the <code>/dev/disk/by-id/google-*</code> tree of a Linux operating system running within the instance. This name can be used to reference the device for mounting, resizing, and so on, from within the instance.</p>
<p>If not specified, the server chooses a default device name to apply to this disk, in the form persistent-disk-x, where x is a number assigned by Google Compute Engine. This field is only applicable for persistent disks.</p></td>
</tr>
<tr class="even">
<td><code>guestOsFeatures[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#RuntimeGuestOsFeature"><code>RuntimeGuestOsFeature</code></a><code> )</code></p>
<p>Output only. Indicates a list of features to enable on the guest operating system. Applicable only for bootable images. Read Enabling guest operating system features to see a list of available options.</p></td>
</tr>
<tr class="odd">
<td><code>index</code></td>
<td><p><code>integer</code></p>
<p>Output only. A zero-based index to this disk, where 0 is reserved for the boot disk. If you have many disks attached to an instance, each disk would have a unique index number.</p></td>
</tr>
<tr class="even">
<td><code>initializeParams</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#LocalDiskInitializeParams"><code>LocalDiskInitializeParams</code></a><code> )</code></p>
<p>Input only. Specifies the parameters for a new disk that will be created alongside the new instance. Use initialization parameters to create boot disks or local SSDs attached to the new instance.</p>
<p>This property is mutually exclusive with the source property; you can only define one or the other, but not both.</p></td>
</tr>
<tr class="odd">
<td><code>interface</code></td>
<td><p><code>string</code></p>
<p>Specifies the disk interface to use for attaching this disk, which is either SCSI or NVME. The default is SCSI. Persistent disks must always use SCSI and the request will fail if you attempt to attach a persistent disk in any other format than SCSI. Local SSDs can use either NVME or SCSI. For performance characteristics of SCSI over NVMe, see Local SSD performance. Valid values:</p>
<ul>
<li><code>NVME</code></li>
<li><code>SCSI</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>kind</code></td>
<td><p><code>string</code></p>
<p>Output only. Type of the resource. Always compute#attachedDisk for attached disks.</p></td>
</tr>
<tr class="odd">
<td><code>licenses[]</code></td>
<td><p><code>string</code></p>
<p>Output only. Any valid publicly visible licenses.</p></td>
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
<p>Specifies a valid partial or full URL to an existing Persistent Disk resource.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Specifies the type of the disk, either <code>SCRATCH</code> or <code>PERSISTENT</code> . If not specified, the default is <code>PERSISTENT</code> . Valid values:</p>
<ul>
<li><code>PERSISTENT</code></li>
<li><code>SCRATCH</code></li>
</ul></td>
</tr>
</tbody>
</table>

## RuntimeGuestOsFeature

Optional. A list of features to enable on the guest operating system. Applicable only for bootable images. Read [Enabling guest operating system features](https://cloud.google.com/compute/docs/images/create-delete-deprecate-private-images#guest-os-features) to see a list of available options. Guest OS features for boot disk.

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
<p>The ID of a supported feature. Read <a href="https://cloud.google.com/compute/docs/images/create-delete-deprecate-private-images#guest-os-features">Enabling guest operating system features</a> to see a list of available options.</p>
<p>Valid values:</p>
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

## LocalDiskInitializeParams

Input only. Specifies the parameters for a new disk that will be created alongside the new instance. Use initialization parameters to create boot disks or local SSDs attached to the new runtime. This property is mutually exclusive with the source property; you can only define one or the other, but not both.

**JSON representation**

```
{
  "description": string,
  "diskName": string,
  "diskSizeGb": string,
  "diskType": enum (DiskType),
  "labels": {
    string: string,
    ...
  }
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                 |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `description` | `string` Optional. Provide this property when creating the disk.                                                                                                                                                                                                                                                |
| `diskName`    | `string` Optional. Specifies the disk name. If not specified, the default is to use the name of the instance. If the disk with the instance name exists already in the given zone/region, a new name will be automatically generated.                                                                           |
| `diskSizeGb`  | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Specifies the size of the disk in base-2 GB. If not specified, the disk will be the same size as the image (usually 10GB). If specified, the size must be equal to or larger than 10GB. Default 100 GB.        |
| `diskType`    | `enum ( `[`DiskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#DiskType)` )` Input only. The type of the boot disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).                   |
| `labels`      | `map (key: string, value: string)` Optional. Labels to apply to this disk. These can be later modified by the disks.setLabels method. This field is only applicable for persistent disks. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

## DiskType

Possible disk types.

| Enums                   |                                |
|-------------------------|--------------------------------|
| `DISK_TYPE_UNSPECIFIED` | Disk type not set.             |
| `PD_STANDARD`           | Standard persistent disk type. |
| `PD_SSD`                | SSD persistent disk type.      |
| `PD_BALANCED`           | Balanced persistent disk type. |
| `PD_EXTREME`            | Extreme persistent disk type.  |

## EncryptionConfig

Represents a custom encryption key configuration that can be applied to a resource. This will encrypt all disks in Virtual Machine.

**JSON representation**

```
{
  "kmsKey": string
}
```

| Fields   |                                                                                                                                                                                                                                                       |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKey` | `string` The Cloud KMS resource identifier of the customer-managed encryption key used to protect a resource, such as a disks. It has the following format: `projects/{PROJECT_ID}/locations/{REGION}/keyRings/{KEY_RING_NAME}/cryptoKeys/{KEY_NAME}` |

## RuntimeShieldedInstanceConfig

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

## RuntimeAcceleratorConfig

Definition of the types of hardware accelerators that can be used. See [Compute Engine AcceleratorTypes](https://cloud.google.com/compute/docs/reference/beta/acceleratorTypes) . Examples:

- `nvidia-tesla-k80`
- `nvidia-tesla-p100`
- `nvidia-tesla-v100`
- `nvidia-tesla-p4`
- `nvidia-tesla-t4`
- `nvidia-tesla-a100`

**JSON representation**

```
{
  "type": enum (AcceleratorType),
  "coreCount": string
}
```

| Fields      |                                                                                                                                                                                                       |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`      | `enum ( `[`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#AcceleratorType)` )` Accelerator model. |
| `coreCount` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Count of cores of this accelerator.                                                                            |

## AcceleratorType

Type of this accelerator.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>ACCELERATOR_TYPE_UNSPECIFIED</code></td>
<td>Accelerator type is not specified.</td>
</tr>
<tr class="even">
<td><code>NVIDIA_TESLA_K80</code></td>
<td><p>Accelerator type is Nvidia Tesla K80.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>NVIDIA_TESLA_P100</code></td>
<td>Accelerator type is Nvidia Tesla P100.</td>
</tr>
<tr class="even">
<td><code>NVIDIA_TESLA_V100</code></td>
<td>Accelerator type is Nvidia Tesla V100.</td>
</tr>
<tr class="odd">
<td><code>NVIDIA_TESLA_P4</code></td>
<td>Accelerator type is Nvidia Tesla P4.</td>
</tr>
<tr class="even">
<td><code>NVIDIA_TESLA_T4</code></td>
<td>Accelerator type is Nvidia Tesla T4.</td>
</tr>
<tr class="odd">
<td><code>NVIDIA_TESLA_A100</code></td>
<td>Accelerator type is Nvidia Tesla A100 - 40GB.</td>
</tr>
<tr class="even">
<td><code>NVIDIA_L4</code></td>
<td>Accelerator type is Nvidia L4.</td>
</tr>
<tr class="odd">
<td><code>TPU_V2</code></td>
<td>(Coming soon) Accelerator type is TPU V2.</td>
</tr>
<tr class="even">
<td><code>TPU_V3</code></td>
<td>(Coming soon) Accelerator type is TPU V3.</td>
</tr>
<tr class="odd">
<td><code>NVIDIA_TESLA_T4_VWS</code></td>
<td>Accelerator type is NVIDIA Tesla T4 Virtual Workstations.</td>
</tr>
<tr class="even">
<td><code>NVIDIA_TESLA_P100_VWS</code></td>
<td>Accelerator type is NVIDIA Tesla P100 Virtual Workstations.</td>
</tr>
<tr class="odd">
<td><code>NVIDIA_TESLA_P4_VWS</code></td>
<td>Accelerator type is NVIDIA Tesla P4 Virtual Workstations.</td>
</tr>
</tbody>
</table>

## NicType

The type of vNIC driver. Default should be UNSPECIFIED_NIC_TYPE.

| Enums                  |                    |
|------------------------|--------------------|
| `UNSPECIFIED_NIC_TYPE` | No type specified. |
| `VIRTIO_NET`           | VIRTIO             |
| `GVNIC`                | GVNIC              |

## BootImage

This type has no fields.

Definition of the boot image used by the Runtime. Used to facilitate runtime upgradeability.

## State

The definition of the states of this runtime.

| Enums               |                                                                                                                         |
|---------------------|-------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | State is not specified.                                                                                                 |
| `STARTING`          | The compute layer is starting the runtime. It is not ready for use.                                                     |
| `PROVISIONING`      | The compute layer is installing required frameworks and registering the runtime with notebook proxy. It cannot be used. |
| `ACTIVE`            | The runtime is currently running. It is ready for use.                                                                  |
| `STOPPING`          | The control logic is stopping the runtime. It cannot be used.                                                           |
| `STOPPED`           | The runtime is stopped. It cannot be used.                                                                              |
| `DELETING`          | The runtime is being deleted. It cannot be used.                                                                        |
| `UPGRADING`         | The runtime is upgrading. It cannot be used.                                                                            |
| `INITIALIZING`      | The runtime is being created and set up. It is not ready for use.                                                       |

## HealthState

The runtime substate.

| Enums                      |                                                                                                                           |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------|
| `HEALTH_STATE_UNSPECIFIED` | The runtime substate is unknown.                                                                                          |
| `HEALTHY`                  | The runtime is known to be in an healthy state (for example, critical daemons are running) Applies to ACTIVE state.       |
| `UNHEALTHY`                | The runtime is known to be in an unhealthy state (for example, critical daemons are not running) Applies to ACTIVE state. |
| `AGENT_NOT_INSTALLED`      | The runtime has not installed health monitoring agent. Applies to ACTIVE state.                                           |
| `AGENT_NOT_RUNNING`        | The runtime health monitoring agent is not running. Applies to ACTIVE state.                                              |

## RuntimeAccessConfig

Specifies the login configuration for Runtime

**JSON representation**

```
{
  "accessType": enum (RuntimeAccessType),
  "runtimeOwner": string,
  "proxyUri": string
}
```

| Fields         |                                                                                                                                                                                                                               |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `accessType`   | `enum ( `[`RuntimeAccessType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#RuntimeAccessType)` )` The type of access mode this instance. |
| `runtimeOwner` | `string` The owner of this runtime after creation. Format: `alias@example.com` Currently supports one owner only.                                                                                                             |
| `proxyUri`     | `string` Output only. The proxy endpoint that is used to access the runtime.                                                                                                                                                  |

## RuntimeAccessType

Possible ways to access runtime. Authentication mode. Currently supports: Single User only.

| Enums                             |                                                                                                                                                                                                                                      |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `RUNTIME_ACCESS_TYPE_UNSPECIFIED` | Unspecified access.                                                                                                                                                                                                                  |
| `SINGLE_USER`                     | Single user login.                                                                                                                                                                                                                   |
| `SERVICE_ACCOUNT`                 | Service Account mode. In Service Account mode, Runtime creator will specify a SA that exists in the consumer project. Using Runtime Service Account field. Users accessing the Runtime need ActAs (Service Account User) permission. |

## RuntimeSoftwareConfig

Specifies the selection and configuration of software inside the runtime. The properties to set on runtime. Properties keys are specified in `key:value` format, for example:

- `idleShutdown: true`
- `idleShutdownTimeout: 180`
- `enableHealthMonitoring: true`

**JSON representation**

```
{
  "notebookUpgradeSchedule": string,
  "idleShutdownTimeout": integer,
  "installGpuDriver": boolean,
  "customGpuDriverPath": string,
  "postStartupScript": string,
  "kernels": [
    {
      object (ContainerImage)
    }
  ],
  "postStartupScriptBehavior": enum (PostStartupScriptBehavior),
  "enableHealthMonitoring": boolean,
  "idleShutdown": boolean,
  "upgradeable": boolean,
  "disableTerminal": boolean,
  "version": string,
  "mixerDisabled": boolean
}
```

| Fields                      |                                                                                                                                                                                                                                              |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `notebookUpgradeSchedule`   | `string` Cron expression in UTC timezone, used to schedule instance auto upgrade. Please follow the [cron format](https://en.wikipedia.org/wiki/Cron) .                                                                                      |
| `idleShutdownTimeout`       | `integer` Time in minutes to wait before shutting down runtime. Default: 180 minutes                                                                                                                                                         |
| `installGpuDriver`          | `boolean` Install Nvidia Driver automatically. Default: True                                                                                                                                                                                 |
| `customGpuDriverPath`       | `string` Specify a custom Cloud Storage path where the GPU driver is stored. If not specified, we'll automatically choose from official GPU drivers.                                                                                         |
| `postStartupScript`         | `string` Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path ( `gs://path-to-file/file-name` ).                                                             |
| `kernels[]`                 | `object ( `[`ContainerImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ContainerImage)` )` Optional. Use a list of container images to use as Kernels in the notebook instance.  |
| `postStartupScriptBehavior` | `enum ( `[`PostStartupScriptBehavior`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#PostStartupScriptBehavior)` )` Behavior for the post startup script. |
| `enableHealthMonitoring`    | `boolean` Verifies core internal services are running. Default: True                                                                                                                                                                         |
| `idleShutdown`              | `boolean` Runtime will automatically shutdown after idle_shutdown_time. Default: True                                                                                                                                                        |
| `upgradeable`               | `boolean` Output only. Bool indicating whether an newer image is available in an image family.                                                                                                                                               |
| `disableTerminal`           | `boolean` Bool indicating whether JupyterLab terminal will be available or not. Default: False                                                                                                                                               |
| `version`                   | `string` Output only. version of boot image such as M100, from release label of the image.                                                                                                                                                   |
| `mixerDisabled`             | `boolean` Bool indicating whether mixer client should be disabled. Default: False                                                                                                                                                            |

## PostStartupScriptBehavior

Behavior for the post startup script.

| Enums                                      |                                                                           |
|--------------------------------------------|---------------------------------------------------------------------------|
| `POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED` | Unspecified post startup script behavior. Will run only once at creation. |
| `RUN_EVERY_START`                          | Runs the post startup script provided during creation at every start.     |
| `DOWNLOAD_AND_RUN_EVERY_START`             | Downloads and runs the provided post startup script at every start.       |

## RuntimeMetrics

Contains runtime daemon metrics, such as OS and kernels and sessions stats.

**JSON representation**

```
{
  "systemMetrics": {
    string: string,
    ...
  }
}
```

| Fields          |                                                                                                                                                                                           |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `systemMetrics` | `map (key: string, value: string)` Output only. The system metrics. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

## RuntimeMigrationEligibility

RuntimeMigrationEligibility represents the feasibility information of a migration from GmN to WbI.

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

| Fields       |                                                                                                                                                                                                                                                                                        |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `warnings[]` | `enum ( `[`Warning`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#Warning)` )` Output only. Certain configurations will be defaulted during the migration.                                         |
| `errors[]`   | `enum ( `[`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#Error)` )` Output only. Certain configurations make the GmN ineligible for an automatic migration. A manual migration is required. |

## Warning

A migration warning message means certain configurations will be defaulted during the migration.

| Enums                          |                                                                                                                                                              |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `WARNING_UNSPECIFIED`          | Default type.                                                                                                                                                |
| `UNSUPPORTED_ACCELERATOR_TYPE` | The GmN uses an accelerator type that's unsupported in WbI. It will be migrated without an accelerator. Users can attach an accelerator after the migration. |
| `UNSUPPORTED_OS`               | The GmN uses an operating system that's unsupported in WbI (e.g. Debian 10). It will be replaced with Debian 11 in WbI.                                      |
| `RESERVED_IP_RANGE`            | This GmN is configured with reserved IP range, which is no longer applicable in WbI.                                                                         |
| `GOOGLE_MANAGED_NETWORK`       | This GmN is configured with a Google managed network. Please provide the `network` and `subnet` options for the migration.                                   |
| `POST_STARTUP_SCRIPT`          | This GmN is configured with a post startup script. Please optionally provide the `postStartupScriptOption` for the migration.                                |
| `SINGLE_USER`                  | This GmN is configured with single user mode. Please optionally provide the `serviceAccount` option for the migration.                                       |

## Error

A migration error message means certain configurations make the GmN ineligible for an automatic migration. A manual migration is required.

| Enums               |                                                                        |
|---------------------|------------------------------------------------------------------------|
| `ERROR_UNSPECIFIED` | Default type.                                                          |
| `CUSTOM_CONTAINER`  | The GmN is configured with custom container(s) and cannot be migrated. |

| Methods                                                                                                                                                                     |                                                                  |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/create)                         | Creates a new Runtime in a given project and location.           |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/delete)                         | Deletes a single Runtime.                                        |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/get)                               | Gets details of a single Runtime.                                |
| [`getIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/getIamPolicy)             | Gets the access control policy for a resource.                   |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/list)                             | Lists Runtimes in a given project and location.                  |
| [`migrate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/migrate)                       | Migrate an existing Runtime to a new Workbench Instance.         |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/patch)                           | Update Notebook Runtime configuration.                           |
| [`reportEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/reportEvent)               | Reports and processes a runtime event.                           |
| [`reset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/reset)                           | Resets a Managed Notebook Runtime.                               |
| [`setIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/setIamPolicy)             | Sets the access control policy on the specified resource.        |
| [`start`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/start)                           | Starts a Managed Notebook Runtime.                               |
| [`stop`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/stop)                             | Stops a Managed Notebook Runtime.                                |
| [`switch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/switch)                         | Switch a Managed Notebook Runtime.                               |
| [`testIamPermissions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/testIamPermissions) | Returns permissions that a caller has on the specified resource. |
