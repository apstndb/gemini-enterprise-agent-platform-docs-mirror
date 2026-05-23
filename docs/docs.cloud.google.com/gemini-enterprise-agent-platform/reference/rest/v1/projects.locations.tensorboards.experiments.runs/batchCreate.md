---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/batchCreate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/batchCreate
title: 'Method: runs.batchCreate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.runs.batchCreate

Batch create TensorboardRuns.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /runs:batchCreate`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the TensorboardExperiment to create the TensorboardRuns in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}` The parent field in the CreateTensorboardRunRequest messages must match this field.

### Request body

The request body contains data with the following structure:

Fields

`requests[]` ` object ( CreateTensorboardRunRequest  ` )

Required. The request message specifying the TensorboardRuns to create. A maximum of 1000 TensorboardRuns can be created in a batch.

### Response body

Response message for `  TensorboardService.BatchCreateTensorboardRuns  ` .

If successful, the response body contains data with the following structure:

Fields

`tensorboardRuns[]` ` object ( TensorboardRun  ` )

The created TensorboardRuns.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tensorboardRuns&quot;: [{object (TensorboardRun)}]}</code></pre></td>
</tr>
</tbody>
</table>

## CreateTensorboardRunRequest

Request message for `  TensorboardService.CreateTensorboardRun  ` .

Fields

`parent` `string`

Required. The resource name of the TensorboardExperiment to create the TensorboardRun in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`

`tensorboardRun` ` object ( TensorboardRun  ` )

Required. The TensorboardRun to create.

`tensorboardRunId` `string`

Required. The id to use for the Tensorboard run, which becomes the final component of the Tensorboard run's resource name.

This value should be 1-128 characters, and valid characters are `/[a-z][0-9]-/` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;tensorboardRun&quot;: {object (TensorboardRun)},&quot;tensorboardRunId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
