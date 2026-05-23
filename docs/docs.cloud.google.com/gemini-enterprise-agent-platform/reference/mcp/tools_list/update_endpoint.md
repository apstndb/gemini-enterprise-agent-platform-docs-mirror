---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/update_endpoint
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/update_endpoint
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `update_endpoint`

Updates specific fields of an existing Agent Platform Endpoint. This is a synchronous operation used for modifying metadata like display names or labels. Format: 'projects/{project\_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'. IMPORTANT: This parameter requires the numeric ID or UUID returned by the list tool, NOT the display name. Guidance: Set the updateMask to 'description' or 'display\_name' based on the update. Supported values: 'display\_name', 'description', 'labels'.

The following sample demonstrate how to use `curl` to invoke the `update_endpoint` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://aiplatform.googleapis.com/mcp/generate&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;update_endpoint&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for `EndpointService.UpdateEndpoint` .

### UpdateEndpointRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;endpoint&quot;: {object (Endpoint)},&quot;updateMask&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`endpoint`

` object ( Endpoint  ` )

Required. The Endpoint which replaces the resource on the server.

`updateMask`

` string ( FieldMask  ` format)

Required. The update mask applies to the resource. See `  google.protobuf.FieldMask  ` .

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Endpoint

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;deployedModels&quot;: [{object (DeployedModel)}],&quot;trafficSplit&quot;: {string: integer,...},&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;network&quot;: string,&quot;enablePrivateServiceConnect&quot;: boolean,&quot;privateServiceConnectConfig&quot;: {object (PrivateServiceConnectConfig)},&quot;modelDeploymentMonitoringJob&quot;: string,&quot;predictRequestResponseLoggingConfig&quot;: {object (PredictRequestResponseLoggingConfig)},&quot;dedicatedEndpointEnabled&quot;: boolean,&quot;dedicatedEndpointDns&quot;: string,&quot;clientConnectionConfig&quot;: {object (ClientConnectionConfig)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean,&quot;genAiAdvancedFeaturesConfig&quot;: {object (GenAiAdvancedFeaturesConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Identifier. The resource name of the Endpoint.

`displayName`

`string`

Required. The display name of the Endpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description`

`string`

The description of the Endpoint.

`deployedModels[]`

` object ( DeployedModel  ` )

Output only. The models deployed in this Endpoint. To add or remove DeployedModels use `EndpointService.DeployModel` and `EndpointService.UndeployModel` respectively.

`trafficSplit`

`map (key: string, value: integer)`

A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel.

If a DeployedModel's ID is not listed in this map, then it receives no traffic.

The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`etag`

`string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize your Endpoints.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Endpoint was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Endpoint was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`encryptionSpec`

` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for an Endpoint. If set, this Endpoint and all sub-resources of this Endpoint will be secured by this key.

`network`

`string`

Optional. The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks) to which the Endpoint should be peered.

Private services access must already be configured for the network. If left unspecified, the Endpoint is not peered with any network.

Only one of the fields, `network` or `enable_private_service_connect` , can be set.

[Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert) : `projects/{project}/global/networks/{network}` . Where `{project}` is a project number, as in `12345` , and `{network}` is network name.

` enablePrivateServiceConnect (deprecated)  `

`boolean`

> This item is deprecated\!

Deprecated: If true, expose the Endpoint via private service connect.

Only one of the fields, `network` or `enable_private_service_connect` , can be set.

`privateServiceConnectConfig`

` object ( PrivateServiceConnectConfig  ` )

Optional. Configuration for private service connect.

`network` and `private_service_connect_config` are mutually exclusive.

`modelDeploymentMonitoringJob`

`string`

Output only. Resource name of the Model Monitoring job associated with this Endpoint if monitoring is enabled by `JobService.CreateModelDeploymentMonitoringJob` . Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`

`predictRequestResponseLoggingConfig`

` object ( PredictRequestResponseLoggingConfig  ` )

Configures the request-response logging for online prediction.

`dedicatedEndpointEnabled`

`boolean`

If true, the endpoint will be exposed through a dedicated DNS \[Endpoint.dedicated\_endpoint\_dns\]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitation will be removed soon.

`dedicatedEndpointDns`

`string`

Output only. DNS of the dedicated endpoint. Will only be populated if dedicated\_endpoint\_enabled is true. Depending on the features enabled, uid might be a random number or a string. For example, if fast\_tryout is enabled, uid will be fasttryout. Format: `https://{endpoint_id}.{region}-{uid}.prediction.vertexai.goog` .

`clientConnectionConfig`

` object ( ClientConnectionConfig  ` )

Configurations that are applied to the endpoint for online prediction.

`satisfiesPzs`

`boolean`

Output only. Reserved for future use.

`satisfiesPzi`

`boolean`

Output only. Reserved for future use.

`genAiAdvancedFeaturesConfig`

` object ( GenAiAdvancedFeaturesConfig  ` )

Optional. Configuration for GenAiAdvancedFeatures. If the endpoint is serving GenAI models, advanced features like native RAG integration can be configured. Currently, only Model Garden models are supported.

### DeployedModel

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;model&quot;: string,&quot;gdcConnectedModel&quot;: string,&quot;modelVersionId&quot;: string,&quot;displayName&quot;: string,&quot;createTime&quot;: string,&quot;explanationSpec&quot;: {object (ExplanationSpec)},&quot;disableExplanations&quot;: boolean,&quot;serviceAccount&quot;: string,&quot;enableContainerLogging&quot;: boolean,&quot;disableContainerLogging&quot;: boolean,&quot;enableAccessLogging&quot;: boolean,&quot;privateEndpoints&quot;: {object (PrivateEndpoints)},&quot;fasterDeploymentConfig&quot;: {object (FasterDeploymentConfig)},&quot;rolloutOptions&quot;: {object (RolloutOptions)},&quot;status&quot;: {object (Status)},&quot;systemLabels&quot;: {string: string,...},&quot;checkpointId&quot;: string,&quot;speculativeDecodingSpec&quot;: {object (SpeculativeDecodingSpec)},// Union field prediction_resources can be only one of the following:&quot;dedicatedResources&quot;: {object (DedicatedResources)},&quot;automaticResources&quot;: {object (AutomaticResources)},&quot;sharedResources&quot;: string,&quot;fullFineTunedResources&quot;: {object (FullFineTunedResources)}// End of list of possible types for union field prediction_resources.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`id`

`string`

Immutable. The ID of the DeployedModel. If not provided upon deployment, Agent Platform will generate a value for this ID.

This value should be 1-10 characters, and valid characters are `/[0-9]/` .

`model`

`string`

The resource name of the Model that this is the deployment of. Note that the Model may be in a different location than the DeployedModel's Endpoint.

The resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2` or `projects/{project}/locations/{location}/models/{model}@golden` if no version is specified, the default version will be deployed.

`gdcConnectedModel`

`string`

GDC pretrained / Gemini model name. The model name is a plain model name, e.g. gemini-1.5-flash-002.

`modelVersionId`

`string`

Output only. The version ID of the model that is deployed.

`displayName`

`string`

The display name of the DeployedModel. If not provided upon creation, the Model's display\_name is used.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when the DeployedModel was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`explanationSpec`

` object ( ExplanationSpec  ` )

Explanation configuration for this DeployedModel.

When deploying a Model using `EndpointService.DeployModel` , this value overrides the value of `Model.explanation_spec` . All fields of `explanation_spec` are optional in the request. If a field of `explanation_spec` is not populated, the value of the same field of `Model.explanation_spec` is inherited. If the corresponding `Model.explanation_spec` is not populated, all fields of the `explanation_spec` will be used for the explanation configuration.

`disableExplanations`

`boolean`

If true, deploy the model without explainable feature, regardless the existence of `Model.explanation_spec` or `explanation_spec` .

`serviceAccount`

`string`

The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project.

Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service account.

`enableContainerLogging`

`boolean`

If true, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging.

Only supported for custom-trained Models and AutoML Tabular Models.

`disableContainerLogging`

`boolean`

For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by default. Please note that the logs incur cost, which are subject to [Cloud Logging pricing](https://cloud.google.com/logging/pricing) .

User can disable container logging by setting this flag to true.

`enableAccessLogging`

`boolean`

If true, online prediction access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each prediction request.

Note that logs may incur a cost, especially if your project receives prediction requests at a high queries per second rate (QPS). Estimate your costs before enabling this option.

`privateEndpoints`

` object ( PrivateEndpoints  ` )

Output only. Provide paths for users to send predict/explain/health requests directly to the deployed model services running on Cloud via private services access. This field is populated if `network` is configured.

`fasterDeploymentConfig`

` object ( FasterDeploymentConfig  ` )

Configuration for faster model deployment.

`rolloutOptions`

` object ( RolloutOptions  ` )

Options for configuring rolling deployments.

`status`

` object ( Status  ` )

Output only. Runtime status of the deployed model.

`systemLabels`

`map (key: string, value: string)`

System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`checkpointId`

`string`

The checkpoint id of the model.

`speculativeDecodingSpec`

` object ( SpeculativeDecodingSpec  ` )

Optional. Spec for configuring speculative decoding.

Union field `prediction_resources` . The prediction (for example, the machine) resources that the DeployedModel uses. The user is billed for the resources (at least their minimal amount) even if the DeployedModel receives no traffic. Not all Models support all resources types. See `Model.supported_deployment_resources_types` . Required except for Large Model Deploy use cases. `prediction_resources` can be only one of the following:

`dedicatedResources`

` object ( DedicatedResources  ` )

A description of resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration.

`automaticResources`

` object ( AutomaticResources  ` )

A description of resources that to large degree are decided by Agent Platform, and require only a modest additional configuration.

`sharedResources`

`string`

The resource name of the shared DeploymentResourcePool to deploy on. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`

`fullFineTunedResources`

` object ( FullFineTunedResources  ` )

Optional. Resources for a full fine tuned model.

### DedicatedResources

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

Fields

`machineSpec`

` object ( MachineSpec  ` )

Required. Immutable. The specification of a single machine being used.

`minReplicaCount`

`integer`

Required. Immutable. The minimum number of machine replicas that will be always deployed on. This value must be greater than or equal to 1.

If traffic increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed.

`maxReplicaCount`

`integer`

Immutable. The maximum number of replicas that may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale to that many replicas is guaranteed (barring service outages). If traffic increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, will use `min_replica_count` as the default value.

The value of this field impacts the charge against Vertex CPU and GPU quotas. Specifically, you will be charged for (max\_replica\_count \* number of cores in the selected machine type) and (max\_replica\_count \* number of GPUs per replica in the selected machine type).

`requiredReplicaCount`

`integer`

Optional. Number of required available replicas for the deployment to succeed. This field is only needed when partial deployment/mutation is desired. If set, the deploy/mutate operation will succeed once available\_replica\_count reaches required\_replica\_count, and the rest of the replicas will be retried. If not set, the default required\_replica\_count will be min\_replica\_count.

`initialReplicaCount`

`integer`

Immutable. Number of initial replicas being deployed on when scaling the workload up from zero or when creating the workload in case `min_replica_count` = 0. When `min_replica_count` \> 0 (meaning that the scale-to-zero feature is not enabled), `initial_replica_count` should not be set. When `min_replica_count` = 0 (meaning that the scale-to-zero feature is enabled), `initial_replica_count` should be larger than zero, but no greater than `max_replica_count` .

`autoscalingMetricSpecs[]`

` object ( AutoscalingMetricSpec  ` )

Immutable. The metric specifications that overrides a resource utilization metric (CPU utilization, accelerator's duty cycle, and so on) target value (default to 60 if not set). At most one entry is allowed per metric.

If `machine_spec.accelerator_count` is above 0, the autoscaling will be based on both CPU utilization and accelerator's duty cycle metrics and scale up when either metrics exceeds its target value while scale down if both metrics are under their target value. The default target value is 60 for both metrics.

If `machine_spec.accelerator_count` is 0, the autoscaling will be based on CPU utilization metric only with default target value 60 if not explicitly set.

For example, in the case of Online Prediction, if you want to override target CPU utilization to 80, you should set `autoscaling_metric_specs.metric_name` to `aiplatform.googleapis.com/prediction/online/cpu/utilization` and `autoscaling_metric_specs.target` to `80` .

`spot`

`boolean`

Optional. If true, schedule the deployment workload on [spot VMs](https://cloud.google.com/kubernetes-engine/docs/concepts/spot-vms) .

`flexStart`

` object ( FlexStart  ` )

Optional. Immutable. If set, use DWS resource to schedule the deployment workload. reference: ( <https://cloud.google.com/blog/products/compute/introducing-dynamic-workload-scheduler> )

`scaleToZeroSpec`

` object ( ScaleToZeroSpec  ` )

Optional. Specification for scale-to-zero feature.

### MachineSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineType&quot;: string,&quot;acceleratorType&quot;: enum (AcceleratorType),&quot;acceleratorCount&quot;: integer,&quot;gpuPartitionSize&quot;: string,&quot;tpuTopology&quot;: string,&quot;multihostGpuNodeCount&quot;: integer,&quot;reservationAffinity&quot;: {object (ReservationAffinity)},&quot;minGpuDriverVersion&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`machineType`

`string`

Immutable. The type of the machine.

See the [list of machine types supported for prediction](https://cloud.google.com/vertex-ai/docs/predictions/configure-compute#machine-types)

See the [list of machine types supported for custom training](https://cloud.google.com/vertex-ai/docs/training/configure-compute#machine-types) .

For `  DeployedModel  ` this field is optional, and the default value is `n1-standard-2` . For `BatchPredictionJob` or as part of `WorkerPoolSpec` this field is required.

`acceleratorType`

`enum ( AcceleratorType` )

Immutable. The type of accelerator(s) that may be attached to the machine as per `accelerator_count` .

`acceleratorCount`

`integer`

The number of accelerators to attach to the machine.

For accelerator optimized machine types ( <https://cloud.google.com/compute/docs/accelerator-optimized-machines> , One may set the accelerator\_count from 1 to N for machine with N GPUs. If accelerator\_count is less than or equal to N / 2, Vertex will co-schedule the replicas of the model into the same VM to save cost.

For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set accelerator\_count to 1 to 8. If accelerator\_count is 1, 2, 3, or 4, Vertex will co-schedule 8, 4, 2, or 2 replicas of the model into the same VM to save cost.

When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM.

Note that the feature is not compatible with `multihost_gpu_node_count` . When multihost\_gpu\_node\_count is set, the co-scheduling will not be enabled.

`gpuPartitionSize`

`string`

Optional. Immutable. The Nvidia GPU partition size.

When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu\_partition\_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances.

The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes.

If set, the accelerator\_count should be set to 1.

`tpuTopology`

`string`

Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu\_topology: "2x2x1").

`multihostGpuNodeCount`

`integer`

Optional. Immutable. The number of nodes per replica for multihost GPU deployments.

`reservationAffinity`

` object ( ReservationAffinity  ` )

Optional. Immutable. Configuration controlling how this resource pool consumes reservation.

`minGpuDriverVersion`

`string`

Optional. Immutable. The minimum GPU driver version that this machine requires. For example, "535.104.06". If not specified, the default GPU driver version will be used by the underlying infrastructure.

### ReservationAffinity

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

Fields

`reservationAffinityType`

`enum ( Type` )

Required. Specifies the reservation affinity type.

`key`

`string`

Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC\_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.

`values[]`

`string`

Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.

### AutoscalingMetricSpec

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

Fields

`metricName`

`string`

Required. The resource metric name. Supported metrics:

  - For Online Prediction:
  - `aiplatform.googleapis.com/prediction/online/accelerator/duty_cycle`
  - `aiplatform.googleapis.com/prediction/online/cpu/utilization`
  - `aiplatform.googleapis.com/prediction/online/request_count`
  - `pubsub.googleapis.com/subscription/num_undelivered_messages`
  - `prometheus.googleapis.com/vertex_dcgm_fi_dev_gpu_util`
  - `prometheus.googleapis.com/vertex_vllm_gpu_cache_usage_perc`
  - `prometheus.googleapis.com/vertex_vllm_num_requests_waiting`

`target`

`integer`

The target resource utilization in percentage (1% - 100%) for the given metric; once the real usage deviates from the target by a certain percentage, the machine replicas change. The default value is 60 (representing 60%) if not provided.

`monitoredResourceLabels`

`map (key: string, value: string)`

Optional. The Cloud Monitoring monitored resource labels as key value pairs used for metrics filtering. See Cloud Monitoring Labels <https://cloud.google.com/monitoring/api/v3/metric-model#generic-label-info>

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### MonitoredResourceLabelsEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### FlexStart

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
  &quot;maxRuntimeDuration&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`maxRuntimeDuration`

` string ( Duration  ` format)

The max duration of the deployment is max\_runtime\_duration. The deployment will be terminated after the duration. The max\_runtime\_duration can be set up to 7 days.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### Duration

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years

`nanos`

`integer`

Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive.

### ScaleToZeroSpec

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

Fields

`minScaleupPeriod`

` string ( Duration  ` format)

Optional. Minimum duration that a deployment will be scaled up before traffic is evaluated for potential scale-down. \[MinValue=300\] (5 minutes) \[MaxValue=28800\] (8 hours)

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`idleScaledownPeriod`

` string ( Duration  ` format)

Optional. Duration of no traffic before scaling to zero. \[MinValue=300\] (5 minutes) \[MaxValue=28800\] (8 hours)

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### AutomaticResources

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
  &quot;minReplicaCount&quot;: integer,
  &quot;maxReplicaCount&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`minReplicaCount`

`integer`

Immutable. The minimum number of replicas that will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas up to `max_replica_count` , and as traffic decreases, some of these extra replicas may be freed. If the requested value is too large, the deployment will error.

`maxReplicaCount`

`integer`

Immutable. The maximum number of replicas that may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale to that many replicas is guaranteed (barring service outages). If traffic increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, a no upper bound for scaling under heavy traffic will be assume, though Agent Platform may be unable to scale beyond certain replica number.

### FullFineTunedResources

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;deploymentType&quot;: enum (DeploymentType),&quot;modelInferenceUnitCount&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`deploymentType`

`enum ( DeploymentType` )

Required. The kind of deployment.

`modelInferenceUnitCount`

`integer`

Optional. The number of model inference units to use for this deployment. This can only be specified for DEPLOYMENT\_TYPE\_PROD. The following table lists the number of model inference units for different model types: \* Gemini 2.5 Flash \* Foundation FMIU: 25 \* Expansion FMIU: 4 \* Gemini 2.5 Pro \* Foundation FMIU: 32 \* Expansion FMIU: 16 \* Veo 3.0 (undistilled) \* Foundation FMIU: 63 \* Expansion FMIU: 7 \* Veo 3.0 (distilled) \* Foundation FMIU: 30 \* Expansion FMIU: 10

### Timestamp

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`nanos`

`integer`

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### ExplanationSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parameters&quot;: {object (ExplanationParameters)},&quot;metadata&quot;: {object (ExplanationMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parameters`

` object ( ExplanationParameters  ` )

Required. Parameters that configure explaining of the Model's predictions.

`metadata`

` object ( ExplanationMetadata  ` )

Optional. Metadata describing the Model's input and output for explanation.

### ExplanationParameters

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;topK&quot;: integer,&quot;outputIndices&quot;: array,// Union field method can be only one of the following:&quot;sampledShapleyAttribution&quot;: {object (SampledShapleyAttribution)},&quot;integratedGradientsAttribution&quot;: {object (IntegratedGradientsAttribution)},&quot;xraiAttribution&quot;: {object (XraiAttribution)},&quot;examples&quot;: {object (Examples)}// End of list of possible types for union field method.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`topK`

`integer`

If populated, returns attributions for top K indices of outputs (defaults to 1). Only applies to Models that predicts more than one outputs (e,g, multi-class Models). When set to -1, returns explanations for all outputs.

`outputIndices`

` array ( ListValue  ` format)

