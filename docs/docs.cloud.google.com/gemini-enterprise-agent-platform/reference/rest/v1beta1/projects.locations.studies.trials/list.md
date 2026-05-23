---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials/list
title: 'Method: trials.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.trials.list

Lists the Trials associated with a Study.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /trials`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Study to list the Trial from. Format: `projects/{project}/locations/{location}/studies/{study}`

### Query parameters

`pageToken` `string`

Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages.

`pageSize` `integer`

Optional. The number of Trials to retrieve per "page" of results. If unspecified, the service will pick an appropriate default.

### Request body

The request body must be empty.

### Response body

Response message for `  VizierService.ListTrials  ` .

If successful, the response body contains data with the following structure:

Fields

`trials[]` ` object ( Trial  ` )

The Trials associated with the Study.

`nextPageToken` `string`

Pass this token as the `pageToken` field of the request for a subsequent call. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trials&quot;: [{object (Trial)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
