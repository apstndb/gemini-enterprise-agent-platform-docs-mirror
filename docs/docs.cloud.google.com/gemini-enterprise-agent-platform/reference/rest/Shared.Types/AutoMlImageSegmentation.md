---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AutoMlImageSegmentation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AutoMlImageSegmentation
title: AutoMlImageSegmentation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

Fields

`inputs` ` object ( AutoMlImageSegmentationInputs  ` )

The input parameters of this TrainingJob.

`metadata` ` object ( AutoMlImageSegmentationMetadata  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputs&quot;: {object (AutoMlImageSegmentationInputs)},&quot;metadata&quot;: {object (AutoMlImageSegmentationMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

## AutoMlImageSegmentationInputs

Fields

`modelType` `enum ( ModelType` )

`budgetMilliNodeHours` `string ( int64 format)`

The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node\_hour = actual\_hour \* number\_of\_nodes\_involved. Or actual\_wall\_clock\_hours = trainBudgetMilliNodeHours / (number\_of\_nodes\_involved \* 1000) For modelType `cloud-high-accuracy-1` (default), the budget must be between 20,000 and 2,000,000 milli node hours, inclusive. The default value is 192,000 which represents one day in wall time (1000 milli \* 24 hours \* 8 nodes).

`baseModelId` `string`

The id of the `base` model. If it is specified, the new model will be trained based on the `base` model. Otherwise, the new model will be trained from scratch. The `base` model must be in the same Project and Location as the new Model to train, and have the same modelType.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelType&quot;: enum (ModelType),&quot;budgetMilliNodeHours&quot;: string,&quot;baseModelId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## AutoMlImageSegmentationMetadata

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
