---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies
title: 'REST Resource: projects.locations.studies'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Study

A message representing a Study.

Fields

`name` `string`

Output only. The name of a study. The study's globally unique identifier. Format: `projects/{project}/locations/{location}/studies/{study}`

`displayName` `string`

Required. Describes the Study, default value is empty string.

`studySpec` `object ( `[`StudySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/StudySpec)` )`

Required. Configuration of the Study.

`state` `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies#State)` )`

Output only. The detailed state of a Study.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time at which the study was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`inactiveReason` `string`

Output only. A human readable reason why the Study is inactive. This should be empty if a study is ACTIVE or COMPLETED.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "studySpec": {
    object (StudySpec)
  },
  "state": enum (State),
  "createTime": string,
  "inactiveReason": string
}
```

## State

Describes the Study state.

| Enums               |                                                                                                     |
|---------------------|-----------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The study state is unspecified.                                                                     |
| `ACTIVE`            | The study is active.                                                                                |
| `INACTIVE`          | The study is stopped due to an internal error.                                                      |
| `COMPLETED`         | The study is done when the service exhausts the parameter search space or maxTrialCount is reached. |

| Methods                                                                                                                        |                                                                                                          |
|--------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/create) | Creates a Study.                                                                                         |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/delete) | Deletes a Study.                                                                                         |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/get)       | Gets a Study by name.                                                                                    |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/list)     | Lists all the studies in a region for an associated project.                                             |
| [`lookup`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/lookup) | Looks a study up using the user-defined display_name field instead of the fully qualified resource name. |
