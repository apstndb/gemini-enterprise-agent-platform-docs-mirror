---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata
title: 'REST Resource: projects.locations.ragCorpora.ragFiles.ragMetadata'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: RagMetadata

metadata for RagFile provided by users.

Fields

`name` `string`

Identifier. Resource name of the RagMetadata. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}/ragFiles/{ragFile}/ragMetadata/{ragMetadata}`

`userSpecifiedMetadata` ` object ( UserSpecifiedMetadata  ` )

user provided metadata.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;userSpecifiedMetadata&quot;: {object (UserSpecifiedMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

## UserSpecifiedMetadata

metadata provided by users.

Fields

`key` `string`

Required. Key of the metadata. The key must be set with type by CreateRagDataSchema.

`value` ` object ( MetadataValue  ` )

value of the metadata. The value must be able to convert to the type according to the data schema.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (MetadataValue)}}</code></pre></td>
</tr>
</tbody>
</table>

## MetadataValue

value of metadata, including all types available in data schema.

Fields

`value` `Union type`

The value of the metadata. `value` can be only one of the following:

`intValue` `string ( int64 format)`

value of int type metadata.

`floatValue` `number`

value of float type metadata.

`strValue` `string`

value of string type metadata.

`datetimeValue` `string`

value of date time type metadata.

`boolValue` `boolean`

value of boolean type metadata.

`listValue` ` object ( MetadataList  ` )

value of list type metadata.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// value&quot;intValue&quot;: string,&quot;floatValue&quot;: number,&quot;strValue&quot;: string,&quot;datetimeValue&quot;: string,&quot;boolValue&quot;: boolean,&quot;listValue&quot;: {object (MetadataList)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## MetadataList

List representation in metadata.

Fields

`values[]` ` object ( MetadataValue  ` )

The values of `LIST` data type metadata.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;values&quot;: [{object (MetadataValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            batchCreate           `

Batch Create one or more RagMetadatas

### `            batchDelete           `

Batch Deletes one or more RagMetadata.

### `            create           `

Creates a RagMetadata.

### `            delete           `

Deletes a RagMetadata.

### `            get           `

Gets a RagMetadata.

### `            list           `

Lists RagMetadata in a RagFile.

### `            patch           `

Updates a RagMetadata.
