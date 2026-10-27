---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search
title: 'Method: projects.locations.dataStores.documents.search'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Searches the Documents of a single DataStore.

Returns ranked sub-document segments, each referring back to the Document it came from and carrying the provenance needed to cite it.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1beta/{parent}/documents:search`

### Path parameters

| Parameters |                                                                                                                      |
|------------|----------------------------------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. The DataStore to search. Format: `projects/{project}/locations/{location}/dataStores/{dataStore}` |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "topK": integer,
  "documentIds": [
    string
  ],
  "rankingSpec": {
    object (RankingSpec)
  },
  "filter": {
    object
  },
  "outputFields": {
    object (OutputFields)
  },

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "textQuery": {
    object (TextQuery)
  }
  // End of mutually exclusive fields.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>topK</code></td>
<td><p><code>integer</code></p>
<p>Optional. Number of results to return. Defaults to 10. Values above 100 are coerced to 100.</p></td>
</tr>
<tr class="even">
<td><code>documentIds[]</code></td>
<td><p><code>string</code></p>
<p>Optional. Restrict the search to these Document IDs. Max 100. If empty, the whole DataStore is searched.</p></td>
</tr>
<tr class="odd">
<td><code>rankingSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#RankingSpec"><code>RankingSpec</code></a><code> )</code></p>
<p>Optional. Controls how results are ranked.</p></td>
</tr>
<tr class="even">
<td><code>filter</code></td>
<td><p><code>object ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#struct"><code>Struct</code></a><code> format)</code></p>
<p>Optional. Restricts the search to segments that match this filter, a JSON object over the field paths of a <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#DocumentSearchResult"><code>DocumentSearchResult</code></a> :</p>
<ul>
<li><code>metadata.&lt;property&gt;</code> : a property declared in the DataStore's <code>documentMetadataSchema</code> , e.g. <code>metadata.category</code> .</li>
<li><code>unstructured_details.page_range.start_page</code> and <code>.end_page</code> : for an <code>UNSTRUCTURED</code> DataStore. Not every segment has a page range; see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#UnstructuredSegmentDetails.FIELDS.page_range"><code>UnstructuredSegmentDetails.page_range</code></a> .</li>
<li><code>video_details.start_offset</code> and <code>.end_offset</code> : in seconds, for a <code>VIDEO</code> DataStore.</li>
</ul>
<p>Comparisons: <code>$eq</code> , <code>$ne</code> , <code>$lt</code> , <code>$lte</code> , <code>$gt</code> , <code>$gte</code> , <code>$in</code> , <code>$nin</code> , <code>$all</code> , and <code>$exists</code> . Combine them with <code>$and</code> , <code>$or</code> , and <code>$not</code> , nested at most two levels deep. For example:</p>
<p>{"$and": [{"metadata.year": {"$gte": 2025}}, {"unstructured_details.page_range.start_page": {"$lte": 20}}]}</p></td>
</tr>
<tr class="odd">
<td><code>outputFields</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#OutputFields"><code>OutputFields</code></a><code> )</code></p>
<p>Optional. Fields to return on each result.</p></td>
</tr>
<tr class="even">
<td>Required. The query to search for. Exactly one query type must be set. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>textQuery</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#TextQuery"><code>TextQuery</code></a><code> )</code></p>
<p>A text query.</p></td>
</tr>
<tr class="even">
<td>End of mutually exclusive fields.</td>
<td></td>
</tr>
</tbody>
</table>

### Response body

Response message for [`DocumentSearchService.SearchDocuments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#google.cloud.vectorsearch.v1beta.DocumentSearchService.SearchDocuments) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "results": [
    {
      object (DocumentSearchResult)
    }
  ],
  "warnings": [
    {
      object (Status)
    }
  ]
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                           |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `results[]`  | `object ( `[`DocumentSearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#DocumentSearchResult)` )` Output only. The matching document segments that match the search criteria, ordered by relevance. |
| `warnings[]` | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/Shared.Types/ListOperationsResponse#Status)` )` Output only. Warnings or non-fatal errors that occurred during execution.                                                                       |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/vectorsearch`
- `https://www.googleapis.com/auth/vectorsearch.readonly`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## TextQuery

A text query.

**JSON representation**

```
{
  "text": string
}
```

| Fields |                                            |
|--------|--------------------------------------------|
| `text` | `string` Required. The text to search for. |

## RankingSpec

Controls how results are ranked.

**JSON representation**

```
{
  "rerankingSpec": {
    object (RerankingSpec)
  }
}
```

