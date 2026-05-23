---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/readUsage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/readUsage
title: 'Method: tensorboards.readUsage'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.readUsage

Returns a list of monthly active users for a given TensorBoard instance.

### Endpoint

get `https: / /{service-endpoint} /v1 /{tensorboard}:readUsage`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`tensorboard` `string`

Required. The name of the Tensorboard resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`

### Request body

The request body must be empty.

### Response body

Response message for `  TensorboardService.ReadTensorboardUsage  ` .

If successful, the response body contains data with the following structure:

Fields

`monthlyUsageData` ` map (key: string, value: object ( PerMonthUsageData  ` ))

Maps year-month (YYYYMM) string to per month usage data.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;monthlyUsageData&quot;: {string: {object (PerMonthUsageData)},...}}</code></pre></td>
</tr>
</tbody>
</table>

## PerMonthUsageData

Per month usage data

Fields

`userUsageData[]` ` object ( PerUserUsageData  ` )

Usage data for each user in the given month.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;userUsageData&quot;: [{object (PerUserUsageData)}]}</code></pre></td>
</tr>
</tbody>
</table>

## PerUserUsageData

Per user usage data.

Fields

`username` `string`

user's username

`viewCount` `string ( int64 format)`

Number of times the user has read data within the Tensorboard.

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
  &quot;username&quot;: string,
  &quot;viewCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
