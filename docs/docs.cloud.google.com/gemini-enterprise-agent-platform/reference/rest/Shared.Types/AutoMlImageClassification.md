---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AutoMlImageClassification
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AutoMlImageClassification
title: AutoMlImageClassification
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A TrainingJob that trains and uploads an AutoML Image Classification Model.

Fields

`inputs` ` object ( AutoMlImageClassificationInputs  ` )

The input parameters of this TrainingJob.

`metadata` ` object ( AutoMlImageClassificationMetadata  ` )

The metadata information.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputs&quot;: {object (AutoMlImageClassificationInputs)},&quot;metadata&quot;: {object (AutoMlImageClassificationMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

## AutoMlImageClassificationInputs

Fields

`modelType` ` enum ( ModelType  ` )

`baseModelId` `string`

The id of the `base` model. If it is specified, the new model will be trained based on the `base` model. Otherwise, the new model will be trained from scratch. The `base` model must be in the same Project and Location as the new Model to train, and have the same modelType.

`budgetMilliNodeHours` `string ( int64 format)`

The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node\_hour = actual\_hour \* number\_of\_nodes\_involved. For modelType `cloud` (default), the budget must be between 8,000 and 800,000 milli node hours, inclusive. The default value is 192,000 which represents one day in wall time, considering 8 nodes are used. For model types `mobile-tf-low-latency-1` , `mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` , the training budget must be between 1,000 and 100,000 milli node hours, inclusive. The default value is 24,000 which represents one day in wall time on a single node that is used.

`disableEarlyStopping` `boolean`

Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Classification might stop training before the entire training budget has been used.

`multiLabel` `boolean`

If false, a single-label (multi-class) Model will be trained (i.e. assuming that for each image just up to one annotation may be applicable). If true, a multi-label Model will be trained (i.e. assuming that for each image multiple annotations may be applicable).

`uptrainBaseModelId` `string`

The id of `base` model for upTraining. If it is specified, the new model will be upTrained based on the `base` model for upTraining. Otherwise, the new model will be trained from scratch. The `base` model for upTraining must be in the same Project and Location as the new Model to train, and have the same modelType.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelType&quot;: enum (ModelType),&quot;baseModelId&quot;: string,&quot;budgetMilliNodeHours&quot;: string,&quot;disableEarlyStopping&quot;: boolean,&quot;multiLabel&quot;: boolean,&quot;uptrainBaseModelId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## AutoMlImageClassificationMetadata

Fields

`costMilliNodeHours` `string ( int64 format)`

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

`successfulStopReason` ` enum ( SuccessfulStopReason  ` )

For successful job completions, this is the reason why the job has finished.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;costMilliNodeHours&quot;: string,&quot;successfulStopReason&quot;: enum (SuccessfulStopReason)}</code></pre></td>
</tr>
</tbody>
</table>
