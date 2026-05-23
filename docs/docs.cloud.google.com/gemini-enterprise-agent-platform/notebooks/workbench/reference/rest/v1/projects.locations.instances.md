---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances
title: 'REST Resource: projects.locations.instances'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Instance

The definition of a notebook instance.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;postStartupScript&quot;: string,&quot;proxyUri&quot;: string,&quot;instanceOwners&quot;: [string],&quot;serviceAccount&quot;: string,&quot;serviceAccountScopes&quot;: [string],&quot;machineType&quot;: string,&quot;acceleratorConfig&quot;: {object (AcceleratorConfig)},&quot;state&quot;: enum (State),&quot;installGpuDriver&quot;: boolean,&quot;customGpuDriverPath&quot;: string,&quot;bootDiskType&quot;: enum (DiskType),&quot;bootDiskSizeGb&quot;: string,&quot;dataDiskType&quot;: enum (DiskType),&quot;dataDiskSizeGb&quot;: string,&quot;noRemoveDataDisk&quot;: boolean,&quot;diskEncryption&quot;: enum (DiskEncryption),&quot;kmsKey&quot;: string,&quot;disks&quot;: [{object (Disk)}],&quot;shieldedInstanceConfig&quot;: {object (ShieldedInstanceConfig)},&quot;noPublicIp&quot;: boolean,&quot;noProxyAccess&quot;: boolean,&quot;network&quot;: string,&quot;subnet&quot;: string,&quot;labels&quot;: {string: string,...},&quot;metadata&quot;: {string: string,...},&quot;tags&quot;: [string],&quot;upgradeHistory&quot;: [{object (UpgradeHistoryEntry)}],&quot;nicType&quot;: enum (NicType),&quot;reservationAffinity&quot;: {object (ReservationAffinity)},&quot;creator&quot;: string,&quot;canIpForward&quot;: boolean,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;instanceMigrationEligibility&quot;: {object (InstanceMigrationEligibility)},// Union field environment can be only one of the following:&quot;vmImage&quot;: {object (VmImage)},&quot;containerImage&quot;: {object (ContainerImage)}// End of list of possible types for union field environment.&quot;migrated&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. The name of this notebook instance. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}`

`postStartupScript`

`string`

Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path ( `gs://path-to-file/file-name` ).

`proxyUri`

`string`

Output only. The proxy endpoint that is used to access the Jupyter notebook.

`instanceOwners[]`

`string`

Input only. The owner of this instance after creation. Format: `alias@example.com`

Currently supports one owner only. If not specified, all of the service account users of your VM instance's service account can use the instance.

`serviceAccount`

`string`

The service account on this instance, giving access to other Google Cloud services. You can use any service account within the same project, but you must have the service account user permission to use the instance.

If not specified, the [Compute Engine default service account](https://cloud.google.com/compute/docs/access/service-accounts#default_service_account) is used.

`serviceAccountScopes[]`

`string`

Optional. The URIs of service account scopes to be included in Compute Engine instances.

If not specified, the following [scopes](https://cloud.google.com/compute/docs/access/service-accounts#accesscopesiam) are defined: - <https://www.googleapis.com/auth/cloud-platform> - <https://www.googleapis.com/auth/userinfo.email> If not using default scopes, you need at least: <https://www.googleapis.com/auth/compute>

`machineType`

`string`

Required. The [Compute Engine machine type](https://cloud.google.com/compute/docs/machine-resource) of this instance.

`acceleratorConfig`

` object ( AcceleratorConfig  ` )

The hardware accelerator used on this instance. If you use accelerators, make sure that your configuration has [enough vCPUs and memory to support the `machineType` you have selected](https://cloud.google.com/compute/docs/gpus/#gpus-list) .

`state`

` enum ( State  ` )

Output only. The state of this instance.

`installGpuDriver`

`boolean`

Whether the end user authorizes Google Cloud to install GPU driver on this instance. If this field is empty or set to false, the GPU driver won't be installed. Only applicable to instances with GPUs.

`customGpuDriverPath`

`string`

Specify a custom Cloud Storage path where the GPU driver is stored. If not specified, we'll automatically choose from official GPU drivers.

`bootDiskType`

` enum ( DiskType  ` )

Input only. The type of the boot disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).

