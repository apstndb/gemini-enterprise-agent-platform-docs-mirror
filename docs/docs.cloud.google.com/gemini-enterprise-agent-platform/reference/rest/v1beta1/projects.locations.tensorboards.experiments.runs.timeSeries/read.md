---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs.timeSeries/read
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs.timeSeries/read
title: 'Method: timeSeries.read'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.runs.timeSeries.read

Reads a TensorboardTimeSeries' data. By default, if the number of data points stored is less than 1000, all data is returned. Otherwise, 1000 data points is randomly selected from this time series and returned. This value can be changed by changing maxDataPoints, which can't be greater than 10k.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{tensorboardTimeSeries}:read`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`tensorboardTimeSeries` `string`

Required. The resource name of the TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{timeSeries}`

### Query parameters

`maxDataPoints` `integer`

The maximum number of TensorboardTimeSeries' data to return.

This value should be a positive integer. This value can be set to -1 to return all data.

`filter` `string`

Reads the TensorboardTimeSeries' data that match the filter expression.

### Request body

The request body must be empty.

### Response body

Response message for `  TensorboardService.ReadTensorboardTimeSeriesData  ` .

If successful, the response body contains data with the following structure:

Fields

`timeSeriesData` ` object ( TimeSeriesData  ` )

The returned time series data.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;timeSeriesData&quot;: {object (TimeSeriesData)}}</code></pre></td>
</tr>
</tbody>
</table>
