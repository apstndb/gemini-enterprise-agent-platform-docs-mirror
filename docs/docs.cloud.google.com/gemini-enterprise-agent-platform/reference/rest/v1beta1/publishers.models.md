---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/publishers.models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/publishers.models
title: 'REST Resource: publishers.models'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: PublisherModel

A Model Garden Publisher Model.

Fields

`name` `string`

Output only. Identifier. The resource name of the PublisherModel.

`versionId` `string`

Output only. Immutable. The version id of the PublisherModel. A new version is committed when a new model version is uploaded under an existing model id. It is an auto-incrementing decimal number in string representation.

`openSourceCategory` ` enum ( OpenSourceCategory  ` )

Required. Indicates the open source category of the publisher model.

`parent` ` object ( Parent  ` )

Optional. The parent that this model was customized from. E.g., Vision API, Natural Language API, LaMDA, T5, etc. Foundation models don't have parents.

`supportedActions` ` object ( CallToAction  ` )

Optional. Supported call-to-action options.

`frameworks[]` `string`

Optional. Additional information about the model's Frameworks.

`launchStage` ` enum ( LaunchStage  ` )

Optional. Indicates the launch stage of the model.

`versionState` ` enum ( VersionState  ` )

Optional. Indicates the state of the model version.

`publisherModelTemplate` `string`

Optional. Output only. Immutable. Used to indicate this model has a publisher model and provide the template of the publisher model resource name.

`predictSchemata` ` object ( PredictSchemata  ` )

Optional. The schemata that describes formats of the PublisherModel's predictions and explanations as given and returned via `  PredictionService.Predict  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;versionId&quot;: string,&quot;openSourceCategory&quot;: enum (OpenSourceCategory),&quot;parent&quot;: {object (Parent)},&quot;supportedActions&quot;: {object (CallToAction)},&quot;frameworks&quot;: [string],&quot;launchStage&quot;: enum (LaunchStage),&quot;versionState&quot;: enum (VersionState),&quot;publisherModelTemplate&quot;: string,&quot;predictSchemata&quot;: {object (PredictSchemata)}}</code></pre></td>
</tr>
</tbody>
</table>

## OpenSourceCategory

An enum representing the open source category of a PublisherModel.

Enums

`OPEN_SOURCE_CATEGORY_UNSPECIFIED`

The open source category is unspecified, which should not be used.

`PROPRIETARY`

Used to indicate the PublisherModel is not open sourced.

`GOOGLE_OWNED_OSS_WITH_GOOGLE_CHECKPOINT`

Used to indicate the PublisherModel is a Google-owned open source model w/ Google checkpoint.

`THIRD_PARTY_OWNED_OSS_WITH_GOOGLE_CHECKPOINT`

Used to indicate the PublisherModel is a 3p-owned open source model w/ Google checkpoint.

`GOOGLE_OWNED_OSS`

Used to indicate the PublisherModel is a Google-owned pure open source model.

`THIRD_PARTY_OWNED_OSS`

Used to indicate the PublisherModel is a 3p-owned pure open source model.

## Parent

The information about the parent of a model.

Fields

`displayName` `string`

Required. The display name of the parent. E.g., LaMDA, T5, Vision API, Natural Language API.

`reference` ` object ( ResourceReference  ` )

Optional. The Google Cloud resource name or the URI reference.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;displayName&quot;: string,&quot;reference&quot;: {object (ResourceReference)}}</code></pre></td>
</tr>
</tbody>
</table>

## ResourceReference

Reference to a resource.

Fields

`reference` `Union type`

`reference` can be only one of the following:

`uri` `string`

The URI of the resource.

`resourceName` `string`

The resource name of the Google Cloud resource.

` useCase (deprecated)  ` `string`

> This item is deprecated\!

Use case (CUJ) of the resource.

` description (deprecated)  ` `string`

> This item is deprecated\!

description of the resource.

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

  // reference
  &quot;uri&quot;: string,
  &quot;resourceName&quot;: string,
  &quot;useCase&quot;: string,
  &quot;description&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## CallToAction

Actions could take on this Publisher Model.

Fields

`viewRestApi` ` object ( ViewRestApi  ` )

Optional. To view Rest API docs.

`openNotebook` ` object ( RegionalResourceReferences  ` )

Optional. Open notebook of the PublisherModel.

`createApplication` ` object ( RegionalResourceReferences  ` )

