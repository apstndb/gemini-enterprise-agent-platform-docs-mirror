---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.servingProfiles/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.servingProfiles/list
title: 'Method: servingProfiles.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.servingProfiles.list

Lists ServingProfiles in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /servingProfiles`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the ServingProfiles from. Format: `projects/{project}/locations/{location}`

### Query parameters

`pageSize` `integer`

Optional. The standard list page size. If unspecified, at most 100 ServingProfiles will be returned. The maximum value is 1000; values above 1000 will be coerced to 1000.

`pageToken` `string`

Optional. The standard list page token.

### Request body

The request body must be empty.

### Response body

Response message for `  ServingProfileService.ListServingProfiles  ` .

If successful, the response body contains data with the following structure:

Fields

`servingProfiles[]` ` object ( ServingProfile  ` )

Output only. A list of ServingProfiles.

`nextPageToken` `string`

Output only. A token to retrieve the next page of results.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;servingProfiles&quot;: [{object (ServingProfile)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
