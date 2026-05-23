---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs.timeSeries/exportTensorboardTimeSeries
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs.timeSeries/exportTensorboardTimeSeries
title: 'Method: timeSeries.exportTensorboardTimeSeries'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.runs.timeSeries.exportTensorboardTimeSeries

Exports a TensorboardTimeSeries' data. data is returned in paginated responses.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{tensorboardTimeSeries}:exportTensorboardTimeSeries`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`tensorboardTimeSeries` `string`

Required. The resource name of the TensorboardTimeSeries to export data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{timeSeries}`

### Request body

The request body contains data with the following structure:

Fields

`filter` `string`

Exports the TensorboardTimeSeries' data that match the filter expression.

`pageSize` `integer`

The maximum number of data points to return per page. The default pageSize is 1000. Values must be between 1 and 10000. Values above 10000 are coerced to 10000.

`pageToken` `string`

A page token, received from a previous `  timeSeries.exportTensorboardTimeSeries  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  timeSeries.exportTensorboardTimeSeries  ` must match the call that provided the page token.

`orderBy` `string`

Field to use to sort the TensorboardTimeSeries' data. By default, TensorboardTimeSeries' data is returned in a pseudo random order.

### Response body

Response message for `  TensorboardService.ExportTensorboardTimeSeriesData  ` .

If successful, the response body contains data with the following structure:

Fields

`timeSeriesDataPoints[]` ` object ( TimeSeriesDataPoint  ` )

The returned time series data points.

`nextPageToken` `string`

A token, which can be sent as `  pageToken  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;timeSeriesDataPoints&quot;: [{object (TimeSeriesDataPoint)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