If populated, only returns attributions that have `output_index` contained in output\_indices. It must be an ndarray of integers, with the same shape of the output it's explaining.

If not populated, returns attributions for `top_k` indices of outputs. If neither top\_k nor output\_indices is populated, returns the argmax index of the outputs.

Only applicable to Models that predict multiple outputs (e,g, multi-class Models that predict multiple classes).

Union field `method` .

`method` can be only one of the following:

`sampledShapleyAttribution`

` object ( SampledShapleyAttribution  ` )

An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features. Refer to this paper for model details: <https://arxiv.org/abs/1306.4265> .

`integratedGradientsAttribution`

` object ( IntegratedGradientsAttribution  ` )

An attribution method that computes Aumann-Shapley values taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1703.01365>

`xraiAttribution`

` object ( XraiAttribution  ` )

An attribution method that redistributes Integrated Gradients attribution to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1906.02825>

XRAI currently performs better on natural images, like a picture of a house or an animal. If the images are taken in artificial environments, like a lab or manufacturing line, or from diagnostic equipment, like x-rays or quality-control cameras, use Integrated Gradients instead.

`examples`

` object ( Examples  ` )

Example-based explanations that returns the nearest neighbors from the provided dataset.

### SampledShapleyAttribution

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
  &quot;pathCount&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`pathCount`

`integer`

Required. The number of feature permutations to consider when approximating the Shapley values.

Valid range of its value is \[1, 50\], inclusively.

