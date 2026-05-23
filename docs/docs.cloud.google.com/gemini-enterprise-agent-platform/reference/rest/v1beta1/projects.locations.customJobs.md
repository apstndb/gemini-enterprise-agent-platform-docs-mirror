---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.customJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.customJobs
title: 'REST Resource: projects.locations.customJobs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: CustomJob

Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded).

Fields

`name` `string`

Output only. Resource name of a CustomJob.

`displayName` `string`

Required. The display name of the CustomJob. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`jobSpec` `object ( CustomJobSpec` )

Required. Job spec.

`state` ` enum ( JobState  ` )

Output only. The detailed state of the job.

`createTime` ` string ( Timestamp  ` format)

Output only. time when the CustomJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime` ` string ( Timestamp  ` format)

Output only. time when the CustomJob for the first time entered the `JOB_STATE_RUNNING` state.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

Output only. time when the CustomJob entered any of the following states: `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. time when the CustomJob was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`error` ` object ( Status  ` )

Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize CustomJobs.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key options for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key.

`webAccessUris` `map (key: string, value: string)`

Output only. URIs for accessing [interactive shells](https://cloud.google.com/vertex-ai/docs/training/monitor-debug-interactive-shell) (one URI for each training node). Only available if `jobSpec.enable_web_access` is `true` .

The keys are names of each node in the training job; for example, `workerpool0-0` for the primary node, `workerpool1-0` for the first node in the second worker pool, and `workerpool1-1` for the second node in the second worker pool.

The values are the URIs for each node's interactive shell.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;jobSpec&quot;: {object (CustomJobSpec)},&quot;state&quot;: enum (JobState),&quot;createTime&quot;: string,&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;updateTime&quot;: string,&quot;error&quot;: {object (Status)},&quot;labels&quot;: {string: string,...},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;webAccessUris&quot;: {string: string,...},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            cancel           `

Cancels a CustomJob.

### `            create           `

Creates a CustomJob.

### `            delete           `

Deletes a CustomJob.

### `            get           `

Gets a CustomJob.

### `            list           `

Lists CustomJobs in a Location.
