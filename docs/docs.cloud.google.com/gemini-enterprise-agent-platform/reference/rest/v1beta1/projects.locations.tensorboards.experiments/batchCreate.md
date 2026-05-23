---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments/batchCreate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments/batchCreate
title: 'Method: experiments.batchCreate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.batchCreate

Batch create TensorboardTimeSeries that belong to a TensorboardExperiment.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent}:batchCreate`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the TensorboardExperiment to create the TensorboardTimeSeries in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}` The TensorboardRuns referenced by the parent fields in the CreateTensorboardTimeSeriesRequest messages must be sub resources of this TensorboardExperiment.

### Request body

The request body contains data with the following structure:

Fields

`requests[]` ` object ( CreateTensorboardTimeSeriesRequest  ` )

Required. The request message specifying the TensorboardTimeSeries to create. A maximum of 1000 TensorboardTimeSeries can be created in a batch.

### Response body

Response message for `  TensorboardService.BatchCreateTensorboardTimeSeries  ` .

If successful, the response body contains data with the following structure:

Fields

`tensorboardTimeSeries[]` ` object ( TensorboardTimeSeries  ` )

The created TensorboardTimeSeries.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tensorboardTimeSeries&quot;: [{object (TensorboardTimeSeries)}]}</code></pre></td>
</tr>
</tbody>
</table>

## CreateTensorboardTimeSeriesRequest

Request message for `  TensorboardService.CreateTensorboardTimeSeries  ` .

Fields

`parent` `string`

Required. The resource name of the TensorboardRun to create the TensorboardTimeSeries in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`

`tensorboardTimeSeriesId` `string`

Optional. The user specified unique id to use for the TensorboardTimeSeries, which becomes the final component of the TensorboardTimeSeries's resource name. This value should match "\[a-z0-9\]\[a-z0-9-\]{0, 127}"

`tensorboardTimeSeries` ` object ( TensorboardTimeSeries  ` )

Required. The TensorboardTimeSeries to create.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;tensorboardTimeSeriesId&quot;: string,&quot;tensorboardTimeSeries&quot;: {object (TensorboardTimeSeries)}}</code></pre></td>
</tr>
</tbody>
</table>
