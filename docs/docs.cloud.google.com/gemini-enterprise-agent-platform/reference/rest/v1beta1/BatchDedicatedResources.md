---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchDedicatedResources
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchDedicatedResources
title: BatchDedicatedResources
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A description of resources that are used for performing batch operations, are dedicated to a Model, and need manual configuration.

Fields

`machineSpec` `object ( MachineSpec` )

Required. Immutable. The specification of a single machine.

`startingReplicaCount` `integer`

Immutable. The number of machine replicas used at the start of the batch operation. If not set, Agent Platform decides starting number, not greater than `  maxReplicaCount  `

`maxReplicaCount` `integer`

Immutable. The maximum number of machine replicas the batch operation may be scaled to. The default value is 10.

`flexStart` ` object ( FlexStart  ` )

Optional. Immutable. If set, use DWS resource to schedule the deployment workload. reference: ( <https://cloud.google.com/blog/products/compute/introducing-dynamic-workload-scheduler> )

`spot` `boolean`

Optional. If true, schedule the deployment workload on [spot VMs](https://cloud.google.com/kubernetes-engine/docs/concepts/spot-vms) .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineSpec&quot;: {object (MachineSpec)},&quot;startingReplicaCount&quot;: integer,&quot;maxReplicaCount&quot;: integer,&quot;flexStart&quot;: {object (FlexStart)},&quot;spot&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>
