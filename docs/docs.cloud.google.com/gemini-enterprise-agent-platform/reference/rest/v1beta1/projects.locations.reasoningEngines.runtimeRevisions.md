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

`spec` `object ( `[`ReasoningEngineSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReasoningEngineSpec)` )`

Immutable. Configurations of the ReasoningEngineRuntimeRevision. Contains only revision specific fields.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ReasoningEngineRuntimeRevision was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state` `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions#State)` )`

Output only. The state of the revision.

**JSON representation**

```
{
  "name": string,
  "spec": {
    object (ReasoningEngineSpec)
  },
  "createTime": string,
  "state": enum (State)
}
```

## State

Possible values of the state of the revision.

| Enums               |                                                                                        |
|---------------------|----------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The unspecified state.                                                                 |
| `ACTIVE`            | Is deployed and ready to be used.                                                      |
| `ARCHIVED`          | Is archived and can no longer receive traffic, only preserved for historical purposes. |

| Methods                                                                                                                                                                 |                                                |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/delete)           | Deletes a reasoning engine revision.           |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/get)                 | Gets a reasoning engine runtime revision.      |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/list)               | Lists runtime revisions in a reasoning engine. |
| [`query`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/query)             | Queries using a reasoning engine.              |
| [`streamQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/streamQuery) | Streams queries using a reasoning engine.      |
