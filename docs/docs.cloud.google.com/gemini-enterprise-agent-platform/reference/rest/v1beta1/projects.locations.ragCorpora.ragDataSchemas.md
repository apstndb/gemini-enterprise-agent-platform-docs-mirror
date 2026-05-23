---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragDataSchemas
title: 'REST Resource: projects.locations.ragCorpora.ragDataSchemas'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: RagDataSchema

The schema of the user specified metadata.

Fields

`name` `string`

Identifier. Resource name of the data schema in the form of: `projects/{projectNumber}/locations/{location}/ragCorpora/{ragCorpus}/ragDataSchemas/{ragDataSchema}` where the {ragDataSchema} part should be the same as the `key` field below.

`key` `string`

Required. The key of this data schema. This key should be matching the key of user specified metadata and unique inside corpus. This value can be up to 63 characters, and valid characters are /\[a-z\]\[0-9\]-/. The first character must be a letter, the last could be a letter or a number.

`schemaDetails` ` object ( RagMetadataSchemaDetails  ` )

The schema details mapping to the key.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;key&quot;: string,&quot;schemaDetails&quot;: {object (RagMetadataSchemaDetails)}}</code></pre></td>
</tr>
</tbody>
</table>

## RagMetadataSchemaDetails

data schema details indicates the data type and the data struct corresponding to the key of user specified metadata.

Fields

`listConfig` ` object ( ListConfig  ` )

Config for List data type.

`type` ` enum ( DataType  ` )

type of the metadata.

`granularity` ` enum ( Granularity  ` )

The granularity associated with this RagMetadataSchema.

`searchStrategy` ` object ( SearchStrategy  ` )

The search strategy for the metadata value of the `key` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;listConfig&quot;: {object (ListConfig)},&quot;type&quot;: enum (DataType),&quot;granularity&quot;: enum (Granularity),&quot;searchStrategy&quot;: {object (SearchStrategy)}}</code></pre></td>
</tr>
</tbody>
</table>

## DataType

data type of the metadata.

Enums

`DATA_TYPE_UNSPECIFIED`

Unspecified type.

`INTEGER`

Integer type.

`FLOAT`

Float type.

`STRING`

String type.

`DATETIME`

Supported formats: %Y-%m-%dT%H:%M:%E\*S%E\*z (absl::RFC3339\_full) %Y-%m-%dT%H:%M:%E\*S %Y-%m-%dT%H:%M%E\*z %Y-%m-%dT%H:%M %Y-%m-%dT%H%E\*z %Y-%m-%dT%H %Y-%m-%d%E\*z %Y-%m-%d %Y-%m %Y

`BOOLEAN`

Boolean type.

`LIST`

List type. - Each element in the list must be of the exact same data schema; otherwise, they are invalid arguments. - Elements cannot be another list (no list of list).

## ListConfig

Config for List data type.

Fields

`valueSchema` ` object ( RagMetadataSchemaDetails  ` )

The value's data type in the list.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;valueSchema&quot;: {object (RagMetadataSchemaDetails)}}</code></pre></td>
</tr>
</tbody>
</table>

## Granularity

The granularity of metadata under this DataSchema.

Enums

`GRANULARITY_UNSPECIFIED`

Unspecified granularity.

`GRANULARITY_FILE_LEVEL`

RagFile-level granularity.

## SearchStrategy

The search strategy for the metadata value of the `key` .

Fields

`searchStrategyType` ` enum ( SearchStrategyType  ` )

The search strategy type to be applied on the metadata key.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;searchStrategyType&quot;: enum (SearchStrategyType)}</code></pre></td>
</tr>
</tbody>
</table>

## SearchStrategyType

The types of search strategies to be applied on the metadata key.

Enums

`SEARCH_STRATEGY_TYPE_UNSPECIFIED`

Unspecified search strategy type.

`NO_SEARCH`

metadata values of the `key` above will not be searchable.

`EXACT_SEARCH`

When searching with `key` , the value must be exactly as the metadata value that has been ingested.

## Methods

### `            batchCreate           `

Batch Create one or more RagDataSchemas

### `            batchDelete           `

Batch Deletes one or more RagDataSchemas

### `            create           `

Creates a RagDataSchema.

### `            delete           `

Deletes a RagDataSchema.

### `            get           `

Gets a RagDataSchema.

### `            list           `

Lists RagDataSchemas in a Location.