Optional. Create application using the PublisherModel.

`openFineTuningPipeline` ` object ( RegionalResourceReferences  ` )

Optional. Open fine-tuning pipeline of the PublisherModel.

`openPromptTuningPipeline` ` object ( RegionalResourceReferences  ` )

Optional. Open prompt-tuning pipeline of the PublisherModel.

`openGenie` ` object ( RegionalResourceReferences  ` )

Optional. Open Genie / Playground.

`deploy` ` object ( Deploy  ` )

Optional. Deploy the PublisherModel to Vertex Endpoint.

`multiDeployVertex` ` object ( DeployVertex  ` )

Optional. Multiple setups to deploy the PublisherModel to Vertex Endpoint.

`deployGke` ` object ( DeployGke  ` )

Optional. Deploy PublisherModel to Google Kubernetes Engine.

`openGenerationAiStudio` ` object ( RegionalResourceReferences  ` )

Optional. Open in Generation AI Studio.

`requestAccess` ` object ( RegionalResourceReferences  ` )

Optional. Request for access.

`openEvaluationPipeline` ` object ( RegionalResourceReferences  ` )

Optional. Open evaluation pipeline of the PublisherModel.

`openNotebooks` ` object ( OpenNotebooks  ` )

Optional. Open notebooks of the PublisherModel.

`openFineTuningPipelines` ` object ( OpenFineTuningPipelines  ` )

Optional. Open fine-tuning pipelines of the PublisherModel.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;viewRestApi&quot;: {object (ViewRestApi)},&quot;openNotebook&quot;: {object (RegionalResourceReferences)},&quot;createApplication&quot;: {object (RegionalResourceReferences)},&quot;openFineTuningPipeline&quot;: {object (RegionalResourceReferences)},&quot;openPromptTuningPipeline&quot;: {object (RegionalResourceReferences)},&quot;openGenie&quot;: {object (RegionalResourceReferences)},&quot;deploy&quot;: {object (Deploy)},&quot;multiDeployVertex&quot;: {object (DeployVertex)},&quot;deployGke&quot;: {object (DeployGke)},&quot;openGenerationAiStudio&quot;: {object (RegionalResourceReferences)},&quot;requestAccess&quot;: {object (RegionalResourceReferences)},&quot;openEvaluationPipeline&quot;: {object (RegionalResourceReferences)},&quot;openNotebooks&quot;: {object (OpenNotebooks)},&quot;openFineTuningPipelines&quot;: {object (OpenFineTuningPipelines)}}</code></pre></td>
</tr>
</tbody>
</table>

## ViewRestApi

Rest API docs.

Fields

`documentations[]` ` object ( Documentation  ` )

Required.

`title` `string`

Required. The title of the view rest API.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;documentations&quot;: [{object (Documentation)}],&quot;title&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## Documentation

A named piece of documentation.

Fields

`title` `string`

Required. E.g., OVERVIEW, USE CASES, DOCUMENTATION, SDK & SAMPLES, JAVA, NODE.JS, etc..

`content` `string`

Required. Content of this piece of document (in Markdown format).

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
  &quot;title&quot;: string,
  &quot;content&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## RegionalResourceReferences

The regional resource name or the URI. Key is region, e.g., us-central1, europe-west2, global, etc..

Fields

`references` ` map (key: string, value: object ( ResourceReference  ` ))

Required.

`title` `string`

Required.

`resourceTitle` `string`

Optional. title of the resource.

`resourceUseCase` `string`

Optional. Use case (CUJ) of the resource.

`resourceDescription` `string`

Optional. description of the resource.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;references&quot;: {string: {object (ResourceReference)},...},&quot;title&quot;: string,&quot;resourceTitle&quot;: string,&quot;resourceUseCase&quot;: string,&quot;resourceDescription&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## OpenNotebooks

Open notebooks.

Fields

`notebooks[]` ` object ( RegionalResourceReferences  ` )

Required. Regional resource references to notebooks.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;notebooks&quot;: [{object (RegionalResourceReferences)}]}</code></pre></td>
</tr>
</tbody>
</table>

## OpenFineTuningPipelines

Open fine tuning pipelines.

Fields

`fineTuningPipelines[]` ` object ( RegionalResourceReferences  ` )

