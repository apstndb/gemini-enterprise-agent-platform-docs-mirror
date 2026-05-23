---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelDeploymentMonitoringJobs/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelDeploymentMonitoringJobs/list
title: 'Method: modelDeploymentMonitoringJobs.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelDeploymentMonitoringJobs.list

Lists ModelDeploymentMonitoringJobs in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /modelDeploymentMonitoringJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}`

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

The standard list page token.

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for `  JobService.ListModelDeploymentMonitoringJobs  ` .

If successful, the response body contains data with the following structure:

Fields

`modelDeploymentMonitoringJobs[]` ` object ( ModelDeploymentMonitoringJob  ` )

A list of ModelDeploymentMonitoringJobs that matches the specified filter in the request.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelDeploymentMonitoringJobs&quot;: [{object (ModelDeploymentMonitoringJob)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
