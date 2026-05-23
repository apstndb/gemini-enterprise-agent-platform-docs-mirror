---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.metadataSchemas
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.metadataSchemas
title: 'REST Resource: projects.locations.metadataStores.metadataSchemas'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: MetadataSchema

Instance of a general MetadataSchema.

Fields

`name` `string`

Output only. The resource name of the MetadataSchema.

`schemaVersion` `string`

The version of the MetadataSchema. The version's format must match the following regular expression: `^[0-9]+[.][0-9]+[.][0-9]+$` , which would allow to order/compare different versions. Example: 1.0.0, 1.0.1, etc.

`schema` `string`

Required. The raw YAML string representation of the MetadataSchema. The combination of \[MetadataSchema.version\] and the schema name given by `title` in \[MetadataSchema.schema\] must be unique within a MetadataStore.

The schema is defined as an OpenAPI 3.0.2 [MetadataSchema Object](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md#schemaObject)

`schemaType` ` enum ( MetadataSchemaType  ` )

The type of the MetadataSchema. This is a property that identifies which metadata types will use the MetadataSchema.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this MetadataSchema was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`description` `string`

description of the metadata Schema

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;schemaVersion&quot;: string,&quot;schema&quot;: string,&quot;schemaType&quot;: enum (MetadataSchemaType),&quot;createTime&quot;: string,&quot;description&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## MetadataSchemaType

Describes the type of the MetadataSchema.

Enums

`METADATA_SCHEMA_TYPE_UNSPECIFIED`

Unspecified type for the MetadataSchema.

`ARTIFACT_TYPE`

A type indicating that the MetadataSchema will be used by Artifacts.

`EXECUTION_TYPE`

A typee indicating that the MetadataSchema will be used by Executions.

`CONTEXT_TYPE`

A state indicating that the MetadataSchema will be used by Contexts.

## Methods

### `            create           `

Creates a MetadataSchema.

### `            get           `

Retrieves a specific MetadataSchema.

### `            list           `

Lists MetadataSchemas.
