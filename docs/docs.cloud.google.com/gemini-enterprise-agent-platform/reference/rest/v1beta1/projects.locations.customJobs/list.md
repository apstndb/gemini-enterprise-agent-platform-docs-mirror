---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.customJobs/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.customJobs/list
title: 'Method: customJobs.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.customJobs.list

Lists CustomJobs in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /customJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the CustomJobs from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

The standard list filter.

Supported fields:

  - `displayName` supports `=` , `!=` comparisons, and `:` wildcard.
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

The standard list page token. Typically obtained via `  ListCustomJobsResponse.next_page_token  ` of the previous `  JobService.ListCustomJobs  ` call.

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for `  JobService.ListCustomJobs  `

If successful, the response body contains data with the following structure:

Fields

`customJobs[]` ` object ( CustomJob  ` )

List of CustomJobs in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListCustomJobsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;customJobs&quot;: [{object (CustomJob)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