`bootDiskSizeGb`

`string ( int64 format)`

Input only. The size of the boot disk in GB attached to this instance, up to a maximum of 64000 GB (64 TB). The minimum recommended value is 100 GB. If not specified, this defaults to 100.

`dataDiskType`

` enum ( DiskType  ` )

Input only. The type of the data disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).

`dataDiskSizeGb`

`string ( int64 format)`

Input only. The size of the data disk in GB attached to this instance, up to a maximum of 64000 GB (64 TB). You can choose the size of the data disk based on how big your notebooks and data are. If not specified, this defaults to 100.

`noRemoveDataDisk`

`boolean`

Input only. If true, the data disk will not be auto deleted when deleting the instance.

`diskEncryption`

` enum ( DiskEncryption  ` )

Input only. Disk encryption method used on the boot and data disks, defaults to GMEK.

`kmsKey`

`string`

Input only. The KMS key used to encrypt the disks, only applicable if diskEncryption is CMEK. Format: `projects/{projectId}/locations/{location}/keyRings/{key_ring_id}/cryptoKeys/{key_id}`

Learn more about [using your own encryption keys](https://docs.cloud.google.com/kms/docs/quickstart) .

`disks[]`

` object ( Disk  ` )

Output only. Attached disks to notebook instance.

`shieldedInstanceConfig`

` object ( ShieldedInstanceConfig  ` )

Optional. Shielded VM configuration. [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) .

`noPublicIp`

`boolean`

If true, no external IP will be assigned to this instance.

`noProxyAccess`

`boolean`

If true, the notebook instance will not register with the proxy.

`network`

`string`

The name of the VPC that this instance is in. Format: `projects/{projectId}/global/networks/{network_id}`

`subnet`

`string`

The name of the subnet that this instance is in. Format: `projects/{projectId}/regions/{region}/subnetworks/{subnetwork_id}`

`labels`

`map (key: string, value: string)`

Labels to apply to this instance. These can be later modified by the setLabels method.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`metadata`

`map (key: string, value: string)`

Custom metadata to apply to this instance. For example, to specify a Cloud Storage bucket for automatic backup, you can use the `gcs-data-bucket` metadata tag. Format: `"--metadata=gcs-data-bucket=BUCKET"` .

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`tags[]`

`string`

Optional. The Compute Engine network tags to add to runtime (see [Add network tags](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).

`upgradeHistory[]`

` object ( UpgradeHistoryEntry  ` )

The upgrade history of this instance.

`nicType`

` enum ( NicType  ` )

Optional. The type of vNIC to be used on this interface. This may be gVNIC or VirtioNet.

`reservationAffinity`

` object ( ReservationAffinity  ` )

Optional. The optional reservation affinity. Setting this field will apply the specified [Zonal Compute Reservation](https://cloud.google.com/compute/docs/instances/reserving-zonal-resources) to this notebook instance.

`creator`

`string`

Output only. Email address of entity that sent original instances.create request.

`canIpForward`

`boolean`

Optional. Flag to enable ip forwarding or not, default false/off. <https://cloud.google.com/vpc/docs/using-routes#canipforward>

`createTime`

` string ( Timestamp  ` format)

Output only. Instance creation time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Instance update time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`instanceMigrationEligibility`

` object ( InstanceMigrationEligibility  ` )

Output only. Checks how feasible a migration from UmN to WbI is.

Union field `environment` . Type of the environment; can be one of VM image, or container image. `environment` can be only one of the following:

`vmImage`

` object ( VmImage  ` )

Use a Compute Engine VM image to start the notebook instance.

`containerImage`

` object ( ContainerImage  ` )

Use a container image to start the notebook instance.

`migrated`

`boolean`

Output only. Bool indicating whether this notebook has been migrated to a Workbench Instance

## AcceleratorConfig

Definition of a hardware accelerator. Note that not all combinations of `type` and `coreCount` are valid. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus/#gpus-list) to find a valid combination. TPUs are not supported.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (AcceleratorType),&quot;coreCount&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

