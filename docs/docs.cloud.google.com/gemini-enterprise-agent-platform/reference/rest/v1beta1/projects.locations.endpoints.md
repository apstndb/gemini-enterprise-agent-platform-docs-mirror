---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints
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

`deployedModels[]` ` object ( DeployedModel  ` )

Output only. The models deployed in this Endpoint. To add or remove DeployedModels use `  EndpointService.DeployModel  ` and `  EndpointService.UndeployModel  ` respectively.

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

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Endpoint was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Endpoint was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for an Endpoint. If set, this Endpoint and all sub-resources of this Endpoint will be secured by this key.

`network` `string`

Optional. The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks) to which the Endpoint should be peered.

Private services access must already be configured for the network. If left unspecified, the Endpoint is not peered with any network.

Only one of the fields, `  network  ` or `  enablePrivateServiceConnect  ` , can be set.

[Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert) : `projects/{project}/global/networks/{network}` . Where `{project}` is a project number, as in `12345` , and `{network}` is network name.

` enablePrivateServiceConnect (deprecated)  ` `boolean`

> This item is deprecated\!

Deprecated: If true, expose the Endpoint via private service connect.

Only one of the fields, `  network  ` or `  enablePrivateServiceConnect  ` , can be set.

`privateServiceConnectConfig` ` object ( PrivateServiceConnectConfig  ` )

Optional. Configuration for private service connect.

`  network  ` and `  privateServiceConnectConfig  ` are mutually exclusive.

`modelDeploymentMonitoringJob` `string`

Output only. Resource name of the Model Monitoring job associated with this Endpoint if monitoring is enabled by `  JobService.CreateModelDeploymentMonitoringJob  ` . Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{modelDeploymentMonitoringJob}`

`predictRequestResponseLoggingConfig` ` object ( PredictRequestResponseLoggingConfig  ` )

Configures the request-response logging for online prediction.

`dedicatedEndpointEnabled` `boolean`

If true, the endpoint will be exposed through a dedicated DNS \[Endpoint.dedicated\_endpoint\_dns\]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitation will be removed soon.

`dedicatedEndpointDns` `string`

Output only. DNS of the dedicated endpoint. Will only be populated if dedicatedEndpointEnabled is true. Depending on the features enabled, uid might be a random number or a string. For example, if fast\_tryout is enabled, uid will be fasttryout. Format: `https://{endpointId}.{region}-{uid}.prediction.vertexai.goog` .

`clientConnectionConfig` ` object ( ClientConnectionConfig  ` )

Configurations that are applied to the endpoint for online prediction.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

`genAiAdvancedFeaturesConfig` ` object ( GenAiAdvancedFeaturesConfig  ` )

Optional. Configuration for GenAiAdvancedFeatures. If the endpoint is serving GenAI models, advanced features like native RAG integration can be configured. Currently, only Model Garden models are supported.

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

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when the DeployedModel was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`explanationSpec` ` object ( ExplanationSpec  ` )

Explanation configuration for this DeployedModel.

When deploying a Model using `  EndpointService.DeployModel  ` , this value overrides the value of `  Model.explanation_spec  ` . All fields of `  explanationSpec  ` are optional in the request. If a field of `  explanationSpec  ` is not populated, the value of the same field of `  Model.explanation_spec  ` is inherited. If the corresponding `  Model.explanation_spec  ` is not populated, all fields of the `  explanationSpec  ` will be used for the explanation configuration.

`disableExplanations` `boolean`

If true, deploy the model without explainable feature, regardless the existence of `  Model.explanation_spec  ` or `  explanationSpec  ` .

`serviceAccount` `string`

The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project.

Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service account.

`enableContainerLogging` `boolean`

If true, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging.

Only supported for custom-trained Models and AutoML Tabular Models.

`disableContainerLogging` `boolean`

For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by default. Please note that the logs incur cost, which are subject to [Cloud Logging pricing](https://cloud.google.com/logging/pricing) .

user can disable container logging by setting this flag to true.

`enableAccessLogging` `boolean`

If true, online prediction access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each prediction request.

Note that logs may incur a cost, especially if your project receives prediction requests at a high queries per second rate (QPS). Estimate your costs before enabling this option.

`privateEndpoints` ` object ( PrivateEndpoints  ` )

Output only. Provide paths for users to send predict/explain/health requests directly to the deployed model services running on Cloud via private services access. This field is populated if `  network  ` is configured.

`fasterDeploymentConfig` ` object ( FasterDeploymentConfig  ` )

Configuration for faster model deployment.

`rolloutOptions` ` object ( RolloutOptions  ` )

Options for configuring rolling deployments.

`status` ` object ( Status  ` )

Output only. Runtime status of the deployed model.

`systemLabels` `map (key: string, value: string)`

System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only.

`checkpointId` `string`

The checkpoint id of the model.

`speculativeDecodingSpec` ` object ( SpeculativeDecodingSpec  ` )