### IntegratedGradientsAttribution

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stepCount&quot;: integer,&quot;smoothGradConfig&quot;: {object (SmoothGradConfig)},&quot;blurBaselineConfig&quot;: {object (BlurBaselineConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stepCount`

`integer`

Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is within the desired error range.

Valid range of its value is \[1, 100\], inclusively.

`smoothGradConfig`

` object ( SmoothGradConfig  ` )

Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf>

`blurBaselineConfig`

` object ( BlurBaselineConfig  ` )

Config for IG with blur baseline.

When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>

### SmoothGradConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;noisySampleCount&quot;: integer,// Union field GradientNoiseSigma can be only one of the following:&quot;noiseSigma&quot;: number,&quot;featureNoiseSigma&quot;: {object (FeatureNoiseSigma)}// End of list of possible types for union field GradientNoiseSigma.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`noisySampleCount`

`integer`

The number of gradient samples to use for approximation. The higher this number, the more accurate the gradient is, but the runtime complexity increases by this factor as well. Valid range of its value is \[1, 50\]. Defaults to 3.

Union field `GradientNoiseSigma` . Represents the standard deviation of the gaussian kernel that will be used to add noise to the interpolated inputs prior to computing gradients. `GradientNoiseSigma` can be only one of the following:

`noiseSigma`

`number`

This is a single float value and will be used to add noise to all the features. Use this field when all features are normalized to have the same distribution: scale to range \[0, 1\], \[-1, 1\] or z-scoring, where features are normalized to have 0-mean and 1-variance. Learn more about [normalization](https://developers.google.com/machine-learning/data-prep/transform/normalization) .

For best results the recommended value is about 10% - 20% of the standard deviation of the input feature. Refer to section 3.2 of the SmoothGrad paper: <https://arxiv.org/pdf/1706.03825.pdf> . Defaults to 0.1.

If the distribution is different per feature, set `feature_noise_sigma` instead for each feature.

`featureNoiseSigma`

` object ( FeatureNoiseSigma  ` )

This is similar to `noise_sigma` , but provides additional flexibility. A separate noise sigma can be provided for each feature, which is useful if their distributions are different. No noise is added to features that are not set. If this field is unset, `noise_sigma` will be used for all features.

### FeatureNoiseSigma

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;noiseSigma&quot;: [{object (NoiseSigmaForFeature)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`noiseSigma[]`

` object ( NoiseSigmaForFeature  ` )

Noise sigma per feature. No noise is added to features that are not set.

### NoiseSigmaForFeature

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
  &quot;name&quot;: string,
  &quot;sigma&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

The name of the input feature for which noise sigma is provided. The features are defined in `explanation metadata inputs` .

`sigma`

`number`

This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to `noise_sigma` but represents the noise added to the current feature. Defaults to 0.1.

### BlurBaselineConfig

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
  &quot;maxBlurSigma&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`maxBlurSigma`

`number`

The standard deviation of the blur kernel for the blurred baseline. The same blurring parameter is used for both the height and the width dimension. If not set, the method defaults to the zero (i.e. black for images) baseline.

### XraiAttribution

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stepCount&quot;: integer,&quot;smoothGradConfig&quot;: {object (SmoothGradConfig)},&quot;blurBaselineConfig&quot;: {object (BlurBaselineConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stepCount`

`integer`

Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is met within the desired error range.

Valid range of its value is \[1, 100\], inclusively.

`smoothGradConfig`

` object ( SmoothGradConfig  ` )

Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf>

`blurBaselineConfig`

` object ( BlurBaselineConfig  ` )

Config for XRAI with blur baseline.

When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>

### Examples

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;gcsSource&quot;: {object (GcsSource)},&quot;neighborCount&quot;: integer,// Union field source can be only one of the following:&quot;exampleGcsSource&quot;: {object (ExampleGcsSource)}// End of list of possible types for union field source.// Union field config can be only one of the following:&quot;nearestNeighborSearchConfig&quot;: value,&quot;presets&quot;: {object (Presets)}// End of list of possible types for union field config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`gcsSource`

` object ( GcsSource  ` )

The Cloud Storage locations that contain the instances to be indexed for approximate nearest neighbor search.

`neighborCount`

`integer`

The number of neighbors to return when querying for examples.

Union field `source` .

`source` can be only one of the following:

`exampleGcsSource`

` object ( ExampleGcsSource  ` )

The Cloud Storage input instances.

Union field `config` .

`config` can be only one of the following:

`nearestNeighborSearchConfig`

` value ( Value  ` format)

The full configuration for the generated index, the semantics are the same as `metadata` and should match [NearestNeighborSearchConfig](https://cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations-example-based#nearest-neighbor-search-config) .

`presets`

` object ( Presets  ` )

Simplified preset configuration, which automatically sets configuration values based on the desired query speed-precision trade-off and modality.

### ExampleGcsSource

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataFormat&quot;: enum (DataFormat),&quot;gcsSource&quot;: {object (GcsSource)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataFormat`

`enum ( DataFormat` )

The format in which instances are given, if not specified, assume it's JSONL format. Currently only JSONL format is supported.

`gcsSource`

` object ( GcsSource  ` )

The Cloud Storage location for the input instances.

### GcsSource

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
  &quot;uris&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`uris[]`

`string`

Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see <https://cloud.google.com/storage/docs/wildcards> .

### Value

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field kind can be only one of the following:&quot;nullValue&quot;: null,&quot;numberValue&quot;: number,&quot;stringValue&quot;: string,&quot;boolValue&quot;: boolean,&quot;structValue&quot;: {object},&quot;listValue&quot;: array// End of list of possible types for union field kind.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `kind` . The kind of value. `kind` can be only one of the following:

`nullValue`

`null`

Represents a JSON `null` .

`numberValue`

`number`

Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type.

`stringValue`

`string`

Represents a JSON string.

`boolValue`

`boolean`

Represents a JSON boolean ( `true` or `false` literal in JSON).

`structValue`

` object ( Struct  ` format)

Represents a JSON object.

`listValue`

` array ( ListValue  ` format)

Represents a JSON array.

### Struct

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
  &quot;fields&quot;: {
    string: value,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fields`

` map (key: string, value: value ( Value  ` format))

Unordered map of dynamically typed values.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### FieldsEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` value ( Value  ` format)

### ListValue

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
  &quot;values&quot;: [
    value
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`values[]`

` value ( Value  ` format)

Repeated field of dynamically typed values.

### Presets

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modality&quot;: enum (Modality),// Union field _query can be only one of the following:&quot;query&quot;: enum (Query)// End of list of possible types for union field _query.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`modality`

`enum ( Modality` )

The modality of the uploaded model, which automatically configures the distance measurement and feature normalization for the underlying example index and queries. If your model does not precisely fit one of these types, it is okay to choose the closest type.

Union field `_query` .

`_query` can be only one of the following:

`query`

`enum ( Query` )

Preset option controlling parameters for speed-precision trade-off when querying for examples. If omitted, defaults to `PRECISE` .

### ExplanationMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputs&quot;: {string: {object (InputMetadata)},...},&quot;outputs&quot;: {string: {object (OutputMetadata)},...},&quot;featureAttributionsSchemaUri&quot;: string,&quot;latentSpaceSource&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`inputs`

` map (key: string, value: object ( InputMetadata  ` ))

Required. Map from feature names to feature input metadata. Keys are the name of the features. Values are the specification of the feature.

An empty InputMetadata is valid. It describes a text feature which has the name specified as the key in `ExplanationMetadata.inputs` . The baseline of the empty feature is chosen by Agent Platform.

For Agent Platform-provided Tensorflow images, the key can be any friendly name of the feature. Once specified, `featureAttributions` are keyed by this key (if not grouped with another feature).

For custom images, the key must match with the key in `instance` .

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`outputs`

` map (key: string, value: object ( OutputMetadata  ` ))

Required. Map from output names to output metadata.

For Agent Platform-provided Tensorflow images, keys can be any user defined string that consists of any UTF-8 characters.

For custom images, keys are the name of the output field in the prediction to be explained.

Currently only one key is allowed.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`featureAttributionsSchemaUri`

`string`

Points to a YAML file stored on Google Cloud Storage describing the format of the `feature attributions` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML tabular Models always have this field populated by Agent Platform. Note: The URI given on output may be different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`latentSpaceSource`

`string`

Name of the source to generate embeddings for example based explanations.

### InputsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (InputMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( InputMetadata  ` )

### InputMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputBaselines&quot;: [value],&quot;inputTensorName&quot;: string,&quot;encoding&quot;: enum (Encoding),&quot;modality&quot;: string,&quot;featureValueDomain&quot;: {object (FeatureValueDomain)},&quot;indicesTensorName&quot;: string,&quot;denseShapeTensorName&quot;: string,&quot;indexFeatureMapping&quot;: [string],&quot;encodedTensorName&quot;: string,&quot;encodedBaselines&quot;: [value],&quot;visualization&quot;: {object (Visualization)},&quot;groupName&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`inputBaselines[]`

` value ( Value  ` format)

Baseline inputs for this feature.

If no baseline is specified, Agent Platform chooses the baseline for this feature. If multiple baselines are specified, Agent Platform returns the average attributions across them in `Attribution.feature_attributions` .

For Agent Platform-provided Tensorflow images (both 1.x and 2.x), the shape of each baseline must match the shape of the input tensor. If a scalar is provided, we broadcast to the same shape as the input tensor.

For custom images, the element of the baselines must be in the same format as the feature's input in the `instance` \[\]. The schema of any single instance may be specified via Endpoint's DeployedModels' `Model's` `PredictSchemata's` `instance_schema_uri` .

`inputTensorName`

`string`

Name of the input tensor for this feature. Required and is only applicable to Agent Platform-provided images for Tensorflow.

`encoding`

`enum ( Encoding` )

Defines how the feature is encoded into the input tensor. Defaults to IDENTITY.

`modality`

`string`

Modality of the feature. Valid values are: numeric, image. Defaults to numeric.

`featureValueDomain`

` object ( FeatureValueDomain  ` )

The domain details of the input feature value. Like min/max, original mean or standard deviation if normalized.

`indicesTensorName`

`string`

Specifies the index of the values of the input tensor. Required when the input tensor is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .

`denseShapeTensorName`

`string`

Specifies the shape of the values of the input if the input is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .

`indexFeatureMapping[]`

`string`

A list of feature names for each index in the input tensor. Required when the input `InputMetadata.encoding` is BAG\_OF\_FEATURES, BAG\_OF\_FEATURES\_SPARSE, INDICATOR.

`encodedTensorName`

`string`

Encoded tensor is a transformation of the input tensor. Must be provided if choosing `Integrated Gradients attribution` or `XRAI attribution` and the input tensor is not differentiable.

An encoded tensor is generated if the input tensor is encoded by a lookup table.

`encodedBaselines[]`

` value ( Value  ` format)

A list of baselines for the encoded tensor.

The shape of each baseline should match the shape of the encoded tensor. If a scalar is provided, Agent Platform broadcasts to the same shape as the encoded tensor.

`visualization`

` object ( Visualization  ` )

Visualization configurations for image explanation.

`groupName`

`string`

Name of the group that the input belongs to. Features with the same group name will be treated as one feature when computing attributions. Features grouped together can have different shapes in value. If provided, there will be one single attribution generated in `Attribution.feature_attributions` , keyed by the group name.

