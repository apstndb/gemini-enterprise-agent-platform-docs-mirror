---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec
title: CustomJobSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents the spec of a CustomJob.

Fields

`persistentResourceId` `string`

Optional. The id of the PersistentResource in the same Project and Location which to run

If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network and CMEK configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected.

`workerPoolSpecs[]` ` object ( WorkerPoolSpec  ` )

Required. The spec of the worker pools including machine type and Docker image. All worker pools except the first one are optional and can be skipped by providing an empty value.

`scheduling` ` object ( Scheduling  ` )

Scheduling options for a CustomJob.

`serviceAccount` `string`

Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. If unspecified, the [Agent Platform Custom code service Agent](https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) for the CustomJob's project is used.

`network` `string`

Optional. The full name of the Compute Engine [network](https://docs.cloud.google.com/compute/docs/networks-and-firewalls#networks) to which the Job should be peered. For example, `projects/12345/global/networks/myVPC` . [Format](https://docs.cloud.google.com/compute/docs/reference/rest/v1/networks/insert) is of the form `projects/{project}/global/networks/{network}` . Where {project} is a project number, as in `12345` , and {network} is a network name.

To specify this field, you must have already [configured VPC Network Peering for Agent Platform](https://cloud.google.com/vertex-ai/docs/general/vpc-peering) .

If this field is left unspecified, the job is not peered with any network.

`reservedIpRanges[]` `string`

Optional. A list of names for the reserved ip ranges under the VPC network that can be used for this job.

If set, we will deploy the job within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network.

Example: \['vertex-ai-ip-range'\].

`pscInterfaceConfig` ` object ( PscInterfaceConfig  ` )

Optional. Configuration for PSC-I for CustomJob.

`baseOutputDirectory` ` object ( GcsDestination  ` )

The Cloud Storage location to store the output of this CustomJob or HyperparameterTuningJob. For HyperparameterTuningJob, the baseOutputDirectory of each child CustomJob backing a Trial is set to a subdirectory of name `  id  ` under its parent HyperparameterTuningJob's baseOutputDirectory.

The following Agent Platform environment variables will be passed to containers or python modules when this field is set:

For CustomJob:

  - AIP\_MODEL\_DIR = `<baseOutputDirectory>/model/`
  - AIP\_CHECKPOINT\_DIR = `<baseOutputDirectory>/checkpoints/`
  - AIP\_TENSORBOARD\_LOG\_DIR = `<baseOutputDirectory>/logs/`

For CustomJob backing a Trial of HyperparameterTuningJob:

  - AIP\_MODEL\_DIR = `<baseOutputDirectory>/<trial_id>/model/`
  - AIP\_CHECKPOINT\_DIR = `<baseOutputDirectory>/<trial_id>/checkpoints/`
  - AIP\_TENSORBOARD\_LOG\_DIR = `<baseOutputDirectory>/<trial_id>/logs/`

`protectedArtifactLocationId` `string`

The id of the location to store protected artifacts. e.g. us-central1. Populate only when the location is different than CustomJob location. List of supported locations: <https://cloud.google.com/vertex-ai/docs/general/locations>

`tensorboard` `string`

