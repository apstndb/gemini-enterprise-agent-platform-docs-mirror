---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.cachedContents/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.cachedContents/list
title: 'Method: cachedContents.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.cachedContents.list

Lists cached contents in a project

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /cachedContents`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent, which owns this collection of cached contents.

### Query parameters

`pageSize` `integer`

Optional. The maximum number of cached contents to return. The service may return fewer than this value. If unspecified, some default (under maximum) number of items will be returned. The maximum value is 1000; values above 1000 will be coerced to 1000.

`pageToken` `string`

Optional. A page token, received from a previous `cachedContents.list` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `cachedContents.list` must match the call that provided the page token.

### Request body

The request body must be empty.

### Response body

Response with a list of CachedContents.

If successful, the response body contains data with the following structure:

Fields

`cachedContents[]` ` object ( CachedContent  ` )

List of cached contents.

`nextPageToken` `string`

A token, which can be sent as `pageToken` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;cachedContents&quot;: [{object (CachedContent)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
