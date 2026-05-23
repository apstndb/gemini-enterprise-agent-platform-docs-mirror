---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts
title: 'REST Resource: projects.locations.metadataStores.contexts'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Context

Instance of a general context.

Fields

`name` `string`

Immutable. The resource name of the Context.

`displayName` `string`

user provided display name of the Context. May be up to 128 Unicode characters.

`etag` `string`

An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your Contexts.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Context (System labels are excluded).

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Context was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Context was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`parentContexts[]` `string`

Output only. A list of resource names of Contexts that are parents of this Context. A Context may have at most 10 parentContexts.

`schemaTitle` `string`

The title of the schema describing the metadata.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`schemaVersion` `string`

The version of the schema in schemaName to use.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`metadata` ` object ( Struct  ` format)

Properties of the Context. top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.

`description` `string`

description of the Context

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
  &quot;name&quot;: string,
  &quot;displayName&quot;: string,
  &quot;etag&quot;: string,
  &quot;labels&quot;: {
    string: string,
    ...
  },
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;parentContexts&quot;: [
    string
  ],
  &quot;schemaTitle&quot;: string,
  &quot;schemaVersion&quot;: string,
  &quot;metadata&quot;: {
    object
  },
  &quot;description&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            addContextArtifactsAndExecutions           `

Adds a set of Artifacts and Executions to a Context.

### `            addContextChildren           `

Adds a set of Contexts as children to a parent Context.

### `            create           `

Creates a Context associated with a MetadataStore.

### `            delete           `

Deletes a stored Context.

### `            get           `

Retrieves a specific Context.

### `            list           `

Lists Contexts on the MetadataStore.

### `            patch           `

Updates a stored Context.

### `            purge           `

Purges Contexts.

### `            queryContextLineageSubgraph           `

Retrieves Artifacts and Executions within the specified Context, connected by Event edges and returned as a LineageSubgraph.

### `            removeContextChildren           `

Remove a set of children contexts from a parent Context.
