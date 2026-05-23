---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess
title: 'Method: datasets.assess'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.assess

Assesses the state or validity of the dataset with respect to a given use case.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:assess`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the Dataset resource. Used only for MULTIMODAL datasets. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

### Request body

The request body contains data with the following structure:

Fields

`geminiRequestReadConfig` ` object ( GeminiRequestReadConfig  ` )

Optional. The Gemini request read config for the dataset.

`assessment_config` `Union type`

The assessment type. `assessment_config` can be only one of the following:

`tuningValidationAssessmentConfig` ` object ( TuningValidationAssessmentConfig  ` )

Optional. Configuration for the tuning validation assessment.

`tuningResourceUsageAssessmentConfig` ` object ( TuningResourceUsageAssessmentConfig  ` )

Optional. Configuration for the tuning resource usage assessment.

`batchPredictionValidationAssessmentConfig` ` object ( BatchPredictionValidationAssessmentConfig  ` )

Optional. Configuration for the batch prediction validation assessment.

`batchPredictionResourceUsageAssessmentConfig` ` object ( BatchPredictionResourceUsageAssessmentConfig  ` )

Optional. Configuration for the batch prediction resource usage assessment.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

## TuningValidationAssessmentConfig

Configuration for the tuning validation assessment.

Fields

`modelName` `string`

Required. The name of the model used for tuning.

`datasetUsage` ` enum ( DatasetUsage  ` )

Required. The dataset usage (e.g. training/validation).

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelName&quot;: string,&quot;datasetUsage&quot;: enum (DatasetUsage)}</code></pre></td>
</tr>
</tbody>
</table>

## DatasetUsage

The dataset usage (e.g. training/validation).

Enums

`DATASET_USAGE_UNSPECIFIED`

Default value. Should not be used.

`SFT_TRAINING`

Supervised fine-tuning training dataset.

`SFT_VALIDATION`

Supervised fine-tuning validation dataset.

## TuningResourceUsageAssessmentConfig

Configuration for the tuning resource usage assessment.

Fields

`modelName` `string`

Required. The name of the model used for tuning.

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
  &quot;modelName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## BatchPredictionValidationAssessmentConfig

Configuration for the batch prediction validation assessment.

Fields

`modelName` `string`

Required. The name of the model used for batch prediction.

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
  &quot;modelName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## BatchPredictionResourceUsageAssessmentConfig

Configuration for the batch prediction resource usage assessment.

Fields

`modelName` `string`

Required. The name of the model used for batch prediction.

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
  &quot;modelName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
