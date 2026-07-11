---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sandboxEnvironments
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sandboxEnvironments
title: 'REST Resource: projects.locations.reasoningEngines.sandboxEnvironments'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: SandboxEnvironment

SandboxEnvironment is a containerized environment that provides a customizable secure execution runtime for AI agents.

Fields

`name` `string`

Identifier. The name of the SandboxEnvironment.

`displayName` `string`

Required. The display name of the SandboxEnvironment.

`createTime` ` string ( Timestamp  ` format)

Output only. The timestamp when this SandboxEnvironment was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. The timestamp when this SandboxEnvironment was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state` ` enum ( State  ` )

Output only. The runtime state of the SandboxEnvironment.

`spec` ` object ( SandboxEnvironmentSpec  ` )

Optional. The configuration of the SandboxEnvironment.

`sandboxEnvironmentTemplate` `string`

Optional. The name of the SandboxEnvironmentTemplate specified in the parent Agent Engine resource that this SandboxEnvironment is created from.

`connectionInfo` ` object ( ConnectionInfo  ` )

Output only. The connection information of the SandboxEnvironment.

`latestSandboxEnvironmentSnapshot` `string`

Output only. The resource name of the latest snapshot taken for this SandboxEnvironment.

`owner` `string`

Optional. owner information for this sandbox environment. A Sandbox can only be restored from a snapshot that belongs to the same owner. If not set, sandbox will be created as the default owner.

`sandboxEnvironmentSnapshot` `string`

Optional. The resource name of the SandboxEnvironmentSnapshot to use for creating this SandboxEnvironment. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sandboxEnvironmentSnapshots/{sandboxEnvironmentSnapshot}`

`expiration` `Union type`

The expiration of the SandboxEnvironment. If not set, the SandboxEnvironment will not be automatically deleted. `expiration` can be only one of the following:

`expireTime` ` string ( Timestamp  ` format)

Optional. timestamp in UTC of when this SandboxEnvironment is considered expired. This is *always* provided on output, regardless of what `expiration` was sent on input.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`ttl` ` string ( Duration  ` format)

Optional. Input only. The TTL for the sandbox environment. The expiration time is computed: now + TTL.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;state&quot;: enum (State),&quot;spec&quot;: {object (SandboxEnvironmentSpec)},&quot;sandboxEnvironmentTemplate&quot;: string,&quot;connectionInfo&quot;: {object (ConnectionInfo)},&quot;latestSandboxEnvironmentSnapshot&quot;: string,&quot;owner&quot;: string,&quot;sandboxEnvironmentSnapshot&quot;: string,// expiration&quot;expireTime&quot;: string,&quot;ttl&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## State

The state of the SandboxEnvironment.

Enums

`STATE_UNSPECIFIED`

The default value. This value is unused.

`STATE_PROVISIONING`

Runtime resources are being allocated for the sandbox environment.

`STATE_RUNNING`

Sandbox runtime is ready for serving.

`STATE_DEPROVISIONING`

Sandbox runtime is halted, performing tear down tasks.

`STATE_TERMINATED`

Sandbox has terminated with underlying runtime failure.

`STATE_DELETED`

Sandbox runtime has been deleted.

## SandboxEnvironmentSpec

The specification of a SandboxEnvironment.

Fields

`sandbox_environment_category` `Union type`

The supported sandbox runtime environment categories. `sandbox_environment_category` can be only one of the following:

`codeExecutionEnvironment` ` object ( CodeExecutionEnvironment  ` )

Optional. The code execution environment.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// sandbox_environment_category&quot;codeExecutionEnvironment&quot;: {object (CodeExecutionEnvironment)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## CodeExecutionEnvironment

The code execution environment with customized settings.

Fields

`machineConfig` ` enum ( MachineConfig  ` )

The machine config of the code execution environment.

`codeLanguage` ` enum ( Language  ` )

The coding language supported in this environment.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineConfig&quot;: enum (MachineConfig),&quot;codeLanguage&quot;: enum (Language)}</code></pre></td>
</tr>
</tbody>
</table>

## MachineConfig

The machine config of the code execution environment.

Enums

`MACHINE_CONFIG_UNSPECIFIED`

The default value: milligcu 2000, memory 1.5Gib

`MACHINE_CONFIG_VCPU4_RAM4GIB`

The default value: milligcu 4000, memory 4 Gib

## Language

The coding language supported by the code execution environment.

Enums

`LANGUAGE_UNSPECIFIED`

The default value. This value is unused.

`LANGUAGE_PYTHON`

The coding language is Python.

`LANGUAGE_JAVASCRIPT`

The coding language is JavaScript.

## ConnectionInfo

The connection information of the SandboxEnvironment.

Fields

`loadBalancerIp` `string`

Output only. The IP address of the load balancer.

`loadBalancerHostname` `string`

Output only. The hostname of the load balancer.

`sandboxInternalIp` `string`

Output only. The internal IP address of the SandboxEnvironment.

`routingToken` `string`

Output only. The routing token for the SandboxEnvironment.

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
  &quot;loadBalancerIp&quot;: string,
  &quot;loadBalancerHostname&quot;: string,
  &quot;sandboxInternalIp&quot;: string,
  &quot;routingToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates a `  SandboxEnvironment  ` in a given reasoning engine.

### `            delete           `

Deletes the specific `  SandboxEnvironment  ` .

### `            execute           `

Executes using a sandbox environment.

### `            get           `

Gets details of the specific `  SandboxEnvironment  ` .

### `            list           `

Lists `  SandboxEnvironment  ` s in a given reasoning engine.

### `            pause           `

Pauses the specific `  SandboxEnvironment  ` .

### `            resume           `

Resumes the specific `  SandboxEnvironment  ` .

### `            snapshot           `

Snapshots the specific `  SandboxEnvironment  ` resource and creates a `  SandboxEnvironmentSnapshot  ` resource.
