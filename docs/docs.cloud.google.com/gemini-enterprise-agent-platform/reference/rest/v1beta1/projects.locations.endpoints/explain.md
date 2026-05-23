---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/explain
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/explain
title: 'Method: endpoints.explain'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.explain

Perform an online explanation.

If `  deployedModelId  ` is specified, the corresponding endpoints.deployModel must have `  explanationSpec  ` populated. If `  deployedModelId  ` is not specified, all DeployedModels must have `  explanationSpec  ` populated.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint}:explain`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint requested to serve the explanation. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains data with the following structure:

Fields

`instances[]` ` value ( Value  ` format)

Required. The instances that are the input to the explanation call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the explanation call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' `  Model's  ` `  PredictSchemata's  ` `  instanceSchemaUri  ` .

`parameters` ` value ( Value  ` format)

The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' `  Model's  ` `  PredictSchemata's  ` `  parametersSchemaUri  ` .

`explanationSpecOverride` ` object ( ExplanationSpecOverride  ` )

If specified, overrides the `  explanationSpec  ` of the DeployedModel. Can be used for explaining prediction results with different configurations, such as: - Explaining top-5 predictions results as opposed to top-1; - Increasing path count or step count of the attribution methods to reduce approximate errors; - Using different baselines for explaining the prediction results.

`concurrentExplanationSpecOverride` ` map (key: string, value: object ( ExplanationSpecOverride  ` ))

Optional. This field is the same as the one above, but supports multiple explanations to occur in parallel. The key can be any string. Each override will be run against the model, then its explanations will be grouped together.

Note - these explanations are run **In Addition** to the default Explanation in the deployed model.

`deployedModelId` `string`

If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding `  Endpoint.traffic_split  ` .

### Response body

Response message for `  PredictionService.Explain  ` .

If successful, the response body contains data with the following structure:

Fields

`explanations[]` ` object ( Explanation  ` )

The explanations of the Model's `  PredictResponse.predictions  ` .

It has the same number of elements as `  instances  ` to be explained.

`concurrentExplanations` ` map (key: string, value: object ( ConcurrentExplanation  ` ))

This field stores the results of the explanations run in parallel with The default explanation strategy/method.

`deployedModelId` `string`

id of the Endpoint's DeployedModel that served this explanation.

`predictions[]` ` value ( Value  ` format)

The predictions that are the output of the predictions call. Same as `  PredictResponse.predictions  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanations&quot;: [{object (Explanation)}],&quot;concurrentExplanations&quot;: {string: {object (ConcurrentExplanation)},...},&quot;deployedModelId&quot;: string,&quot;predictions&quot;: [value]}</code></pre></td>
</tr>
</tbody>
</table>

## ExplanationSpecOverride

The `  ExplanationSpec  ` entries that can be overridden at `  online explanation  ` time.

Fields

`parameters` ` object ( ExplanationParameters  ` )

The parameters to be overridden. Note that the attribution method cannot be changed. If not specified, no parameter is overridden.

`metadata` ` object ( ExplanationMetadataOverride  ` )

The metadata to be overridden. If not specified, no metadata is overridden.

`examplesOverride` ` object ( ExamplesOverride  ` )

The example-based explanations parameter overrides.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parameters&quot;: {object (ExplanationParameters)},&quot;metadata&quot;: {object (ExplanationMetadataOverride)},&quot;examplesOverride&quot;: {object (ExamplesOverride)}}</code></pre></td>
</tr>
</tbody>
</table>

## ExplanationMetadataOverride

The `  ExplanationMetadata  ` entries that can be overridden at `  online explanation  ` time.

Fields

`inputs` ` map (key: string, value: object ( InputMetadataOverride  ` ))

Required. Overrides the `  input metadata  ` of the features. The key is the name of the feature to be overridden. The keys specified here must exist in the input metadata to be overridden. If a feature is not specified here, the corresponding feature's input metadata is not overridden.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputs&quot;: {string: {object (InputMetadataOverride)},...}}</code></pre></td>
</tr>
</tbody>
</table>

## InputMetadataOverride

The `  input metadata  ` entries to be overridden.

Fields

`inputBaselines[]` ` value ( Value  ` format)

baseline inputs for this feature.

This overrides the `input_baseline` field of the `  ExplanationMetadata.InputMetadata  ` object of the corresponding feature's input metadata. If it's not specified, the original baselines are not overridden.

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
  &quot;inputBaselines&quot;: [
    value
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## ExamplesOverride

Overrides for example-based explanations.

Fields

`neighborCount` `integer`

The number of neighbors to return.

`crowdingCount` `integer`

The number of neighbors to return that have the same crowding tag.

`restrictions[]` ` object ( ExamplesRestrictionsNamespace  ` )

Restrict the resulting nearest neighbors to respect these constraints.

`returnEmbeddings` `boolean`

If true, return the embeddings instead of neighbors.

`dataFormat` ` enum ( DataFormat  ` )

The format of the data being provided with each call.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;neighborCount&quot;: integer,&quot;crowdingCount&quot;: integer,&quot;restrictions&quot;: [{object (ExamplesRestrictionsNamespace)}],&quot;returnEmbeddings&quot;: boolean,&quot;dataFormat&quot;: enum (DataFormat)}</code></pre></td>
</tr>
</tbody>
</table>

## ExamplesRestrictionsNamespace

Restrictions namespace for example-based explanations overrides.

Fields

`namespaceName` `string`

The namespace name.

`allow[]` `string`

The list of allowed tags.

`deny[]` `string`

The list of deny tags.

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
  &quot;namespaceName&quot;: string,
  &quot;allow&quot;: [
    string
  ],
  &quot;deny&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## DataFormat

data format enum.

Enums

`DATA_FORMAT_UNSPECIFIED`

Unspecified format. Must not be used.

`INSTANCES`

Provided data is a set of model inputs.

`EMBEDDINGS`

Provided data is a set of embeddings.

## ConcurrentExplanation

This message is a wrapper grouping Concurrent Explanations.

Fields

`explanations[]` ` object ( Explanation  ` )

The explanations of the Model's `  PredictResponse.predictions  ` .

It has the same number of elements as `  instances  ` to be explained.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanations&quot;: [{object (Explanation)}]}</code></pre></td>
</tr>
</tbody>
</table>
