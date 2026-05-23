---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/list
title: 'Method: tuningJobs.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tuningJobs.list

Lists tuning jobs in a location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /tuningJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the location to list the tuning jobs from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Optional. The standard list filter.

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token.

Typically obtained from `  ListTuningJobsResponse.next_page_token  ` of the previous `  GenAiTuningService.ListTuningJobs  ` call.

### Request body

The request body must be empty.

### Response body

Response message for `  GenAiTuningService.ListTuningJobs  `

If successful, the response body contains data with the following structure:

Fields

`tuningJobs[]` ` object ( TuningJob  ` )

The tuning jobs that match the request.

`nextPageToken` `string`

A token to retrieve the next page of results.

Pass this token in a subsequent \[GenAiTuningService.ListTuningJobs\] call to retrieve the next page of results.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tuningJobs&quot;: [{object (TuningJob)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
