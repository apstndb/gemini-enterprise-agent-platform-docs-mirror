---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/searchExamples
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/searchExamples
title: 'Method: exampleStores.searchExamples'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.exampleStores.searchExamples

Search for similar Examples for given selection criteria.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{exampleStore}:searchExamples`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`exampleStore` `string`

Required. The name of the ExampleStore resource that examples are retrieved from. Format: `projects/{project}/locations/{location}/exampleStores/{exampleStore}`

### Request body

The request body contains data with the following structure:

Fields

`topK` `string ( int64 format)`

Optional. The number of similar examples to return.

`parameters` `Union type`

The parameters to search for similar examples. This includes which value to use for similarity search and the filters that should be applied to the search. Filters limit which examples are considered as candidates for similarity search. `parameters` can be only one of the following:

`storedContentsExampleParameters` ` object ( StoredContentsExampleParameters  ` )

The parameters of StoredContentsExamples to be searched.

### Response body

Response message for `  ExampleStoreService.SearchExamples  ` .

If successful, the response body contains data with the following structure:

Fields

`results[]` ` object ( SimilarExample  ` )

The results of searching for similar examples.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;results&quot;: [{object (SimilarExample)}]}</code></pre></td>
</tr>
</tbody>
</table>

## StoredContentsExampleParameters

The metadata filters that will be used to search StoredContentsExamples. If a field is unspecified, then no filtering for that field will be applied

Fields

`functionNames` ` object ( ExamplesArrayFilter  ` )

Optional. The function names for filtering.

`query` `Union type`

The query to use to retrieve similar StoredContentsExamples. `query` can be only one of the following:

`searchKey` `string`

The exact search key to use for retrieval.

`contentSearchKey` ` object ( ContentSearchKey  ` )

The chat history to use to generate the search key for retrieval.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;functionNames&quot;: {object (ExamplesArrayFilter)},// query&quot;searchKey&quot;: string,&quot;contentSearchKey&quot;: {object (ContentSearchKey)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ContentSearchKey

The chat history to use to generate the search key for retrieval.

Fields

`contents[]` ` object ( Content  ` )

Required. The conversation for generating a search key.

`searchKeyGenerationMethod` ` object ( SearchKeyGenerationMethod  ` )

Required. The method of generating a search key.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contents&quot;: [{object (Content)}],&quot;searchKeyGenerationMethod&quot;: {object (SearchKeyGenerationMethod)}}</code></pre></td>
</tr>
</tbody>
</table>

## SimilarExample

The result of the similar example.

Fields

`example` ` object ( Example  ` )

The example that is similar to the searched query.

`similarityScore` `number`

The similarity score of this example.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;example&quot;: {object (Example)},&quot;similarityScore&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>
