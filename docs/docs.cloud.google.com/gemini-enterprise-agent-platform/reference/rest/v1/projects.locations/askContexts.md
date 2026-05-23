---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/askContexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/askContexts
title: 'Method: locations.askContexts'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.askContexts

Agentic Retrieval Ask API for RAG.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent}:askContexts`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .

### Request body

The request body contains data with the following structure:

Fields

`query` ` object ( RagQuery  ` )

Required. Single RAG retrieve query.

`tools[]` ` object ( Tool  ` )

Optional. The tools to use for locations.askContexts.

### Response body

Response message for `  VertexRagService.AskContexts  ` .

If successful, the response body contains data with the following structure:

Fields

`response` `string`

The Retrieval Response.

`contexts` ` object ( RagContexts  ` )

The contexts of the query.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;response&quot;: string,&quot;contexts&quot;: {object (RagContexts)}}</code></pre></td>
</tr>
</tbody>
</table>
