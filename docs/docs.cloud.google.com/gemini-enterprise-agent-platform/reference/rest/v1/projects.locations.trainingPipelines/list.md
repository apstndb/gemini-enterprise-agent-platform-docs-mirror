---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/list
title: 'Method: trainingPipelines.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.trainingPipelines.list

Lists TrainingPipelines in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /trainingPipelines`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the TrainingPipelines from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

The standard list filter.

Supported fields:

  - `displayName` supports `=` , `!=` comparisons, and `:` wildcard.
  - `state` supports `=` , `!=` comparisons.
  - `trainingTaskDefinition` `=` , `!=` comparisons, and `:` wildcard.
  - `createTime` supports `=` , `!=` , `<` , `<=` , `>` , `>=` comparisons. `createTime` must be in RFC 3339 format.
  - `labels` supports general map functions that is: `labels.key=value` - key:value equality \`labels.key:\* - key existence

Some examples of using the filter are:

  - `state="PIPELINE_STATE_SUCCEEDED" AND displayName:"my_pipeline_*"`
  - `state!="PIPELINE_STATE_FAILED" OR displayName="my_pipeline"`
  - `NOT displayName="my_pipeline"`
  - `createTime>"2021-05-18T00:00:00Z"`
  - `trainingTaskDefinition:"*automlTextClassification*"`

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained via `  ListTrainingPipelinesResponse.next_page_token  ` of the previous `  PipelineService.ListTrainingPipelines  ` call.

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for `  PipelineService.ListTrainingPipelines  `

If successful, the response body contains data with the following structure:

Fields

`trainingPipelines[]` ` object ( TrainingPipeline  ` )

List of TrainingPipelines in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListTrainingPipelinesRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trainingPipelines&quot;: [{object (TrainingPipeline)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