| Fields          |                                                                                                                                                                                                                                                    |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `rerankingSpec` | `object ( `[`RerankingSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#RerankingSpec)` )` Optional. Controls the re-ranking stage. |

## RerankingSpec

Configuration for semantic re-ranking applied to candidate results after hybrid retrieval and Reciprocal Rank Fusion (RRF).

**JSON representation**

```
{
  "enabled": boolean,
  "rankOversamplingFactor": integer
}
```

| Fields                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enabled`                | `boolean` Optional. Whether to re-rank the fused results. Defaults to false: results are returned in RRF-fused order unless the caller opts in. When enabled, re-ranking uses `semantic-ranker-fast@latest` on the Vertex Ranking Service, and requires the Discovery Engine API to be enabled on the caller's project. Not supported for a `VIDEO` DataStore: a request that enables it fails with `INVALID_ARGUMENT` .                                                                                                                                                                                                                                  |
| `rankOversamplingFactor` | `integer` Optional. The factor by which to oversample candidates before re-ranking. The total number of candidates retrieved for re-ranking is `min(rankOversamplingFactor * topK, 200)` . After re-ranking, results are trimmed to [`SearchDocumentsRequest.top_k`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#body.request_body.FIELDS.top_k) . Ignored unless `enabled` is true. When enabled, defaults to 5 (retrieving `min(5 * topK, 200)` candidates, with a maximum of 200). To re-rank without oversampling, set this field to 1. |

## OutputFields

Fields to return on each [`DocumentSearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#DocumentSearchResult) , beyond those every result carries.

**JSON representation**

```
{
  "metadata": [
    string
  ]
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metadata[]` | `string` Optional. Metadata properties to return in [`DocumentSearchResult.document.metadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents#Document.FIELDS.metadata) , named as declared in the DataStore's `documentMetadataSchema` . A nested property is named by its dotted path, e.g. `address.city` , without the `metadata.` prefix `filter` uses. `"*"` returns every declared property. Unset returns none. A property the Document has no value for is omitted. |

## DocumentSearchResult

A single matching segment of a Document.

**JSON representation**

```
{
  "document": {
    object (Document)
  },

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "videoDetails": {
    object (VideoSegmentDetails)
  },
  "unstructuredDetails": {
    object (UnstructuredSegmentDetails)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `document`                                                                                                                                                                                                                            | `object ( `[`Document`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents#Document)` )` Output only. The Document this segment came from, including its resource name and the Cloud Storage location it was ingested from. Note that not all Document fields are populated. For the full Document, call documents.get on the returned document name. |
| Details of where the segment sits within its Document. Which field is set follows the parent DataStore's `document_type` . The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `videoDetails`                                                                                                                                                                                                                        | `object ( `[`VideoSegmentDetails`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#VideoSegmentDetails)` )` Set when the parent DataStore's `documentType` is `VIDEO` .                                                                                                                                                                     |
| `unstructuredDetails`                                                                                                                                                                                                                 | `object ( `[`UnstructuredSegmentDetails`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#UnstructuredSegmentDetails)` )` Set when the parent DataStore's `documentType` is `UNSTRUCTURED` .                                                                                                                                                |
| End of mutually exclusive fields.                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

## VideoSegmentDetails

Locates a segment within a video Document.

**JSON representation**

```
{
  "startOffset": string,
  "endOffset": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                           |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startOffset` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Output only. Where this segment begins, relative to the start of the source video. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
| `endOffset`   | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Output only. Where this segment ends, relative to the start of the source video. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .   |

## UnstructuredSegmentDetails

Locates a segment within an unstructured Document, and carries its text.

**JSON representation**

```
{
  "contentSnippet": string,
  "pageRange": {
    object (PageRange)
  }
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `contentSnippet` | `string` Output only. Text content of the segment.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `pageRange`      | `object ( `[`PageRange`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/search#PageRange)` )` Output only. Where the segment sits in the source document. Set for PDF, PowerPoint and Excel files, where a page is a PDF page, a slide or a sheet. For plain-text and Word files, set only when the file is split into pages ( `pageSegmentationConfig` with digital parsing); the pages are then consecutive sections of the text, numbered in order. |

## PageRange

A page range within the source document. Pages are 1-based and the range is inclusive; a single page is represented as `startPage == endPage` .

**JSON representation**

```
{
  "startPage": string,
  "endPage": string
}
```

| Fields      |                                                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------|
| `startPage` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. First page of the range. |
| `endPage`   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Last page of the range.  |
