---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills.revisions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills.revisions
title: 'REST Resource: projects.locations.skills.revisions'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: SkillRevision

A revision of a Skill.

Fields

`name` `string`

Identifier. The resource name of the Skill Revision. Format: `projects/{project}/locations/{location}/skills/{skill}/revisions/{revision}`

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Skill Revision was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`skill` `object ( `[`Skill`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills#Skill)` )`

Output only. The state of the Skill at this revision.

`state` `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills.revisions#State)` )`

Output only. The state of the Skill Revision.

**JSON representation**

```
{
  "name": string,
  "createTime": string,
  "skill": {
    object (Skill)
  },
  "state": enum (State)
}
```

## State

The state of the Skill Revision.

| Enums               |                                                        |
|---------------------|--------------------------------------------------------|
| `STATE_UNSPECIFIED` | The state of the Skill Revision is unspecified.        |
| `ACTIVE`            | The Skill Revision is active.                          |
| `CREATING`          | The Skill Revision is being created.                   |
| `FAILED`            | The Skill Revision was created, but failed to process. |
| `DELETING`          | The Skill Revision is being deleted.                   |

| Methods                                                                                                                                  |                                   |
|------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills.revisions/get)   | Get a Skill Revision.             |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills.revisions/list) | List Skill Revisions for a Skill. |
