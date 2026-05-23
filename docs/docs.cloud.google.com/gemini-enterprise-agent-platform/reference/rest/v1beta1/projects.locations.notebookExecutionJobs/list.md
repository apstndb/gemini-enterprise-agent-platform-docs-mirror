---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookExecutionJobs/list
title: 'Method: notebookExecutionJobs.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.notebookExecutionJobs.list

Lists NotebookExecutionJobs in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /notebookExecutionJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to list the NotebookExecutionJobs. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Optional. An expression for filtering the results of the request. For field names both snake\_case and camelCase are supported.

  - `notebookExecutionJob` supports = and \!=. `notebookExecutionJob` represents the NotebookExecutionJob id.
  - `displayName` supports = and \!= and regex.
  - `schedule` supports = and \!= and regex.

Some examples: \* `notebookExecutionJob="123"` \* `notebookExecutionJob="my-execution-job"` \* `displayName="myDisplayName"` and `displayName=~"myDisplayNameRegex"`

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via `  ListNotebookExecutionJobsResponse.next_page_token  ` of the previous `  NotebookService.ListNotebookExecutionJobs  ` call.

`orderBy` `string`

Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields:

  - `displayName`
  - `createTime`
  - `updateTime`

Example: `displayName, createTime desc` .

`view` ` enum ( NotebookExecutionJobView  ` )

Optional. The NotebookExecutionJob view. Defaults to BASIC.

### Request body

The request body must be empty.

### Response body

Response message for \[NotebookService.CreateNotebookExecutionJob\]

If successful, the response body contains data with the following structure:

Fields

`notebookExecutionJobs[]` ` object ( NotebookExecutionJob  ` )

List of NotebookExecutionJobs in the requested page.

`nextPageToken` `string`

A token to retrieve next page of results. Pass to `  ListNotebookExecutionJobsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;notebookExecutionJobs&quot;: [{object (NotebookExecutionJob)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
