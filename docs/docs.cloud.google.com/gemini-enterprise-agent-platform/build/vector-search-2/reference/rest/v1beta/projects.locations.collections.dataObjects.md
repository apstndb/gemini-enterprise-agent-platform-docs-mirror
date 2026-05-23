---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects
title: 'REST Resource: projects.locations.collections.dataObjects'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: DataObject

A dataObject resource in Vector Search.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;dataObjectId&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;data&quot;: {object},&quot;vectors&quot;: {string: {object (Vector)},...},&quot;etag&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Identifier. The fully qualified resource name of the dataObject.

Format: `projects/{project}/locations/{location}/collections/{collection}/dataObjects/{dataObjectId}` The dataObjectId must be 1-63 characters long, and comply with [RFC1035](https://www.ietf.org/rfc/rfc1035.txt) .

`dataObjectId`

`string`

Output only. The id of the dataObject.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp the dataObject was created at.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp the dataObject was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`data`

` object ( Struct  ` format)

Optional. The data of the dataObject.

`vectors`

` map (key: string, value: object ( Vector  ` ))

Optional. The vectors of the dataObject.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`etag`

`string`

Optional. The etag of the dataObject.

## Vector

A vector which can be either dense or sparse.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;values&quot;: [number],// Union field vector_type can be only one of the following:&quot;dense&quot;: {object (DenseVector)},&quot;sparse&quot;: {object (SparseVector)}// End of list of possible types for union field vector_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` values[] (deprecated)  `

`number`

> This item is deprecated\!

Deprecated: Use `dense` or `sparse` instead.

Union field `vector_type` . The type of the vector. `vector_type` can be only one of the following:

`dense`

` object ( DenseVector  ` )

A dense vector.

`sparse`

` object ( SparseVector  ` )

A sparse vector.

## DenseVector

A dense vector.

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
  &quot;values&quot;: [
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`values[]`

`number`

Required. The values of the vector.

## SparseVector

A sparse vector.

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
  &quot;values&quot;: [
    number
  ],
  &quot;indices&quot;: [
    integer
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`values[]`

`number`

Required. The values of the vector.

`indices[]`

`integer`

Required. The corresponding indices for the values.

## Methods

### `            aggregate           `

Aggregates data objects.

### `            batchCreate           `

Creates a batch of dataObjects.

### `            batchDelete           `

Deletes dataObjects in a batch.

### `            batchSearch           `

Batch searches data objects.

### `            batchUpdate           `

Updates dataObjects in a batch.

### `            create           `

Creates a dataObject.

### `            delete           `

Deletes a dataObject.

### `            get           `

Gets a data object.

### `            patch           `

Updates a dataObject.

### `            query           `

Queries data objects.

### `            search           `

Searches data objects.