### FeatureValueDomain

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
  &quot;minValue&quot;: number,
  &quot;maxValue&quot;: number,
  &quot;originalMean&quot;: number,
  &quot;originalStddev&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`minValue`

`number`

The minimum permissible value for this feature.

`maxValue`

`number`

The maximum permissible value for this feature.

`originalMean`

`number`

If this input feature has been normalized to a mean value of 0, the original\_mean specifies the mean value of the domain prior to normalization.

`originalStddev`

`number`

If this input feature has been normalized to a standard deviation of 1.0, the original\_stddev specifies the standard deviation of the domain prior to normalization.

### Visualization

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (Type),&quot;polarity&quot;: enum (Polarity),&quot;colorMap&quot;: enum (ColorMap),&quot;clipPercentUpperbound&quot;: number,&quot;clipPercentLowerbound&quot;: number,&quot;overlayType&quot;: enum (OverlayType)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

`enum ( Type` )

Type of the image visualization. Only applicable to `Integrated Gradients attribution` . OUTLINES shows regions of attribution, while PIXELS shows per-pixel attribution. Defaults to OUTLINES.

`polarity`

`enum ( Polarity` )

Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.

`colorMap`

`enum ( ColorMap` )

The color scheme used for the highlighted areas.

Defaults to PINK\_GREEN for `Integrated Gradients attribution` , which shows positive attributions in green and negative in pink.

Defaults to VIRIDIS for `XRAI attribution` , which highlights the most influential regions in yellow and the least influential in blue.

`clipPercentUpperbound`

`number`

Excludes attributions above the specified percentile from the highlighted areas. Using the clip\_percent\_upperbound and clip\_percent\_lowerbound together can be useful for filtering out noise and making it easier to see areas of strong attribution. Defaults to 99.9.

`clipPercentLowerbound`

`number`

Excludes attributions below the specified percentile, from the highlighted areas. Defaults to 62.

`overlayType`

`enum ( OverlayType` )

How the original image is displayed in the visualization. Adjusting the overlay can help increase visual clarity if the original image makes it difficult to view the visualization. Defaults to NONE.

### OutputsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (OutputMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( OutputMetadata  ` )

### OutputMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outputTensorName&quot;: string,// Union field display_name_mapping can be only one of the following:&quot;indexDisplayNameMapping&quot;: value,&quot;displayNameMappingKey&quot;: string// End of list of possible types for union field display_name_mapping.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outputTensorName`

`string`

Name of the output tensor. Required and is only applicable to Agent Platform provided images for Tensorflow.

Union field `display_name_mapping` . Defines how to map `Attribution.output_index` to `Attribution.output_display_name` .

If neither of the fields are specified, `Attribution.output_display_name` will not be populated. `display_name_mapping` can be only one of the following:

`indexDisplayNameMapping`

` value ( Value  ` format)

Static mapping between the index and display name.

Use this if the outputs are a deterministic n-dimensional array, e.g. a list of scores of all the classes in a pre-defined order for a multi-classification Model. It's not feasible if the outputs are non-deterministic, e.g. the Model produces top-k classes or sort the outputs by their values.

The shape of the value must be an n-dimensional array of strings. The number of dimensions must match that of the outputs to be explained. The `Attribution.output_display_name` is populated by locating in the mapping with `Attribution.output_index` .

`displayNameMappingKey`

`string`

Specify a field name in the prediction to look for the display name.

Use this if the prediction contains the display names for the outputs.

The display names in the prediction must have the same shape of the outputs, so that it can be located by `Attribution.output_index` for a specific output.

### PrivateEndpoints

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
  &quot;predictHttpUri&quot;: string,
  &quot;explainHttpUri&quot;: string,
  &quot;healthHttpUri&quot;: string,
  &quot;serviceAttachment&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`predictHttpUri`

`string`

Output only. Http(s) path to send prediction requests.

`explainHttpUri`

`string`

Output only. Http(s) path to send explain requests.

`healthHttpUri`

`string`

Output only. Http(s) path to send health check requests.

`serviceAttachment`

`string`

Output only. The name of the service attachment resource. Populated if private service connect is enabled.

### FasterDeploymentConfig

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
  &quot;fastTryoutEnabled&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fastTryoutEnabled`

`boolean`

If true, enable fast tryout feature for this deployed model.

### RolloutOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;previousDeployedModel&quot;: string,&quot;revisionNumber&quot;: integer,// Union field max_unavailable can be only one of the following:&quot;maxUnavailableReplicas&quot;: integer,&quot;maxUnavailablePercentage&quot;: integer// End of list of possible types for union field max_unavailable.// Union field max_surge can be only one of the following:&quot;maxSurgeReplicas&quot;: integer,&quot;maxSurgePercentage&quot;: integer// End of list of possible types for union field max_surge.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`previousDeployedModel`

`string`

ID of the DeployedModel that this deployment should replace.

`revisionNumber`

`integer`

Output only. Read-only. Revision number determines the relative priority of DeployedModels in the same rollout. The DeployedModel with the largest revision number specifies the intended state of the deployment.

Union field `max_unavailable` . Configures how many replicas are allowed to be unavailable during a rolling deployment. `max_unavailable` can be only one of the following:

`maxUnavailableReplicas`

`integer`

Absolute count of replicas allowed to be unavailable.

`maxUnavailablePercentage`

`integer`

Percentage of replicas allowed to be unavailable. For autoscaling deployments, this refers to the target replica count.

Union field `max_surge` . Configures how many additional replicas can be provisioned during a rolling deployment. `max_surge` can be only one of the following:

`maxSurgeReplicas`

`integer`

Absolute count of allowed additional replicas.

`maxSurgePercentage`

`integer`

Percentage of allowed additional replicas. For autoscaling deployments, this refers to the target replica count.

### Status

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
  &quot;message&quot;: string,
  &quot;lastUpdateTime&quot;: string,
  &quot;availableReplicaCount&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`message`

`string`

Output only. The latest deployed model's status message (if any).

`lastUpdateTime`

` string ( Timestamp  ` format)

Output only. The time at which the status was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`availableReplicaCount`

`integer`

Output only. The number of available replicas of the deployed model.

### SystemLabelsEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### SpeculativeDecodingSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;speculativeTokenCount&quot;: integer,// Union field speculation can be only one of the following:&quot;draftModelSpeculation&quot;: {object (DraftModelSpeculation)},&quot;ngramSpeculation&quot;: {object (NgramSpeculation)}// End of list of possible types for union field speculation.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`speculativeTokenCount`

`integer`

The number of speculative tokens to generate at each step.

Union field `speculation` . The type of speculation method to use. `speculation` can be only one of the following:

`draftModelSpeculation`

` object ( DraftModelSpeculation  ` )

draft model speculation.

`ngramSpeculation`

` object ( NgramSpeculation  ` )

N-Gram speculation.

### DraftModelSpeculation

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
  &quot;draftModel&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`draftModel`

`string`

Required. The resource name of the draft model.

### NgramSpeculation

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
  &quot;ngramSize&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`ngramSize`

`integer`

The number of last N input tokens used as ngram to search/match against the previous prompt sequence. This is equal to the N in N-Gram. The default value is 3 if not specified.

### TrafficSplitEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`integer`

### LabelsEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### EncryptionSpec

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
  &quot;kmsKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kmsKeyName`

`string`

Required. Resource name of the Cloud KMS key used to protect the resource.

The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` .

### PrivateServiceConnectConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enablePrivateServiceConnect&quot;: boolean,&quot;projectAllowlist&quot;: [string],&quot;pscAutomationConfigs&quot;: [{object (PSCAutomationConfig)}],&quot;enableSecurePrivateServiceConnect&quot;: boolean,&quot;serviceAttachment&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enablePrivateServiceConnect`

`boolean`

Required. If true, expose the IndexEndpoint via private service connect.

`projectAllowlist[]`

`string`

A list of Projects from which the forwarding rule will target the service attachment.

`pscAutomationConfigs[]`

` object ( PSCAutomationConfig  ` )

Optional. List of projects and networks where the PSC endpoints will be created. This field is used by Online Inference(Prediction) only.

`enableSecurePrivateServiceConnect`

`boolean`

Optional. If set to true, enable secure private service connect with IAM authorization. Otherwise, private service connect will be done without authorization. Note latency will be slightly increased if authorization is enabled.

`serviceAttachment`

`string`

Output only. The name of the generated service attachment resource. This is only populated if the endpoint is deployed with PrivateServiceConnect.

### PSCAutomationConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;projectId&quot;: string,&quot;network&quot;: string,&quot;ipAddress&quot;: string,&quot;forwardingRule&quot;: string,&quot;state&quot;: enum (PSCAutomationState),&quot;errorMessage&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. Project id used to create forwarding rule.

`network`

`string`

Required. The full name of the Google Compute Engine [network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks) . [Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/get) : `projects/{project}/global/networks/{network}` .

`ipAddress`

`string`

Output only. IP address rule created by the PSC service automation.

`forwardingRule`

`string`

Output only. Forwarding rule created by the PSC service automation.

`state`

`enum ( PSCAutomationState` )

Output only. The state of the PSC service automation.

`errorMessage`

`string`

Output only. Error message if the PSC service automation failed.

### PredictRequestResponseLoggingConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enabled&quot;: boolean,&quot;samplingRate&quot;: number,&quot;errorSamplingRate&quot;: number,&quot;bigqueryDestination&quot;: {object (BigQueryDestination)},&quot;requestResponseLoggingSchemaVersion&quot;: string,&quot;enableOtelLogging&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enabled`

`boolean`

If logging is enabled or not.

`samplingRate`

`number`

Percentage of requests to be logged, expressed as a fraction in range(0,1\].

`errorSamplingRate`

`number`

Optional. Percentage of failed requests to be logged, expressed as a fraction in range \[0,1\]. Only non-transient errors will be logged (currently `500/Internal` errors).

`bigqueryDestination`

` object ( BigQueryDestination  ` )

BigQuery table for logging. If only given a project, a new dataset will be created with name `logging_<endpoint-display-name>_<endpoint-id>` where will be made BigQuery-dataset-name compatible (e.g. most special characters will become underscores). If no table name is given, a new table will be created with name `request_response_logging`

`requestResponseLoggingSchemaVersion`

`string`

Output only. The schema version used in creating the BigQuery table for the request response logging. The versions are "v1" and "v2". The current default version is "v1".

`enableOtelLogging`

`boolean`

This field is used for large models. If true, in addition to the original large model logs, logs will be converted in OTel schema format, and saved in otel\_log column. Default value is false.

### BigQueryDestination

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
  &quot;outputUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outputUri`

`string`

Required. BigQuery URI to a project or table, up to 2000 characters long.

When only the project is specified, the Dataset and Table is created. When the full table reference is specified, the Dataset must exist and table must not exist.

Accepted forms:

  - BigQuery path. For example: `bq://projectId` or `bq://projectId.bqDatasetId` or `bq://projectId.bqDatasetId.bqTableId` .

### ClientConnectionConfig

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
  &quot;inferenceTimeout&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`inferenceTimeout`

` string ( Duration  ` format)