` enum ( AcceleratorType  ` )

Type of this accelerator.

`coreCount`

`string ( int64 format)`

Count of cores of this accelerator.

## AcceleratorType

Definition of the types of hardware accelerators that can be used on this instance.

Enums

`ACCELERATOR_TYPE_UNSPECIFIED`

Accelerator type is not specified.

`NVIDIA_TESLA_K80`

Accelerator type is Nvidia Tesla K80.

`NVIDIA_TESLA_P100`

Accelerator type is Nvidia Tesla P100.

`NVIDIA_TESLA_V100`

Accelerator type is Nvidia Tesla V100.

`NVIDIA_TESLA_P4`

Accelerator type is Nvidia Tesla P4.

`NVIDIA_TESLA_T4`

Accelerator type is Nvidia Tesla T4.

`NVIDIA_TESLA_A100`

Accelerator type is Nvidia Tesla A100.

`NVIDIA_L4`

Accelerator type is Nvidia Tesla L4.

`NVIDIA_A100_80GB`

Accelerator type is Nvidia Tesla A100 80GB.

`NVIDIA_TESLA_T4_VWS`

Accelerator type is NVIDIA Tesla T4 Virtual Workstations.

`NVIDIA_TESLA_P100_VWS`

Accelerator type is NVIDIA Tesla P100 Virtual Workstations.

`NVIDIA_TESLA_P4_VWS`

Accelerator type is NVIDIA Tesla P4 Virtual Workstations.

`NVIDIA_H100_80GB`

Accelerator type is NVIDIA H100 80GB.

`NVIDIA_H100_MEGA_80GB`

Accelerator type is NVIDIA H100 Mega 80GB.

`TPU_V2`

(Coming soon) Accelerator type is TPU V2.

`TPU_V3`

(Coming soon) Accelerator type is TPU V3.

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

`REGISTERING`

The instance is getting registered.

`SUSPENDING`

The instance is suspending.

`SUSPENDED`

The instance is suspended.

## DiskType

Possible disk types for notebook instances.

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

## DiskEncryption

Definition of the disk encryption options.

Enums

`DISK_ENCRYPTION_UNSPECIFIED`

Disk encryption is not specified.

`GMEK`

Use Google managed encryption keys to encrypt the boot disk.

`CMEK`

Use customer managed encryption keys to encrypt the boot disk.

## Disk

An instance-attached disk resource.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;autoDelete&quot;: boolean,&quot;boot&quot;: boolean,&quot;deviceName&quot;: string,&quot;diskSizeGb&quot;: string,&quot;guestOsFeatures&quot;: [{object (GuestOsFeature)}],&quot;index&quot;: string,&quot;interface&quot;: string,&quot;kind&quot;: string,&quot;licenses&quot;: [string],&quot;mode&quot;: string,&quot;source&quot;: string,&quot;type&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`autoDelete`

`boolean`

Indicates whether the disk will be auto-deleted when the instance is deleted (but not when the disk is detached from the instance).

`boot`

`boolean`

Indicates that this is a boot disk. The virtual machine will use the first partition of the disk for its root filesystem.

`deviceName`

`string`

Indicates a unique device name of your choice that is reflected into the `/dev/disk/by-id/google-*` tree of a Linux operating system running within the instance. This name can be used to reference the device for mounting, resizing, and so on, from within the instance.

If not specified, the server chooses a default device name to apply to this disk, in the form persistent-disk-x, where x is a number assigned by Google Compute Engine.This field is only applicable for persistent disks.

`diskSizeGb`

`string ( int64 format)`

Indicates the size of the disk in base-2 GB.

`guestOsFeatures[]`

` object ( GuestOsFeature  ` )

Indicates a list of features to enable on the guest operating system. Applicable only for bootable images. Read Enabling guest operating system features to see a list of available options.

`index`

`string ( int64 format)`

A zero-based index to this disk, where 0 is reserved for the boot disk. If you have many disks attached to an instance, each disk would have a unique index number.

`interface`

`string`

