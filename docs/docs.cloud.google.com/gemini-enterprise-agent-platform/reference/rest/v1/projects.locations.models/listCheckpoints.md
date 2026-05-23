---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/listCheckpoints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/listCheckpoints
title: 'Method: models.listCheckpoints'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.listCheckpoints

Lists checkpoints of the specified model version.

### Endpoint

get `https: / /{service-endpoint} /v1 /{name}:listCheckpoints`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the model version to list checkpoints for. `projects/{project}/locations/{location}/models/{model}@{version}` Example: `projects/{project}/locations/{location}/models/{model}@2` or `projects/{project}/locations/{location}/models/{model}@golden` If no version id or alias is specified, the latest version will be used.

### Query parameters

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via `  nextPageToken  ` of the previous `  models.listCheckpoints  ` call.

### Request body

The request body must be empty.

### Response body

Response message for `  ModelService.ListModelVersionCheckpoints  `

If successful, the response body contains data with the following structure:

Fields

`checkpoints[]` ` object ( ModelVersionCheckpoint  ` )

List of Model version checkpoints.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListModelVersionCheckpointsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;checkpoints&quot;: [{object (ModelVersionCheckpoint)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## ModelVersionCheckpoint

> This item is deprecated\!

Describes the machine learning model version checkpoint.

Fields

`checkpointId` `string`

The id of the checkpoint.

`epoch` `string ( int64 format)`

The epoch of the checkpoint.

`step` `string ( int64 format)`

The step of the checkpoint.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;checkpointId&quot;: string,
  &quot;epoch&quot;: string,
  &quot;step&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
