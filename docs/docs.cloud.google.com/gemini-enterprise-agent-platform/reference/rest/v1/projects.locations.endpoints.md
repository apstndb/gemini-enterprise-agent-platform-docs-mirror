---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints
title: 'REST Resource: projects.locations.endpoints'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Endpoint

Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations.

Fields

`name` `string`

Identifier. The resource name of the Endpoint.

`displayName` `string`

Required. The display name of the Endpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

The description of the Endpoint.

`deployedModels[]` `object ( `[`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel)` )`

Output only. The models deployed in this Endpoint. To add or remove DeployedModels use [`EndpointService.DeployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel#google.cloud.aiplatform.v1.EndpointService.DeployModel) and [`EndpointService.UndeployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/undeployModel#google.cloud.aiplatform.v1.EndpointService.UndeployModel) respectively.

`trafficSplit` `map (key: string, value: integer)`

A map from a DeployedModel's id to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel.

If a DeployedModel's id is not listed in this map, then it receives no traffic.

The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment.

`etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your endpoints.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Endpoint was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Endpoint was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec)` )`

Customer-managed encryption key spec for an Endpoint. If set, this Endpoint and all sub-resources of this Endpoint will be secured by this key.

`network` `string`

Optional. The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks) to which the Endpoint should be peered.

Private services access must already be configured for the network. If left unspecified, the Endpoint is not peered with any network.

Only one of the fields, [`network`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint.FIELDS.network) or [`enablePrivateServiceConnect`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint.FIELDS.enable_private_service_connect) , can be set.

[Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert) : `projects/{project}/global/networks/{network}` . Where `{project}` is a project number, as in `12345` , and `{network}` is network name.

`enablePrivateServiceConnect `**`(deprecated)`** `boolean`

> This item is deprecated!

Deprecated: If true, expose the Endpoint via private service connect.

Only one of the fields, [`network`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint.FIELDS.network) or [`enablePrivateServiceConnect`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint.FIELDS.enable_private_service_connect) , can be set.

`privateServiceConnectConfig` `object ( `[`PrivateServiceConnectConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PrivateServiceConnectConfig)` )`

Optional. Configuration for private service connect.

[`network`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint.FIELDS.network) and [`privateServiceConnectConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint.FIELDS.private_service_connect_config) are mutually exclusive.

`modelDeploymentMonitoringJob` `string`

Output only. Resource name of the Model Monitoring job associated with this Endpoint if monitoring is enabled by [`JobService.CreateModelDeploymentMonitoringJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/create#google.cloud.aiplatform.v1.JobService.CreateModelDeploymentMonitoringJob) . Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{modelDeploymentMonitoringJob}`

`predictRequestResponseLoggingConfig` `object ( `[`PredictRequestResponseLoggingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#PredictRequestResponseLoggingConfig)` )`

Configures the request-response logging for online prediction.

`dedicatedEndpointEnabled` `boolean`

If true, the endpoint will be exposed through a dedicated DNS \[Endpoint.dedicated_endpoint_dns\]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitation will be removed soon.

`dedicatedEndpointDns` `string`

Output only. DNS of the dedicated endpoint. Will only be populated if dedicatedEndpointEnabled is true. Depending on the features enabled, uid might be a random number or a string. For example, if fast_tryout is enabled, uid will be fasttryout. Format: `https://{endpointId}.{region}-{uid}.prediction.vertexai.goog` .

`clientConnectionConfig` `object ( `[`ClientConnectionConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#ClientConnectionConfig)` )`

Configurations that are applied to the endpoint for online prediction.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

`genAiAdvancedFeaturesConfig` `object ( `[`GenAiAdvancedFeaturesConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#GenAiAdvancedFeaturesConfig)` )`

Optional. Configuration for GenAiAdvancedFeatures. If the endpoint is serving GenAI models, advanced features like native RAG integration can be configured. Currently, only Model Garden models are supported.

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
  }
}
```

## DeployedModel

A deployment of a Model. endpoints contain one or more DeployedModels.

Fields

`id` `string`

Immutable. The id of the DeployedModel. If not provided upon deployment, Agent Platform will generate a value for this id.

This value should be 1-10 characters, and valid characters are `/[0-9]/` .

`model` `string`

The resource name of the Model that this is the deployment of. Note that the Model may be in a different location than the DeployedModel's Endpoint.

The resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2` or `projects/{project}/locations/{location}/models/{model}@golden` if no version is specified, the default version will be deployed.

`gdcConnectedModel` `string`

GDC pretrained / Gemini model name. The model name is a plain model name, e.g. gemini-1.5-flash-002.

`modelVersionId` `string`

Output only. The version id of the model that is deployed.

`displayName` `string`

The display name of the DeployedModel. If not provided upon creation, the Model's displayName is used.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when the DeployedModel was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`explanationSpec` `object ( `[`ExplanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec)` )`