Customizable online prediction request timeout.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### GenAiAdvancedFeaturesConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragConfig&quot;: {object (RagConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`ragConfig`

` object ( RagConfig  ` )

Configuration for Retrieval Augmented Generation feature.

### RagConfig

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
  &quot;enableRag&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enableRag`

`boolean`

If true, enable Retrieval Augmented Generation in ChatCompletion request. Once enabled, the endpoint will be identified as GenAI endpoint and Arthedain router will be used.

### FieldMask

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
  &quot;paths&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`paths[]`

`string`

The set of field mask paths.

## Output Schema

Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.

### Endpoint

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;deployedModels&quot;: [{object (DeployedModel)}],&quot;trafficSplit&quot;: {string: integer,...},&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;network&quot;: string,&quot;enablePrivateServiceConnect&quot;: boolean,&quot;privateServiceConnectConfig&quot;: {object (PrivateServiceConnectConfig)},&quot;modelDeploymentMonitoringJob&quot;: string,&quot;predictRequestResponseLoggingConfig&quot;: {object (PredictRequestResponseLoggingConfig)},&quot;dedicatedEndpointEnabled&quot;: boolean,&quot;dedicatedEndpointDns&quot;: string,&quot;clientConnectionConfig&quot;: {object (ClientConnectionConfig)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean,&quot;genAiAdvancedFeaturesConfig&quot;: {object (GenAiAdvancedFeaturesConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Identifier. The resource name of the Endpoint.

`displayName`

`string`

Required. The display name of the Endpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description`

`string`

The description of the Endpoint.

`deployedModels[]`

` object ( DeployedModel  ` )

Output only. The models deployed in this Endpoint. To add or remove DeployedModels use `EndpointService.DeployModel` and `EndpointService.UndeployModel` respectively.

`trafficSplit`

`map (key: string, value: integer)`

A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel.

If a DeployedModel's ID is not listed in this map, then it receives no traffic.

The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`etag`

`string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize your Endpoints.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Endpoint was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Endpoint was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`encryptionSpec`

` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for an Endpoint. If set, this Endpoint and all sub-resources of this Endpoint will be secured by this key.

`network`

`string`

Optional. The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks) to which the Endpoint should be peered.

Private services access must already be configured for the network. If left unspecified, the Endpoint is not peered with any network.

Only one of the fields, `network` or `enable_private_service_connect` , can be set.

[Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert) : `projects/{project}/global/networks/{network}` . Where `{project}` is a project number, as in `12345` , and `{network}` is network name.

` enablePrivateServiceConnect (deprecated)  `

`boolean`

> This item is deprecated\!

Deprecated: If true, expose the Endpoint via private service connect.

Only one of the fields, `network` or `enable_private_service_connect` , can be set.

`privateServiceConnectConfig`

` object ( PrivateServiceConnectConfig  ` )

Optional. Configuration for private service connect.

`network` and `private_service_connect_config` are mutually exclusive.

`modelDeploymentMonitoringJob`

`string`

Output only. Resource name of the Model Monitoring job associated with this Endpoint if monitoring is enabled by `JobService.CreateModelDeploymentMonitoringJob` . Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`

`predictRequestResponseLoggingConfig`

` object ( PredictRequestResponseLoggingConfig  ` )

Configures the request-response logging for online prediction.

`dedicatedEndpointEnabled`

`boolean`

If true, the endpoint will be exposed through a dedicated DNS \[Endpoint.dedicated\_endpoint\_dns\]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitation will be removed soon.

`dedicatedEndpointDns`

`string`

Output only. DNS of the dedicated endpoint. Will only be populated if dedicated\_endpoint\_enabled is true. Depending on the features enabled, uid might be a random number or a string. For example, if fast\_tryout is enabled, uid will be fasttryout. Format: `https://{endpoint_id}.{region}-{uid}.prediction.vertexai.goog` .

`clientConnectionConfig`

` object ( ClientConnectionConfig  ` )

Configurations that are applied to the endpoint for online prediction.

`satisfiesPzs`

`boolean`

Output only. Reserved for future use.

`satisfiesPzi`

`boolean`

Output only. Reserved for future use.

`genAiAdvancedFeaturesConfig`

` object ( GenAiAdvancedFeaturesConfig  ` )

Optional. Configuration for GenAiAdvancedFeatures. If the endpoint is serving GenAI models, advanced features like native RAG integration can be configured. Currently, only Model Garden models are supported.

### DeployedModel

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;model&quot;: string,&quot;gdcConnectedModel&quot;: string,&quot;modelVersionId&quot;: string,&quot;displayName&quot;: string,&quot;createTime&quot;: string,&quot;explanationSpec&quot;: {object (ExplanationSpec)},&quot;disableExplanations&quot;: boolean,&quot;serviceAccount&quot;: string,&quot;enableContainerLogging&quot;: boolean,&quot;disableContainerLogging&quot;: boolean,&quot;enableAccessLogging&quot;: boolean,&quot;privateEndpoints&quot;: {object (PrivateEndpoints)},&quot;fasterDeploymentConfig&quot;: {object (FasterDeploymentConfig)},&quot;rolloutOptions&quot;: {object (RolloutOptions)},&quot;status&quot;: {object (Status)},&quot;systemLabels&quot;: {string: string,...},&quot;checkpointId&quot;: string,&quot;speculativeDecodingSpec&quot;: {object (SpeculativeDecodingSpec)},// Union field prediction_resources can be only one of the following:&quot;dedicatedResources&quot;: {object (DedicatedResources)},&quot;automaticResources&quot;: {object (AutomaticResources)},&quot;sharedResources&quot;: string,&quot;fullFineTunedResources&quot;: {object (FullFineTunedResources)}// End of list of possible types for union field prediction_resources.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`id`

`string`

Immutable. The ID of the DeployedModel. If not provided upon deployment, Agent Platform will generate a value for this ID.

This value should be 1-10 characters, and valid characters are `/[0-9]/` .

`model`

`string`

The resource name of the Model that this is the deployment of. Note that the Model may be in a different location than the DeployedModel's Endpoint.

The resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2` or `projects/{project}/locations/{location}/models/{model}@golden` if no version is specified, the default version will be deployed.

`gdcConnectedModel`

`string`

GDC pretrained / Gemini model name. The model name is a plain model name, e.g. gemini-1.5-flash-002.

`modelVersionId`

`string`

Output only. The version ID of the model that is deployed.

`displayName`

`string`

The display name of the DeployedModel. If not provided upon creation, the Model's display\_name is used.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when the DeployedModel was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`explanationSpec`

` object ( ExplanationSpec  ` )

Explanation configuration for this DeployedModel.

When deploying a Model using `EndpointService.DeployModel` , this value overrides the value of `Model.explanation_spec` . All fields of `explanation_spec` are optional in the request. If a field of `explanation_spec` is not populated, the value of the same field of `Model.explanation_spec` is inherited. If the corresponding `Model.explanation_spec` is not populated, all fields of the `explanation_spec` will be used for the explanation configuration.

`disableExplanations`

`boolean`

If true, deploy the model without explainable feature, regardless the existence of `Model.explanation_spec` or `explanation_spec` .

`serviceAccount`

`string`

The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project.

Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service account.

`enableContainerLogging`

`boolean`

If true, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging.

Only supported for custom-trained Models and AutoML Tabular Models.

`disableContainerLogging`

`boolean`

For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by default. Please note that the logs incur cost, which are subject to [Cloud Logging pricing](https://cloud.google.com/logging/pricing) .

User can disable container logging by setting this flag to true.

`enableAccessLogging`

`boolean`

If true, online prediction access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each prediction request.

Note that logs may incur a cost, especially if your project receives prediction requests at a high queries per second rate (QPS). Estimate your costs before enabling this option.

`privateEndpoints`

` object ( PrivateEndpoints  ` )

Output only. Provide paths for users to send predict/explain/health requests directly to the deployed model services running on Cloud via private services access. This field is populated if `network` is configured.

`fasterDeploymentConfig`

` object ( FasterDeploymentConfig  ` )

Configuration for faster model deployment.

`rolloutOptions`

` object ( RolloutOptions  ` )

Options for configuring rolling deployments.

`status`

` object ( Status  ` )

Output only. Runtime status of the deployed model.

`systemLabels`

`map (key: string, value: string)`

System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`checkpointId`

`string`

The checkpoint id of the model.

`speculativeDecodingSpec`

` object ( SpeculativeDecodingSpec  ` )

Optional. Spec for configuring speculative decoding.

Union field `prediction_resources` . The prediction (for example, the machine) resources that the DeployedModel uses. The user is billed for the resources (at least their minimal amount) even if the DeployedModel receives no traffic. Not all Models support all resources types. See `Model.supported_deployment_resources_types` . Required except for Large Model Deploy use cases. `prediction_resources` can be only one of the following:

`dedicatedResources`

` object ( DedicatedResources  ` )

A description of resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration.

`automaticResources`

` object ( AutomaticResources  ` )

A description of resources that to large degree are decided by Agent Platform, and require only a modest additional configuration.

`sharedResources`

`string`

The resource name of the shared DeploymentResourcePool to deploy on. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`

`fullFineTunedResources`

` object ( FullFineTunedResources  ` )

Optional. Resources for a full fine tuned model.

### DedicatedResources

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

Fields

`machineSpec`

` object ( MachineSpec  ` )

Required. Immutable. The specification of a single machine being used.

`minReplicaCount`

`integer`

Required. Immutable. The minimum number of machine replicas that will be always deployed on. This value must be greater than or equal to 1.

If traffic increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed.

`maxReplicaCount`

`integer`

Immutable. The maximum number of replicas that may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale to that many replicas is guaranteed (barring service outages). If traffic increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, will use `min_replica_count` as the default value.

The value of this field impacts the charge against Vertex CPU and GPU quotas. Specifically, you will be charged for (max\_replica\_count \* number of cores in the selected machine type) and (max\_replica\_count \* number of GPUs per replica in the selected machine type).

`requiredReplicaCount`

`integer`

Optional. Number of required available replicas for the deployment to succeed. This field is only needed when partial deployment/mutation is desired. If set, the deploy/mutate operation will succeed once available\_replica\_count reaches required\_replica\_count, and the rest of the replicas will be retried. If not set, the default required\_replica\_count will be min\_replica\_count.

`initialReplicaCount`

`integer`

Immutable. Number of initial replicas being deployed on when scaling the workload up from zero or when creating the workload in case `min_replica_count` = 0. When `min_replica_count` \> 0 (meaning that the scale-to-zero feature is not enabled), `initial_replica_count` should not be set. When `min_replica_count` = 0 (meaning that the scale-to-zero feature is enabled), `initial_replica_count` should be larger than zero, but no greater than `max_replica_count` .

`autoscalingMetricSpecs[]`

` object ( AutoscalingMetricSpec  ` )

Immutable. The metric specifications that overrides a resource utilization metric (CPU utilization, accelerator's duty cycle, and so on) target value (default to 60 if not set). At most one entry is allowed per metric.

If `machine_spec.accelerator_count` is above 0, the autoscaling will be based on both CPU utilization and accelerator's duty cycle metrics and scale up when either metrics exceeds its target value while scale down if both metrics are under their target value. The default target value is 60 for both metrics.

If `machine_spec.accelerator_count` is 0, the autoscaling will be based on CPU utilization metric only with default target value 60 if not explicitly set.

For example, in the case of Online Prediction, if you want to override target CPU utilization to 80, you should set `autoscaling_metric_specs.metric_name` to `aiplatform.googleapis.com/prediction/online/cpu/utilization` and `autoscaling_metric_specs.target` to `80` .

`spot`

`boolean`

Optional. If true, schedule the deployment workload on [spot VMs](https://cloud.google.com/kubernetes-engine/docs/concepts/spot-vms) .

`flexStart`

` object ( FlexStart  ` )

Optional. Immutable. If set, use DWS resource to schedule the deployment workload. reference: ( <https://cloud.google.com/blog/products/compute/introducing-dynamic-workload-scheduler> )

`scaleToZeroSpec`

` object ( ScaleToZeroSpec  ` )

Optional. Specification for scale-to-zero feature.

### MachineSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineType&quot;: string,&quot;acceleratorType&quot;: enum (AcceleratorType),&quot;acceleratorCount&quot;: integer,&quot;gpuPartitionSize&quot;: string,&quot;tpuTopology&quot;: string,&quot;multihostGpuNodeCount&quot;: integer,&quot;reservationAffinity&quot;: {object (ReservationAffinity)},&quot;minGpuDriverVersion&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`machineType`

`string`

Immutable. The type of the machine.

See the [list of machine types supported for prediction](https://cloud.google.com/vertex-ai/docs/predictions/configure-compute#machine-types)

See the [list of machine types supported for custom training](https://cloud.google.com/vertex-ai/docs/training/configure-compute#machine-types) .

For `  DeployedModel  ` this field is optional, and the default value is `n1-standard-2` . For `BatchPredictionJob` or as part of `WorkerPoolSpec` this field is required.

`acceleratorType`

`enum ( AcceleratorType` )

Immutable. The type of accelerator(s) that may be attached to the machine as per `accelerator_count` .

`acceleratorCount`

`integer`

The number of accelerators to attach to the machine.

For accelerator optimized machine types ( <https://cloud.google.com/compute/docs/accelerator-optimized-machines> , One may set the accelerator\_count from 1 to N for machine with N GPUs. If accelerator\_count is less than or equal to N / 2, Vertex will co-schedule the replicas of the model into the same VM to save cost.

For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set accelerator\_count to 1 to 8. If accelerator\_count is 1, 2, 3, or 4, Vertex will co-schedule 8, 4, 2, or 2 replicas of the model into the same VM to save cost.

When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM.

Note that the feature is not compatible with `multihost_gpu_node_count` . When multihost\_gpu\_node\_count is set, the co-scheduling will not be enabled.

`gpuPartitionSize`

`string`

Optional. Immutable. The Nvidia GPU partition size.

When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu\_partition\_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances.

The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes.

If set, the accelerator\_count should be set to 1.

`tpuTopology`

`string`

Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu\_topology: "2x2x1").

`multihostGpuNodeCount`

`integer`

Optional. Immutable. The number of nodes per replica for multihost GPU deployments.

`reservationAffinity`

` object ( ReservationAffinity  ` )

Optional. Immutable. Configuration controlling how this resource pool consumes reservation.

`minGpuDriverVersion`

`string`

Optional. Immutable. The minimum GPU driver version that this machine requires. For example, "535.104.06". If not specified, the default GPU driver version will be used by the underlying infrastructure.

### ReservationAffinity

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

Fields

`reservationAffinityType`

`enum ( Type` )

Required. Specifies the reservation affinity type.

`key`

`string`

Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC\_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.

`values[]`

`string`

Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.

### AutoscalingMetricSpec

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

Fields

`metricName`

`string`

Required. The resource metric name. Supported metrics:

  - For Online Prediction:
  - `aiplatform.googleapis.com/prediction/online/accelerator/duty_cycle`
  - `aiplatform.googleapis.com/prediction/online/cpu/utilization`
  - `aiplatform.googleapis.com/prediction/online/request_count`
  - `pubsub.googleapis.com/subscription/num_undelivered_messages`
  - `prometheus.googleapis.com/vertex_dcgm_fi_dev_gpu_util`
  - `prometheus.googleapis.com/vertex_vllm_gpu_cache_usage_perc`
  - `prometheus.googleapis.com/vertex_vllm_num_requests_waiting`

`target`

`integer`

The target resource utilization in percentage (1% - 100%) for the given metric; once the real usage deviates from the target by a certain percentage, the machine replicas change. The default value is 60 (representing 60%) if not provided.

`monitoredResourceLabels`

`map (key: string, value: string)`

Optional. The Cloud Monitoring monitored resource labels as key value pairs used for metrics filtering. See Cloud Monitoring Labels <https://cloud.google.com/monitoring/api/v3/metric-model#generic-label-info>

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### MonitoredResourceLabelsEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### FlexStart

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
  &quot;maxRuntimeDuration&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`maxRuntimeDuration`

` string ( Duration  ` format)

The max duration of the deployment is max\_runtime\_duration. The deployment will be terminated after the duration. The max\_runtime\_duration can be set up to 7 days.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### Duration

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years

`nanos`

`integer`

Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive.

### ScaleToZeroSpec

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

Fields

`minScaleupPeriod`

` string ( Duration  ` format)

Optional. Minimum duration that a deployment will be scaled up before traffic is evaluated for potential scale-down. \[MinValue=300\] (5 minutes) \[MaxValue=28800\] (8 hours)

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`idleScaledownPeriod`

` string ( Duration  ` format)

Optional. Duration of no traffic before scaling to zero. \[MinValue=300\] (5 minutes) \[MaxValue=28800\] (8 hours)

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### AutomaticResources

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
  &quot;minReplicaCount&quot;: integer,
  &quot;maxReplicaCount&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`minReplicaCount`

`integer`

Immutable. The minimum number of replicas that will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas up to `max_replica_count` , and as traffic decreases, some of these extra replicas may be freed. If the requested value is too large, the deployment will error.

`maxReplicaCount`

`integer`

Immutable. The maximum number of replicas that may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale to that many replicas is guaranteed (barring service outages). If traffic increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, a no upper bound for scaling under heavy traffic will be assume, though Agent Platform may be unable to scale beyond certain replica number.

### FullFineTunedResources

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;deploymentType&quot;: enum (DeploymentType),&quot;modelInferenceUnitCount&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`deploymentType`

`enum ( DeploymentType` )

Required. The kind of deployment.

`modelInferenceUnitCount`

`integer`

Optional. The number of model inference units to use for this deployment. This can only be specified for DEPLOYMENT\_TYPE\_PROD. The following table lists the number of model inference units for different model types: \* Gemini 2.5 Flash \* Foundation FMIU: 25 \* Expansion FMIU: 4 \* Gemini 2.5 Pro \* Foundation FMIU: 32 \* Expansion FMIU: 16 \* Veo 3.0 (undistilled) \* Foundation FMIU: 63 \* Expansion FMIU: 7 \* Veo 3.0 (distilled) \* Foundation FMIU: 30 \* Expansion FMIU: 10

### Timestamp

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`nanos`

`integer`

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### ExplanationSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parameters&quot;: {object (ExplanationParameters)},&quot;metadata&quot;: {object (ExplanationMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parameters`

` object ( ExplanationParameters  ` )

Required. Parameters that configure explaining of the Model's predictions.

`metadata`

` object ( ExplanationMetadata  ` )

Optional. Metadata describing the Model's input and output for explanation.

### ExplanationParameters

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;topK&quot;: integer,&quot;outputIndices&quot;: array,// Union field method can be only one of the following:&quot;sampledShapleyAttribution&quot;: {object (SampledShapleyAttribution)},&quot;integratedGradientsAttribution&quot;: {object (IntegratedGradientsAttribution)},&quot;xraiAttribution&quot;: {object (XraiAttribution)},&quot;examples&quot;: {object (Examples)}// End of list of possible types for union field method.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`topK`

`integer`

If populated, returns attributions for top K indices of outputs (defaults to 1). Only applies to Models that predicts more than one outputs (e,g, multi-class Models). When set to -1, returns explanations for all outputs.

`outputIndices`

` array ( ListValue  ` format)

If populated, only returns attributions that have `output_index` contained in output\_indices. It must be an ndarray of integers, with the same shape of the output it's explaining.

If not populated, returns attributions for `top_k` indices of outputs. If neither top\_k nor output\_indices is populated, returns the argmax index of the outputs.

Only applicable to Models that predict multiple outputs (e,g, multi-class Models that predict multiple classes).

Union field `method` .

`method` can be only one of the following:

`sampledShapleyAttribution`

` object ( SampledShapleyAttribution  ` )

An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features. Refer to this paper for model details: <https://arxiv.org/abs/1306.4265> .

`integratedGradientsAttribution`

` object ( IntegratedGradientsAttribution  ` )

An attribution method that computes Aumann-Shapley values taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1703.01365>

`xraiAttribution`

` object ( XraiAttribution  ` )

An attribution method that redistributes Integrated Gradients attribution to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1906.02825>

XRAI currently performs better on natural images, like a picture of a house or an animal. If the images are taken in artificial environments, like a lab or manufacturing line, or from diagnostic equipment, like x-rays or quality-control cameras, use Integrated Gradients instead.

`examples`

` object ( Examples  ` )

Example-based explanations that returns the nearest neighbors from the provided dataset.

### SampledShapleyAttribution

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
  &quot;pathCount&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`pathCount`

`integer`

Required. The number of feature permutations to consider when approximating the Shapley values.

Valid range of its value is \[1, 50\], inclusively.

