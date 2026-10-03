---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `create_endpoint`

Creates a Agent Platform Endpoint resource within a Google Cloud project. This acts as a logical serving host and stable URL for online predictions. Create this first before deploying any models for real-time inference. Format: 'projects/{project_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `create_endpoint` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "create_endpoint",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `EndpointService.CreateEndpoint` .

### CreateEndpointRequest

**JSON representation**

```
{
  "parent": string,
  "endpoint": {
    object (Endpoint)
  },
  "endpointId": string
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`     | `string` Required. The resource name of the Location to create the Endpoint in. Format: `projects/{project}/locations/{location}`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `endpoint`   | `object ( `[`Endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Endpoint)` )` Required. The Endpoint to create.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `endpointId` | `string` Immutable. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Agent Platform will generate a value for this ID. If the first character is a letter, this value may be up to 63 characters, and valid characters are `[a-z0-9-]` . The last character must be a letter or number. If the first character is a number, this value may be up to 9 characters, and valid characters are `[0-9]` with no leading zeros. When using HTTP/JSON, this field is populated based on a query string argument, such as `?endpoint_id=12345` . This is the fallback for fields that are not included in either the URI or the body. |

### Endpoint

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "deployedModels": [
    {
      object (DeployedModel)
    }
  ],
  "trafficSplit": {
    string: integer,
    ...
  },
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "network": string,
  "enablePrivateServiceConnect": boolean,
  "privateServiceConnectConfig": {
    object (PrivateServiceConnectConfig)
  },
  "modelDeploymentMonitoringJob": string,
  "predictRequestResponseLoggingConfig": {
    object (PredictRequestResponseLoggingConfig)
  },
  "dedicatedEndpointEnabled": boolean,
  "dedicatedEndpointDns": string,
  "clientConnectionConfig": {
    object (ClientConnectionConfig)
  },
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean,
  "genAiAdvancedFeaturesConfig": {
    object (GenAiAdvancedFeaturesConfig)
  },
  "publisherModelConfig": {
    object (PublisherModelConfig)
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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Identifier. The resource name of the Endpoint.</p></td>
</tr>
<tr class="even">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>Required. The display name of the Endpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>The description of the Endpoint.</p></td>
</tr>
<tr class="even">
<td><code>deployedModels[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.DeployedModel"><code>DeployedModel</code></a><code> )</code></p>
<p>Output only. The models deployed in this Endpoint. To add or remove DeployedModels use <code>EndpointService.DeployModel</code> and <code>EndpointService.UndeployModel</code> respectively.</p></td>
</tr>
<tr class="odd">
<td><code>trafficSplit</code></td>
<td><p><code>map (key: string, value: integer)</code></p>
<p>A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel.</p>
<p>If a DeployedModel's ID is not listed in this map, then it receives no traffic.</p>
<p>The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>etag</code></td>
<td><p><code>string</code></p>
<p>Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.</p></td>
</tr>
<tr class="odd">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>The labels with user-defined metadata to organize your Endpoints.</p>
<p>Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.</p>
<p>See <a href="https://goo.gl/xmQnxf">https://goo.gl/xmQnxf</a> for more information and examples of labels.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this Endpoint was created.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>updateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this Endpoint was last updated.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>encryptionSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.EncryptionSpec"><code>EncryptionSpec</code></a><code> )</code></p>
<p>Customer-managed encryption key spec for an Endpoint. If set, this Endpoint and all sub-resources of this Endpoint will be secured by this key.</p></td>
</tr>
<tr class="odd">
<td><code>network</code></td>
<td><p><code>string</code></p>
<p>Optional. The full name of the Google Compute Engine <a href="https://cloud.google.com//compute/docs/networks-and-firewalls#networks">network</a> to which the Endpoint should be peered.</p>
<p>Private services access must already be configured for the network. If left unspecified, the Endpoint is not peered with any network.</p>
<p>Only one of the fields, <code>network</code> or <code>enable_private_service_connect</code> , can be set.</p>
<p><a href="https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert">Format</a> : <code>projects/{project}/global/networks/{network}</code> . Where <code>{project}</code> is a project number, as in <code>12345</code> , and <code>{network}</code> is network name.</p></td>
</tr>
<tr class="even">
<td><code>enablePrivateServiceConnect </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated: If true, expose the Endpoint via private service connect.</p>
<p>Only one of the fields, <code>network</code> or <code>enable_private_service_connect</code> , can be set.</p></td>
</tr>
<tr class="odd">
<td><code>privateServiceConnectConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.PrivateServiceConnectConfig"><code>PrivateServiceConnectConfig</code></a><code> )</code></p>
<p>Optional. Configuration for private service connect.</p>
<p><code>network</code> and <code>private_service_connect_config</code> are mutually exclusive.</p></td>
</tr>
<tr class="even">
<td><code>modelDeploymentMonitoringJob</code></td>
<td><p><code>string</code></p>
<p>Output only. Resource name of the Model Monitoring job associated with this Endpoint if monitoring is enabled by <code>JobService.CreateModelDeploymentMonitoringJob</code> . Format: <code>projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}</code></p></td>
</tr>
<tr class="odd">
<td><code>predictRequestResponseLoggingConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.PredictRequestResponseLoggingConfig"><code>PredictRequestResponseLoggingConfig</code></a><code> )</code></p>
<p>Configures the request-response logging for online prediction.</p></td>
</tr>
<tr class="even">
<td><code>dedicatedEndpointEnabled</code></td>
<td><p><code>boolean</code></p>
<p>If true, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitation will be removed soon.</p></td>
</tr>
<tr class="odd">
<td><code>dedicatedEndpointDns</code></td>
<td><p><code>string</code></p>
<p>Output only. DNS of the dedicated endpoint. Will only be populated if dedicated_endpoint_enabled is true. Depending on the features enabled, uid might be a random number or a string. For example, if fast_tryout is enabled, uid will be fasttryout. Format: <code>https://{endpoint_id}.{region}-{uid}.prediction.vertexai.goog</code> .</p></td>
</tr>
<tr class="even">
<td><code>clientConnectionConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.ClientConnectionConfig"><code>ClientConnectionConfig</code></a><code> )</code></p>
<p>Configurations that are applied to the endpoint for online prediction.</p></td>
</tr>
<tr class="odd">
<td><code>satisfiesPzs</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Reserved for future use.</p></td>
</tr>
<tr class="even">
<td><code>satisfiesPzi</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Reserved for future use.</p></td>
</tr>
<tr class="odd">
<td><code>genAiAdvancedFeaturesConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.GenAiAdvancedFeaturesConfig"><code>GenAiAdvancedFeaturesConfig</code></a><code> )</code></p>
<p>Optional. Configuration for GenAiAdvancedFeatures. If the endpoint is serving GenAI models, advanced features like native RAG integration can be configured. Currently, only Model Garden models are supported.</p></td>
</tr>
<tr class="even">
<td><code>publisherModelConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.PublisherModelConfig"><code>PublisherModelConfig</code></a><code> )</code></p>
<p>Optional. Configuration for a Publisher Model. This message contains details about a publisher model used with this Endpoint, such as logging config or data sharing settings.</p></td>
</tr>
</tbody>
</table>

### DeployedModel

**JSON representation**

```
{
  "id": string,
  "model": string,
  "gdcConnectedModel": string,
  "modelVersionId": string,
  "displayName": string,
  "createTime": string,
  "explanationSpec": {
    object (ExplanationSpec)
  },
  "disableExplanations": boolean,
  "serviceAccount": string,
  "enableContainerLogging": boolean,
  "disableContainerLogging": boolean,
  "enableAccessLogging": boolean,
  "privateEndpoints": {
    object (PrivateEndpoints)
  },
  "fasterDeploymentConfig": {
    object (FasterDeploymentConfig)
  },
  "rolloutOptions": {
    object (RolloutOptions)
  },
  "status": {
    object (Status)
  },
  "systemLabels": {
    string: string,
    ...
  },
  "checkpointId": string,
  "speculativeDecodingSpec": {
    object (SpeculativeDecodingSpec)
  },

  // Union field prediction_resources can be only one of the following:
  "dedicatedResources": {
    object (DedicatedResources)
  },
  "automaticResources": {
    object (AutomaticResources)
  },
  "sharedResources": string,
  "fullFineTunedResources": {
    object (FullFineTunedResources)
  }
  // End of list of possible types for union field prediction_resources.
}
```

| Fields                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`                                                                                                                                                                                                                                                                                                                                                                                                                                                | `string` Immutable. The ID of the DeployedModel. If not provided upon deployment, Agent Platform will generate a value for this ID. This value should be 1-10 characters, and valid characters are `/[0-9]/` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `model`                                                                                                                                                                                                                                                                                                                                                                                                                                             | `string` The resource name of the Model that this is the deployment of. Note that the Model may be in a different location than the DeployedModel's Endpoint. The resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2` or `projects/{project}/locations/{location}/models/{model}@golden` if no version is specified, the default version will be deployed.                                                                                                                                                                                                                                         |
| `gdcConnectedModel`                                                                                                                                                                                                                                                                                                                                                                                                                                 | `string` GDC pretrained / Gemini model name. The model name is a plain model name, e.g. gemini-1.5-flash-002.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `modelVersionId`                                                                                                                                                                                                                                                                                                                                                                                                                                    | `string` Output only. The version ID of the model that is deployed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `displayName`                                                                                                                                                                                                                                                                                                                                                                                                                                       | `string` The display name of the DeployedModel. If not provided upon creation, the Model's display_name is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `createTime`                                                                                                                                                                                                                                                                                                                                                                                                                                        | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when the DeployedModel was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                 |
| `explanationSpec`                                                                                                                                                                                                                                                                                                                                                                                                                                   | `object ( `[`ExplanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.ExplanationSpec)` )` Explanation configuration for this DeployedModel. When deploying a Model using `EndpointService.DeployModel` , this value overrides the value of `Model.explanation_spec` . All fields of `explanation_spec` are optional in the request. If a field of `explanation_spec` is not populated, the value of the same field of `Model.explanation_spec` is inherited. If the corresponding `Model.explanation_spec` is not populated, all fields of the `explanation_spec` will be used for the explanation configuration. |
| `disableExplanations`                                                                                                                                                                                                                                                                                                                                                                                                                               | `boolean` If true, deploy the model without explainable feature, regardless the existence of `Model.explanation_spec` or `explanation_spec` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `serviceAccount`                                                                                                                                                                                                                                                                                                                                                                                                                                    | `string` The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project. Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service account.                                                                                                                                                                                                                                                                                                                           |
| `enableContainerLogging`                                                                                                                                                                                                                                                                                                                                                                                                                            | `boolean` If true, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging. Only supported for custom-trained Models and AutoML Tabular Models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `disableContainerLogging`                                                                                                                                                                                                                                                                                                                                                                                                                           | `boolean` For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by default. Please note that the logs incur cost, which are subject to [Cloud Logging pricing](https://cloud.google.com/logging/pricing) . User can disable container logging by setting this flag to true.                                                                                                                                                                                                                                                                                                                 |
| `enableAccessLogging`                                                                                                                                                                                                                                                                                                                                                                                                                               | `boolean` If true, online prediction access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each prediction request. Note that logs may incur a cost, especially if your project receives prediction requests at a high queries per second rate (QPS). Estimate your costs before enabling this option.                                                                                                                                                                                                                                                                                                   |
| `privateEndpoints`                                                                                                                                                                                                                                                                                                                                                                                                                                  | `object ( `[`PrivateEndpoints`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.PrivateEndpoints)` )` Output only. Provide paths for users to send predict/explain/health requests directly to the deployed model services running on Cloud via private services access. This field is populated if `network` is configured.                                                                                                                                                                                                                                                                                                |
| `fasterDeploymentConfig`                                                                                                                                                                                                                                                                                                                                                                                                                            | `object ( `[`FasterDeploymentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.FasterDeploymentConfig)` )` Configuration for faster model deployment.                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `rolloutOptions`                                                                                                                                                                                                                                                                                                                                                                                                                                    | `object ( `[`RolloutOptions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.RolloutOptions)` )` Options for configuring rolling deployments.                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `status`                                                                                                                                                                                                                                                                                                                                                                                                                                            | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Status)` )` Output only. Runtime status of the deployed model.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `systemLabels`                                                                                                                                                                                                                                                                                                                                                                                                                                      | `map (key: string, value: string)` System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `checkpointId`                                                                                                                                                                                                                                                                                                                                                                                                                                      | `string` The checkpoint id of the model.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `speculativeDecodingSpec`                                                                                                                                                                                                                                                                                                                                                                                                                           | `object ( `[`SpeculativeDecodingSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.SpeculativeDecodingSpec)` )` Optional. Spec for configuring speculative decoding.                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Union field `prediction_resources` . The prediction (for example, the machine) resources that the DeployedModel uses. The user is billed for the resources (at least their minimal amount) even if the DeployedModel receives no traffic. Not all Models support all resources types. See `Model.supported_deployment_resources_types` . Required except for Large Model Deploy use cases. `prediction_resources` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `dedicatedResources`                                                                                                                                                                                                                                                                                                                                                                                                                                | `object ( `[`DedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.DedicatedResources)` )` A description of resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration.                                                                                                                                                                                                                                                                                                                                                                                        |
| `automaticResources`                                                                                                                                                                                                                                                                                                                                                                                                                                | `object ( `[`AutomaticResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.AutomaticResources)` )` A description of resources that to large degree are decided by Agent Platform, and require only a modest additional configuration.                                                                                                                                                                                                                                                                                                                                                                                |
| `sharedResources`                                                                                                                                                                                                                                                                                                                                                                                                                                   | `string` The resource name of the shared DeploymentResourcePool to deploy on. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `fullFineTunedResources`                                                                                                                                                                                                                                                                                                                                                                                                                            | `object ( `[`FullFineTunedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.FullFineTunedResources)` )` Optional. Resources for a full fine tuned model.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

### DedicatedResources

**JSON representation**

```
{
  "machineSpec": {
    object (MachineSpec)
  },
  "minReplicaCount": integer,
  "maxReplicaCount": integer,
  "requiredReplicaCount": integer,
  "initialReplicaCount": integer,
  "autoscalingMetricSpecs": [
    {
      object (AutoscalingMetricSpec)
    }
  ],
  "spot": boolean,
  "flexStart": {
    object (FlexStart)
  },
  "scaleToZeroSpec": {
    object (ScaleToZeroSpec)
  }
}
```

| Fields                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineSpec`              | `object ( `[`MachineSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.MachineSpec)` )` Required. Immutable. The specification of a single machine being used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `minReplicaCount`          | `integer` Required. Immutable. The minimum number of machine replicas that will be always deployed on. This value must be greater than or equal to 1. If traffic increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `maxReplicaCount`          | `integer` Immutable. The maximum number of replicas that may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale to that many replicas is guaranteed (barring service outages). If traffic increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, will use `min_replica_count` as the default value. The value of this field impacts the charge against Agent Platform CPU and GPU quotas. Specifically, you will be charged for (max_replica_count \* number of cores in the selected machine type) and (max_replica_count \* number of GPUs per replica in the selected machine type).                                                                                                                                                                                                                                                                                                                                                                                 |
| `requiredReplicaCount`     | `integer` Optional. Number of required available replicas for the deployment to succeed. This field is only needed when partial deployment/mutation is desired. If set, the deploy/mutate operation will succeed once available_replica_count reaches required_replica_count, and the rest of the replicas will be retried. If not set, the default required_replica_count will be min_replica_count.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `initialReplicaCount`      | `integer` Immutable. Number of initial replicas being deployed on when scaling the workload up from zero or when creating the workload in case `min_replica_count` = 0. When `min_replica_count` \> 0 (meaning that the scale-to-zero feature is not enabled), `initial_replica_count` should not be set. When `min_replica_count` = 0 (meaning that the scale-to-zero feature is enabled), `initial_replica_count` should be larger than zero, but no greater than `max_replica_count` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `autoscalingMetricSpecs[]` | `object ( `[`AutoscalingMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.AutoscalingMetricSpec)` )` Immutable. The metric specifications that overrides a resource utilization metric (CPU utilization, accelerator's duty cycle, and so on) target value (default to 60 if not set). At most one entry is allowed per metric. If `machine_spec.accelerator_count` is above 0, the autoscaling will be based on both CPU utilization and accelerator's duty cycle metrics and scale up when either metrics exceeds its target value while scale down if both metrics are under their target value. The default target value is 60 for both metrics. If `machine_spec.accelerator_count` is 0, the autoscaling will be based on CPU utilization metric only with default target value 60 if not explicitly set. For example, in the case of Online Prediction, if you want to override target CPU utilization to 80, you should set `autoscaling_metric_specs.metric_name` to `aiplatform.googleapis.com/prediction/online/cpu/utilization` and `autoscaling_metric_specs.target` to `80` . |
| `spot`                     | `boolean` Optional. If true, schedule the deployment workload on [spot VMs](https://cloud.google.com/kubernetes-engine/docs/concepts/spot-vms) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `flexStart`                | `object ( `[`FlexStart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.FlexStart)` )` Optional. Immutable. If set, use DWS resource to schedule the deployment workload. reference: ( <https://cloud.google.com/blog/products/compute/introducing-dynamic-workload-scheduler> )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `scaleToZeroSpec`          | `object ( `[`ScaleToZeroSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.ScaleToZeroSpec)` )` Optional. Specification for scale-to-zero feature.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

### MachineSpec

**JSON representation**

```
{
  "machineType": string,
  "acceleratorType": enum (AcceleratorType),
  "acceleratorCount": integer,
  "gpuPartitionSize": string,
  "tpuTopology": string,
  "multihostGpuNodeCount": integer,
  "reservationAffinity": {
    object (ReservationAffinity)
  },
  "minGpuDriverVersion": string
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineType`           | `string` Immutable. The type of the machine. See the [list of machine types supported for prediction](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#machine-types) See the [list of machine types supported for custom training](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . For [`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.DeployedModel) this field is optional, and the default value is `n1-standard-2` . For `BatchPredictionJob` or as part of `WorkerPoolSpec` this field is required.                                                                                                                                                                                                                                                                                                                                      |
| `acceleratorType`       | `enum ( `[`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.AcceleratorType)` )` Immutable. The type of accelerator(s) that may be attached to the machine as per `accelerator_count` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `acceleratorCount`      | `integer` The number of accelerators to attach to the machine. For [accelerator optimized machine types](https://cloud.google.com/compute/docs/accelerator-optimized-machines) , One may set the accelerator_count from 1 to N for machine with N GPUs. If accelerator_count is less than or equal to N / 2, Agent Platform co-schedules the replicas of the model into the same VM to save cost. For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set accelerator_count to 1 to 8. If accelerator_count is 1, 2, 3, or 4, Agent Platform co-schedules 8, 4, 2, or 2 replicas of the model into the same VM to save cost. When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM. Note that the feature is not compatible with `multihost_gpu_node_count` . When multihost_gpu_node_count is set, the co-scheduling will not be enabled. |
| `gpuPartitionSize`      | `string` Optional. Immutable. The Nvidia GPU partition size. When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu_partition_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances. The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes. If set, the accelerator_count should be set to 1.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `tpuTopology`           | `string` Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu_topology: "2x2x1").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `multihostGpuNodeCount` | `integer` Optional. Immutable. The number of nodes per replica for multihost GPU deployments.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `reservationAffinity`   | `object ( `[`ReservationAffinity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.ReservationAffinity)` )` Optional. Immutable. Configuration controlling how this resource pool consumes reservation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `minGpuDriverVersion`   | `string` Optional. Immutable. The minimum GPU driver version that this machine requires. For example, "535.104.06". If not specified, the default GPU driver version will be used by the underlying infrastructure.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

### ReservationAffinity

**JSON representation**

```
{
  "reservationAffinityType": enum (Type),
  "key": string,
  "values": [
    string
  ]
}
```

| Fields                    |                                                                                                                                                                                                                                      |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservationAffinityType` | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Type)` )` Required. Specifies the reservation affinity type.                                  |
| `key`                     | `string` Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value. |
| `values[]`                | `string` Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.                                                                           |

### AutoscalingMetricSpec

**JSON representation**

```
{
  "metricName": string,
  "target": integer,
  "monitoredResourceLabels": {
    string: string,
    ...
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
<td><code>metricName</code></td>
<td><p><code>string</code></p>
<p>Required. The resource metric name. Supported metrics:</p>
<ul>
<li>For Online Prediction:</li>
<li><code>aiplatform.googleapis.com/prediction/online/accelerator/duty_cycle</code></li>
<li><code>aiplatform.googleapis.com/prediction/online/cpu/utilization</code></li>
<li><code>aiplatform.googleapis.com/prediction/online/request_count</code></li>
<li><code>pubsub.googleapis.com/subscription/num_undelivered_messages</code></li>
<li><code>prometheus.googleapis.com/vertex_dcgm_fi_dev_gpu_util</code></li>
<li><code>prometheus.googleapis.com/vertex_vllm_gpu_cache_usage_perc</code></li>
<li><code>prometheus.googleapis.com/vertex_vllm_num_requests_waiting</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>target</code></td>
<td><p><code>integer</code></p>
<p>The target resource utilization in percentage (1% - 100%) for the given metric; once the real usage deviates from the target by a certain percentage, the machine replicas change. The default value is 60 (representing 60%) if not provided.</p></td>
</tr>
<tr class="odd">
<td><code>monitoredResourceLabels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Optional. The Cloud Monitoring monitored resource labels as key value pairs used for metrics filtering. See Cloud Monitoring Labels <a href="https://cloud.google.com/monitoring/api/v3/metric-model#generic-label-info">https://cloud.google.com/monitoring/api/v3/metric-model#generic-label-info</a></p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
</tbody>
</table>

### MonitoredResourceLabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### FlexStart

**JSON representation**

```
{
  "maxRuntimeDuration": string
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                            |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `maxRuntimeDuration` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` The max duration of the deployment is max_runtime_duration. The deployment will be terminated after the duration. The max_runtime_duration can be set up to 7 days. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |

### Duration

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years                                                                                    |
| `nanos`   | `integer` Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive. |

### ScaleToZeroSpec

**JSON representation**

```
{
  "minScaleupPeriod": string,
  "idleScaledownPeriod": string
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `minScaleupPeriod`    | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. Minimum duration that a deployment will be scaled up before traffic is evaluated for potential scale-down. \[MinValue=300\] (5 minutes) \[MaxValue=28800\] (8 hours) A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
| `idleScaledownPeriod` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. Duration of no traffic before scaling to zero. \[MinValue=300\] (5 minutes) \[MaxValue=28800\] (8 hours) A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .                                                             |

### AutomaticResources

**JSON representation**

```
{
  "minReplicaCount": integer,
  "maxReplicaCount": integer
}
```

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `minReplicaCount` | `integer` Immutable. The minimum number of replicas that will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas up to `max_replica_count` , and as traffic decreases, some of these extra replicas may be freed. If the requested value is too large, the deployment will error.                                                                                                                                                                                                                                                          |
| `maxReplicaCount` | `integer` Immutable. The maximum number of replicas that may be deployed on when the traffic against it increases. If the requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale to that many replicas is guaranteed (barring service outages). If traffic increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, a no upper bound for scaling under heavy traffic will be assume, though Agent Platform may be unable to scale beyond certain replica number. |

### FullFineTunedResources

**JSON representation**

```
{
  "deploymentType": enum (DeploymentType),
  "modelInferenceUnitCount": integer
}
```

| Fields                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `deploymentType`          | `enum ( `[`DeploymentType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.DeploymentType)` )` Required. The kind of deployment.                                                                                                                                                                                                                                                                                                    |
| `modelInferenceUnitCount` | `integer` Optional. The number of model inference units to use for this deployment. This can only be specified for DEPLOYMENT_TYPE_PROD. The following table lists the number of model inference units for different model types: \* Gemini 2.5 Flash \* Foundation FMIU: 25 \* Expansion FMIU: 4 \* Gemini 2.5 Pro \* Foundation FMIU: 32 \* Expansion FMIU: 16 \* Veo 3.0 (undistilled) \* Foundation FMIU: 63 \* Expansion FMIU: 7 \* Veo 3.0 (distilled) \* Foundation FMIU: 30 \* Expansion FMIU: 10 |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### ExplanationSpec

**JSON representation**

```
{
  "parameters": {
    object (ExplanationParameters)
  },
  "metadata": {
    object (ExplanationMetadata)
  }
}
```

| Fields       |                                                                                                                                                                                                                                                                 |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parameters` | `object ( `[`ExplanationParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.ExplanationParameters)` )` Required. Parameters that configure explaining of the Model's predictions. |
| `metadata`   | `object ( `[`ExplanationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.ExplanationMetadata)` )` Optional. Metadata describing the Model's input and output for explanation.    |

### ExplanationParameters

**JSON representation**

```
{
  "topK": integer,
  "outputIndices": array,

  // Union field method can be only one of the following:
  "sampledShapleyAttribution": {
    object (SampledShapleyAttribution)
  },
  "integratedGradientsAttribution": {
    object (IntegratedGradientsAttribution)
  },
  "xraiAttribution": {
    object (XraiAttribution)
  },
  "examples": {
    object (Examples)
  }
  // End of list of possible types for union field method.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `topK`                                                            | `integer` If populated, returns attributions for top K indices of outputs (defaults to 1). Only applies to Models that predicts more than one outputs (e,g, multi-class Models). When set to -1, returns explanations for all outputs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `outputIndices`                                                   | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` If populated, only returns attributions that have `output_index` contained in output_indices. It must be an ndarray of integers, with the same shape of the output it's explaining. If not populated, returns attributions for `top_k` indices of outputs. If neither top_k nor output_indices is populated, returns the argmax index of the outputs. Only applicable to Models that predict multiple outputs (e,g, multi-class Models that predict multiple classes).                                                                                                                             |
| Union field `method` . `method` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `sampledShapleyAttribution`                                       | `object ( `[`SampledShapleyAttribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.SampledShapleyAttribution)` )` An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features. Refer to this paper for model details: <https://arxiv.org/abs/1306.4265> .                                                                                                                                                                                                           |
| `integratedGradientsAttribution`                                  | `object ( `[`IntegratedGradientsAttribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.IntegratedGradientsAttribution)` )` An attribution method that computes Aumann-Shapley values taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1703.01365>                                                                                                                                                                                                                                                                                                 |
| `xraiAttribution`                                                 | `object ( `[`XraiAttribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.XraiAttribution)` )` An attribution method that redistributes Integrated Gradients attribution to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1906.02825> XRAI currently performs better on natural images, like a picture of a house or an animal. If the images are taken in artificial environments, like a lab or manufacturing line, or from diagnostic equipment, like x-rays or quality-control cameras, use Integrated Gradients instead. |
| `examples`                                                        | `object ( `[`Examples`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Examples)` )` Example-based explanations that returns the nearest neighbors from the provided dataset.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

### SampledShapleyAttribution

**JSON representation**

```
{
  "pathCount": integer
}
```

| Fields      |                                                                                                                                                               |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pathCount` | `integer` Required. The number of feature permutations to consider when approximating the Shapley values. Valid range of its value is \[1, 50\], inclusively. |

### IntegratedGradientsAttribution

**JSON representation**

```
{
  "stepCount": integer,
  "smoothGradConfig": {
    object (SmoothGradConfig)
  },
  "blurBaselineConfig": {
    object (BlurBaselineConfig)
  }
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stepCount`          | `integer` Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is within the desired error range. Valid range of its value is \[1, 100\], inclusively.                                                                                                                                                                                                                                    |
| `smoothGradConfig`   | `object ( `[`SmoothGradConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.SmoothGradConfig)` )` Config for SmoothGrad approximation of gradients. When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf> |
| `blurBaselineConfig` | `object ( `[`BlurBaselineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.BlurBaselineConfig)` )` Config for IG with blur baseline. When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>                                |

### SmoothGradConfig

**JSON representation**

```
{
  "noisySampleCount": integer,

  // Union field GradientNoiseSigma can be only one of the following:
  "noiseSigma": number,
  "featureNoiseSigma": {
    object (FeatureNoiseSigma)
  }
  // End of list of possible types for union field GradientNoiseSigma.
}
```

| Fields                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `noisySampleCount`                                                                                                                                                                                                                         | `integer` The number of gradient samples to use for approximation. The higher this number, the more accurate the gradient is, but the runtime complexity increases by this factor as well. Valid range of its value is \[1, 50\]. Defaults to 3.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `GradientNoiseSigma` . Represents the standard deviation of the gaussian kernel that will be used to add noise to the interpolated inputs prior to computing gradients. `GradientNoiseSigma` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `noiseSigma`                                                                                                                                                                                                                               | `number` This is a single float value and will be used to add noise to all the features. Use this field when all features are normalized to have the same distribution: scale to range \[0, 1\], \[-1, 1\] or z-scoring, where features are normalized to have 0-mean and 1-variance. Learn more about [normalization](https://developers.google.com/machine-learning/data-prep/transform/normalization) . For best results the recommended value is about 10% - 20% of the standard deviation of the input feature. Refer to section 3.2 of the SmoothGrad paper: <https://arxiv.org/pdf/1706.03825.pdf> . Defaults to 0.1. If the distribution is different per feature, set `feature_noise_sigma` instead for each feature. |
| `featureNoiseSigma`                                                                                                                                                                                                                        | `object ( `[`FeatureNoiseSigma`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.FeatureNoiseSigma)` )` This is similar to `noise_sigma` , but provides additional flexibility. A separate noise sigma can be provided for each feature, which is useful if their distributions are different. No noise is added to features that are not set. If this field is unset, `noise_sigma` will be used for all features.                                                                                                                                                                                                                                       |

### FeatureNoiseSigma

**JSON representation**

```
{
  "noiseSigma": [
    {
      object (NoiseSigmaForFeature)
    }
  ]
}
```

| Fields         |                                                                                                                                                                                                                                                             |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `noiseSigma[]` | `object ( `[`NoiseSigmaForFeature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.NoiseSigmaForFeature)` )` Noise sigma per feature. No noise is added to features that are not set. |

### NoiseSigmaForFeature

**JSON representation**

```
{
  "name": string,
  "sigma": number
}
```

| Fields  |                                                                                                                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`  | `string` The name of the input feature for which noise sigma is provided. The features are defined in `explanation metadata inputs` .                                                                                                               |
| `sigma` | `number` This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to `noise_sigma` but represents the noise added to the current feature. Defaults to 0.1. |

### BlurBaselineConfig

**JSON representation**

```
{
  "maxBlurSigma": number
}
```

| Fields         |                                                                                                                                                                                                                                             |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `maxBlurSigma` | `number` The standard deviation of the blur kernel for the blurred baseline. The same blurring parameter is used for both the height and the width dimension. If not set, the method defaults to the zero (i.e. black for images) baseline. |

### XraiAttribution

**JSON representation**

```
{
  "stepCount": integer,
  "smoothGradConfig": {
    object (SmoothGradConfig)
  },
  "blurBaselineConfig": {
    object (BlurBaselineConfig)
  }
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stepCount`          | `integer` Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is met within the desired error range. Valid range of its value is \[1, 100\], inclusively.                                                                                                                                                                                                                                |
| `smoothGradConfig`   | `object ( `[`SmoothGradConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.SmoothGradConfig)` )` Config for SmoothGrad approximation of gradients. When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf> |
| `blurBaselineConfig` | `object ( `[`BlurBaselineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.BlurBaselineConfig)` )` Config for XRAI with blur baseline. When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>                              |

### Examples

**JSON representation**

```
{
  "gcsSource": {
    object (GcsSource)
  },
  "neighborCount": integer,

  // Union field source can be only one of the following:
  "exampleGcsSource": {
    object (ExampleGcsSource)
  }
  // End of list of possible types for union field source.

  // Union field config can be only one of the following:
  "nearestNeighborSearchConfig": value,
  "presets": {
    object (Presets)
  }
  // End of list of possible types for union field config.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                                                                                                       |
|-------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `gcsSource`                                                       | `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.GcsSource)` )` The Cloud Storage locations that contain the instances to be indexed for approximate nearest neighbor search.                                                                                            |
| `neighborCount`                                                   | `integer` The number of neighbors to return when querying for examples.                                                                                                                                                                                                                                                                                               |
| Union field `source` . `source` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                       |
| `exampleGcsSource`                                                | `object ( `[`ExampleGcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.ExampleGcsSource)` )` The Cloud Storage input instances.                                                                                                                                                         |
| Union field `config` . `config` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                       |
| `nearestNeighborSearchConfig`                                     | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` The full configuration for the generated index, the semantics are the same as `metadata` and should match [NearestNeighborSearchConfig](https://cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations-example-based#nearest-neighbor-search-config) . |
| `presets`                                                         | `object ( `[`Presets`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Presets)` )` Simplified preset configuration, which automatically sets configuration values based on the desired query speed-precision trade-off and modality.                                                            |

### ExampleGcsSource

**JSON representation**

```
{
  "dataFormat": enum (DataFormat),
  "gcsSource": {
    object (GcsSource)
  }
}
```

| Fields       |                                                                                                                                                                                                                                                                                             |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataFormat` | `enum ( `[`DataFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.DataFormat)` )` The format in which instances are given, if not specified, assume it's JSONL format. Currently only JSONL format is supported. |
| `gcsSource`  | `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.GcsSource)` )` The Cloud Storage location for the input instances.                                                                            |

### GcsSource

**JSON representation**

```
{
  "uris": [
    string
  ]
}
```

| Fields   |                                                                                                                                                                                         |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uris[]` | `string` Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see <https://cloud.google.com/storage/docs/wildcards> . |

### Value

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean,
  "structValue": {
    object
  },
  "listValue": array
  // End of list of possible types for union field kind.
}
```

| Fields                                                                           |                                                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . The kind of value. `kind` can be only one of the following: |                                                                                                                                                                                                                                                |
| `nullValue`                                                                      | `null` Represents a JSON `null` .                                                                                                                                                                                                              |
| `numberValue`                                                                    | `number` Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type. |
| `stringValue`                                                                    | `string` Represents a JSON string.                                                                                                                                                                                                             |
| `boolValue`                                                                      | `boolean` Represents a JSON boolean ( `true` or `false` literal in JSON).                                                                                                                                                                      |
| `structValue`                                                                    | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Represents a JSON object.                                                                                                                     |
| `listValue`                                                                      | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` Represents a JSON array.                                                                                                                |

### Struct

**JSON representation**

```
{
  "fields": {
    string: value,
    ...
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                          |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map (key: string, value: value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format))` Unordered map of dynamically typed values. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### FieldsEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### ListValue

**JSON representation**

```
{
  "values": [
    value
  ]
}
```

| Fields     |                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Repeated field of dynamically typed values. |

### Presets

**JSON representation**

```
{
  "modality": enum (Modality),

  // Union field _query can be only one of the following:
  "query": enum (Query)
  // End of list of possible types for union field _query.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                              |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `modality`                                                        | `enum ( `[`Modality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Modality)` )` The modality of the uploaded model, which automatically configures the distance measurement and feature normalization for the underlying example index and queries. If your model does not precisely fit one of these types, it is okay to choose the closest type. |
| Union field `_query` . `_query` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `query`                                                           | `enum ( `[`Query`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Query)` )` Preset option controlling parameters for speed-precision trade-off when querying for examples. If omitted, defaults to `PRECISE` .                                                                                                                                        |

### ExplanationMetadata

**JSON representation**

```
{
  "inputs": {
    string: {
      object (InputMetadata)
    },
    ...
  },
  "outputs": {
    string: {
      object (OutputMetadata)
    },
    ...
  },
  "featureAttributionsSchemaUri": string,
  "latentSpaceSource": string
}
```

| Fields                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `inputs`                       | `map (key: string, value: object ( `[`InputMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.InputMetadata)` ))` Required. Map from feature names to feature input metadata. Keys are the name of the features. Values are the specification of the feature. An empty InputMetadata is valid. It describes a text feature which has the name specified as the key in `ExplanationMetadata.inputs` . The baseline of the empty feature is chosen by Agent Platform. For Agent Platform-provided Tensorflow images, the key can be any friendly name of the feature. Once specified, `featureAttributions` are keyed by this key (if not grouped with another feature). For custom images, the key must match with the key in `instance` . An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `outputs`                      | `map (key: string, value: object ( `[`OutputMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.OutputMetadata)` ))` Required. Map from output names to output metadata. For Agent Platform-provided Tensorflow images, keys can be any user defined string that consists of any UTF-8 characters. For custom images, keys are the name of the output field in the prediction to be explained. Currently only one key is allowed. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                                                                                                          |
| `featureAttributionsSchemaUri` | `string` Points to a YAML file stored on Google Cloud Storage describing the format of the `feature attributions` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML tabular Models always have this field populated by Agent Platform. Note: The URI given on output may be different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.                                                                                                                                                                                                                                                                                                                                                                                                       |
| `latentSpaceSource`            | `string` Name of the source to generate embeddings for example based explanations.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

### InputsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (InputMetadata)
  }
}
```

| Fields  |                                                                                                                                                                      |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                             |
| `value` | `object ( `[`InputMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.InputMetadata)` )` |

### InputMetadata

**JSON representation**

```
{
  "inputBaselines": [
    value
  ],
  "inputTensorName": string,
  "encoding": enum (Encoding),
  "modality": string,
  "featureValueDomain": {
    object (FeatureValueDomain)
  },
  "indicesTensorName": string,
  "denseShapeTensorName": string,
  "indexFeatureMapping": [
    string
  ],
  "encodedTensorName": string,
  "encodedBaselines": [
    value
  ],
  "visualization": {
    object (Visualization)
  },
  "groupName": string
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `inputBaselines[]`      | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Baseline inputs for this feature. If no baseline is specified, Agent Platform chooses the baseline for this feature. If multiple baselines are specified, Agent Platform returns the average attributions across them in `Attribution.feature_attributions` . For Agent Platform-provided Tensorflow images (both 1.x and 2.x), the shape of each baseline must match the shape of the input tensor. If a scalar is provided, we broadcast to the same shape as the input tensor. For custom images, the element of the baselines must be in the same format as the feature's input in the `instance` \[\]. The schema of any single instance may be specified via Endpoint's DeployedModels' `Model's` `PredictSchemata's` `instance_schema_uri` . |
| `inputTensorName`       | `string` Name of the input tensor for this feature. Required and is only applicable to Agent Platform-provided images for Tensorflow.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `encoding`              | `enum ( `[`Encoding`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Encoding)` )` Defines how the feature is encoded into the input tensor. Defaults to IDENTITY.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `modality`              | `string` Modality of the feature. Valid values are: numeric, image. Defaults to numeric.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `featureValueDomain`    | `object ( `[`FeatureValueDomain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.FeatureValueDomain)` )` The domain details of the input feature value. Like min/max, original mean or standard deviation if normalized.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `indicesTensorName`     | `string` Specifies the index of the values of the input tensor. Required when the input tensor is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `denseShapeTensorName`  | `string` Specifies the shape of the values of the input if the input is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `indexFeatureMapping[]` | `string` A list of feature names for each index in the input tensor. Required when the input `InputMetadata.encoding` is BAG_OF_FEATURES, BAG_OF_FEATURES_SPARSE, INDICATOR.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `encodedTensorName`     | `string` Encoded tensor is a transformation of the input tensor. Must be provided if choosing `Integrated Gradients attribution` or `XRAI attribution` and the input tensor is not differentiable. An encoded tensor is generated if the input tensor is encoded by a lookup table.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `encodedBaselines[]`    | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` A list of baselines for the encoded tensor. The shape of each baseline should match the shape of the encoded tensor. If a scalar is provided, Agent Platform broadcasts to the same shape as the encoded tensor.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `visualization`         | `object ( `[`Visualization`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Visualization)` )` Visualization configurations for image explanation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `groupName`             | `string` Name of the group that the input belongs to. Features with the same group name will be treated as one feature when computing attributions. Features grouped together can have different shapes in value. If provided, there will be one single attribution generated in `Attribution.feature_attributions` , keyed by the group name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

### FeatureValueDomain

**JSON representation**

```
{
  "minValue": number,
  "maxValue": number,
  "originalMean": number,
  "originalStddev": number
}
```

| Fields           |                                                                                                                                                                               |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `minValue`       | `number` The minimum permissible value for this feature.                                                                                                                      |
| `maxValue`       | `number` The maximum permissible value for this feature.                                                                                                                      |
| `originalMean`   | `number` If this input feature has been normalized to a mean value of 0, the original_mean specifies the mean value of the domain prior to normalization.                     |
| `originalStddev` | `number` If this input feature has been normalized to a standard deviation of 1.0, the original_stddev specifies the standard deviation of the domain prior to normalization. |

### Visualization

**JSON representation**

```
{
  "type": enum (Type),
  "polarity": enum (Polarity),
  "colorMap": enum (ColorMap),
  "clipPercentUpperbound": number,
  "clipPercentLowerbound": number,
  "overlayType": enum (OverlayType)
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`                  | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Type_1)` )` Type of the image visualization. Only applicable to `Integrated Gradients attribution` . OUTLINES shows regions of attribution, while PIXELS shows per-pixel attribution. Defaults to OUTLINES.                                                                                                                                 |
| `polarity`              | `enum ( `[`Polarity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.Polarity)` )` Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.                                                                                                                                                                                                                     |
| `colorMap`              | `enum ( `[`ColorMap`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.ColorMap)` )` The color scheme used for the highlighted areas. Defaults to PINK_GREEN for `Integrated Gradients attribution` , which shows positive attributions in green and negative in pink. Defaults to VIRIDIS for `XRAI attribution` , which highlights the most influential regions in yellow and the least influential in blue. |
| `clipPercentUpperbound` | `number` Excludes attributions above the specified percentile from the highlighted areas. Using the clip_percent_upperbound and clip_percent_lowerbound together can be useful for filtering out noise and making it easier to see areas of strong attribution. Defaults to 99.9.                                                                                                                                                                                                  |
| `clipPercentLowerbound` | `number` Excludes attributions below the specified percentile, from the highlighted areas. Defaults to 62.                                                                                                                                                                                                                                                                                                                                                                         |
| `overlayType`           | `enum ( `[`OverlayType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.OverlayType)` )` How the original image is displayed in the visualization. Adjusting the overlay can help increase visual clarity if the original image makes it difficult to view the visualization. Defaults to NONE.                                                                                                              |

### OutputsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (OutputMetadata)
  }
}
```

| Fields  |                                                                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                               |
| `value` | `object ( `[`OutputMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.OutputMetadata)` )` |

### OutputMetadata

**JSON representation**

```
{
  "outputTensorName": string,

  // Union field display_name_mapping can be only one of the following:
  "indexDisplayNameMapping": value,
  "displayNameMappingKey": string
  // End of list of possible types for union field display_name_mapping.
}
```

| Fields                                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `outputTensorName`                                                                                                                                                                                                                                                                  | `string` Name of the output tensor. Required and is only applicable to Agent Platform provided images for Tensorflow.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Union field `display_name_mapping` . Defines how to map `Attribution.output_index` to `Attribution.output_display_name` . If neither of the fields are specified, `Attribution.output_display_name` will not be populated. `display_name_mapping` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `indexDisplayNameMapping`                                                                                                                                                                                                                                                           | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Static mapping between the index and display name. Use this if the outputs are a deterministic n-dimensional array, e.g. a list of scores of all the classes in a pre-defined order for a multi-classification Model. It's not feasible if the outputs are non-deterministic, e.g. the Model produces top-k classes or sort the outputs by their values. The shape of the value must be an n-dimensional array of strings. The number of dimensions must match that of the outputs to be explained. The `Attribution.output_display_name` is populated by locating in the mapping with `Attribution.output_index` . |
| `displayNameMappingKey`                                                                                                                                                                                                                                                             | `string` Specify a field name in the prediction to look for the display name. Use this if the prediction contains the display names for the outputs. The display names in the prediction must have the same shape of the outputs, so that it can be located by `Attribution.output_index` for a specific output.                                                                                                                                                                                                                                                                                                                                                                                                  |

### PrivateEndpoints

**JSON representation**

```
{
  "predictHttpUri": string,
  "explainHttpUri": string,
  "healthHttpUri": string,
  "serviceAttachment": string
}
```

| Fields              |                                                                                                                     |
|---------------------|---------------------------------------------------------------------------------------------------------------------|
| `predictHttpUri`    | `string` Output only. Http(s) path to send prediction requests.                                                     |
| `explainHttpUri`    | `string` Output only. Http(s) path to send explain requests.                                                        |
| `healthHttpUri`     | `string` Output only. Http(s) path to send health check requests.                                                   |
| `serviceAttachment` | `string` Output only. The name of the service attachment resource. Populated if private service connect is enabled. |

### FasterDeploymentConfig

**JSON representation**

```
{
  "fastTryoutEnabled": boolean
}
```

| Fields              |                                                                        |
|---------------------|------------------------------------------------------------------------|
| `fastTryoutEnabled` | `boolean` If true, enable fast tryout feature for this deployed model. |

### RolloutOptions

**JSON representation**

```
{
  "previousDeployedModel": string,
  "revisionNumber": integer,

  // Union field max_unavailable can be only one of the following:
  "maxUnavailableReplicas": integer,
  "maxUnavailablePercentage": integer
  // End of list of possible types for union field max_unavailable.

  // Union field max_surge can be only one of the following:
  "maxSurgeReplicas": integer,
  "maxSurgePercentage": integer
  // End of list of possible types for union field max_surge.
}
```

| Fields                                                                                                                                                                      |                                                                                                                                                                                                                              |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `previousDeployedModel`                                                                                                                                                     | `string` ID of the DeployedModel that this deployment should replace.                                                                                                                                                        |
| `revisionNumber`                                                                                                                                                            | `integer` Output only. Read-only. Revision number determines the relative priority of DeployedModels in the same rollout. The DeployedModel with the largest revision number specifies the intended state of the deployment. |
| Union field `max_unavailable` . Configures how many replicas are allowed to be unavailable during a rolling deployment. `max_unavailable` can be only one of the following: |                                                                                                                                                                                                                              |
| `maxUnavailableReplicas`                                                                                                                                                    | `integer` Absolute count of replicas allowed to be unavailable.                                                                                                                                                              |
| `maxUnavailablePercentage`                                                                                                                                                  | `integer` Percentage of replicas allowed to be unavailable. For autoscaling deployments, this refers to the target replica count.                                                                                            |
| Union field `max_surge` . Configures how many additional replicas can be provisioned during a rolling deployment. `max_surge` can be only one of the following:             |                                                                                                                                                                                                                              |
| `maxSurgeReplicas`                                                                                                                                                          | `integer` Absolute count of allowed additional replicas.                                                                                                                                                                     |
| `maxSurgePercentage`                                                                                                                                                        | `integer` Percentage of allowed additional replicas. For autoscaling deployments, this refers to the target replica count.                                                                                                   |

### Status

**JSON representation**

```
{
  "message": string,
  "lastUpdateTime": string,
  "availableReplicaCount": integer
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `message`               | `string` Output only. The latest deployed model's status message (if any).                                                                                                                                                                                                                                                                                                                                                        |
| `lastUpdateTime`        | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The time at which the status was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `availableReplicaCount` | `integer` Output only. The number of available replicas of the deployed model.                                                                                                                                                                                                                                                                                                                                                    |

### SystemLabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### SpeculativeDecodingSpec

**JSON representation**

```
{
  "speculativeTokenCount": integer,

  // Union field speculation can be only one of the following:
  "draftModelSpeculation": {
    object (DraftModelSpeculation)
  },
  "ngramSpeculation": {
    object (NgramSpeculation)
  }
  // End of list of possible types for union field speculation.
}
```

| Fields                                                                                                             |                                                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `speculativeTokenCount`                                                                                            | `integer` The number of speculative tokens to generate at each step.                                                                                                                                          |
| Union field `speculation` . The type of speculation method to use. `speculation` can be only one of the following: |                                                                                                                                                                                                               |
| `draftModelSpeculation`                                                                                            | `object ( `[`DraftModelSpeculation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.DraftModelSpeculation)` )` draft model speculation. |
| `ngramSpeculation`                                                                                                 | `object ( `[`NgramSpeculation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.NgramSpeculation)` )` N-Gram speculation.                |

### DraftModelSpeculation

**JSON representation**

```
{
  "draftModel": string
}
```

| Fields       |                                                          |
|--------------|----------------------------------------------------------|
| `draftModel` | `string` Required. The resource name of the draft model. |

### NgramSpeculation

**JSON representation**

```
{
  "ngramSize": integer
}
```

| Fields      |                                                                                                                                                                                            |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ngramSize` | `integer` The number of last N input tokens used as ngram to search/match against the previous prompt sequence. This is equal to the N in N-Gram. The default value is 3 if not specified. |

### TrafficSplitEntry

**JSON representation**

```
{
  "key": string,
  "value": integer
}
```

| Fields  |           |
|---------|-----------|
| `key`   | `string`  |
| `value` | `integer` |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### EncryptionSpec

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Required. Resource name of the Cloud KMS key used to protect the resource. The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

### PrivateServiceConnectConfig

**JSON representation**

```
{
  "enablePrivateServiceConnect": boolean,
  "projectAllowlist": [
    string
  ],
  "pscAutomationConfigs": [
    {
      object (PSCAutomationConfig)
    }
  ],
  "enableSecurePrivateServiceConnect": boolean,
  "serviceAttachment": string
}
```

| Fields                              |                                                                                                                                                                                                                                                                                                                            |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enablePrivateServiceConnect`       | `boolean` Required. If true, expose the IndexEndpoint via private service connect.                                                                                                                                                                                                                                         |
| `projectAllowlist[]`                | `string` A list of Projects from which the forwarding rule will target the service attachment.                                                                                                                                                                                                                             |
| `pscAutomationConfigs[]`            | `object ( `[`PSCAutomationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.PSCAutomationConfig)` )` Optional. List of projects and networks where the PSC endpoints will be created. This field is used by Online Inference(Prediction) only. |
| `enableSecurePrivateServiceConnect` | `boolean` Optional. If set to true, enable secure private service connect with IAM authorization. Otherwise, private service connect will be done without authorization. Note latency will be slightly increased if authorization is enabled.                                                                              |
| `serviceAttachment`                 | `string` Output only. The name of the generated service attachment resource. This is only populated if the endpoint is deployed with PrivateServiceConnect.                                                                                                                                                                |

### PSCAutomationConfig

**JSON representation**

```
{
  "projectId": string,
  "network": string,
  "ipAddress": string,
  "forwardingRule": string,
  "state": enum (PSCAutomationState),
  "errorMessage": string
}
```

| Fields           |                                                                                                                                                                                                                                                                                    |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId`      | `string` Required. Project id used to create forwarding rule.                                                                                                                                                                                                                      |
| `network`        | `string` Required. The full name of the Google Compute Engine [network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks) . [Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/get) : `projects/{project}/global/networks/{network}` . |
| `ipAddress`      | `string` Output only. IP address rule created by the PSC service automation.                                                                                                                                                                                                       |
| `forwardingRule` | `string` Output only. Forwarding rule created by the PSC service automation.                                                                                                                                                                                                       |
| `state`          | `enum ( `[`PSCAutomationState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.PSCAutomationState)` )` Output only. The state of the PSC service automation.                                                 |
| `errorMessage`   | `string` Output only. Error message if the PSC service automation failed.                                                                                                                                                                                                          |

### PredictRequestResponseLoggingConfig

**JSON representation**

```
{
  "enabled": boolean,
  "samplingRate": number,
  "errorSamplingRate": number,
  "bigqueryDestination": {
    object (BigQueryDestination)
  },
  "requestResponseLoggingSchemaVersion": string,
  "enableOtelLogging": boolean
}
```

| Fields                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enabled`                             | `boolean` If logging is enabled or not.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `samplingRate`                        | `number` Percentage of requests to be logged, expressed as a fraction in range(0,1\].                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `errorSamplingRate`                   | `number` Optional. Percentage of failed requests to be logged, expressed as a fraction in range \[0,1\]. Only non-transient errors will be logged (currently `500/Internal` errors).                                                                                                                                                                                                                                                                                                                                                  |
| `bigqueryDestination`                 | `object ( `[`BigQueryDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.BigQueryDestination)` )` BigQuery table for logging. If only given a project, a new dataset will be created with name `logging_<endpoint-display-name>_<endpoint-id>` where will be made BigQuery-dataset-name compatible (e.g. most special characters will become underscores). If no table name is given, a new table will be created with name `request_response_logging` |
| `requestResponseLoggingSchemaVersion` | `string` Output only. The schema version used in creating the BigQuery table for the request response logging. The versions are "v1" and "v2". The current default version is "v1".                                                                                                                                                                                                                                                                                                                                                   |
| `enableOtelLogging`                   | `boolean` This field is used for large models. If true, in addition to the original large model logs, logs will be converted in OTel schema format, and saved in otel_log column. Default value is false.                                                                                                                                                                                                                                                                                                                             |

### BigQueryDestination

**JSON representation**

```
{
  "outputUri": string
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
<td><code>outputUri</code></td>
<td><p><code>string</code></p>
<p>Required. BigQuery URI to a project or table, up to 2000 characters long.</p>
<p>When only the project is specified, the Dataset and Table is created. When the full table reference is specified, the Dataset must exist and table must not exist.</p>
<p>Accepted forms:</p>
<ul>
<li>BigQuery path. For example: <code>bq://projectId</code> or <code>bq://projectId.bqDatasetId</code> or <code>bq://projectId.bqDatasetId.bqTableId</code> .</li>
</ul></td>
</tr>
</tbody>
</table>

### ClientConnectionConfig

**JSON representation**

```
{
  "inferenceTimeout": string
}
```

| Fields             |                                                                                                                                                                                                                                                        |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `inferenceTimeout` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Customizable online prediction request timeout. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |

### GenAiAdvancedFeaturesConfig

**JSON representation**

```
{
  "ragConfig": {
    object (RagConfig)
  }
}
```

| Fields      |                                                                                                                                                                                                                        |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ragConfig` | `object ( `[`RagConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.RagConfig)` )` Configuration for Retrieval Augmented Generation feature. |

### RagConfig

**JSON representation**

```
{
  "enableRag": boolean
}
```

| Fields      |                                                                                                                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableRag` | `boolean` If true, enable Retrieval Augmented Generation in ChatCompletion request. Once enabled, the endpoint will be identified as GenAI endpoint and Arthedain router will be used. |

### PublisherModelConfig

**JSON representation**

```
{
  "loggingConfig": {
    object (PredictRequestResponseLoggingConfig)
  },
  "dataSharingEnabledProvider": enum (ModelProvider)
}
```

| Fields                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `loggingConfig`              | `object ( `[`PredictRequestResponseLoggingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.PredictRequestResponseLoggingConfig)` )` Optional. The prediction request/response logging config.                                                                                                                                                                                |
| `dataSharingEnabledProvider` | `enum ( `[`ModelProvider`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.ModelProvider)` )` Optional. The model provider (publisher) for which the customer has enabled data sharing. For publisher models that are configured to require data sharing, a prediction request is only allowed when the model's publisher matches this provider. Otherwise, the request is rejected. |

### AcceleratorType

Represents a hardware accelerator type.

| Enums                          |                                                                                                                        |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------|
| `ACCELERATOR_TYPE_UNSPECIFIED` | Unspecified accelerator type, which means no accelerator.                                                              |
| `NVIDIA_TESLA_K80`             | Deprecated: Nvidia Tesla K80 GPU has reached end of support, see <https://cloud.google.com/compute/docs/eol/k80-eol> . |
| `NVIDIA_TESLA_P100`            | Nvidia Tesla P100 GPU.                                                                                                 |
| `NVIDIA_TESLA_V100`            | Nvidia Tesla V100 GPU.                                                                                                 |
| `NVIDIA_TESLA_P4`              | Nvidia Tesla P4 GPU.                                                                                                   |
| `NVIDIA_TESLA_T4`              | Nvidia Tesla T4 GPU.                                                                                                   |
| `NVIDIA_TESLA_A100`            | Nvidia Tesla A100 GPU.                                                                                                 |
| `NVIDIA_A100_80GB`             | Nvidia A100 80GB GPU.                                                                                                  |
| `NVIDIA_L4`                    | Nvidia L4 GPU.                                                                                                         |
| `NVIDIA_H100_80GB`             | Nvidia H100 80Gb GPU.                                                                                                  |
| `NVIDIA_H100_MEGA_80GB`        | Nvidia H100 Mega 80Gb GPU.                                                                                             |
| `NVIDIA_H200_141GB`            | Nvidia H200 141Gb GPU.                                                                                                 |
| `NVIDIA_B200`                  | Nvidia B200 GPU.                                                                                                       |
| `NVIDIA_GB200`                 | Nvidia GB200 GPU.                                                                                                      |
| `NVIDIA_RTX_PRO_6000`          | Nvidia RTX Pro 6000 GPU.                                                                                               |
| `TPU_V2`                       | TPU v2.                                                                                                                |
| `TPU_V3`                       | TPU v3.                                                                                                                |
| `TPU_V4_POD`                   | TPU v4.                                                                                                                |
| `TPU_V5_LITEPOD`               | TPU v5.                                                                                                                |

### Type

Identifies a type of reservation affinity.

| Enums                  |                                                                                                                         |
|------------------------|-------------------------------------------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED`     | Default value. This should not be used.                                                                                 |
| `NO_RESERVATION`       | Do not consume from any reserved capacity, only use on-demand.                                                          |
| `ANY_RESERVATION`      | Consume any reservation available, falling back to on-demand.                                                           |
| `SPECIFIC_RESERVATION` | Consume from a specific reservation. When chosen, the reservation must be identified via the `key` and `values` fields. |

### DeploymentType

The type of deployment.

| Enums                         |                              |
|-------------------------------|------------------------------|
| `DEPLOYMENT_TYPE_UNSPECIFIED` | Unspecified deployment type. |
| `DEPLOYMENT_TYPE_EVAL`        | Eval deployment type.        |
| `DEPLOYMENT_TYPE_PROD`        | Prod deployment type.        |

### DataFormat

The format of the input example instances.

| Enums                     |                                      |
|---------------------------|--------------------------------------|
| `DATA_FORMAT_UNSPECIFIED` | Format unspecified, used when unset. |
| `JSONL`                   | Examples are stored in JSONL files.  |

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### Query

Preset option controlling parameters for query speed-precision trade-off

| Enums     |                                                                |
|-----------|----------------------------------------------------------------|
| `PRECISE` | More precise neighbors as a trade-off against slower response. |
| `FAST`    | Faster response as a trade-off against less precise neighbors. |

### Modality

Preset option controlling parameters for different modalities

| Enums                  |                                                                   |
|------------------------|-------------------------------------------------------------------|
| `MODALITY_UNSPECIFIED` | Should not be set. Added as a recommended best practice for enums |
| `IMAGE`                | IMAGE modality                                                    |
| `TEXT`                 | TEXT modality                                                     |
| `TABULAR`              | TABULAR modality                                                  |

### Encoding

Defines how a feature is encoded. Defaults to IDENTITY.

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
<td><code>ENCODING_UNSPECIFIED</code></td>
<td>Default value. This is the same as IDENTITY.</td>
</tr>
<tr class="even">
<td><code>IDENTITY</code></td>
<td>The tensor represents one feature.</td>
</tr>
<tr class="odd">
<td><code>BAG_OF_FEATURES</code></td>
<td><p>The tensor represents a bag of features where each index maps to a feature. <code>InputMetadata.index_feature_mapping</code> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [27, 6.0, 150]
index_feature_mapping = [&quot;age&quot;, &quot;height&quot;, &quot;weight&quot;]</code></pre></td>
</tr>
<tr class="even">
<td><code>BAG_OF_FEATURES_SPARSE</code></td>
<td><p>The tensor represents a bag of features where each index maps to a feature. Zero values in the tensor indicates feature being non-existent. <code>InputMetadata.index_feature_mapping</code> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [2, 0, 5, 0, 1]
index_feature_mapping = [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;, &quot;e&quot;]</code></pre></td>
</tr>
<tr class="odd">
<td><code>INDICATOR</code></td>
<td><p>The tensor is a list of binaries representing whether a feature exists or not (1 indicates existence). <code>InputMetadata.index_feature_mapping</code> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [1, 0, 1, 0, 1]
index_feature_mapping = [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;, &quot;e&quot;]</code></pre></td>
</tr>
<tr class="even">
<td><code>COMBINED_EMBEDDING</code></td>
<td><p>The tensor is encoded into a 1-dimensional array represented by an encoded tensor. <code>InputMetadata.encoded_tensor_name</code> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [&quot;This&quot;, &quot;is&quot;, &quot;a&quot;, &quot;test&quot;, &quot;.&quot;]
encoded = [0.1, 0.2, 0.3, 0.4, 0.5]</code></pre></td>
</tr>
<tr class="odd">
<td><code>CONCAT_EMBEDDING</code></td>
<td><p>Select this encoding when the input tensor is encoded into a 2-dimensional array represented by an encoded tensor. <code>InputMetadata.encoded_tensor_name</code> must be provided for this encoding. The first dimension of the encoded tensor's shape is the same as the input tensor's shape. For example:</p>
<pre data-fenced=""><code>input = [&quot;This&quot;, &quot;is&quot;, &quot;a&quot;, &quot;test&quot;, &quot;.&quot;]
encoded = [[0.1, 0.2, 0.3, 0.4, 0.5],
           [0.2, 0.1, 0.4, 0.3, 0.5],
           [0.5, 0.1, 0.3, 0.5, 0.4],
           [0.5, 0.3, 0.1, 0.2, 0.4],
           [0.4, 0.3, 0.2, 0.5, 0.1]]</code></pre></td>
</tr>
</tbody>
</table>

### Type

Type of the image visualization. Only applicable to `Integrated Gradients attribution` .

| Enums              |                                                                                 |
|--------------------|---------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED` | Should not be used.                                                             |
| `PIXELS`           | Shows which pixel contributed to the image prediction.                          |
| `OUTLINES`         | Shows which region contributed to the image prediction by outlining the region. |

### Polarity

Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.

| Enums                  |                                                                                                      |
|------------------------|------------------------------------------------------------------------------------------------------|
| `POLARITY_UNSPECIFIED` | Default value. This is the same as POSITIVE.                                                         |
| `POSITIVE`             | Highlights the pixels/outlines that were most influential to the model's prediction.                 |
| `NEGATIVE`             | Setting polarity to negative highlights areas that does not lead to the models's current prediction. |
| `BOTH`                 | Shows both positive and negative attributions.                                                       |

### ColorMap

The color scheme used for highlighting areas.

| Enums                   |                                                                                                                                                                                            |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `COLOR_MAP_UNSPECIFIED` | Should not be used.                                                                                                                                                                        |
| `PINK_GREEN`            | Positive: green. Negative: pink.                                                                                                                                                           |
| `VIRIDIS`               | Viridis color map: A perceptually uniform color mapping which is easier to see by those with colorblindness and progresses from yellow to green to blue. Positive: yellow. Negative: blue. |
| `RED`                   | Positive: red. Negative: red.                                                                                                                                                              |
| `GREEN`                 | Positive: green. Negative: green.                                                                                                                                                          |
| `RED_GREEN`             | Positive: green. Negative: red.                                                                                                                                                            |
| `PINK_WHITE_GREEN`      | PiYG palette.                                                                                                                                                                              |

### OverlayType

How the original image is displayed in the visualization.

| Enums                      |                                                                                                               |
|----------------------------|---------------------------------------------------------------------------------------------------------------|
| `OVERLAY_TYPE_UNSPECIFIED` | Default value. This is the same as NONE.                                                                      |
| `NONE`                     | No overlay.                                                                                                   |
| `ORIGINAL`                 | The attributions are shown on top of the original image.                                                      |
| `GRAYSCALE`                | The attributions are shown on top of grayscaled version of the original image.                                |
| `MASK_BLACK`               | The attributions are used as a mask to reveal predictive parts of the image and hide the un-predictive parts. |

### PSCAutomationState

The state of the PSC service automation.

| Enums                              |                                           |
|------------------------------------|-------------------------------------------|
| `PSC_AUTOMATION_STATE_UNSPECIFIED` | Should not be used.                       |
| `PSC_AUTOMATION_STATE_SUCCESSFUL`  | The PSC service automation is successful. |
| `PSC_AUTOMATION_STATE_FAILED`      | The PSC service automation has failed.    |

### ModelProvider

A model provider (publisher) that prediction data may be shared with.

| Enums                        |                             |
|------------------------------|-----------------------------|
| `MODEL_PROVIDER_UNSPECIFIED` | Unspecified model provider. |
| `ANTHROPIC`                  | Anthropic.                  |

## Output Schema

This resource represents a long-running operation that is the result of a network API call.

### Operation

**JSON representation**

```
{
  "name": string,
  "metadata": {
    "@type": string,
    field1: ...,
    ...
  },
  "done": boolean,

  // Union field result can be only one of the following:
  "error": {
    object (Status)
  },
  "response": {
    "@type": string,
    field1: ...,
    ...
  }
  // End of list of possible types for union field result.
}
```

| Fields                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                                                                                                                                                                          | `string` The server-assigned name, which is only unique within the same service that originally returns it. If you use the default HTTP mapping, the `name` should be a resource name ending with `operations/{unique_id}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `metadata`                                                                                                                                                                                                                                                                                                                      | `object` Service-specific metadata associated with the operation. It typically contains progress information and common metadata such as create time. Some services might not provide such metadata. Any method that returns a long-running operation should document the metadata type, if any. An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .                                                                                                                                                                                                                     |
| `done`                                                                                                                                                                                                                                                                                                                          | `boolean` If the value is `false` , it means the operation is still in progress. If `true` , the operation is completed, and either `error` or `response` is available.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Union field `result` . The operation result, which can be either an `error` or a valid `response` . If `done` == `false` , neither `error` nor `response` is set. If `done` == `true` , exactly one of `error` or `response` can be set. Some services might not provide the result. `result` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `error`                                                                                                                                                                                                                                                                                                                         | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` The error result of the operation in case of failure or cancellation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `response`                                                                                                                                                                                                                                                                                                                      | `object` The normal, successful response of the operation. If the original method returns no data on success, such as `Delete` , the response is `google.protobuf.Empty` . If the original method is standard `Get` / `Create` / `Update` , the response should be the resource. For other methods, the response should have the type `XxxResponse` , where `Xxx` is the original method name. For example, if the original method name is `TakeSnapshot()` , the inferred response type is `TakeSnapshotResponse` . An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` . |

### Any

**JSON representation**

```
{
  "typeUrl": string,
  "value": string
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `typeUrl` | `string` Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name. Example: type.googleapis.com/google.protobuf.StringValue This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them. The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests. All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected. In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs. |
| `value`   | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Holds a Protobuf serialization of the type described by type_url. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### Status

**JSON representation**

```
{
  "code": integer,
  "message": string,
  "details": [
    {
      "@type": string,
      field1: ...,
      ...
    }
  ]
}
```

| Fields      |                                                                                                                                                                                                                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`      | `integer` The status code, which should be an enum value of `google.rpc.Code` .                                                                                                                                                                                                                              |
| `message`   | `string` A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.                                                                                                      |
| `details[]` | `object` A list of messages that carry the error details. There is a common set of message types for APIs to use. An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` . |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ❌ \| Read Only Hint: ❌ \| Open World Hint: ❌