Optional. The name of a Agent Platform `  Tensorboard  ` resource to which this CustomJob will upload Tensorboard logs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`

`enableWebAccess` `boolean`

Optional. Whether you want Agent Platform to enable [interactive shell access](https://cloud.google.com/vertex-ai/docs/training/monitor-debug-interactive-shell) to training containers.

If set to `true` , you can access interactive shells at the URIs given by `  CustomJob.web_access_uris  ` or `  Trial.web_access_uris  ` (within `  HyperparameterTuningJob.trials  ` ).

`enableDashboardAccess` `boolean`

Optional. Whether you want Agent Platform to enable access to the customized dashboard in training chief container.

If set to `true` , you can access the dashboard at the URIs given by `  CustomJob.web_access_uris  ` or `  Trial.web_access_uris  ` (within `  HyperparameterTuningJob.trials  ` ).

`experiment` `string`

Optional. The Experiment associated with this job. Format: `projects/{project}/locations/{location}/metadataStores/{metadataStores}/contexts/{experiment-name}`

`experimentRun` `string`

Optional. The Experiment Run associated with this job. Format: `projects/{project}/locations/{location}/metadataStores/{metadataStores}/contexts/{experiment-name}-{experiment-run-name}`

`models[]` `string`

Optional. The name of the Model resources for which to generate a mapping to artifact URIs. Applicable only to some of the Google-provided custom jobs. Format: `projects/{project}/locations/{location}/models/{model}`

In order to retrieve a specific version of the model, also provide the version id or version alias. Example: `projects/{project}/locations/{location}/models/{model}@2` or `projects/{project}/locations/{location}/models/{model}@golden` If no version id or alias is specified, the "default" version will be returned. The "default" version alias is created for the first version of the model, and can be moved to other versions later on. There will be exactly one default version.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;persistentResourceId&quot;: string,&quot;workerPoolSpecs&quot;: [{object (WorkerPoolSpec)}],&quot;scheduling&quot;: {object (Scheduling)},&quot;serviceAccount&quot;: string,&quot;network&quot;: string,&quot;reservedIpRanges&quot;: [string],&quot;pscInterfaceConfig&quot;: {object (PscInterfaceConfig)},&quot;baseOutputDirectory&quot;: {object (GcsDestination)},&quot;protectedArtifactLocationId&quot;: string,&quot;tensorboard&quot;: string,&quot;enableWebAccess&quot;: boolean,&quot;enableDashboardAccess&quot;: boolean,&quot;experiment&quot;: string,&quot;experimentRun&quot;: string,&quot;models&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

## WorkerPoolSpec

Represents the spec of a worker pool in a job.

Fields

`machineSpec` ` object ( MachineSpec  ` )

Optional. Immutable. The specification of a single machine.

`replicaCount` `string ( int64 format)`

Optional. The number of worker replicas to use for this worker pool.

`nfsMounts[]` ` object ( NfsMount  ` )

Optional. List of NFS mount spec.

`lustreMounts[]` ` object ( LustreMount  ` )

Optional. List of Lustre mounts.

`diskSpec` ` object ( DiskSpec  ` )

Disk spec.

`task` `Union type`

The custom task to be executed in this worker pool. `task` can be only one of the following:

`containerSpec` ` object ( ContainerSpec  ` )

The custom container task.

`pythonPackageSpec` ` object ( PythonPackageSpec  ` )

The Python packaged task.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineSpec&quot;: {object (MachineSpec)},&quot;replicaCount&quot;: string,&quot;nfsMounts&quot;: [{object (NfsMount)}],&quot;lustreMounts&quot;: [{object (LustreMount)}],&quot;diskSpec&quot;: {object (DiskSpec)},// task&quot;containerSpec&quot;: {object (ContainerSpec)},&quot;pythonPackageSpec&quot;: {object (PythonPackageSpec)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## PythonPackageSpec

The spec of a Python packaged code.

Fields

`executorImageUri` `string`

Required. The URI of a container image in Artifact Registry that will run the provided Python package. Agent Platform provides a wide range of executor images with pre-installed packages to meet users' various use cases. See the list of [pre-built containers for training](https://cloud.google.com/vertex-ai/docs/training/pre-built-containers) . You must use an image from this list.

`packageUris[]` `string`

Required. The Google Cloud Storage location of the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100.

`pythonModule` `string`

Required. The Python module name to run after installing the packages.

`args[]` `string`

Command line arguments to be passed to the Python task.

`env[]` ` object ( EnvVar  ` )

Environment variables to be passed to the python module. Maximum limit is 100.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;executorImageUri&quot;: string,&quot;packageUris&quot;: [string],&quot;pythonModule&quot;: string,&quot;args&quot;: [string],&quot;env&quot;: [{object (EnvVar)}]}</code></pre></td>
</tr>
</tbody>
</table>

## MachineSpec

Specification of a single machine.

Fields

`machineType` `string`

Immutable. The type of the machine.

See the [list of machine types supported for prediction](https://cloud.google.com/vertex-ai/docs/predictions/configure-compute#machine-types)

See the [list of machine types supported for custom training](https://cloud.google.com/vertex-ai/docs/training/configure-compute#machine-types) .

For `  DeployedModel  ` this field is optional, and the default value is `n1-standard-2` . For `  BatchPredictionJob  ` or as part of `  WorkerPoolSpec  ` this field is required.

`acceleratorType` ` enum ( AcceleratorType  ` )

Immutable. The type of accelerator(s) that may be attached to the machine as per `  acceleratorCount  ` .

`acceleratorCount` `integer`

The number of accelerators to attach to the machine.

For accelerator optimized machine types ( <https://cloud.google.com/compute/docs/accelerator-optimized-machines> , One may set the acceleratorCount from 1 to N for machine with N GPUs. If acceleratorCount is less than or equal to N / 2, Vertex will co-schedule the replicas of the model into the same VM to save cost.

For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set acceleratorCount to 1 to 8. If acceleratorCount is 1, 2, 3, or 4, Vertex will co-schedule 8, 4, 2, or 2 replicas of the model into the same VM to save cost.

When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM.

Note that the feature is not compatible with \[multihostGpuNodeCount\]\[\]. When multihostGpuNodeCount is set, the co-scheduling will not be enabled.

`gpuPartitionSize` `string`

Optional. Immutable. The Nvidia GPU partition size.

When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpuPartitionSize="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances.

The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes.

If set, the acceleratorCount should be set to 1.

`tpuTopology` `string`

Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpuTopology: "2x2x1").

`reservationAffinity` ` object ( ReservationAffinity  ` )

Optional. Immutable. Configuration controlling how this resource pool consumes reservation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineType&quot;: string,&quot;acceleratorType&quot;: enum (AcceleratorType),&quot;acceleratorCount&quot;: integer,&quot;gpuPartitionSize&quot;: string,&quot;tpuTopology&quot;: string,&quot;reservationAffinity&quot;: {object (ReservationAffinity)}}</code></pre></td>
</tr>
</tbody>
</table>

## ReservationAffinity

A ReservationAffinity can be used to configure a Agent Platform resource (e.g., a DeployedModel) to draw its Compute Engine resources from a Shared Reservation, or exclusively from on-demand capacity.

Fields

`reservationAffinityType` ` enum ( Type  ` )

Required. Specifies the reservation affinity type.

`key` `string`

Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC\_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.

`values[]` `string`

Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;reservationAffinityType&quot;: enum (Type),&quot;key&quot;: string,&quot;values&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

## NfsMount

Represents a mount configuration for Network File System (NFS) to mount.

Fields

`server` `string`

Required. IP address of the NFS server.

`path` `string`

Required. Source path exported from NFS server. Has to start with '/', and combined with the ip address, it indicates the source mount path in the form of `server:path`

`mountPoint` `string`

Required. Destination mount path. The NFS will be mounted for the user under /mnt/nfs/

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
  &quot;server&quot;: string,
  &quot;path&quot;: string,
  &quot;mountPoint&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## LustreMount

Represents a mount configuration for Lustre file system.

Fields

`instanceIp` `string`

Required. IP address of the Lustre instance.

`volumeHandle` `string`

Required. The unique identifier of the Lustre volume.

`filesystem` `string`

Required. The name of the Lustre filesystem.

`mountPoint` `string`

Required. Destination mount path. The Lustre file system will be mounted for the user under /mnt/lustre/

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
  &quot;instanceIp&quot;: string,
  &quot;volumeHandle&quot;: string,
  &quot;filesystem&quot;: string,
  &quot;mountPoint&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## DiskSpec

Represents the spec of disk options.

Fields

`bootDiskType` `string`

type of the boot disk. For non-A3U machines, the default value is "pd-ssd", for A3U machines, the default value is "hyperdisk-balanced". Valid values: "pd-ssd" (Persistent Disk Solid state Drive), "pd-standard" (Persistent Disk Hard Disk Drive) or "hyperdisk-balanced".

`bootDiskSizeGb` `integer`

Size in GB of the boot disk (default is 100GB).

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
  &quot;bootDiskType&quot;: string,
  &quot;bootDiskSizeGb&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## Scheduling

All parameters related to queuing and scheduling of custom jobs.

Fields

`timeout` ` string ( Duration  ` format)

Optional. The maximum job running time. The default is 7 days.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`restartJobOnWorkerRestart` `boolean`

Optional. Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job.

`strategy` ` enum ( Strategy  ` )

Optional. This determines which type of scheduling strategy to use.

`disableRetries` `boolean`

Optional. Indicates if the job should retry for internal errors after the job starts running. If true, overrides `Scheduling.restart_job_on_worker_restart` to false.

`maxWaitDuration` ` string ( Duration  ` format)

Optional. This is the maximum duration that a job will wait for the requested resources to be provisioned if the scheduling strategy is set to \[Strategy.DWS\_FLEX\_START\]. If set to 0, the job will wait indefinitely. The default is 24 hours.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;timeout&quot;: string,&quot;restartJobOnWorkerRestart&quot;: boolean,&quot;strategy&quot;: enum (Strategy),&quot;disableRetries&quot;: boolean,&quot;maxWaitDuration&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## PscInterfaceConfig

Configuration for PSC-I.

Fields

`networkAttachment` `string`

Optional. The name of the Compute Engine [network attachment](https://cloud.google.com/vpc/docs/about-network-attachments) to attach to the resource within the region and user project. To specify this field, you must have already [created a network attachment](https://cloud.google.com/vpc/docs/create-manage-network-attachments#create-network-attachments) . This field is only used for resources using PSC-I.

`dnsPeeringConfigs[]` ` object ( DnsPeeringConfig  ` )

Optional. DNS peering configurations. When specified, Agent Platform will attempt to configure DNS peering zones in the tenant project VPC to resolve the specified domains using the target network's Cloud DNS. The user must grant the dns.peer role to the Agent Platform service Agent on the target project.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;networkAttachment&quot;: string,&quot;dnsPeeringConfigs&quot;: [{object (DnsPeeringConfig)}]}</code></pre></td>
</tr>
</tbody>
</table>

## DnsPeeringConfig

DNS peering configuration. These configurations are used to create DNS peering zones in the Vertex tenant project VPC, enabling resolution of records within the specified domain hosted in the target network's Cloud DNS.

Fields

`domain` `string`

Required. The DNS name suffix of the zone being peered to, e.g., "my-internal-domain.corp.". Must end with a dot.

`targetProject` `string`

Required. The project id hosting the Cloud DNS managed zone that contains the 'domain'. The Agent Platform service Agent requires the dns.peer role on this project.

`targetNetwork` `string`

Required. The VPC network name in the targetProject where the DNS zone specified by 'domain' is visible.

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
  &quot;domain&quot;: string,
  &quot;targetProject&quot;: string,
  &quot;targetNetwork&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## GcsDestination

The Google Cloud Storage location where the output is to be written to.

Fields

`outputUriPrefix` `string`

Required. Google Cloud Storage URI to output directory. If the uri doesn't end with '/', a '/' will be automatically appended. The directory is created if it doesn't exist.

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
  &quot;outputUriPrefix&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
