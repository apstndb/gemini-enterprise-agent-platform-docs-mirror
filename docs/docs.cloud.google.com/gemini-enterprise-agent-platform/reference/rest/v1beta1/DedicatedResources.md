---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DedicatedResources
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DedicatedResources
title: DedicatedResources
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A description of resources that are dedicated to a DeployedModel or DeployedIndex, and that need a higher degree of manual configuration.

Fields

`machineSpec` `object ( MachineSpec` )

Required. Immutable. The specification of a single machine being used.

`minReplicaCount` `integer`

Required. Immutable. The minimum number of machine replicas that will be always deployed on. This value must be greater than or equal to 1.

If traffic increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed.

`maxReplicaCount` `integer`

Immutable. The maximum number of replicas that may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale to that many replicas is guaranteed (barring service outages). If traffic increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, will use `  minReplicaCount  ` as the default value.

The value of this field impacts the charge against Vertex CPU and GPU quotas. Specifically, you will be charged for (maxReplicaCount \* number of cores in the selected machine type) and (maxReplicaCount \* number of GPUs per replica in the selected machine type).

`requiredReplicaCount` `integer`

Optional. Number of required available replicas for the deployment to succeed. This field is only needed when partial deployment/mutation is desired. If set, the deploy/mutate operation will succeed once availableReplicaCount reaches requiredReplicaCount, and the rest of the replicas will be retried. If not set, the default requiredReplicaCount will be minReplicaCount.

`initialReplicaCount` `integer`

Immutable. Number of initial replicas being deployed on when scaling the workload up from zero or when creating the workload in case `  minReplicaCount  ` = 0. When `  minReplicaCount  ` \> 0 (meaning that the scale-to-zero feature is not enabled), `  initialReplicaCount  ` should not be set. When `  minReplicaCount  ` = 0 (meaning that the scale-to-zero feature is enabled), `  initialReplicaCount  ` should be larger than zero, but no greater than `  maxReplicaCount  ` .

`autoscalingMetricSpecs[]` ` object ( AutoscalingMetricSpec  ` )

Immutable. The metric specifications that overrides a resource utilization metric (CPU utilization, accelerator's duty cycle, and so on) target value (default to 60 if not set). At most one entry is allowed per metric.

If `machineSpec.accelerator_count` is above 0, the autoscaling will be based on both CPU utilization and accelerator's duty cycle metrics and scale up when either metrics exceeds its target value while scale down if both metrics are under their target value. The default target value is 60 for both metrics.

If `machineSpec.accelerator_count` is 0, the autoscaling will be based on CPU utilization metric only with default target value 60 if not explicitly set.

For example, in the case of Online Prediction, if you want to override target CPU utilization to 80, you should set `  autoscalingMetricSpecs.metric_name  ` to `aiplatform.googleapis.com/prediction/online/cpu/utilization` and `  autoscalingMetricSpecs.target  ` to `80` .

`spot` `boolean`

Optional. If true, schedule the deployment workload on [spot VMs](https://cloud.google.com/kubernetes-engine/docs/concepts/spot-vms) .

`flexStart` ` object ( FlexStart  ` )

Optional. Immutable. If set, use DWS resource to schedule the deployment workload. reference: ( <https://cloud.google.com/blog/products/compute/introducing-dynamic-workload-scheduler> )

`scaleToZeroSpec` ` object ( ScaleToZeroSpec  ` )

Optional. Specification for scale-to-zero feature.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineSpec&quot;: {object (MachineSpec)},&quot;minReplicaCount&quot;: integer,&quot;maxReplicaCount&quot;: integer,&quot;requiredReplicaCount&quot;: integer,&quot;initialReplicaCount&quot;: integer,&quot;autoscalingMetricSpecs&quot;: [{object (AutoscalingMetricSpec)}],&quot;spot&quot;: boolean,&quot;flexStart&quot;: {object (FlexStart)},&quot;scaleToZeroSpec&quot;: {object (ScaleToZeroSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

## AutoscalingMetricSpec

The metric specification that defines the target resource utilization (CPU utilization, accelerator's duty cycle, and so on) for calculating the desired replica count.

Fields

`metricName` `string`

Required. The resource metric name. Supported metrics:

  - For Online Prediction:
  - `aiplatform.googleapis.com/prediction/online/accelerator/duty_cycle`
  - `aiplatform.googleapis.com/prediction/online/cpu/utilization`
  - `aiplatform.googleapis.com/prediction/online/request_count`
  - `pubsub.googleapis.com/subscription/num_undelivered_messages`
  - `prometheus.googleapis.com/vertex_dcgm_fi_dev_gpu_util`
  - `prometheus.googleapis.com/vertex_vllm_gpu_cache_usage_perc`
  - `prometheus.googleapis.com/vertex_vllm_num_requests_waiting`

`target` `integer`

The target resource utilization in percentage (1% - 100%) for the given metric; once the real usage deviates from the target by a certain percentage, the machine replicas change. The default value is 60 (representing 60%) if not provided.

`monitoredResourceLabels` `map (key: string, value: string)`

Optional. The Cloud Monitoring monitored resource labels as key value pairs used for metrics filtering. See Cloud Monitoring Labels <https://cloud.google.com/monitoring/api/v3/metric-model#generic-label-info>

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
  &quot;metricName&quot;: string,
  &quot;target&quot;: integer,
  &quot;monitoredResourceLabels&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

## ScaleToZeroSpec

Specification for scale-to-zero feature.

Fields

`minScaleupPeriod` ` string ( Duration  ` format)

Optional. Minimum duration that a deployment will be scaled up before traffic is evaluated for potential scale-down. \[MinValue=300\] (5 minutes) \[MaxValue=28800\] (8 hours)

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`idleScaledownPeriod` ` string ( Duration  ` format)

Optional. Duration of no traffic before scaling to zero. \[MinValue=300\] (5 minutes) \[MaxValue=28800\] (8 hours)

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;minScaleupPeriod&quot;: string,
  &quot;idleScaledownPeriod&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
