---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GroundingMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GroundingMetadata
title: GroundingMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Information about the sources that support the content of a response.

When grounding is enabled, the model returns citations for claims in the response. This object contains the retrieved sources.

Fields

`webSearchQueries[]` `string`

Optional. The web search queries that were used to generate the content. This field is populated only when the grounding source is Google Search.

`imageSearchQueries[]` `string`

Optional. The image search queries that were used to generate the content. This field is populated only when the grounding source is Google Search with the Image Search searchType enabled.

`retrievalQueries[]` `string`

Optional. The queries that were executed by the retrieval tools. This field is populated only when the grounding source is a retrieval tool, such as Agent Platform Search.

`groundingChunks[]` ` object ( GroundingChunk  ` )

A list of supporting references retrieved from the grounding source. This field is populated when the grounding source is Google Search, Agent Platform Search, or Google Maps.

`groundingSupports[]` ` object ( GroundingSupport  ` )

Optional. A list of grounding supports that connect the generated content to the grounding chunks. This field is populated when the grounding source is Google Search or Agent Platform Search.

`sourceFlaggingUris[]` ` object ( SourceFlaggingUri  ` )

Optional. Output only. A list of URIs that can be used to flag a place or review for inappropriate content. This field is populated only when the grounding source is Google Maps.

`searchEntryPoint` ` object ( SearchEntryPoint  ` )

Optional. A web search entry point that can be used to display search results. This field is populated only when the grounding source is Google Search.

`retrievalMetadata` ` object ( RetrievalMetadata  ` )

Optional. Output only. metadata related to the retrieval grounding source.

` googleMapsWidgetContextToken (deprecated)  ` `string`

> This item is deprecated\!

Optional. Output only. Deprecated: The Google Maps contextual widget behavior in Grounding with Google Maps is being deprecated; this field is planned for removal and will no longer be populated once removed.

A token that can be used to render a Google Maps widget with the contextual data. This field is populated only when the grounding source is Google Maps.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;webSearchQueries&quot;: [string],&quot;imageSearchQueries&quot;: [string],&quot;retrievalQueries&quot;: [string],&quot;groundingChunks&quot;: [{object (GroundingChunk)}],&quot;groundingSupports&quot;: [{object (GroundingSupport)}],&quot;sourceFlaggingUris&quot;: [{object (SourceFlaggingUri)}],&quot;searchEntryPoint&quot;: {object (SearchEntryPoint)},&quot;retrievalMetadata&quot;: {object (RetrievalMetadata)},&quot;googleMapsWidgetContextToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## SearchEntryPoint

An entry point for displaying Google Search results.

A `SearchEntryPoint` is populated when the grounding source for a model's response is Google Search. It provides information that you can use to display the search results in your application.

Fields

`renderedContent` `string`

Optional. An HTML snippet that can be embedded in a web page or an application's webview. This snippet displays a search result, including the title, URL, and a brief description of the search result.

`sdkBlob` `string ( bytes format)`

Optional. A base64-encoded JSON object that contains a list of search queries and their corresponding search URLs. This information can be used to build a custom search UI.

A base64-encoded string.

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
  &quot;renderedContent&quot;: string,
  &quot;sdkBlob&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## GroundingChunk

A piece of evidence that supports a claim made by the model.

This is used to show a citation for a claim made by the model. When grounding is enabled, the model returns a `GroundingChunk` that contains a reference to the source of the information.

Fields

`chunk_type` `Union type`

The source of the grounding chunk, which can be from Google Search, Agent Platform Search, or Google Maps. `chunk_type` can be only one of the following:

`web` ` object ( Web  ` )

A grounding chunk from a web page, typically from Google Search. See the `Web` message for details.

`retrievedContext` ` object ( RetrievedContext  ` )

A grounding chunk from a data source retrieved by a retrieval tool, such as Agent Platform Search. See the `RetrievedContext` message for details

`maps` ` object ( Maps  ` )

A grounding chunk from Google Maps. See the `Maps` message for details.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// chunk_type&quot;web&quot;: {object (Web)},&quot;retrievedContext&quot;: {object (RetrievedContext)},&quot;maps&quot;: {object (Maps)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Web

A `Web` chunk is a piece of evidence that comes from a web page. It contains the URI of the web page, the title of the page, and the domain of the page. This is used to provide the user with a link to the source of the information.

Fields

`uri` `string`

The URI of the web page that contains the evidence.

`title` `string`

The title of the web page that contains the evidence.

`domain` `string`

The domain of the web page that contains the evidence. This can be used to filter out low-quality sources.

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
  &quot;uri&quot;: string,
  &quot;title&quot;: string,
  &quot;domain&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## RetrievedContext

Context retrieved from a data source to ground the model's response. This is used when a retrieval tool fetches information from a user-provided corpus or a public dataset.

Fields

`context_details` `Union type`

Provides tool-specific details about the retrieved context. This allows for different types of retrieval tools to return their own specific metadata. `context_details` can be only one of the following:

`ragChunk` ` object ( RagChunk  ` )