Indicates the disk interface to use for attaching this disk, which is either SCSI or NVME. The default is SCSI. Persistent disks must always use SCSI and the request will fail if you attempt to attach a persistent disk in any other format than SCSI. Local SSDs can use either NVME or SCSI. For performance characteristics of SCSI over NVMe, see Local SSD performance. Valid values:

  - `NVME`
  - `SCSI`

`kind`

`string`

Type of the resource. Always compute\#attachedDisk for attached disks.

`licenses[]`

`string`

A list of publicly visible licenses. Reserved for Google's use. A License represents billing and aggregate usage data for public and marketplace images.

`mode`

`string`

The mode in which to attach this disk, either `READ_WRITE` or `READ_ONLY` . If not specified, the default is to attach the disk in `READ_WRITE` mode. Valid values:

  - `READ_ONLY`
  - `READ_WRITE`

`source`

`string`

Indicates a valid partial or full URL to an existing Persistent Disk resource.

`type`

`string`

Indicates the type of the disk, either `SCRATCH` or `PERSISTENT` . Valid values:

  - `PERSISTENT`
  - `SCRATCH`

## GuestOsFeature

Guest OS features for boot disk.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;type&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

`string`

The ID of a supported feature. Read Enabling guest operating system features to see a list of available options. Valid values:

  - `FEATURE_TYPE_UNSPECIFIED`
  - `MULTI_IP_SUBNET`
  - `SECURE_BOOT`
  - `UEFI_COMPATIBLE`
  - `VIRTIO_SCSI_MULTIQUEUE`
  - `WINDOWS`

## ShieldedInstanceConfig

