---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments/write
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments/write
title: 'Method: experiments.write'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.write

Write time series data points of multiple TensorboardTimeSeries in multiple TensorboardRun's. If any data fail to be ingested, an error is returned.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{tensorboardExperiment}:write`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`tensorboardExperiment` `string`

Required. The resource name of the TensorboardExperiment to write data to. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`

### Request body

The request body contains data with the following structure:

Fields

`writeRunDataRequests[]` ` object ( WriteTensorboardRunDataRequest  ` )

Required. Requests containing per-run TensorboardTimeSeries data to write.

### Response body

If successful, the response body is empty.

## WriteTensorboardRunDataRequest

Request message for `  TensorboardService.WriteTensorboardRunData  ` .

Fields

`tensorboardRun` `string`

Required. The resource name of the TensorboardRun to write data to. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`

`timeSeriesData[]` ` object ( TimeSeriesData  ` )

Required. The TensorboardTimeSeries data to write. Values with in a time series are indexed by their step value. Repeated writes to the same step will overwrite the existing value for that step. The upper limit of data points per write request is 5000.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tensorboardRun&quot;: string,&quot;timeSeriesData&quot;: [{object (TimeSeriesData)}]}</code></pre></td>
</tr>
</tbody>
</table>
