---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/retrieveContexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/retrieveContexts
title: 'Method: locations.retrieveContexts'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.retrieveContexts

Retrieves relevant contexts for a query.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent}:retrieveContexts`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .

### Request body

The request body contains data with the following structure:

Fields

`query` ` object ( RagQuery  ` )

Required. Single RAG retrieve query.

`data_source` `Union type`

Data Source to retrieve contexts. `data_source` can be only one of the following:

`vertexRagStore` ` object ( VertexRagStore  ` )

The data source for Vertex RagStore.

### Response body

Response message for `  VertexRagService.RetrieveContexts  ` .

If successful, the response body contains data with the following structure:

Fields

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contexts&quot;: {object (RagContexts)}}</code></pre></td>
</tr>
</tbody>
</table>

## VertexRagStore

The data source for Vertex RagStore.

Fields

`ragResources[]` ` object ( RagResource  ` )

Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.

` vectorDistanceThreshold (deprecated)  ` `number`

> This item is deprecated\!

Optional. Only return contexts with vector distance smaller than the threshold.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragResources&quot;: [{object (RagResource)}],&quot;vectorDistanceThreshold&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## RagResource

The definition of the Rag resource.

Fields

`ragCorpus` `string`

Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

`ragFileIds[]` `string`

Optional. ragFileId. The files should be in the same ragCorpus set in ragCorpus field.

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
  &quot;ragCorpus&quot;: string,
  &quot;ragFileIds&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>