A set of Shielded Instance options. See [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) . Not all combinations are valid.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;enableSecureBoot&quot;: boolean,
  &quot;enableVtpm&quot;: boolean,
  &quot;enableIntegrityMonitoring&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enableSecureBoot`

`boolean`

Defines whether the instance has Secure Boot enabled.

Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails. Disabled by default.

`enableVtpm`

`boolean`

Defines whether the instance has the vTPM enabled. Enabled by default.

`enableIntegrityMonitoring`

`boolean`

Defines whether the instance has integrity monitoring enabled.

Enables monitoring and attestation of the boot integrity of the instance. The attestation is performed against the integrity policy baseline. This baseline is initially derived from the implicitly trusted boot image when the instance is created. Enabled by default.

## UpgradeHistoryEntry

The entry of VM image upgrade history.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;snapshot&quot;: string,&quot;vmImage&quot;: string,&quot;containerImage&quot;: string,&quot;framework&quot;: string,&quot;version&quot;: string,&quot;state&quot;: enum (State),&quot;createTime&quot;: string,&quot;targetImage&quot;: string,&quot;action&quot;: enum (Action),&quot;targetVersion&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`snapshot`

`string`

The snapshot of the boot disk of this notebook instance before upgrade.

`vmImage`

`string`

The VM image before this instance upgrade.

`containerImage`

`string`

The container image before this instance upgrade.

`framework`

`string`

The framework of this notebook instance.

`version`

`string`

The version of the notebook instance before this upgrade.

`state`

` enum ( State  ` )

The state of this instance upgrade history entry.

`createTime`

` string ( Timestamp  ` format)

The time that this instance upgrade history entry is created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

` targetImage (deprecated)  `

`string`

> This item is deprecated\!

Target VM Image. Format: `ainotebooks-vm/project/image-name/name` .

`action`

` enum ( Action  ` )

Action. Rolloback or Upgrade.

`targetVersion`

`string`

Target VM Version, like m63.

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

## Action

The definition of operations of this upgrade history entry.

Enums

`ACTION_UNSPECIFIED`

Operation is not specified.

`UPGRADE`

Upgrade.

`ROLLBACK`

Rollback.

## NicType

The type of vNIC driver. Default should be UNSPECIFIED\_NIC\_TYPE.

Enums

`UNSPECIFIED_NIC_TYPE`

No type specified.

`VIRTIO_NET`

VIRTIO

`GVNIC`

GVNIC

## ReservationAffinity

Reservation Affinity for consuming Zonal reservation.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;consumeReservationType&quot;: enum (Type),&quot;key&quot;: string,&quot;values&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`consumeReservationType`

` enum ( Type  ` )

Optional. Type of reservation to consume

`key`

`string`

Optional. Corresponds to the label key of reservation resource.

`values[]`

`string`

Optional. Corresponds to the label values of reservation resource.

## Type

Indicates whether to consume capacity from an reservation or not.

Enums

`TYPE_UNSPECIFIED`

Default type.

`NO_RESERVATION`

Do not consume from any allocated capacity.

`ANY_RESERVATION`

Consume any reservation available.

`SPECIFIC_RESERVATION`

Must consume from a specific reservation. Must specify key value fields for specifying the reservations.

## InstanceMigrationEligibility

InstanceMigrationEligibility represents the feasibility information of a migration from UmN to WbI.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;warnings&quot;: [enum (Warning)],&quot;errors&quot;: [enum (Error)]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`warnings[]`

` enum ( Warning  ` )

Output only. Certain configurations will be defaulted during the migration.

`errors[]`

` enum ( Error  ` )

Output only. Certain configurations make the UmN ineligible for an automatic migration. A manual migration is required.

## Warning

A migration warning message means certain configurations will be defaulted during the migration.

Enums

`WARNING_UNSPECIFIED`

Default type.

`UNSUPPORTED_MACHINE_TYPE`

The UmN uses an machine type that's unsupported in WbI. It will be migrated with the default machine type e2-standard-4. Users can change the machine type after the migration.

`UNSUPPORTED_ACCELERATOR_TYPE`

The UmN uses an accelerator type that's unsupported in WbI. It will be migrated without an accelerator. User can attach an accelerator after the migration.

`UNSUPPORTED_OS`

The UmN uses an operating system that's unsupported in WbI (e.g. Debian 10, Ubuntu). It will be replaced with Debian 11 in WbI.

`NO_REMOVE_DATA_DISK`

This UmN is configured with noRemoveDataDisk, which is no longer available in WbI.

`GCS_BACKUP`

This UmN is configured with the Cloud Storage backup feature, which is no longer available in WbI.

`POST_STARTUP_SCRIPT`

This UmN is configured with a post startup script. Please optionally provide the `postStartupScriptOption` for the migration.

## Error

A migration error message means certain configurations make the UmN ineligible for an automatic migration. A manual migration is required.

Enums

`ERROR_UNSPECIFIED`

Default type.

`DATAPROC_HUB`

The UmN uses Dataproc Hub and cannot be migrated.

## Methods

### `            create           `

Creates a new Instance in a given project and location.

### `            delete           `

Deletes a single Instance.

### `            diagnose           `

Creates a Diagnostic File and runs Diagnostic Tool given an Instance.

### `            get           `

Gets details of a single Instance.

### `            getIamPolicy           `

Gets the access control policy for a resource.

### `            getInstanceHealth           `

Checks whether a notebook instance is healthy.

### `            isUpgradeable           `

Checks whether a notebook instance is upgradable.

### `            list           `

Lists instances in a given project and location.

### `            migrate           `

Migrates an existing User-Managed Notebook to Workbench Instances.

### `            register           `

Registers an existing legacy notebook instance to the Notebooks API server.

### `            report           `

Allows notebook instances to report their latest instance information to the Notebooks API server.

### `            reset           `

Resets a notebook instance.

### `            rollback           `

Rollbacks a notebook instance to the previous version.

### `            setAccelerator           `

Updates the guest accelerators of a single Instance.

### `            setIamPolicy           `

Sets the access control policy on the specified resource.

### `            setLabels           `

Replaces all the labels of an Instance.

### `            setMachineType           `

Updates the machine type of a single Instance.

### `            start           `

Starts a notebook instance.

### `            stop           `

Stops a notebook instance.

### `            testIamPermissions           `

Returns permissions that a caller has on the specified resource.

### `            updateConfig           `

Update Notebook Instance configurations.

### `            updateMetadataItems           `

Add/update metadata items for an instance.

### `            updateShieldedInstanceConfig           `

Updates the Shielded instance configuration of a single Instance.

### `            upgrade           `

Upgrades a notebook instance to the latest version.
