---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes
title: 'REST Resource: projects.locations.runtimes'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Runtime

The definition of a Runtime for a managed notebook instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;state&quot;: enum (State),&quot;healthState&quot;: enum (HealthState),&quot;accessConfig&quot;: {object (RuntimeAccessConfig)},&quot;softwareConfig&quot;: {object (RuntimeSoftwareConfig)},&quot;metrics&quot;: {object (RuntimeMetrics)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;labels&quot;: {string: string,...},&quot;runtimeMigrationEligibility&quot;: {object (RuntimeMigrationEligibility)},// Union field runtime_type can be only one of the following:&quot;virtualMachine&quot;: {object (VirtualMachine)}// End of list of possible types for union field runtime_type.&quot;migrated&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. The resource name of the runtime. Format: `projects/{project}/locations/{location}/runtimes/{runtimeId}`

`state`

` enum ( State  ` )

Output only. Runtime state.

`healthState`

` enum ( HealthState  ` )

Output only. Runtime healthState.

`accessConfig`

` object ( RuntimeAccessConfig  ` )

The config settings for accessing runtime.

`softwareConfig`

` object ( RuntimeSoftwareConfig  ` )

The config settings for software inside the runtime.

`metrics`

` object ( RuntimeMetrics  ` )

Output only. Contains Runtime daemon metrics such as Service status and JupyterLab stats.

`createTime`

` string ( Timestamp  ` format)