Explanation configuration for this DeployedModel.

When deploying a Model using [`EndpointService.DeployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel#google.cloud.aiplatform.v1.EndpointService.DeployModel) , this value overrides the value of [`Model.explanation_spec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.explanation_spec) . All fields of [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel.FIELDS.explanation_spec) are optional in the request. If a field of [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel.FIELDS.explanation_spec) is not populated, the value of the same field of [`Model.explanation_spec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.explanation_spec) is inherited. If the corresponding [`Model.explanation_spec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.explanation_spec) is not populated, all fields of the [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel.FIELDS.explanation_spec) will be used for the explanation configuration.

`disableExplanations` `boolean`

If true, deploy the model without explainable feature, regardless the existence of [`Model.explanation_spec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.explanation_spec) or [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel.FIELDS.explanation_spec) .

`serviceAccount` `string`

The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project.

Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service account.

`disableContainerLogging` `boolean`

For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by default. Please note that the logs incur cost, which are subject to [Cloud Logging pricing](https://cloud.google.com/logging/pricing) .

user can disable container logging by setting this flag to true.

`enableAccessLogging` `boolean`

If true, online prediction access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each prediction request.

Note that logs may incur a cost, especially if your project receives prediction requests at a high queries per second rate (QPS). Estimate your costs before enabling this option.

`privateEndpoints` `object ( `[`PrivateEndpoints`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#PrivateEndpoints)` )`

Output only. Provide paths for users to send predict/explain/health requests directly to the deployed model services running on Cloud via private services access. This field is populated if [`network`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint.FIELDS.network) is configured.

`fasterDeploymentConfig` `object ( `[`FasterDeploymentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#FasterDeploymentConfig)` )`

Configuration for faster model deployment.

`status` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Status)` )`

Output only. Runtime status of the deployed model.

`systemLabels` `map (key: string, value: string)`

System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only.

`checkpointId` `string`

The checkpoint id of the model.

`speculativeDecodingSpec` `object ( `[`SpeculativeDecodingSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#SpeculativeDecodingSpec)` )`

Optional. Spec for configuring speculative decoding.

`prediction_resources` `Union type`

The prediction (for example, the machine) resources that the DeployedModel uses. The user is billed for the resources (at least their minimal amount) even if the DeployedModel receives no traffic. Not all Models support all resources types. See [`Model.supported_deployment_resources_types`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.supported_deployment_resources_types) . Required except for Large Model Deploy use cases. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`dedicatedResources` `object ( `[`DedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DedicatedResources)` )`

A description of resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration.

`automaticResources` `object ( `[`AutomaticResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/AutomaticResources)` )`

A description of resources that to large degree are decided by Agent Platform, and require only a modest additional configuration.

`sharedResources` `string`

The resource name of the shared DeploymentResourcePool to deploy on. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deploymentResourcePool}`

End of mutually exclusive fields.

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
  "disableContainerLogging": boolean,
  "enableAccessLogging": boolean,
  "privateEndpoints": {
    object (PrivateEndpoints)
  },
  "fasterDeploymentConfig": {
    object (FasterDeploymentConfig)
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

  // prediction_resources
  "dedicatedResources": {
    object (DedicatedResources)
  },
  "automaticResources": {
    object (AutomaticResources)
  },
  "sharedResources": string
  // Union type
}
```

## PrivateEndpoints

PrivateEndpoints proto is used to provide paths for users to send requests privately. To send request via private service access, use predictHttpUri, explainHttpUri or healthHttpUri. To send request via private service connect, use serviceAttachment.

Fields

`predictHttpUri` `string`

Output only. Http(s) path to send prediction requests.

`explainHttpUri` `string`

Output only. Http(s) path to send explain requests.

`healthHttpUri` `string`

Output only. Http(s) path to send health check requests.

`serviceAttachment` `string`

Output only. The name of the service attachment resource. Populated if private service connect is enabled.

**JSON representation**

```
{
  "predictHttpUri": string,
  "explainHttpUri": string,
  "healthHttpUri": string,
  "serviceAttachment": string
}
```

## FasterDeploymentConfig

Configuration for faster model deployment.

Fields

`fastTryoutEnabled` `boolean`

If true, enable fast tryout feature for this deployed model.

**JSON representation**

```
{
  "fastTryoutEnabled": boolean
}
```

## Status

Runtime status of the deployed model.

Fields

`message` `string`

Output only. The latest deployed model's status message (if any).

`lastUpdateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. The time at which the status was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`availableReplicaCount` `integer`

Output only. The number of available replicas of the deployed model.

**JSON representation**

```
{
  "message": string,
  "lastUpdateTime": string,
  "availableReplicaCount": integer
}
```

## SpeculativeDecodingSpec

Configuration for Speculative Decoding.

Fields

`speculativeTokenCount` `integer`

The number of speculative tokens to generate at each step.

`speculation` `Union type`

The type of speculation method to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`draftModelSpeculation` `object ( `[`DraftModelSpeculation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DraftModelSpeculation)` )`

draft model speculation.

`ngramSpeculation` `object ( `[`NgramSpeculation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#NgramSpeculation)` )`

N-Gram speculation.

End of mutually exclusive fields.

**JSON representation**

```
{
  "speculativeTokenCount": integer,

  // speculation
  "draftModelSpeculation": {
    object (DraftModelSpeculation)
  },
  "ngramSpeculation": {
    object (NgramSpeculation)
  }
  // Union type
}
```

## DraftModelSpeculation

Draft model speculation works by using the smaller model to generate candidate tokens for speculative decoding.

Fields

`draftModel` `string`

Required. The resource name of the draft model.

**JSON representation**

```
{
  "draftModel": string
}
```

## NgramSpeculation

N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

Fields

`ngramSize` `integer`

The number of last N input tokens used as ngram to search/match against the previous prompt sequence. This is equal to the N in N-Gram. The default value is 3 if not specified.

**JSON representation**

```
{
  "ngramSize": integer
}
```

## PredictRequestResponseLoggingConfig

Configuration for logging request-response to a BigQuery table.

Fields

`enabled` `boolean`

If logging is enabled or not.

`samplingRate` `number`

Percentage of requests to be logged, expressed as a fraction in range(0,1\].

`bigqueryDestination` `object ( `[`BigQueryDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BigQueryDestination)` )`

BigQuery table for logging. If only given a project, a new dataset will be created with name `logging_<endpoint-display-name>_<endpoint-id>` where will be made BigQuery-dataset-name compatible (e.g. most special characters will become underscores). If no table name is given, a new table will be created with name `request_response_logging`

**JSON representation**

```
{
  "enabled": boolean,
  "samplingRate": number,
  "bigqueryDestination": {
    object (BigQueryDestination)
  }
}
```

## ClientConnectionConfig

Configurations (e.g. inference timeout) that are applied on your endpoints.

Fields

`inferenceTimeout` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Customizable online prediction request timeout.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

**JSON representation**

```
{
  "inferenceTimeout": string
}
```

## GenAiAdvancedFeaturesConfig

Configuration for GenAiAdvancedFeatures.

Fields

`ragConfig` `object ( `[`RagConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#RagConfig)` )`

Configuration for Retrieval Augmented Generation feature.

**JSON representation**

```
{
  "ragConfig": {
    object (RagConfig)
  }
}
```

## RagConfig

Configuration for Retrieval Augmented Generation feature.

Fields

`enableRag` `boolean`

If true, enable Retrieval Augmented Generation in ChatCompletion request. Once enabled, the endpoint will be identified as GenAI endpoint and Arthedain router will be used.

**JSON representation**

```
{
  "enableRag": boolean
}
```

| Methods                                                                                                                                                          |                                                                                                                   |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| [`computeTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/computeTokens)                   | Return a list of tokens based on the input text.                                                                  |
| [`countTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/countTokens)                       | Perform a token counting.                                                                                         |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/create)                                 | Creates an Endpoint.                                                                                              |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/delete)                                 | Deletes an Endpoint.                                                                                              |
| [`deployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel)                       | Deploys a Model into this Endpoint, creating a DeployedModel within it.                                           |
| [`directPredict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/directPredict)                   | Perform an unary online prediction request to a gRPC model server for Vertex first-party products and frameworks. |
| [`directRawPredict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/directRawPredict)             | Perform an unary online prediction request to a gRPC model server for custom containers.                          |
| [`explain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain)                               | Perform an online explanation.                                                                                    |
| [`generateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/generateContent)               | Generate content with multimodal inputs.                                                                          |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/get)                                       | Gets an Endpoint.                                                                                                 |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/list)                                     | Lists Endpoints in a Location.                                                                                    |
| [`mutateDeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/mutateDeployedModel)       | Updates an existing deployed model.                                                                               |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/patch)                                   | Updates an Endpoint.                                                                                              |
| [`predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict)                               | Perform an online inference.                                                                                      |
| [`rawPredict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/rawPredict)                         | Perform an online prediction with an arbitrary HTTP payload.                                                      |
| [`serverStreamingPredict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/serverStreamingPredict) | Perform a server-side streaming online prediction request for Vertex LLM streaming.                               |
| [`streamGenerateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/streamGenerateContent)   | Generate content with multimodal inputs with streaming support.                                                   |
| [`streamRawPredict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/streamRawPredict)             | Perform a streaming online prediction with an arbitrary HTTP payload.                                             |
| [`undeployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/undeployModel)                   | Undeploys a Model from an Endpoint, removing a DeployedModel from it, and freeing all resources it's using.       |
| [`update`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/update)                                 | Updates an Endpoint with a long running operation.                                                                |
