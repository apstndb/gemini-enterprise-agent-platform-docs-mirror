---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/list
title: 'Method: studies.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.list

Lists all the studies in a region for an associated project.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /studies`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the Study from. Format: `projects/{project}/locations/{location}`

### Query parameters

`pageToken` `string`

Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages.

`pageSize` `integer`

Optional. The maximum number of studies to return per "page" of results. If unspecified, service will pick an appropriate default.

### Request body

The request body must be empty.

### Response body

Response message for `  VizierService.ListStudies  ` .

If successful, the response body contains data with the following structure:

Fields

`studies[]` ` object ( Study  ` )

The studies associated with the project.

`nextPageToken` `string`

Passes this token as the `pageToken` field of the request for a subsequent call. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;studies&quot;: [{object (Study)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
