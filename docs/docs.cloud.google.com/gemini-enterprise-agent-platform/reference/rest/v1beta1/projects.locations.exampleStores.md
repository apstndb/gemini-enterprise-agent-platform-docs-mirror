---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores
title: 'REST Resource: projects.locations.exampleStores'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ExampleStore

Represents an executable service to manage and retrieve examples.

Fields

`name` `string`

Identifier. The resource name of the ExampleStore. This is a unique identifier. Format: projects/{project}/locations/{location}/exampleStores/{exampleStore}

`displayName` `string`

Required. Display name of the ExampleStore.

`description` `string`

Optional. description of the ExampleStore.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ExampleStore was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ExampleStore was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`exampleStoreConfig` ` object ( ExampleStoreConfig  ` )

Required. Example Store config.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;exampleStoreConfig&quot;: {object (ExampleStoreConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## ExampleStoreConfig

Configuration for the Example Store.

Fields

`vertexEmbeddingModel` `string`

Required. The embedding model to be used for vector embedding. Immutable. Supported models: \* "text-embedding-005" \* "text-multilingual-embedding-002"

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
  &quot;vertexEmbeddingModel&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Create an ExampleStore.

### `            delete           `

Delete an ExampleStore.

### `            fetchExamples           `

Get Examples from the Example Store.

### `            get           `

Get an ExampleStore.

### `            list           `

List ExampleStores in a Location.

### `            patch           `

Update an ExampleStore.

### `            removeExamples           `

Remove Examples from the Example Store.

### `            searchExamples           `

Search for similar Examples for given selection criteria.

### `            upsertExamples           `

Create or update Examples in the Example Store.