### IntegratedGradientsAttribution

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stepCount&quot;: integer,&quot;smoothGradConfig&quot;: {object (SmoothGradConfig)},&quot;blurBaselineConfig&quot;: {object (BlurBaselineConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stepCount`

`integer`

Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is within the desired error range.

Valid range of its value is \[1, 100\], inclusively.

`smoothGradConfig`

` object ( SmoothGradConfig  ` )

Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf>

`blurBaselineConfig`

` object ( BlurBaselineConfig  ` )

Config for IG with blur baseline.

When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>

### SmoothGradConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;noisySampleCount&quot;: integer,// Union field GradientNoiseSigma can be only one of the following:&quot;noiseSigma&quot;: number,&quot;featureNoiseSigma&quot;: {object (FeatureNoiseSigma)}// End of list of possible types for union field GradientNoiseSigma.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`noisySampleCount`

`integer`

The number of gradient samples to use for approximation. The higher this number, the more accurate the gradient is, but the runtime complexity increases by this factor as well. Valid range of its value is \[1, 50\]. Defaults to 3.

Union field `GradientNoiseSigma` . Represents the standard deviation of the gaussian kernel that will be used to add noise to the interpolated inputs prior to computing gradients. `GradientNoiseSigma` can be only one of the following:

`noiseSigma`

`number`

This is a single float value and will be used to add noise to all the features. Use this field when all features are normalized to have the same distribution: scale to range \[0, 1\], \[-1, 1\] or z-scoring, where features are normalized to have 0-mean and 1-variance. Learn more about [normalization](https://developers.google.com/machine-learning/data-prep/transform/normalization) .

For best results the recommended value is about 10% - 20% of the standard deviation of the input feature. Refer to section 3.2 of the SmoothGrad paper: <https://arxiv.org/pdf/1706.03825.pdf> . Defaults to 0.1.

If the distribution is different per feature, set `feature_noise_sigma` instead for each feature.

`featureNoiseSigma`

` object ( FeatureNoiseSigma  ` )

This is similar to `noise_sigma` , but provides additional flexibility. A separate noise sigma can be provided for each feature, which is useful if their distributions are different. No noise is added to features that are not set. If this field is unset, `noise_sigma` will be used for all features.

### FeatureNoiseSigma

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;noiseSigma&quot;: [{object (NoiseSigmaForFeature)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`noiseSigma[]`

` object ( NoiseSigmaForFeature  ` )

Noise sigma per feature. No noise is added to features that are not set.

### NoiseSigmaForFeature

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
  &quot;name&quot;: string,
  &quot;sigma&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

The name of the input feature for which noise sigma is provided. The features are defined in `explanation metadata inputs` .

`sigma`

`number`

This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to `noise_sigma` but represents the noise added to the current feature. Defaults to 0.1.

### BlurBaselineConfig

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
  &quot;maxBlurSigma&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`maxBlurSigma`

`number`

The standard deviation of the blur kernel for the blurred baseline. The same blurring parameter is used for both the height and the width dimension. If not set, the method defaults to the zero (i.e. black for images) baseline.

### XraiAttribution

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stepCount&quot;: integer,&quot;smoothGradConfig&quot;: {object (SmoothGradConfig)},&quot;blurBaselineConfig&quot;: {object (BlurBaselineConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stepCount`

`integer`

Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is met within the desired error range.

Valid range of its value is \[1, 100\], inclusively.

`smoothGradConfig`

` object ( SmoothGradConfig  ` )

Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf>

`blurBaselineConfig`

` object ( BlurBaselineConfig  ` )

Config for XRAI with blur baseline.

When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>

### Examples

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;gcsSource&quot;: {object (GcsSource)},&quot;neighborCount&quot;: integer,// Union field source can be only one of the following:&quot;exampleGcsSource&quot;: {object (ExampleGcsSource)}// End of list of possible types for union field source.// Union field config can be only one of the following:&quot;nearestNeighborSearchConfig&quot;: value,&quot;presets&quot;: {object (Presets)}// End of list of possible types for union field config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`gcsSource`

` object ( GcsSource  ` )

The Cloud Storage locations that contain the instances to be indexed for approximate nearest neighbor search.

`neighborCount`

`integer`

The number of neighbors to return when querying for examples.

Union field `source` .

`source` can be only one of the following:

`exampleGcsSource`

` object ( ExampleGcsSource  ` )

The Cloud Storage input instances.

Union field `config` .

`config` can be only one of the following:

`nearestNeighborSearchConfig`

` value ( Value  ` format)

The full configuration for the generated index, the semantics are the same as `metadata` and should match [NearestNeighborSearchConfig](https://cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations-example-based#nearest-neighbor-search-config) .

`presets`

` object ( Presets  ` )

Simplified preset configuration, which automatically sets configuration values based on the desired query speed-precision trade-off and modality.

### ExampleGcsSource

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataFormat&quot;: enum (DataFormat),&quot;gcsSource&quot;: {object (GcsSource)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataFormat`

`enum ( DataFormat` )

The format in which instances are given, if not specified, assume it's JSONL format. Currently only JSONL format is supported.

`gcsSource`

` object ( GcsSource  ` )

The Cloud Storage location for the input instances.

### GcsSource

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
  &quot;uris&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`uris[]`

`string`

Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see <https://cloud.google.com/storage/docs/wildcards> .

### Value

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field kind can be only one of the following:&quot;nullValue&quot;: null,&quot;numberValue&quot;: number,&quot;stringValue&quot;: string,&quot;boolValue&quot;: boolean,&quot;structValue&quot;: {object},&quot;listValue&quot;: array// End of list of possible types for union field kind.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `kind` . The kind of value. `kind` can be only one of the following:

`nullValue`

`null`

Represents a JSON `null` .

`numberValue`

`number`

Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type.

`stringValue`

`string`

Represents a JSON string.

`boolValue`

`boolean`

Represents a JSON boolean ( `true` or `false` literal in JSON).

`structValue`

` object ( Struct  ` format)

Represents a JSON object.

`listValue`

` array ( ListValue  ` format)

Represents a JSON array.

### Struct

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
  &quot;fields&quot;: {
    string: value,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fields`

` map (key: string, value: value ( Value  ` format))

Unordered map of dynamically typed values.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### FieldsEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` value ( Value  ` format)

### ListValue

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
  &quot;values&quot;: [
    value
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`values[]`

` value ( Value  ` format)

Repeated field of dynamically typed values.

### Presets

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modality&quot;: enum (Modality),// Union field _query can be only one of the following:&quot;query&quot;: enum (Query)// End of list of possible types for union field _query.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`modality`

`enum ( Modality` )

The modality of the uploaded model, which automatically configures the distance measurement and feature normalization for the underlying example index and queries. If your model does not precisely fit one of these types, it is okay to choose the closest type.

Union field `_query` .

`_query` can be only one of the following:

`query`

`enum ( Query` )

Preset option controlling parameters for speed-precision trade-off when querying for examples. If omitted, defaults to `PRECISE` .

### ExplanationMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputs&quot;: {string: {object (InputMetadata)},...},&quot;outputs&quot;: {string: {object (OutputMetadata)},...},&quot;featureAttributionsSchemaUri&quot;: string,&quot;latentSpaceSource&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`inputs`

` map (key: string, value: object ( InputMetadata  ` ))

Required. Map from feature names to feature input metadata. Keys are the name of the features. Values are the specification of the feature.

An empty InputMetadata is valid. It describes a text feature which has the name specified as the key in `ExplanationMetadata.inputs` . The baseline of the empty feature is chosen by Agent Platform.

For Agent Platform-provided Tensorflow images, the key can be any friendly name of the feature. Once specified, `featureAttributions` are keyed by this key (if not grouped with another feature).

For custom images, the key must match with the key in `instance` .

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`outputs`

` map (key: string, value: object ( OutputMetadata  ` ))

Required. Map from output names to output metadata.

For Agent Platform-provided Tensorflow images, keys can be any user defined string that consists of any UTF-8 characters.

For custom images, keys are the name of the output field in the prediction to be explained.

Currently only one key is allowed.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`featureAttributionsSchemaUri`

`string`

Points to a YAML file stored on Google Cloud Storage describing the format of the `feature attributions` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML tabular Models always have this field populated by Agent Platform. Note: The URI given on output may be different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`latentSpaceSource`

`string`

Name of the source to generate embeddings for example based explanations.

### InputsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (InputMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( InputMetadata  ` )

### InputMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputBaselines&quot;: [value],&quot;inputTensorName&quot;: string,&quot;encoding&quot;: enum (Encoding),&quot;modality&quot;: string,&quot;featureValueDomain&quot;: {object (FeatureValueDomain)},&quot;indicesTensorName&quot;: string,&quot;denseShapeTensorName&quot;: string,&quot;indexFeatureMapping&quot;: [string],&quot;encodedTensorName&quot;: string,&quot;encodedBaselines&quot;: [value],&quot;visualization&quot;: {object (Visualization)},&quot;groupName&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`inputBaselines[]`

` value ( Value  ` format)

Baseline inputs for this feature.

If no baseline is specified, Agent Platform chooses the baseline for this feature. If multiple baselines are specified, Agent Platform returns the average attributions across them in `Attribution.feature_attributions` .

For Agent Platform-provided Tensorflow images (both 1.x and 2.x), the shape of each baseline must match the shape of the input tensor. If a scalar is provided, we broadcast to the same shape as the input tensor.

For custom images, the element of the baselines must be in the same format as the feature's input in the `instance` \[\]. The schema of any single instance may be specified via Endpoint's DeployedModels' `Model's` `PredictSchemata's` `instance_schema_uri` .

`inputTensorName`

`string`

Name of the input tensor for this feature. Required and is only applicable to Agent Platform-provided images for Tensorflow.

`encoding`

`enum ( Encoding` )

Defines how the feature is encoded into the input tensor. Defaults to IDENTITY.

`modality`

`string`

Modality of the feature. Valid values are: numeric, image. Defaults to numeric.

`featureValueDomain`

` object ( FeatureValueDomain  ` )

The domain details of the input feature value. Like min/max, original mean or standard deviation if normalized.

`indicesTensorName`

`string`

Specifies the index of the values of the input tensor. Required when the input tensor is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .

`denseShapeTensorName`

`string`

Specifies the shape of the values of the input if the input is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .

`indexFeatureMapping[]`

`string`

A list of feature names for each index in the input tensor. Required when the input `InputMetadata.encoding` is BAG\_OF\_FEATURES, BAG\_OF\_FEATURES\_SPARSE, INDICATOR.

`encodedTensorName`

`string`

Encoded tensor is a transformation of the input tensor. Must be provided if choosing `Integrated Gradients attribution` or `XRAI attribution` and the input tensor is not differentiable.

An encoded tensor is generated if the input tensor is encoded by a lookup table.

`encodedBaselines[]`

` value ( Value  ` format)

A list of baselines for the encoded tensor.

The shape of each baseline should match the shape of the encoded tensor. If a scalar is provided, Agent Platform broadcasts to the same shape as the encoded tensor.

`visualization`

` object ( Visualization  ` )

Visualization configurations for image explanation.

`groupName`

`string`

Name of the group that the input belongs to. Features with the same group name will be treated as one feature when computing attributions. Features grouped together can have different shapes in value. If provided, there will be one single attribution generated in `Attribution.feature_attributions` , keyed by the group name.

### FeatureValueDomain

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
  &quot;minValue&quot;: number,
  &quot;maxValue&quot;: number,
  &quot;originalMean&quot;: number,
  &quot;originalStddev&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`minValue`

`number`

The minimum permissible value for this feature.

`maxValue`

`number`

The maximum permissible value for this feature.

`originalMean`

`number`

If this input feature has been normalized to a mean value of 0, the original\_mean specifies the mean value of the domain prior to normalization.

`originalStddev`

`number`

If this input feature has been normalized to a standard deviation of 1.0, the original\_stddev specifies the standard deviation of the domain prior to normalization.

