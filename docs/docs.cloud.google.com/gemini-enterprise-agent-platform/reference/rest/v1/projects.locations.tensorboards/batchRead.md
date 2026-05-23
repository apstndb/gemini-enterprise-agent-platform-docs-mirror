---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/batchRead
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/batchRead
title: 'Method: tensorboards.batchRead'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.batchRead

Reads multiple TensorboardTimeSeries' data. The data point number limit is 1000 for scalars, 100 for tensors and blob references. If the number of data points stored is less than the limit, all data is returned. Otherwise, the number limit of data points is randomly selected from this time series and returned.

### Endpoint

get `https: / /{service-endpoint} /v1 /{tensorboard}:batchRead`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`tensorboard` `string`

Required. The resource name of the Tensorboard containing TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}` . The TensorboardTimeSeries referenced by `  timeSeries  ` must be sub resources of this Tensorboard.

### Query parameters

`timeSeries[]` `string`

Required. The resource names of the TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{timeSeries}`

### Request body

The request body must be empty.

### Response body

Response message for `  TensorboardService.BatchReadTensorboardTimeSeriesData  ` .

If successful, the response body contains data with the following structure:

Fields

`timeSeriesData[]` ` object ( TimeSeriesData  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;timeSeriesData&quot;: [{object (TimeSeriesData)}]}</code></pre></td>
</tr>
</tbody>
</table>
