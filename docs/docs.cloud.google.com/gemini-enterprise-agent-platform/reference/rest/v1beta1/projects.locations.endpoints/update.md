---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/update
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/update
title: 'Method: endpoints.update'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.update

Updates an Endpoint with a long running operation.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint.name}:update`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint.name` `string`

Identifier. The resource name of the Endpoint.

### Request body

The request body contains data with the following structure:

Fields

`endpoint.displayName` `string`

Required. The display name of the Endpoint. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`endpoint.description` `string`

The description of the Endpoint.

`endpoint.deployedModels[]` ` object ( DeployedModel  ` )

Output only. The models deployed in this Endpoint. To add or remove DeployedModels use `  EndpointService.DeployModel  ` and `  EndpointService.UndeployModel  ` respectively.

`endpoint.trafficSplit` `map (key: string, value: integer)`

A map from a DeployedModel's id to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel.

If a DeployedModel's id is not listed in this map, then it receives no traffic.

The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at a moment.

`endpoint.etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`endpoint.labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your endpoints.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`endpoint.createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Endpoint was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endpoint.updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Endpoint was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endpoint.encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for an Endpoint. If set, this Endpoint and all sub-resources of this Endpoint will be secured by this key.

`endpoint.network` `string`

Optional. The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks) to which the Endpoint should be peered.

Private services access must already be configured for the network. If left unspecified, the Endpoint is not peered with any network.

Only one of the fields, `  network  ` or `  enablePrivateServiceConnect  ` , can be set.

[Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert) : `projects/{project}/global/networks/{network}` . Where `{project}` is a project number, as in `12345` , and `{network}` is network name.

` endpoint.enablePrivateServiceConnect (deprecated)  ` `boolean`

Deprecated: If true, expose the Endpoint via private service connect.

Only one of the fields, `  network  ` or `  enablePrivateServiceConnect  ` , can be set.

`endpoint.privateServiceConnectConfig` ` object ( PrivateServiceConnectConfig  ` )

Optional. Configuration for private service connect.

`  network  ` and `  privateServiceConnectConfig  ` are mutually exclusive.

`endpoint.modelDeploymentMonitoringJob` `string`

Output only. Resource name of the Model Monitoring job associated with this Endpoint if monitoring is enabled by `  JobService.CreateModelDeploymentMonitoringJob  ` . Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{modelDeploymentMonitoringJob}`

`endpoint.predictRequestResponseLoggingConfig` ` object ( PredictRequestResponseLoggingConfig  ` )

Configures the request-response logging for online prediction.

`endpoint.dedicatedEndpointEnabled` `boolean`

If true, the endpoint will be exposed through a dedicated DNS \[Endpoint.dedicated\_endpoint\_dns\]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitation will be removed soon.

`endpoint.dedicatedEndpointDns` `string`

Output only. DNS of the dedicated endpoint. Will only be populated if dedicatedEndpointEnabled is true. Depending on the features enabled, uid might be a random number or a string. For example, if fast\_tryout is enabled, uid will be fasttryout. Format: `https://{endpointId}.{region}-{uid}.prediction.vertexai.goog` .

`endpoint.clientConnectionConfig` ` object ( ClientConnectionConfig  ` )

Configurations that are applied to the endpoint for online prediction.

`endpoint.satisfiesPzs` `boolean`

Output only. reserved for future use.

`endpoint.satisfiesPzi` `boolean`

Output only. reserved for future use.

`endpoint.genAiAdvancedFeaturesConfig` ` object ( GenAiAdvancedFeaturesConfig  ` )

Optional. Configuration for GenAiAdvancedFeatures. If the endpoint is serving GenAI models, advanced features like native RAG integration can be configured. Currently, only Model Garden models are supported.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