### Visualization

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (Type),&quot;polarity&quot;: enum (Polarity),&quot;colorMap&quot;: enum (ColorMap),&quot;clipPercentUpperbound&quot;: number,&quot;clipPercentLowerbound&quot;: number,&quot;overlayType&quot;: enum (OverlayType)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

`enum ( Type` )

Type of the image visualization. Only applicable to `Integrated Gradients attribution` . OUTLINES shows regions of attribution, while PIXELS shows per-pixel attribution. Defaults to OUTLINES.

`polarity`

`enum ( Polarity` )

Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.

`colorMap`

`enum ( ColorMap` )

The color scheme used for the highlighted areas.

Defaults to PINK\_GREEN for `Integrated Gradients attribution` , which shows positive attributions in green and negative in pink.

Defaults to VIRIDIS for `XRAI attribution` , which highlights the most influential regions in yellow and the least influential in blue.

`clipPercentUpperbound`

`number`

Excludes attributions above the specified percentile from the highlighted areas. Using the clip\_percent\_upperbound and clip\_percent\_lowerbound together can be useful for filtering out noise and making it easier to see areas of strong attribution. Defaults to 99.9.

`clipPercentLowerbound`

`number`

Excludes attributions below the specified percentile, from the highlighted areas. Defaults to 62.

`overlayType`

`enum ( OverlayType` )

How the original image is displayed in the visualization. Adjusting the overlay can help increase visual clarity if the original image makes it difficult to view the visualization. Defaults to NONE.

### OutputsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (OutputMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( OutputMetadata  ` )

### OutputMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outputTensorName&quot;: string,// Union field display_name_mapping can be only one of the following:&quot;indexDisplayNameMapping&quot;: value,&quot;displayNameMappingKey&quot;: string// End of list of possible types for union field display_name_mapping.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outputTensorName`

`string`

Name of the output tensor. Required and is only applicable to Agent Platform provided images for Tensorflow.

Union field `display_name_mapping` . Defines how to map `Attribution.output_index` to `Attribution.output_display_name` .

If neither of the fields are specified, `Attribution.output_display_name` will not be populated. `display_name_mapping` can be only one of the following:

`indexDisplayNameMapping`

` value ( Value  ` format)

Static mapping between the index and display name.

Use this if the outputs are a deterministic n-dimensional array, e.g. a list of scores of all the classes in a pre-defined order for a multi-classification Model. It's not feasible if the outputs are non-deterministic, e.g. the Model produces top-k classes or sort the outputs by their values.

The shape of the value must be an n-dimensional array of strings. The number of dimensions must match that of the outputs to be explained. The `Attribution.output_display_name` is populated by locating in the mapping with `Attribution.output_index` .

`displayNameMappingKey`

`string`

Specify a field name in the prediction to look for the display name.

Use this if the prediction contains the display names for the outputs.

The display names in the prediction must have the same shape of the outputs, so that it can be located by `Attribution.output_index` for a specific output.

### PrivateEndpoints

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
  &quot;predictHttpUri&quot;: string,
  &quot;explainHttpUri&quot;: string,
  &quot;healthHttpUri&quot;: string,
  &quot;serviceAttachment&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`predictHttpUri`

`string`

Output only. Http(s) path to send prediction requests.

`explainHttpUri`

`string`

Output only. Http(s) path to send explain requests.

`healthHttpUri`

`string`

Output only. Http(s) path to send health check requests.

`serviceAttachment`

`string`

Output only. The name of the service attachment resource. Populated if private service connect is enabled.

### FasterDeploymentConfig

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
  &quot;fastTryoutEnabled&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fastTryoutEnabled`

`boolean`

If true, enable fast tryout feature for this deployed model.

### RolloutOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;previousDeployedModel&quot;: string,&quot;revisionNumber&quot;: integer,// Union field max_unavailable can be only one of the following:&quot;maxUnavailableReplicas&quot;: integer,&quot;maxUnavailablePercentage&quot;: integer// End of list of possible types for union field max_unavailable.// Union field max_surge can be only one of the following:&quot;maxSurgeReplicas&quot;: integer,&quot;maxSurgePercentage&quot;: integer// End of list of possible types for union field max_surge.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`previousDeployedModel`

`string`

ID of the DeployedModel that this deployment should replace.

`revisionNumber`

`integer`

Output only. Read-only. Revision number determines the relative priority of DeployedModels in the same rollout. The DeployedModel with the largest revision number specifies the intended state of the deployment.

Union field `max_unavailable` . Configures how many replicas are allowed to be unavailable during a rolling deployment. `max_unavailable` can be only one of the following:

`maxUnavailableReplicas`

`integer`

Absolute count of replicas allowed to be unavailable.

`maxUnavailablePercentage`

`integer`

Percentage of replicas allowed to be unavailable. For autoscaling deployments, this refers to the target replica count.

Union field `max_surge` . Configures how many additional replicas can be provisioned during a rolling deployment. `max_surge` can be only one of the following:

`maxSurgeReplicas`

`integer`

Absolute count of allowed additional replicas.

`maxSurgePercentage`

`integer`

Percentage of allowed additional replicas. For autoscaling deployments, this refers to the target replica count.

### Status

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
  &quot;message&quot;: string,
  &quot;lastUpdateTime&quot;: string,
  &quot;availableReplicaCount&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`message`

`string`

Output only. The latest deployed model's status message (if any).

`lastUpdateTime`

` string ( Timestamp  ` format)

Output only. The time at which the status was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`availableReplicaCount`

`integer`

Output only. The number of available replicas of the deployed model.

### SystemLabelsEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### SpeculativeDecodingSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;speculativeTokenCount&quot;: integer,// Union field speculation can be only one of the following:&quot;draftModelSpeculation&quot;: {object (DraftModelSpeculation)},&quot;ngramSpeculation&quot;: {object (NgramSpeculation)}// End of list of possible types for union field speculation.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`speculativeTokenCount`

`integer`

The number of speculative tokens to generate at each step.

Union field `speculation` . The type of speculation method to use. `speculation` can be only one of the following:

`draftModelSpeculation`

` object ( DraftModelSpeculation  ` )

draft model speculation.

`ngramSpeculation`

` object ( NgramSpeculation  ` )

N-Gram speculation.

### DraftModelSpeculation

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
  &quot;draftModel&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`draftModel`

`string`

Required. The resource name of the draft model.

### NgramSpeculation

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
  &quot;ngramSize&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`ngramSize`

`integer`

The number of last N input tokens used as ngram to search/match against the previous prompt sequence. This is equal to the N in N-Gram. The default value is 3 if not specified.

### TrafficSplitEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`integer`

### LabelsEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### EncryptionSpec

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
  &quot;kmsKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kmsKeyName`

`string`

Required. Resource name of the Cloud KMS key used to protect the resource.

The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` .

### PrivateServiceConnectConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enablePrivateServiceConnect&quot;: boolean,&quot;projectAllowlist&quot;: [string],&quot;pscAutomationConfigs&quot;: [{object (PSCAutomationConfig)}],&quot;enableSecurePrivateServiceConnect&quot;: boolean,&quot;serviceAttachment&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enablePrivateServiceConnect`

`boolean`

Required. If true, expose the IndexEndpoint via private service connect.

`projectAllowlist[]`

`string`

A list of Projects from which the forwarding rule will target the service attachment.

`pscAutomationConfigs[]`

` object ( PSCAutomationConfig  ` )

Optional. List of projects and networks where the PSC endpoints will be created. This field is used by Online Inference(Prediction) only.

`enableSecurePrivateServiceConnect`

`boolean`

Optional. If set to true, enable secure private service connect with IAM authorization. Otherwise, private service connect will be done without authorization. Note latency will be slightly increased if authorization is enabled.

`serviceAttachment`

`string`

Output only. The name of the generated service attachment resource. This is only populated if the endpoint is deployed with PrivateServiceConnect.

### PSCAutomationConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;projectId&quot;: string,&quot;network&quot;: string,&quot;ipAddress&quot;: string,&quot;forwardingRule&quot;: string,&quot;state&quot;: enum (PSCAutomationState),&quot;errorMessage&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. Project id used to create forwarding rule.

`network`

`string`

Required. The full name of the Google Compute Engine [network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks) . [Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/get) : `projects/{project}/global/networks/{network}` .

`ipAddress`

`string`

Output only. IP address rule created by the PSC service automation.

`forwardingRule`

`string`

Output only. Forwarding rule created by the PSC service automation.

`state`

`enum ( PSCAutomationState` )

Output only. The state of the PSC service automation.

`errorMessage`

`string`

Output only. Error message if the PSC service automation failed.

### PredictRequestResponseLoggingConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enabled&quot;: boolean,&quot;samplingRate&quot;: number,&quot;errorSamplingRate&quot;: number,&quot;bigqueryDestination&quot;: {object (BigQueryDestination)},&quot;requestResponseLoggingSchemaVersion&quot;: string,&quot;enableOtelLogging&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enabled`

`boolean`

If logging is enabled or not.

`samplingRate`

`number`

Percentage of requests to be logged, expressed as a fraction in range(0,1\].

`errorSamplingRate`

`number`

Optional. Percentage of failed requests to be logged, expressed as a fraction in range \[0,1\]. Only non-transient errors will be logged (currently `500/Internal` errors).

`bigqueryDestination`

` object ( BigQueryDestination  ` )

BigQuery table for logging. If only given a project, a new dataset will be created with name `logging_<endpoint-display-name>_<endpoint-id>` where will be made BigQuery-dataset-name compatible (e.g. most special characters will become underscores). If no table name is given, a new table will be created with name `request_response_logging`

`requestResponseLoggingSchemaVersion`

`string`

Output only. The schema version used in creating the BigQuery table for the request response logging. The versions are "v1" and "v2". The current default version is "v1".

`enableOtelLogging`

`boolean`

This field is used for large models. If true, in addition to the original large model logs, logs will be converted in OTel schema format, and saved in otel\_log column. Default value is false.

### BigQueryDestination

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
  &quot;outputUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outputUri`

`string`

Required. BigQuery URI to a project or table, up to 2000 characters long.

When only the project is specified, the Dataset and Table is created. When the full table reference is specified, the Dataset must exist and table must not exist.

Accepted forms:

  - BigQuery path. For example: `bq://projectId` or `bq://projectId.bqDatasetId` or `bq://projectId.bqDatasetId.bqTableId` .

### ClientConnectionConfig

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
  &quot;inferenceTimeout&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`inferenceTimeout`

` string ( Duration  ` format)

Customizable online prediction request timeout.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### GenAiAdvancedFeaturesConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragConfig&quot;: {object (RagConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`ragConfig`

` object ( RagConfig  ` )

Configuration for Retrieval Augmented Generation feature.

### RagConfig

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
  &quot;enableRag&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enableRag`

`boolean`

If true, enable Retrieval Augmented Generation in ChatCompletion request. Once enabled, the endpoint will be identified as GenAI endpoint and Arthedain router will be used.

### Tool Annotations

Destructive Hint: ✅ | Idempotent Hint: ✅ | Read Only Hint: ❌ | Open World Hint: ❌
