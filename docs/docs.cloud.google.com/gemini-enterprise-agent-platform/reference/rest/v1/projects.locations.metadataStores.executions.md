---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions
title: 'REST Resource: projects.locations.metadataStores.executions'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Execution

Instance of a general execution.

Fields

`name` `string`

Output only. The resource name of the Execution.

`displayName` `string`

user provided display name of the Execution. May be up to 128 Unicode characters.

`state` ` enum ( State  ` )

The state of this Execution. This is a property of the Execution, and does not imply or capture any ongoing process. This property is managed by clients (such as Agent Platform Pipelines) and the system does not prescribe or check the validity of state transitions.

`etag` `string`

An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your Executions.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Execution (System labels are excluded).

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Execution was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Execution was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`schemaTitle` `string`

The title of the schema describing the metadata.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`schemaVersion` `string`

The version of the schema in `schemaTitle` to use.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`metadata` ` object ( Struct  ` format)

Properties of the Execution. top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.

`description` `string`

description of the Execution

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;state&quot;: enum (State),&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;schemaTitle&quot;: string,&quot;schemaVersion&quot;: string,&quot;metadata&quot;: {object},&quot;description&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

### State

Describes the state of the Execution.

Enums

`STATE_UNSPECIFIED`

Unspecified Execution state

`NEW`

The Execution is new

`RUNNING`

The Execution is running

`COMPLETE`

The Execution has finished running

`FAILED`

The Execution has failed

`CACHED`

The Execution completed through Cache hit.

`CANCELLED`

The Execution was cancelled.

## Methods

### `            addExecutionEvents           `

Adds Events to the specified Execution.

### `            create           `

Creates an Execution associated with a MetadataStore.

### `            delete           `

Deletes an Execution.

### `            get           `

Retrieves a specific Execution.

### `            list           `

Lists Executions in the MetadataStore.

### `            patch           `

Updates a stored Execution.

### `            purge           `

Purges Executions.

### `            queryExecutionInputsAndOutputs           `

Obtains the set of input and output Artifacts for this Execution, in the form of LineageSubgraph that also contains the Execution and connecting Events.
