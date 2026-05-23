---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/aggregate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/aggregate
title: 'Method: projects.locations.collections.dataObjects.aggregate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Aggregates data objects.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1beta/{parent}/dataObjects:aggregate`

### Path parameters

Parameters

`parent`

`string`

Required. The resource name of the Collection for which to query. Format: `projects/{project}/locations/{location}/collections/{collection}`

### Request body

The request body contains data with the following structure:

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;filter&quot;: {object},&quot;aggregate&quot;: enum (AggregationMethod)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`filter`

` object ( Struct  ` format)

Optional. A JSON filter expression, e.g. {"genre": {"$eq": "sci-fi"}}, represented as a google.protobuf.Struct.

`aggregate`

` enum ( AggregationMethod  ` )

Required. The aggregation method to apply to the query.

### Response body

Response message for `  DataObjectSearchService.AggregateDataObjects  ` .

If successful, the response body contains data with the following structure:

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
  &quot;aggregateResults&quot;: [
    {
      object
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`aggregateResults[]`

` object ( Struct  ` format)

Output only. The aggregated results of the query.

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

  - `vectorsearch.dataObjects.query`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

## AggregationMethod

Aggregation methods.

Enums

`AGGREGATION_METHOD_UNSPECIFIED`

Should not be used.

`COUNT`

Count the number of data objects that match the filter.