Additional context for a Retrieval-Augmented Generation (RAG) retrieval result. This is populated only when the RAG retrieval tool is used.

`uri` `string`

The URI of the retrieved data source.

`title` `string`

The title of the retrieved data source.

`text` `string`

The content of the retrieved data source.

`documentName` `string`

Output only. The full resource name of the referenced Agent Platform Search document. This is used to identify the specific document that was retrieved. The format is `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}/branches/{branch}/documents/{document}` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// context_details&quot;ragChunk&quot;: {object (RagChunk)}// Union type&quot;uri&quot;: string,&quot;title&quot;: string,&quot;text&quot;: string,&quot;documentName&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## Maps

A `Maps` chunk is a piece of evidence that comes from Google Maps, containing information about places or routes. This is used to provide the user with rich, location-based information.

Fields

`placeAnswerSources` ` object ( PlaceAnswerSources  ` )

The sources that were used to generate the place answer. This includes review snippets and photos that were used to generate the answer, as well as URIs to flag content.

`uri` `string`

The URI of the place.

`title` `string`

The title of the place.

`text` `string`

The text of the place answer.

`placeId` `string`

This Place's resource name, in `places/{placeId}` format. This can be used to look up the place in the Google Maps API.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;placeAnswerSources&quot;: {object (PlaceAnswerSources)},&quot;uri&quot;: string,&quot;title&quot;: string,&quot;text&quot;: string,&quot;placeId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## PlaceAnswerSources

The sources that were used to generate the place answer. This includes review snippets and photos that were used to generate the answer, as well as URIs to flag content.

Fields

`reviewSnippets[]` ` object ( ReviewSnippet  ` )

Snippets of reviews that were used to generate the answer.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;reviewSnippets&quot;: [{object (ReviewSnippet)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ReviewSnippet

A review snippet that is used to generate the answer.

Fields

`reviewId` `string`

The id of the review that is being referenced.

`googleMapsUri` `string`

A link to show the review on Google Maps.

`title` `string`

The title of the review.

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
  &quot;reviewId&quot;: string,
  &quot;googleMapsUri&quot;: string,
  &quot;title&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## GroundingSupport

A collection of supporting references for a segment or part of the model's response.

Fields

`groundingChunkIndices[]` `integer`

A list of indices into the `groundingChunks` field of the `GroundingMetadata` message. These indices specify which grounding chunks support the claim made in the content segment.

For example, if this field has the values `[1, 3]` , it means that `groundingChunks[1]` and `groundingChunks[3]` are the sources for the claim in the content segment.

`confidenceScores[]` `number`

The confidence scores for the support references. This list is parallel to the `groundingChunkIndices` list. A score is a value between 0.0 and 1.0, with a higher score indicating a higher confidence that the reference supports the claim.

For Gemini 2.0 and before, this list has the same size as `groundingChunkIndices` . For Gemini 2.5 and later, this list is empty and should be ignored.

`renderedParts[]` `integer`

Indices into the `renderedParts` field of the `GroundingMetadata` message. These indices specify which rendered parts are associated with this support message.

`segment` ` object ( Segment  ` )

The content segment that this support message applies to.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;groundingChunkIndices&quot;: [integer],&quot;confidenceScores&quot;: [number],&quot;renderedParts&quot;: [integer],&quot;segment&quot;: {object (Segment)}}</code></pre></td>
</tr>
</tbody>
</table>

## Segment

A segment of the content.

Fields

`partIndex` `integer`

Output only. The index of the `Part` object that this segment belongs to. This is useful for associating the segment with a specific part of the content.

`startIndex` `integer`

Output only. The start index of the segment in the `Part` , measured in bytes. This marks the beginning of the segment and is inclusive, meaning the byte at this index is the first byte of the segment.

`endIndex` `integer`

Output only. The end index of the segment in the `Part` , measured in bytes. This marks the end of the segment and is exclusive, meaning the segment includes content up to, but not including, the byte at this index.

`text` `string`

Output only. The text of the segment.

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
  &quot;partIndex&quot;: integer,
  &quot;startIndex&quot;: integer,
  &quot;endIndex&quot;: integer,
  &quot;text&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## RetrievalMetadata

metadata related to the retrieval grounding source. This is part of the `GroundingMetadata` returned when grounding is enabled.

Fields

`googleSearchDynamicRetrievalScore` `number`

Optional. A score indicating how likely it is that a Google Search query could help answer the prompt. The score is in the range of `[0, 1]` . A score of 1 means the model is confident that a search will be helpful, and 0 means it is not. This score is populated only when Google Search grounding and dynamic retrieval are enabled. The score is used to determine whether to trigger a search.

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
  &quot;googleSearchDynamicRetrievalScore&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## SourceFlaggingUri

A URI that can be used to flag a place or review for inappropriate content. This is populated only when the grounding source is Google Maps.

Fields

`sourceId` `string`

The id of the place or review.

`flagContentUri` `string`

The URI that can be used to flag the content.

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
  &quot;sourceId&quot;: string,
  &quot;flagContentUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
