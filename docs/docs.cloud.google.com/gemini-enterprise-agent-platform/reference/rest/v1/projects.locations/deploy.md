---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/deploy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/deploy
title: 'Method: locations.deploy'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.deploy

Deploys a model to a new endpoint.

### Endpoint

post `https: / /{service-endpoint} /v1 /{destination}:deploy`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`destination` `string`

Required. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`modelConfig` ` object ( ModelConfig  ` )

Optional. The model config to use for the deployment. If not specified, the default model config will be used.

`endpointConfig` ` object ( EndpointConfig  ` )

Optional. The endpoint config to use for the deployment. If not specified, the default endpoint config will be used.

`deployConfig` ` object ( DeployConfig  ` )

Optional. The deploy config to use for the deployment. If not specified, the default deploy config will be used.

`artifacts` `Union type`

The artifacts to deploy. `artifacts` can be only one of the following:

`publisherModelName` `string`

The Model Garden model to deploy. Format: `publishers/{publisher}/models/{publisherModel}@{versionId}` , or `publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001` .

`huggingFaceModelId` `string`

The Hugging Face model to deploy. Format: Hugging Face model id like `google/gemma-2-2b-it` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## ModelConfig

The model config to use for the deployment.

Fields

`acceptEula` `boolean`

Optional. Whether the user accepts the End user License Agreement (EULA) for the model.

`huggingFaceAccessToken` `string`

Optional. The Hugging Face read access token used to access the model artifacts of gated models.

`huggingFaceCacheEnabled` `boolean`

Optional. If true, the model will deploy with a cached version instead of directly downloading the model artifacts from Hugging Face. This is suitable for VPC-SC users with limited internet access.

`modelDisplayName` `string`

Optional. The user-specified display name of the uploaded model. If not set, a default name will be used.

`containerSpec` ` object ( ModelContainerSpec  ` )

Optional. The specification of the container that is to be used when deploying. If not set, the default container spec will be used.

`modelUserId` `string`

Optional. The id to use for the uploaded Model, which will become the final component of the model resource name. When not provided, Agent Platform will generate a value for this id. When Model Registry model is provided, this field will be ignored.

This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number or hyphen.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;acceptEula&quot;: boolean,&quot;huggingFaceAccessToken&quot;: string,&quot;huggingFaceCacheEnabled&quot;: boolean,&quot;modelDisplayName&quot;: string,&quot;containerSpec&quot;: {object (ModelContainerSpec)},&quot;modelUserId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## EndpointConfig

The endpoint config to use for the deployment.

Fields

`endpointDisplayName` `string`

Optional. The user-specified display name of the endpoint. If not set, a default name will be used.

` dedicatedEndpointEnabled (deprecated)  ` `boolean`

> This item is deprecated\!

Optional. Deprecated. Use dedicatedEndpointDisabled instead. If true, the endpoint will be exposed through a dedicated DNS \[Endpoint.dedicated\_endpoint\_dns\]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitations will be removed soon.

`dedicatedEndpointDisabled` `boolean`

Optional. By default, if dedicated endpoint is enabled and private service connect config is not set, the endpoint will be exposed through a dedicated DNS \[Endpoint.dedicated\_endpoint\_dns\]. If private service connect config is set, the endpoint will be exposed through private service connect. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitations will be removed soon.

If this field is set to true, the dedicated endpoint will be disabled and the deployed model will be exposed through the shared DNS {region}-aiplatform.googleapis.com.

`privateServiceConnectConfig` ` object ( PrivateServiceConnectConfig  ` )

Optional. Configuration for private service connect. If set, the endpoint will be exposed through private service connect.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your endpoints.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`endpointUserId` `string`

Optional. Immutable. The id to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Agent Platform will generate a value for this id.

If the first character is a letter, this value may be up to 63 characters, and valid characters are `[a-z0-9-]` . The last character must be a letter or number.

If the first character is a number, this value may be up to 9 characters, and valid characters are `[0-9]` with no leading zeros.

When using HTTP/JSON, this field is populated based on a query string argument, such as `?endpointId=12345` . This is the fallback for fields that are not included in either the URI or the body.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;endpointDisplayName&quot;: string,&quot;dedicatedEndpointEnabled&quot;: boolean,&quot;dedicatedEndpointDisabled&quot;: boolean,&quot;privateServiceConnectConfig&quot;: {object (PrivateServiceConnectConfig)},&quot;labels&quot;: {string: string,...},&quot;endpointUserId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## DeployConfig

The deploy config to use for the deployment.

Fields

`dedicatedResources` ` object ( DedicatedResources  ` )

Optional. The dedicated resources to use for the endpoint. If not set, the default resources will be used.

`fastTryoutEnabled` `boolean`

Optional. If true, enable the QMT fast tryout feature for this model if possible.

`systemLabels` `map (key: string, value: string)`

Optional. System labels for Model Garden deployments. These labels are managed by Google and for tracking purposes only.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dedicatedResources&quot;: {object (DedicatedResources)},&quot;fastTryoutEnabled&quot;: boolean,&quot;systemLabels&quot;: {string: string,...}}</code></pre></td>
</tr>
</tbody>
</table>