Output only. Runtime creation time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Runtime update time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels`

`map (key: string, value: string)`

Optional. The labels to associate with this Managed Notebook or Runtime. Label **keys** must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . Label **values** may be empty, but, if present, must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . No more than 32 labels can be associated with a cluster.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`runtimeMigrationEligibility`

` object ( RuntimeMigrationEligibility  ` )

Output only. Checks how feasible a migration from GmN to WbI is.

Union field `runtime_type` . Type of the runtime; currently only supports Compute Engine VM. `runtime_type` can be only one of the following:

`virtualMachine`

` object ( VirtualMachine  ` )

Use a Compute Engine VM image to start the managed notebook instance.

`migrated`

`boolean`

Output only. Bool indicating whether this notebook has been migrated to a Workbench Instance

## VirtualMachine

Runtime using Virtual Machine for computing.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;instanceName&quot;: string,&quot;instanceId&quot;: string,&quot;virtualMachineConfig&quot;: {object (VirtualMachineConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`instanceName`

`string`

Output only. The user-friendly name of the Managed Compute Engine instance.

`instanceId`

`string`

Output only. The unique identifier of the Managed Compute Engine instance.

`virtualMachineConfig`

` object ( VirtualMachineConfig  ` )

Virtual Machine configuration settings.

## VirtualMachineConfig

The config settings for virtual machine.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;zone&quot;: string,&quot;machineType&quot;: string,&quot;containerImages&quot;: [{object (ContainerImage)}],&quot;dataDisk&quot;: {object (LocalDisk)},&quot;encryptionConfig&quot;: {object (EncryptionConfig)},&quot;shieldedInstanceConfig&quot;: {object (RuntimeShieldedInstanceConfig)},&quot;acceleratorConfig&quot;: {object (RuntimeAcceleratorConfig)},&quot;network&quot;: string,&quot;subnet&quot;: string,&quot;internalIpOnly&quot;: boolean,&quot;tags&quot;: [string],&quot;guestAttributes&quot;: {string: string,...},&quot;metadata&quot;: {string: string,...},&quot;labels&quot;: {string: string,...},&quot;nicType&quot;: enum (NicType),&quot;reservedIpRange&quot;: string,&quot;bootImage&quot;: {object (BootImage)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`zone`

`string`

Output only. The zone where the virtual machine is located. If using regional request, the notebooks service will pick a location in the corresponding runtime region. On a get request, zone will always be present. Example: \* `us-central1-b`

`machineType`

`string`

Required. The Compute Engine machine type used for runtimes. Short name is valid. Examples: \* `n1-standard-2` \* `e2-standard-8`

`containerImages[]`

` object ( ContainerImage  ` )

Optional. Use a list of container images to use as Kernels in the notebook instance.

`dataDisk`

` object ( LocalDisk  ` )

Required. Data disk option configuration settings.

`encryptionConfig`

` object ( EncryptionConfig  ` )

Optional. Encryption settings for virtual machine data disk.

`shieldedInstanceConfig`

` object ( RuntimeShieldedInstanceConfig  ` )

Optional. Shielded VM Instance configuration settings.

`acceleratorConfig`

` object ( RuntimeAcceleratorConfig  ` )

Optional. The Compute Engine accelerator configuration for this runtime.

`network`

`string`

Optional. The Compute Engine network to be used for machine communications. Cannot be specified with subnetwork. If neither `network` nor `subnet` is specified, the "default" network of the project is used, if it exists.

A full URL or partial URI. Examples:

  - `https://www.googleapis.com/compute/v1/projects/[projectId]/global/networks/default`
  - `projects/[projectId]/global/networks/default`

Runtimes are managed resources inside Google Infrastructure. Runtimes support the following network configurations:

  - Google Managed Network (Network & subnet are empty)
  - Consumer Project VPC (network & subnet are required). Requires configuring Private Service Access.
  - Shared VPC (network & subnet are required). Requires configuring Private Service Access.

`subnet`

`string`

Optional. The Compute Engine subnetwork to be used for machine communications. Cannot be specified with network.

A full URL or partial URI are valid. Examples:

  - `https://www.googleapis.com/compute/v1/projects/[projectId]/regions/us-east1/subnetworks/sub0`
  - `projects/[projectId]/regions/us-east1/subnetworks/sub0`

`internalIpOnly`

`boolean`

Optional. If true, runtime will only have internal IP addresses. By default, runtimes are not restricted to internal IP addresses, and will have ephemeral external IP addresses assigned to each vm. This `internalIpOnly` restriction can only be enabled for subnetwork enabled networks, and all dependencies must be configured to be accessible without external IP addresses.

`tags[]`

`string`

Optional. The Compute Engine network tags to add to runtime (see [Add network tags](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).

`guestAttributes`

`map (key: string, value: string)`

Output only. The Compute Engine guest attributes. (see [Project and instance guest attributes](https://cloud.google.com/compute/docs/storing-retrieving-metadata#guestAttributes) ).

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`metadata`

`map (key: string, value: string)`

Optional. The Compute Engine metadata entries to add to virtual machine. (see [Project and instance metadata](https://cloud.google.com/compute/docs/storing-retrieving-metadata#project_and_instance_metadata) ).

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`labels`

`map (key: string, value: string)`

Optional. The labels to associate with this runtime. Label **keys** must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . Label **values** may be empty, but, if present, must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . No more than 32 labels can be associated with a cluster.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`nicType`

` enum ( NicType  ` )

Optional. The type of vNIC to be used on this interface. This may be gVNIC or VirtioNet.

`reservedIpRange`

`string`

Optional. Reserved IP Range name is used for VPC Peering. The subnetwork allocation will use the range *name* if it's assigned.

Example: managed-notebooks-range-c

    PEERING_RANGE_NAME_3=managed-notebooks-range-c
    gcloud compute addresses create $PEERING_RANGE_NAME_3 \
      --global \
      --prefix-length=24 \
      --description="Google Cloud Managed Notebooks Range 24 c" \
      --network=$NETWORK \
      --addresses=192.168.0.0 \
      --purpose=VPC_PEERING

Field value will be: `managed-notebooks-range-c`

`bootImage`

` object ( BootImage  ` )

Optional. Boot image metadata used for runtime upgradeability.

## LocalDisk

A Local attached disk resource.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;autoDelete&quot;: boolean,&quot;boot&quot;: boolean,&quot;deviceName&quot;: string,&quot;guestOsFeatures&quot;: [{object (RuntimeGuestOsFeature)}],&quot;index&quot;: integer,&quot;initializeParams&quot;: {object (LocalDiskInitializeParams)},&quot;interface&quot;: string,&quot;kind&quot;: string,&quot;licenses&quot;: [string],&quot;mode&quot;: string,&quot;source&quot;: string,&quot;type&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`autoDelete`

`boolean`

Optional. Output only. Specifies whether the disk will be auto-deleted when the instance is deleted (but not when the disk is detached from the instance).

`boot`

`boolean`

Optional. Output only. Indicates that this is a boot disk. The virtual machine will use the first partition of the disk for its root filesystem.

`deviceName`

`string`

Optional. Output only. Specifies a unique device name of your choice that is reflected into the `/dev/disk/by-id/google-*` tree of a Linux operating system running within the instance. This name can be used to reference the device for mounting, resizing, and so on, from within the instance.

If not specified, the server chooses a default device name to apply to this disk, in the form persistent-disk-x, where x is a number assigned by Google Compute Engine. This field is only applicable for persistent disks.

`guestOsFeatures[]`

` object ( RuntimeGuestOsFeature  ` )

Output only. Indicates a list of features to enable on the guest operating system. Applicable only for bootable images. Read Enabling guest operating system features to see a list of available options.

`index`

`integer`

Output only. A zero-based index to this disk, where 0 is reserved for the boot disk. If you have many disks attached to an instance, each disk would have a unique index number.

`initializeParams`

` object ( LocalDiskInitializeParams  ` )

Input only. Specifies the parameters for a new disk that will be created alongside the new instance. Use initialization parameters to create boot disks or local SSDs attached to the new instance.

This property is mutually exclusive with the source property; you can only define one or the other, but not both.

`interface`

`string`

Specifies the disk interface to use for attaching this disk, which is either SCSI or NVME. The default is SCSI. Persistent disks must always use SCSI and the request will fail if you attempt to attach a persistent disk in any other format than SCSI. Local SSDs can use either NVME or SCSI. For performance characteristics of SCSI over NVMe, see Local SSD performance. Valid values:

  - `NVME`
  - `SCSI`

`kind`

`string`

Output only. Type of the resource. Always compute\#attachedDisk for attached disks.

`licenses[]`

`string`

Output only. Any valid publicly visible licenses.

`mode`

`string`

The mode in which to attach this disk, either `READ_WRITE` or `READ_ONLY` . If not specified, the default is to attach the disk in `READ_WRITE` mode. Valid values:

  - `READ_ONLY`
  - `READ_WRITE`

`source`

`string`

Specifies a valid partial or full URL to an existing Persistent Disk resource.

`type`

`string`

Specifies the type of the disk, either `SCRATCH` or `PERSISTENT` . If not specified, the default is `PERSISTENT` . Valid values:

  - `PERSISTENT`
  - `SCRATCH`

## RuntimeGuestOsFeature

Optional. A list of features to enable on the guest operating system. Applicable only for bootable images. Read [Enabling guest operating system features](https://cloud.google.com/compute/docs/images/create-delete-deprecate-private-images#guest-os-features) to see a list of available options. Guest OS features for boot disk.

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

The ID of a supported feature. Read [Enabling guest operating system features](https://cloud.google.com/compute/docs/images/create-delete-deprecate-private-images#guest-os-features) to see a list of available options.

Valid values:

  - `FEATURE_TYPE_UNSPECIFIED`
  - `MULTI_IP_SUBNET`
  - `SECURE_BOOT`
  - `UEFI_COMPATIBLE`
  - `VIRTIO_SCSI_MULTIQUEUE`
  - `WINDOWS`

## LocalDiskInitializeParams

Input only. Specifies the parameters for a new disk that will be created alongside the new instance. Use initialization parameters to create boot disks or local SSDs attached to the new runtime. This property is mutually exclusive with the source property; you can only define one or the other, but not both.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;description&quot;: string,&quot;diskName&quot;: string,&quot;diskSizeGb&quot;: string,&quot;diskType&quot;: enum (DiskType),&quot;labels&quot;: {string: string,...}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`description`

`string`

Optional. Provide this property when creating the disk.

`diskName`

`string`

Optional. Specifies the disk name. If not specified, the default is to use the name of the instance. If the disk with the instance name exists already in the given zone/region, a new name will be automatically generated.

`diskSizeGb`

`string ( int64 format)`

Optional. Specifies the size of the disk in base-2 GB. If not specified, the disk will be the same size as the image (usually 10GB). If specified, the size must be equal to or larger than 10GB. Default 100 GB.

`diskType`

` enum ( DiskType  ` )

Input only. The type of the boot disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).

`labels`

`map (key: string, value: string)`

Optional. Labels to apply to this disk. These can be later modified by the disks.setLabels method. This field is only applicable for persistent disks.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

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

## EncryptionConfig

Represents a custom encryption key configuration that can be applied to a resource. This will encrypt all disks in Virtual Machine.

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
  &quot;kmsKey&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kmsKey`

`string`

The Cloud KMS resource identifier of the customer-managed encryption key used to protect a resource, such as a disks. It has the following format: `projects/{PROJECT_ID}/locations/{REGION}/keyRings/{KEY_RING_NAME}/cryptoKeys/{KEY_NAME}`

## RuntimeShieldedInstanceConfig

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

## RuntimeAcceleratorConfig

Definition of the types of hardware accelerators that can be used. See [Compute Engine AcceleratorTypes](https://cloud.google.com/compute/docs/reference/beta/acceleratorTypes) . Examples:

  - `nvidia-tesla-k80`
  - `nvidia-tesla-p100`
  - `nvidia-tesla-v100`
  - `nvidia-tesla-p4`
  - `nvidia-tesla-t4`
  - `nvidia-tesla-a100`

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

Accelerator model.

`coreCount`

`string ( int64 format)`

Count of cores of this accelerator.

## AcceleratorType

Type of this accelerator.

Enums

`ACCELERATOR_TYPE_UNSPECIFIED`

Accelerator type is not specified.

`NVIDIA_TESLA_K80`

Accelerator type is Nvidia Tesla K80.

> This item is deprecated\!

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

`NVIDIA_L4`

Accelerator type is Nvidia L4.

`TPU_V2`

(Coming soon) Accelerator type is TPU V2.

`TPU_V3`

(Coming soon) Accelerator type is TPU V3.

`NVIDIA_TESLA_T4_VWS`

Accelerator type is NVIDIA Tesla T4 Virtual Workstations.

`NVIDIA_TESLA_P100_VWS`

Accelerator type is NVIDIA Tesla P100 Virtual Workstations.

`NVIDIA_TESLA_P4_VWS`

Accelerator type is NVIDIA Tesla P4 Virtual Workstations.

## NicType

The type of vNIC driver. Default should be UNSPECIFIED\_NIC\_TYPE.

Enums

`UNSPECIFIED_NIC_TYPE`

No type specified.

`VIRTIO_NET`

VIRTIO

`GVNIC`

GVNIC

## BootImage

This type has no fields.

Definition of the boot image used by the Runtime. Used to facilitate runtime upgradeability.

## State

The definition of the states of this runtime.

Enums

`STATE_UNSPECIFIED`

State is not specified.

`STARTING`

The compute layer is starting the runtime. It is not ready for use.

`PROVISIONING`

The compute layer is installing required frameworks and registering the runtime with notebook proxy. It cannot be used.

`ACTIVE`

The runtime is currently running. It is ready for use.

`STOPPING`

The control logic is stopping the runtime. It cannot be used.

`STOPPED`

The runtime is stopped. It cannot be used.

`DELETING`

The runtime is being deleted. It cannot be used.

`UPGRADING`

The runtime is upgrading. It cannot be used.

`INITIALIZING`

The runtime is being created and set up. It is not ready for use.

## HealthState

The runtime substate.

Enums

`HEALTH_STATE_UNSPECIFIED`

The runtime substate is unknown.

`HEALTHY`

The runtime is known to be in an healthy state (for example, critical daemons are running) Applies to ACTIVE state.

`UNHEALTHY`

The runtime is known to be in an unhealthy state (for example, critical daemons are not running) Applies to ACTIVE state.

`AGENT_NOT_INSTALLED`

The runtime has not installed health monitoring agent. Applies to ACTIVE state.

`AGENT_NOT_RUNNING`

The runtime health monitoring agent is not running. Applies to ACTIVE state.

## RuntimeAccessConfig

Specifies the login configuration for Runtime

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;accessType&quot;: enum (RuntimeAccessType),&quot;runtimeOwner&quot;: string,&quot;proxyUri&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`accessType`

` enum ( RuntimeAccessType  ` )

The type of access mode this instance.

`runtimeOwner`

`string`

The owner of this runtime after creation. Format: `alias@example.com` Currently supports one owner only.

`proxyUri`

`string`

Output only. The proxy endpoint that is used to access the runtime.

## RuntimeAccessType

Possible ways to access runtime. Authentication mode. Currently supports: Single User only.

Enums

`RUNTIME_ACCESS_TYPE_UNSPECIFIED`

Unspecified access.

`SINGLE_USER`

Single user login.

`SERVICE_ACCOUNT`

Service Account mode. In Service Account mode, Runtime creator will specify a SA that exists in the consumer project. Using Runtime Service Account field. Users accessing the Runtime need ActAs (Service Account User) permission.

## RuntimeSoftwareConfig

Specifies the selection and configuration of software inside the runtime. The properties to set on runtime. Properties keys are specified in `key:value` format, for example:

  - `idleShutdown: true`
  - `idleShutdownTimeout: 180`
  - `enableHealthMonitoring: true`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;notebookUpgradeSchedule&quot;: string,&quot;idleShutdownTimeout&quot;: integer,&quot;installGpuDriver&quot;: boolean,&quot;customGpuDriverPath&quot;: string,&quot;postStartupScript&quot;: string,&quot;kernels&quot;: [{object (ContainerImage)}],&quot;postStartupScriptBehavior&quot;: enum (PostStartupScriptBehavior),&quot;enableHealthMonitoring&quot;: boolean,&quot;idleShutdown&quot;: boolean,&quot;upgradeable&quot;: boolean,&quot;disableTerminal&quot;: boolean,&quot;version&quot;: string,&quot;mixerDisabled&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`notebookUpgradeSchedule`

`string`

Cron expression in UTC timezone, used to schedule instance auto upgrade. Please follow the [cron format](https://en.wikipedia.org/wiki/Cron) .

`idleShutdownTimeout`

`integer`

Time in minutes to wait before shutting down runtime. Default: 180 minutes

`installGpuDriver`

`boolean`

Install Nvidia Driver automatically. Default: True

`customGpuDriverPath`

`string`

Specify a custom Cloud Storage path where the GPU driver is stored. If not specified, we'll automatically choose from official GPU drivers.

`postStartupScript`

`string`

Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path ( `gs://path-to-file/file-name` ).

`kernels[]`

` object ( ContainerImage  ` )

Optional. Use a list of container images to use as Kernels in the notebook instance.

`postStartupScriptBehavior`

` enum ( PostStartupScriptBehavior  ` )

Behavior for the post startup script.

`enableHealthMonitoring`

`boolean`

Verifies core internal services are running. Default: True

`idleShutdown`

`boolean`

Runtime will automatically shutdown after idle\_shutdown\_time. Default: True

`upgradeable`

`boolean`

Output only. Bool indicating whether an newer image is available in an image family.

`disableTerminal`

`boolean`

Bool indicating whether JupyterLab terminal will be available or not. Default: False

`version`

`string`

Output only. version of boot image such as M100, from release label of the image.

`mixerDisabled`

`boolean`

Bool indicating whether mixer client should be disabled. Default: False

## PostStartupScriptBehavior

Behavior for the post startup script.

Enums

`POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED`

Unspecified post startup script behavior. Will run only once at creation.

`RUN_EVERY_START`

Runs the post startup script provided during creation at every start.

`DOWNLOAD_AND_RUN_EVERY_START`

Downloads and runs the provided post startup script at every start.

## RuntimeMetrics

Contains runtime daemon metrics, such as OS and kernels and sessions stats.

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
  &quot;systemMetrics&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`systemMetrics`

`map (key: string, value: string)`

Output only. The system metrics.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

## RuntimeMigrationEligibility

RuntimeMigrationEligibility represents the feasibility information of a migration from GmN to WbI.

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

Output only. Certain configurations make the GmN ineligible for an automatic migration. A manual migration is required.

## Warning

A migration warning message means certain configurations will be defaulted during the migration.

Enums

`WARNING_UNSPECIFIED`

Default type.

`UNSUPPORTED_ACCELERATOR_TYPE`

The GmN uses an accelerator type that's unsupported in WbI. It will be migrated without an accelerator. Users can attach an accelerator after the migration.

`UNSUPPORTED_OS`

The GmN uses an operating system that's unsupported in WbI (e.g. Debian 10). It will be replaced with Debian 11 in WbI.

`RESERVED_IP_RANGE`

This GmN is configured with reserved IP range, which is no longer applicable in WbI.

`GOOGLE_MANAGED_NETWORK`

This GmN is configured with a Google managed network. Please provide the `network` and `subnet` options for the migration.

`POST_STARTUP_SCRIPT`

This GmN is configured with a post startup script. Please optionally provide the `postStartupScriptOption` for the migration.

`SINGLE_USER`

This GmN is configured with single user mode. Please optionally provide the `serviceAccount` option for the migration.

## Error

A migration error message means certain configurations make the GmN ineligible for an automatic migration. A manual migration is required.

Enums

`ERROR_UNSPECIFIED`

Default type.

`CUSTOM_CONTAINER`

The GmN is configured with custom container(s) and cannot be migrated.

## Methods

### `            create           `

Creates a new Runtime in a given project and location.

### `            delete           `

Deletes a single Runtime.

### `            get           `

Gets details of a single Runtime.

### `            getIamPolicy           `

Gets the access control policy for a resource.

### `            list           `

Lists Runtimes in a given project and location.

### `            migrate           `

Migrate an existing Runtime to a new Workbench Instance.

### `            patch           `

Update Notebook Runtime configuration.

### `            reportEvent           `

Reports and processes a runtime event.

### `            reset           `

Resets a Managed Notebook Runtime.

### `            setIamPolicy           `

Sets the access control policy on the specified resource.

### `            start           `

Starts a Managed Notebook Runtime.

### `            stop           `

Stops a Managed Notebook Runtime.

### `            switch           `

Switch a Managed Notebook Runtime.

### `            testIamPermissions           `

Returns permissions that a caller has on the specified resource.
