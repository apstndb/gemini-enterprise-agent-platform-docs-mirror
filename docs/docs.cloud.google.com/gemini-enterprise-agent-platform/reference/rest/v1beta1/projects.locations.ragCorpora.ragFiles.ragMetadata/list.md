---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/list
title: 'Method: ragMetadata.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.ragCorpora.ragFiles.ragMetadata.list

Lists RagMetadata in a RagFile.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /ragMetadata`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the RagFile from which to list the RagMetadata. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}/ragFiles/{ragFile}`

### Query parameters

`pageSize` `integer`

Optional. The standard list page size. The maximum value is 100. If not specified, a default value of 100 will be used.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via `  ListRagMetadataResponse.next_page_token  ` of the previous `  VertexRagDataService.ListRagMetadata  ` call.

### Request body

The request body must be empty.

### Response body

Response message for `  VertexRagDataService.ListRagMetadata  ` .

If successful, the response body contains data with the following structure:

Fields

`ragMetadata[]` ` object ( RagMetadata  ` )

List of RagMetadata in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListRagMetadataRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragMetadata&quot;: [{object (RagMetadata)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
