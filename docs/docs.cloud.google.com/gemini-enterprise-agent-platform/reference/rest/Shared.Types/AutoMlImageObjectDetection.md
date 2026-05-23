---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AutoMlImageObjectDetection
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AutoMlImageObjectDetection
title: AutoMlImageObjectDetection
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

Fields

`inputs` ` object ( AutoMlImageObjectDetectionInputs  ` )

The input parameters of this TrainingJob.

`metadata` ` object ( AutoMlImageObjectDetectionMetadata  ` )

The metadata information

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputs&quot;: {object (AutoMlImageObjectDetectionInputs)},&quot;metadata&quot;: {object (AutoMlImageObjectDetectionMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

## AutoMlImageObjectDetectionInputs

Fields

`modelType` `enum ( ModelType` )

`budgetMilliNodeHours` `string ( int64 format)`

The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node\_hour = actual\_hour \* number\_of\_nodes\_involved. For modelType `cloud` (default), the budget must be between 20,000 and 900,000 milli node hours, inclusive. The default value is 216,000 which represents one day in wall time, considering 9 nodes are used. For model types `mobile-tf-low-latency-1` , `mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` the training budget must be between 1,000 and 100,000 milli node hours, inclusive. The default value is 24,000 which represents one day in wall time on a single node that is used.

`disableEarlyStopping` `boolean`

Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelType&quot;: enum (ModelType),&quot;budgetMilliNodeHours&quot;: string,&quot;disableEarlyStopping&quot;: boolean,&quot;uptrainBaseModelId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## AutoMlImageObjectDetectionMetadata

Fields

`costMilliNodeHours` `string ( int64 format)`

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

`successfulStopReason` `enum ( SuccessfulStopReason` )

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
