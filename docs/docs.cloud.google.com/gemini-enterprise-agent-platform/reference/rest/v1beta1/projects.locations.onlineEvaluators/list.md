---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.onlineEvaluators/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.onlineEvaluators/list
title: 'Method: onlineEvaluators.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.onlineEvaluators.list

Lists the OnlineEvaluators for the given project and location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /onlineEvaluators`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent resource of the OnlineEvaluators to list. Format: projects/{project}/locations/{location}.

### Query parameters

`pageSize` `integer`

Optional. The maximum number of OnlineEvaluators to return. The service may return fewer than this value. If unspecified, at most 50 OnlineEvaluators will be returned. The maximum value is 100; values above 100 will be coerced to 100. Based on aip.dev/158.

`pageToken` `string`

Optional. A token identifying a page of results the server should return. Based on aip.dev/158.

`filter` `string`

Optional. Standard list filter. Supported fields: \* `createTime` \* `updateTime` \* `agentResource` Example: `createTime>"2026-01-01T00:00:00-04:00"` where the timestamp is in RFC 3339 format) Based on aip.dev/160.

`orderBy` `string`

Optional. A comma-separated list of fields to order by. The default sorting order is ascending. Use "desc" after a field name for descending. Supported fields: \* `createTime` \* `updateTime`

Example: `createTime desc` . Based on aip.dev/132.

### Request body

The request body must be empty.

### Response body

Response message for onlineEvaluators.list.

If successful, the response body contains data with the following structure:

Fields

`onlineEvaluators[]` ` object ( OnlineEvaluator  ` )

A list of OnlineEvaluators matching the request.

`nextPageToken` `string`

A token to retrieve the next page. Absence of this field indicates there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;onlineEvaluators&quot;: [{object (OnlineEvaluator)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
