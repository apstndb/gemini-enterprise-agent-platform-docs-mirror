---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions
title: 'REST Resource: projects.locations.reasoningEngines.runtimeRevisions'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ReasoningEngineRuntimeRevision

ReasoningEngineRuntimeRevision is a specific version of the runtime related part of ReasoningEngine. Contains only the fields that are revision specific.

Fields

`name` `string`

Identifier. The resource name of the ReasoningEngineRuntimeRevision. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/runtimeRevisions/{runtime_revision}`

`spec` ` object ( ReasoningEngineSpec  ` )

Immutable. Configurations of the ReasoningEngineRuntimeRevision. Contains only revision specific fields.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ReasoningEngineRuntimeRevision was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state` ` enum ( State  ` )

Output only. The state of the revision.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;spec&quot;: {object (ReasoningEngineSpec)},&quot;createTime&quot;: string,&quot;state&quot;: enum (State)}</code></pre></td>
</tr>
</tbody>
</table>

## State

Possible values of the state of the revision.

Enums

`STATE_UNSPECIFIED`

The unspecified state.

`ACTIVE`

Is deployed and ready to be used.

`DEPRECATED`

Is deprecated, may not be used, only preserved for historical purposes.

## Methods

### `            delete           `

Deletes a reasoning engine revision.

### `            get           `

Gets a reasoning engine runtime revision.

### `            list           `

Lists runtime revisions in a reasoning engine.

### `            query           `

Queries using a reasoning engine.

### `            streamQuery           `

Streams queries using a reasoning engine.
