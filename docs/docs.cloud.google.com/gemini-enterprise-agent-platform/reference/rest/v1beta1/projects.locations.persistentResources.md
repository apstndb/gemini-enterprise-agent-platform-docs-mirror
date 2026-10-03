---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources
title: 'REST Resource: projects.locations.persistentResources'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: PersistentResource

Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec.

Fields

`name` `string`

Immutable. Resource name of a PersistentResource.

`displayName` `string`

Optional. The display name of the PersistentResource. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`resourcePools[]` `object ( `[`ResourcePool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources#ResourcePool)` )`

Required. The spec of the pools of different resources.

`state` `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources#State)` )`

Output only. The detailed state of a Study.

`error` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. Only populated when persistent resource's state is `STOPPING` or `ERROR` .

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the PersistentResource was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the PersistentResource for the first time entered the `RUNNING` state.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the PersistentResource was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize PersistentResource.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`network` `string`

Optional. The full name of the Compute Engine [network](https://docs.cloud.google.com/compute/docs/networks-and-firewalls#networks) to peered with Agent Platform to host the persistent resources. For example, `projects/12345/global/networks/myVPC` . [Format](https://docs.cloud.google.com/compute/docs/reference/rest/v1/networks/insert) is of the form `projects/{project}/global/networks/{network}` . Where {project} is a project number, as in `12345` , and {network} is a network name.

To specify this field, you must have already [configured VPC Network Peering for Agent Platform](https://cloud.google.com/vertex-ai/docs/general/vpc-peering) .

If this field is left unspecified, the resources aren't peered with any network.

`pscInterfaceConfig` `object ( ``PscInterfaceConfig`` )`

Optional. Configuration for PSC-I for PersistentResource.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/EncryptionSpec)` )`

Optional. Customer-managed encryption key spec for a PersistentResource. If set, this PersistentResource and all sub-resources of this PersistentResource will be secured by this key.

`resourceRuntimeSpec` `object ( `[`ResourceRuntimeSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources#ResourceRuntimeSpec)` )`

Optional. Persistent Resource runtime spec. For example, used for Ray cluster configuration.

`resourceRuntime` `object ( `[`ResourceRuntime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources#ResourceRuntime)` )`

Output only. Runtime information of the Persistent Resource.

`reservedIpRanges[]` `string`

Optional. A list of names for the reserved IP ranges under the VPC network that can be used for this persistent resource.

If set, we will deploy the persistent resource within the provided IP ranges. Otherwise, the persistent resource is deployed to any IP ranges under the provided VPC network.

Example: \['vertex-ai-ip-range'\].

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "resourcePools": [
    {
      object (ResourcePool)
    }
  ],
  "state": enum (State),
  "error": {
    object (Status)
  },
  "createTime": string,
  "startTime": string,
  "updateTime": string,
  "labels": {
    string: string,
    ...
  },
  "network": string,
  "pscInterfaceConfig": {
    object (PscInterfaceConfig)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "resourceRuntimeSpec": {
    object (ResourceRuntimeSpec)
  },
  "resourceRuntime": {
    object (ResourceRuntime)
  },
  "reservedIpRanges": [
    string
  ],
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean
}
```

## ResourcePool

Represents the spec of a group of resources of the same type, for example machine type, disk, and accelerators, in a PersistentResource.

Fields

`id` `string`

Immutable. The unique id in a PersistentResource for referring to this resource pool. user can specify it if necessary. Otherwise, it's generated automatically.

`machineSpec` `object ( ``MachineSpec`` )`

Required. Immutable. The specification of a single machine.

`diskSpec` `object ( ``DiskSpec`` )`

Optional. Disk spec for the machine in this node pool.

`usedReplicaCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The number of machines currently in use by training jobs for this resource pool. Will replace idle_replica_count.

`autoscalingSpec` `object ( `[`AutoscalingSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources#AutoscalingSpec)` )`

Optional. Optional spec to configure GKE or Ray-on-Vertex autoscaling

`replicaCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. The total number of machines to use for this resource pool.

**JSON representation**

```
{
  "id": string,
  "machineSpec": {
    object (MachineSpec)
  },
  "diskSpec": {
    object (DiskSpec)
  },
  "usedReplicaCount": string,
  "autoscalingSpec": {
    object (AutoscalingSpec)
  },
  "replicaCount": string
}
```

## AutoscalingSpec

The min/max number of replicas allowed if enabling autoscaling

Fields

`minReplicaCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. min replicas in the node pool, must be ≤ replicaCount and \< maxReplicaCount or will throw error. For autoscaling enabled Ray-on-Vertex, we allow minReplicaCount of a resource_pool to be 0 to match the OSS Ray behavior( <https://docs.ray.io/en/latest/cluster/vms/user-guides/configuring-autoscaling.html#cluster-config-parameters)> . As for Persistent Resource, the minReplicaCount must be \> 0, we added a corresponding validation inside CreatePersistentResourceRequestValidator.java.

`maxReplicaCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. max replicas in the node pool, must be ≥ replicaCount and \> minReplicaCount or will throw error

**JSON representation**

```
{
  "minReplicaCount": string,
  "maxReplicaCount": string
}
```

## State

Describes the PersistentResource state.

| Enums               |                                                                                                                                                  |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Not set.                                                                                                                                         |
| `PROVISIONING`      | The PROVISIONING state indicates the persistent resources is being created.                                                                      |
| `RUNNING`           | The RUNNING state indicates the persistent resource is healthy and fully usable.                                                                 |
| `STOPPING`          | The STOPPING state indicates the persistent resource is being deleted.                                                                           |
| `ERROR`             | The ERROR state indicates the persistent resource may be unusable. Details can be found in the `error` field.                                    |
| `REBOOTING`         | The REBOOTING state indicates the persistent resource is being rebooted (PR is not available right now but is expected to be ready again later). |
| `UPDATING`          | The UPDATING state indicates the persistent resource is being updated.                                                                           |

## ResourceRuntimeSpec

Configuration for the runtime on a PersistentResource instance, including but not limited to:

- service accounts used to run the workloads.
- Whether to make it a dedicated Ray Cluster.

Fields

`serviceAccountSpec` `object ( `[`ServiceAccountSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources#ServiceAccountSpec)` )`

Optional. Configure the use of workload identity on the PersistentResource

`raySpec` `object ( `[`RaySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources#RaySpec)` )`

Optional. Ray cluster configuration. Required when creating a dedicated RayCluster on the PersistentResource.

**JSON representation**

```
{
  "serviceAccountSpec": {
    object (ServiceAccountSpec)
  },
  "raySpec": {
    object (RaySpec)
  }
}
```

## ServiceAccountSpec

Configuration for the use of custom service account to run the workloads.

Fields

`enableCustomServiceAccount` `boolean`

Required. If true, custom user-managed service account is enforced to run any workloads (for example, Vertex Jobs) on the resource. Otherwise, uses the [Agent Platform Custom code service Agent](https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) .

`serviceAccount` `string`

Optional. Required when all below conditions are met \* `enableCustomServiceAccount` is true; \* any runtime is specified via `ResourceRuntimeSpec` on creation time, for example, Ray

The users must have `iam.serviceAccounts.actAs` permission on this service account and then the specified runtime containers will run as it.

Do not set this field if you want to submit jobs using custom service account to this PersistentResource after creation, but only specify the `serviceAccount` inside the job.

**JSON representation**

```
{
  "enableCustomServiceAccount": boolean,
  "serviceAccount": string
}
```

## RaySpec

Configuration information for the Ray cluster. For experimental launch, Ray cluster creation and Persistent cluster creation are 1:1 mapping: We will provision all the nodes within the Persistent cluster as Ray nodes.

Fields

`imageUri` `string`

Optional. Default image for user to choose a preferred ML framework (for example, TensorFlow or Pytorch) by choosing from [Vertex prebuilt images](https://cloud.google.com/vertex-ai/docs/training/pre-built-containers) . Either this or the resourcePoolImages is required. Use this field if you need all the resource pools to have the same Ray image. Otherwise, use the {@code resourcePoolImages} field.

`nfsMounts[]` `object ( ``NfsMount`` )`

Optional. Use if you want to mount to any NFS storages.

`resourcePoolImages` `map (key: string, value: string)`

Optional. Required if imageUri isn't set. A map of resource_pool_id to prebuild Ray image if user need to use different images for different head/worker pools. This map needs to cover all the resource pool ids. Example: { "ray_head_node_pool": "head image" "ray_worker_node_pool1": "worker image" "ray_worker_node_pool2": "another worker image" }

`headNodeResourcePoolId` `string`

Optional. This will be used to indicate which resource pool will serve as the Ray head node(the first node within that pool). Will use the machine from the first workerpool as the head node by default if this field isn't set.

`rayMetricSpec` `object ( `[`RayMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources#RayMetricSpec)` )`

Optional. Ray metrics configurations.

`rayLogsSpec` `object ( `[`RayLogsSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources#RayLogsSpec)` )`

Optional. OSS Ray logging configurations.

**JSON representation**

```
{
  "imageUri": string,
  "nfsMounts": [
    {
      object (NfsMount)
    }
  ],
  "resourcePoolImages": {
    string: string,
    ...
  },
  "headNodeResourcePoolId": string,
  "rayMetricSpec": {
    object (RayMetricSpec)
  },
  "rayLogsSpec": {
    object (RayLogsSpec)
  }
}
```

## RayMetricSpec

Configuration for the Ray metrics.

Fields

`disabled` `boolean`

Optional. Flag to disable the Ray metrics collection.

**JSON representation**

```
{
  "disabled": boolean
}
```

## RayLogsSpec

Configuration for the Ray OSS Logs.

Fields

`disabled` `boolean`

Optional. Flag to disable the export of Ray OSS logs to Cloud Logging.

**JSON representation**

```
{
  "disabled": boolean
}
```

## ResourceRuntime

Persistent Cluster runtime information as output

Fields

`accessUris` `map (key: string, value: string)`

Output only. URIs for user to connect to the Cluster. Example: { "RAY_HEAD_NODE_INTERNAL_IP": "head-node-IP:10001" "RAY_DASHBOARD_URI": "ray-dashboard-address:8888" }

`notebookRuntimeTemplate `**`(deprecated)`** `string`

> This item is deprecated!

Output only. The resource name of NotebookRuntimeTemplate for the RoV Persistent Cluster The NotebokRuntimeTemplate is created in the same VPC (if set), and with the same Ray and Python version as the Persistent Cluster. Example: "projects/1000/locations/us-central1/notebookRuntimeTemplates/abc123"

**JSON representation**

```
{
  "accessUris": {
    string: string,
    ...
  },
  "notebookRuntimeTemplate": string
}
```

| Methods                                                                                                                                         |                                          |
|-------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources/create) | Creates a PersistentResource.            |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources/delete) | Deletes a PersistentResource.            |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources/get)       | Gets a PersistentResource.               |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources/list)     | Lists PersistentResources in a Location. |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources/patch)   | Updates a PersistentResource.            |
| [`reboot`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources/reboot) | Reboots a PersistentResource.            |
