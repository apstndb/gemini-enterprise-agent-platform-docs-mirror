---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchDedicatedResources
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchDedicatedResources
title: BatchDedicatedResources
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A description of resources that are used for performing batch operations, are dedicated to a Model, and need manual configuration.

Fields

`machineSpec` `object ( ``MachineSpec`` )`

Required. Immutable. The specification of a single machine.

`startingReplicaCount` `integer`

Immutable. The number of machine replicas used at the start of the batch operation. If not set, Agent Platform decides starting number, not greater than [`maxReplicaCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchDedicatedResources#FIELDS.max_replica_count)

`maxReplicaCount` `integer`

Immutable. The maximum number of machine replicas the batch operation may be scaled to. The default value is 10.

`flexStart` `object ( `[`FlexStart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FlexStart)` )`

Optional. Immutable. If set, use DWS resource to schedule the deployment workload. reference: ( <https://cloud.google.com/blog/products/compute/introducing-dynamic-workload-scheduler> )

`spot` `boolean`

Optional. If true, schedule the deployment workload on [spot VMs](https://cloud.google.com/kubernetes-engine/docs/concepts/spot-vms) .

**JSON representation**

```
{
  "machineSpec": {
    object (MachineSpec)
  },
  "startingReplicaCount": integer,
  "maxReplicaCount": integer,
  "flexStart": {
    object (FlexStart)
  },
  "spot": boolean
}
```
