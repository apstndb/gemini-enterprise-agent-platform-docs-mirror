---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.skills
title: 'REST Resource: projects.locations.skills'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Skill

A skill.

Fields

`name` `string`

Identifier. The resource name of the Skill. Format: `projects/{project}/locations/{location}/skills/{skill}`

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Skill was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Skill was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`displayName` `string`

Required. Provides the display name of the Skill. This should align with `name` in the `SKILL.md` file.

`description` `string`

Required. Describes the Skill. Should describe both what the skill does and when to use it. Should include specific keywords that help agents identify relevant tasks. This should align with `description` in the `SKILL.md` file.

`license` `string`

Optional. Specifies the license of the Skill. This should be an SPDX license identifier (e.g., "MIT", "Apache-2.0"). See <https://spdx.org/licenses/> . This should align with `license` in the `SKILL.md` file.

`compatibility` `string`

Optional. Specifies the compatibility of the Skill. Indicates environment requirements (intended product, system packages, network access, etc.). This should align with `compatibility` in the `SKILL.md` file.

`zippedFilesystem` `string ( bytes format)`

Required. Provides the zipped filesystem of the Skill. This should contain the `SKILL.md` file at the root of the zip and optional directories for scripts, references, and assets. Directory should align with the directory structure specified at <https://agentskills.io/specification#directory-structure> .

A base64-encoded string.

`state` ` enum ( State  ` )

Output only. The state of the Skill.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize Skills.

`sha256` `string`

Output only. The SHA256 checksum of the zipped filesystem.

`skillSource` ` enum ( SkillSource  ` )

Output only. The source of the Skill.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;license&quot;: string,&quot;compatibility&quot;: string,&quot;zippedFilesystem&quot;: string,&quot;state&quot;: enum (State),&quot;labels&quot;: {string: string,...},&quot;sha256&quot;: string,&quot;skillSource&quot;: enum (SkillSource)}</code></pre></td>
</tr>
</tbody>
</table>

### State

The state of the Skill.

Enums

`STATE_UNSPECIFIED`

The state of the Skill is unspecified.

`ACTIVE`

The Skill is active.

`CREATING`

The Skill is being created.

`FAILED`

The Skill was created, but failed to process.

`DELETING`

The Skill is being deleted.

### SkillSource

The source of the Skill (system or user-created).

Enums

`SKILL_SOURCE_UNSPECIFIED`

The skill source is unspecified.

`USER`

The skill is created by a user.

`SYSTEM`

The skill is a system skill.

## Methods

### `            create           `

Create a Skill.

### `            delete           `

Delete a Skill.

### `            get           `

Get a Skill.

### `            list           `

List Skills.

### `            patch           `

Update a Skill.

### `            retrieve           `

Retrieves skills.
