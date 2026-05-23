---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.environments
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.environments
title: 'REST Resource: projects.locations.environments'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Environment

Definition of a software environment that is used to start a notebook instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;postStartupScript&quot;: string,&quot;createTime&quot;: string,// Union field image_type can be only one of the following:&quot;vmImage&quot;: {object (VmImage)},&quot;containerImage&quot;: {object (ContainerImage)}// End of list of possible types for union field image_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. Name of this environment. Format: `projects/{projectId}/locations/{location}/environments/{environmentId}`

`displayName`

`string`

Display name of this environment for the UI.

`description`

`string`

A brief description of this environment.

`postStartupScript`

`string`

Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path. Example: `"gs://path-to-file/file-name"`

`createTime`

` string ( Timestamp  ` format)

Output only. The time at which this environment was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

Union field `image_type` . Type of the environment; can be one of VM image, or container image. `image_type` can be only one of the following:

`vmImage`

` object ( VmImage  ` )

Use a Compute Engine VM image to start the notebook instance.

`containerImage`

` object ( ContainerImage  ` )

Use a container image to start the notebook instance.

## Methods

### `            create           `

Creates a new Environment.

### `            delete           `

Deletes a single Environment.

### `            get           `

Gets details of a single Environment.

### `            list           `

Lists environments in a project.