Required. Regional resource references to fine tuning pipelines.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;fineTuningPipelines&quot;: [{object (RegionalResourceReferences)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Deploy

Model metadata that is needed for UploadModel or DeployModel/CreateEndpoint requests.

Fields

`modelDisplayName` `string`

Optional. Default model display name.

`largeModelReference` ` object ( LargeModelReference  ` )

Optional. Large model reference. When this is set, modelArtifactSpec is not needed.

`containerSpec` ` object ( ModelContainerSpec  ` )

Optional. The specification of the container that is to be used when deploying this Model in Agent Platform. Not present for Large Models.

`artifactUri` `string`

Optional. The path to the directory containing the Model artifact and any of its supporting files.

`title` `string`

Required. The title of the regional resource reference.

`publicArtifactUri` `string`

Optional. The signed URI for ephemeral Cloud Storage access to model artifact.

`prediction_resources` `Union type`

The prediction (for example, the machine) resources that the DeployedModel uses. `prediction_resources` can be only one of the following:

`dedicatedResources` ` object ( DedicatedResources  ` )

A description of resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration.

`automaticResources` ` object ( AutomaticResources  ` )

A description of resources that to large degree are decided by Agent Platform, and require only a modest additional configuration.

`sharedResources` `string`

The resource name of the shared DeploymentResourcePool to deploy on. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deploymentResourcePool}`

`deployTaskName` `string`

Optional. The name of the deploy task (e.g., "text to image generation").

`deployMetadata` ` object ( DeployMetadata  ` )

Optional. metadata information about this deployment config.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelDisplayName&quot;: string,&quot;largeModelReference&quot;: {object (LargeModelReference)},&quot;containerSpec&quot;: {object (ModelContainerSpec)},&quot;artifactUri&quot;: string,&quot;title&quot;: string,&quot;publicArtifactUri&quot;: string,// prediction_resources&quot;dedicatedResources&quot;: {object (DedicatedResources)},&quot;automaticResources&quot;: {object (AutomaticResources)},&quot;sharedResources&quot;: string// Union type&quot;deployTaskName&quot;: string,&quot;deployMetadata&quot;: {object (DeployMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

## LargeModelReference

Contains information about the Large Model.

Fields

`name` `string`

Required. The unique name of the large Foundation or pre-built model. Like "chat-bison", "text-bison". Or model name with version id, like "chat-bison@001", "text-bison@005", etc.

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
  &quot;name&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## DeployMetadata

metadata information about the deployment for managing deployment config.

Fields

`labels` `map (key: string, value: string)`

Optional. Labels for the deployment config. For managing deployment config like verifying, source of deployment config, etc.

`sampleRequest` `string`

Optional. Sample request for deployed endpoint.

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
  &quot;labels&quot;: {
    string: string,
    ...
  },
  &quot;sampleRequest&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## DeployVertex

Multiple setups to deploy the PublisherModel.

Fields

`multiDeployVertex[]` ` object ( Deploy  ` )

Optional. One click deployment configurations.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;multiDeployVertex&quot;: [{object (Deploy)}]}</code></pre></td>
</tr>
</tbody>
</table>

## DeployGke

Configurations for PublisherModel GKE deployment

Fields

`gkeYamlConfigs[]` `string`

Optional. GKE deployment configuration in yaml format.

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
  &quot;gkeYamlConfigs&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## LaunchStage

An enum representing the launch stage of a PublisherModel.

Enums

`LAUNCH_STAGE_UNSPECIFIED`

The model launch stage is unspecified.

`EXPERIMENTAL`

Used to indicate the PublisherModel is at Experimental launch stage, available to a small set of customers.

`PRIVATE_PREVIEW`

Used to indicate the PublisherModel is at Private Preview launch stage, only available to a small set of customers, although a larger set of customers than an Experimental launch. Previews are the first launch stage used to get feedback from customers.

`PUBLIC_PREVIEW`

Used to indicate the PublisherModel is at Public Preview launch stage, available to all customers, although not supported for production workloads.

`GA`

Used to indicate the PublisherModel is at GA launch stage, available to all customers and ready for production workload.

## VersionState

An enum representing the state of the PublicModelVersion.

Enums

`VERSION_STATE_UNSPECIFIED`

The version state is unspecified.

`VERSION_STATE_STABLE`

Used to indicate the version is stable.

`VERSION_STATE_UNSTABLE`

Used to indicate the version is unstable.

## Methods

### `            get           `

Gets a Model Garden publisher model.

### `            list           `

Lists publisher models in Model Garden.
