---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs.timeSeries/readBlobData
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs.timeSeries/readBlobData
title: 'Method: timeSeries.readBlobData'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.runs.timeSeries.readBlobData

Gets bytes of TensorboardBlobs. This is to allow reading blob data stored in consumer project's Cloud Storage bucket without users having to obtain Cloud Storage access permission.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{timeSeries}:readBlobData`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`timeSeries` `string`

Required. The resource name of the TensorboardTimeSeries to list Blobs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{timeSeries}`

### Query parameters

`blobIds[]` `string`

IDs of the blobs to read.

### Request body

The request body must be empty.

### Response body

Response message for `  TensorboardService.ReadTensorboardBlobData  ` .

If successful, the response body contains data with the following structure:

Fields

`blobs[]` ` object ( TensorboardBlob  ` )

blob messages containing blob bytes.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;blobs&quot;: [{object (TensorboardBlob)}]}</code></pre></td>
</tr>
</tbody>
</table>