Optional. Spec for configuring speculative decoding.

`prediction_resources` `Union type`

The prediction (for example, the machine) resources that the DeployedModel uses. The user is billed for the resources (at least their minimal amount) even if the DeployedModel receives no traffic. Not all Models support all resources types. See `  Model.supported_deployment_resources_types  ` . Required except for Large Model Deploy use cases. `prediction_resources` can be only one of the following:

`dedicatedResources` ` object ( DedicatedResources  ` )

A description of resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration.

`automaticResources` ` object ( AutomaticResources  ` )

A description of resources that to large degree are decided by Agent Platform, and require only a modest additional configuration.

`sharedResources` `string`

The resource name of the shared DeploymentResourcePool to deploy on. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deploymentResourcePool}`

`fullFineTunedResources` ` object ( FullFineTunedResources  ` )

Optional. Resources for a full fine tuned model.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;model&quot;: string,&quot;gdcConnectedModel&quot;: string,&quot;modelVersionId&quot;: string,&quot;displayName&quot;: string,&quot;createTime&quot;: string,&quot;explanationSpec&quot;: {object (ExplanationSpec)},&quot;disableExplanations&quot;: boolean,&quot;serviceAccount&quot;: string,&quot;enableContainerLogging&quot;: boolean,&quot;disableContainerLogging&quot;: boolean,&quot;enableAccessLogging&quot;: boolean,&quot;privateEndpoints&quot;: {object (PrivateEndpoints)},&quot;fasterDeploymentConfig&quot;: {object (FasterDeploymentConfig)},&quot;rolloutOptions&quot;: {object (RolloutOptions)},&quot;status&quot;: {object (Status)},&quot;systemLabels&quot;: {string: string,...},&quot;checkpointId&quot;: string,&quot;speculativeDecodingSpec&quot;: {object (SpeculativeDecodingSpec)},// prediction_resources&quot;dedicatedResources&quot;: {object (DedicatedResources)},&quot;automaticResources&quot;: {object (AutomaticResources)},&quot;sharedResources&quot;: string,&quot;fullFineTunedResources&quot;: {object (FullFineTunedResources)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FullFineTunedResources

Resources for an fft model.

Fields

`deploymentType` ` enum ( DeploymentType  ` )

Required. The kind of deployment.

`modelInferenceUnitCount` `integer`

Optional. The number of model inference units to use for this deployment. This can only be specified for DEPLOYMENT\_TYPE\_PROD. The following table lists the number of model inference units for different model types: \* Gemini 2.5 Flash \* Foundation FMIU: 25 \* Expansion FMIU: 4 \* Gemini 2.5 Pro \* Foundation FMIU: 32 \* Expansion FMIU: 16 \* Veo 3.0 (undistilled) \* Foundation FMIU: 63 \* Expansion FMIU: 7 \* Veo 3.0 (distilled) \* Foundation FMIU: 30 \* Expansion FMIU: 10

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

## DeploymentType

The type of deployment.

Enums

`DEPLOYMENT_TYPE_UNSPECIFIED`

Unspecified deployment type.

`DEPLOYMENT_TYPE_EVAL`

Eval deployment type.

`DEPLOYMENT_TYPE_PROD`

Prod deployment type.

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

## FasterDeploymentConfig

Configuration for faster model deployment.

Fields

`fastTryoutEnabled` `boolean`

If true, enable fast tryout feature for this deployed model.

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

## RolloutOptions

Configuration for rolling deployments.

Fields

`previousDeployedModel` `string`

id of the DeployedModel that this deployment should replace.

`revisionNumber` `integer`

Output only. Read-only. Revision number determines the relative priority of DeployedModels in the same rollout. The DeployedModel with the largest revision number specifies the intended state of the deployment.

`max_unavailable` `Union type`

Configures how many replicas are allowed to be unavailable during a rolling deployment. `max_unavailable` can be only one of the following:

`maxUnavailableReplicas` `integer`

Absolute count of replicas allowed to be unavailable.

`maxUnavailablePercentage` `integer`

Percentage of replicas allowed to be unavailable. For autoscaling deployments, this refers to the target replica count.

`max_surge` `Union type`

Configures how many additional replicas can be provisioned during a rolling deployment. `max_surge` can be only one of the following:

`maxSurgeReplicas` `integer`

Absolute count of allowed additional replicas.

`maxSurgePercentage` `integer`

Percentage of allowed additional replicas. For autoscaling deployments, this refers to the target replica count.

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
  &quot;previousDeployedModel&quot;: string,
  &quot;revisionNumber&quot;: integer,

  // max_unavailable
  &quot;maxUnavailableReplicas&quot;: integer,
  &quot;maxUnavailablePercentage&quot;: integer
  // Union type

  // max_surge
  &quot;maxSurgeReplicas&quot;: integer,
  &quot;maxSurgePercentage&quot;: integer
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## Status

Runtime status of the deployed model.

Fields

`message` `string`

Output only. The latest deployed model's status message (if any).

`lastUpdateTime` ` string ( Timestamp  ` format)

Output only. The time at which the status was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`availableReplicaCount` `integer`

Output only. The number of available replicas of the deployed model.

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

## SpeculativeDecodingSpec

Configuration for Speculative Decoding.

Fields

`speculativeTokenCount` `integer`

The number of speculative tokens to generate at each step.

`speculation` `Union type`

The type of speculation method to use. `speculation` can be only one of the following:

`draftModelSpeculation` ` object ( DraftModelSpeculation  ` )

draft model speculation.

`ngramSpeculation` ` object ( NgramSpeculation  ` )

N-Gram speculation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;speculativeTokenCount&quot;: integer,// speculation&quot;draftModelSpeculation&quot;: {object (DraftModelSpeculation)},&quot;ngramSpeculation&quot;: {object (NgramSpeculation)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## DraftModelSpeculation

Draft model speculation works by using the smaller model to generate candidate tokens for speculative decoding.

Fields

`draftModel` `string`

Required. The resource name of the draft model.

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

## NgramSpeculation

N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

Fields

`ngramSize` `integer`

The number of last N input tokens used as ngram to search/match against the previous prompt sequence. This is equal to the N in N-Gram. The default value is 3 if not specified.

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

## PredictRequestResponseLoggingConfig

Configuration for logging request-response to a BigQuery table.

Fields

`enabled` `boolean`

If logging is enabled or not.

`samplingRate` `number`

Percentage of requests to be logged, expressed as a fraction in range(0,1\].

`errorSamplingRate` `number`

Optional. Percentage of failed requests to be logged, expressed as a fraction in range \[0,1\]. Only non-transient errors will be logged (currently `500/Internal` errors).

`bigqueryDestination` ` object ( BigQueryDestination  ` )

BigQuery table for logging. If only given a project, a new dataset will be created with name `logging_<endpoint-display-name>_<endpoint-id>` where will be made BigQuery-dataset-name compatible (e.g. most special characters will become underscores). If no table name is given, a new table will be created with name `request_response_logging`

`requestResponseLoggingSchemaVersion` `string`

Output only. The schema version used in creating the BigQuery table for the request response logging. The versions are "v1" and "v2". The current default version is "v1".

`enableOtelLogging` `boolean`

This field is used for large models. If true, in addition to the original large model logs, logs will be converted in OTel schema format, and saved in otel\_log column. Default value is false.

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

## ClientConnectionConfig

Configurations (e.g. inference timeout) that are applied on your endpoints.

Fields

`inferenceTimeout` ` string ( Duration  ` format)

Customizable online prediction request timeout.

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
  &quot;inferenceTimeout&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## GenAiAdvancedFeaturesConfig

Configuration for GenAiAdvancedFeatures.

Fields

`ragConfig` ` object ( RagConfig  ` )

Configuration for Retrieval Augmented Generation feature.

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

## RagConfig

Configuration for Retrieval Augmented Generation feature.

Fields

`enableRag` `boolean`

If true, enable Retrieval Augmented Generation in ChatCompletion request. Once enabled, the endpoint will be identified as GenAI endpoint and Arthedain router will be used.

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

## Methods

### `            computeTokens           `

Return a list of tokens based on the input text.

### `            countTokens           `

Perform a token counting.

### `            create           `

Creates an Endpoint.

### `            delete           `

Deletes an Endpoint.

### `            deployModel           `

Deploys a Model into this Endpoint, creating a DeployedModel within it.

### `            directPredict           `

Perform an unary online prediction request to a gRPC model server for Vertex first-party products and frameworks.

### `            directRawPredict           `

Perform an unary online prediction request to a gRPC model server for custom containers.

### `            explain           `

Perform an online explanation.

### `            generateContent           `

Generate content with multimodal inputs.

### `            get           `

Gets an Endpoint.

### `            getIamPolicy           `

Gets the access control policy for a resource.

### `            list           `

Lists Endpoints in a Location.

### `            mutateDeployedModel           `

Updates an existing deployed model.

### `            patch           `

Updates an Endpoint.

### `            predict           `

Perform an online inference.

### `            predictLongRunning           `

### `            rawPredict           `

Perform an online prediction with an arbitrary HTTP payload.

### `            serverStreamingPredict           `

Perform a server-side streaming online prediction request for Vertex LLM streaming.

### `            setIamPolicy           `

Sets the access control policy on the specified resource.

### `            streamGenerateContent           `

Generate content with multimodal inputs with streaming support.

### `            streamRawPredict           `

Perform a streaming online prediction with an arbitrary HTTP payload.

### `            testIamPermissions           `

Returns permissions that a caller has on the specified resource.

### `            undeployModel           `

Undeploys a Model from an Endpoint, removing a DeployedModel from it, and freeing all resources it's using.

### `            update           `

Updates an Endpoint with a long running operation.
