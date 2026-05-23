---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs/list
title: 'Method: modelMonitoringJobs.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelMonitors.modelMonitoringJobs.list

Lists ModelMonitoringJobs. Callers may choose to read across multiple Monitors as per [AIP-159](https://google.aip.dev/159) by using '-' (the hyphen or dash character) as a wildcard character instead of modelMonitor id in the parent. Format `projects/{projectId}/locations/{location}/moodelMonitors/-/modelMonitoringJobs`

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /modelMonitoringJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent of the ModelMonitoringJob. Format: `projects/{project}/locations/{location}/modelMonitors/{modelMonitor}`

### Query parameters

`filter` `string`

The standard list filter. More detail in [AIP-160](https://google.aip.dev/160) .

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token.

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for `  ModelMonitoringService.ListModelMonitoringJobs  ` .

If successful, the response body contains data with the following structure:

Fields

`modelMonitoringJobs[]` ` object ( ModelMonitoringJob  ` )

A list of ModelMonitoringJobs that matches the specified filter in the request.

`nextPageToken` `string`

The standard List next-page token.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelMonitoringJobs&quot;: [{object (ModelMonitoringJob)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
