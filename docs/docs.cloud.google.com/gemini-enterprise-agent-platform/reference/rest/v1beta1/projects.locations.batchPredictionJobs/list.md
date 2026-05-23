---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs/list
title: 'Method: batchPredictionJobs.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.batchPredictionJobs.list

Lists BatchPredictionJobs in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /batchPredictionJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the BatchPredictionJobs from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

The standard list filter.

Supported fields:

  - `displayName` supports `=` , `!=` comparisons, and `:` wildcard.
  - `modelDisplayName` supports `=` , `!=` comparisons.
  - `state` supports `=` , `!=` comparisons.
  - `createTime` supports `=` , `!=` , `<` , `<=` , `>` , `>=` comparisons. `createTime` must be in RFC 3339 format.
  - `labels` supports general map functions that is: `labels.key=value` - key:value equality \`labels.key:\* - key existence

Some examples of using the filter are:

  - `state="JOB_STATE_SUCCEEDED" AND displayName:"my_job_*"`
  - `state!="JOB_STATE_FAILED" OR displayName="my_job"`
  - `NOT displayName="my_job"`
  - `createTime>"2021-05-18T00:00:00Z"`
  - `labels.keyA=valueA`
  - `labels.keyB:*`

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained via `  ListBatchPredictionJobsResponse.next_page_token  ` of the previous `  JobService.ListBatchPredictionJobs  ` call.

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for `  JobService.ListBatchPredictionJobs  `

If successful, the response body contains data with the following structure:

Fields

`batchPredictionJobs[]` ` object ( BatchPredictionJob  ` )

List of BatchPredictionJobs in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListBatchPredictionJobsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;batchPredictionJobs&quot;: [{object (BatchPredictionJob)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
