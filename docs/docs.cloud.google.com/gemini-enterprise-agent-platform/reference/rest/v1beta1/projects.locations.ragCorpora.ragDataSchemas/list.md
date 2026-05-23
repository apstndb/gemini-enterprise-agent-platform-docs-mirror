---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas/list
title: 'Method: ragDataSchemas.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.ragDataSchemas.list

Lists RagDataSchemas in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /ragDataSchemas`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the RagCorpus from which to list the RagDataSchemas. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

### Query parameters

`pageSize` `integer`

Optional. The standard list page size. The maximum value is 100. If not specified, a default value of 100 will be used.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via `  ListRagDataSchemasResponse.next_page_token  ` of the previous `  VertexRagDataService.ListRagDataSchemas  ` call.

### Request body

The request body must be empty.

### Response body

Response message for `  VertexRagDataService.ListRagDataSchemas  ` .

If successful, the response body contains data with the following structure:

Fields

`ragDataSchemas[]` ` object ( RagDataSchema  ` )

List of RagDataSchemas in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListRagDataSchemasRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragDataSchemas&quot;: [{object (RagDataSchema)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
