---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments
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

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. The timestamp when this SandboxEnvironment was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. The timestamp when this SandboxEnvironment was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state` `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#State)` )`

Output only. The runtime state of the SandboxEnvironment.

`spec` `object ( `[`SandboxEnvironmentSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#SandboxEnvironmentSpec)` )`

Optional. The configuration of the SandboxEnvironment.

`sandboxEnvironmentTemplate` `string`

Optional. The name of the SandboxEnvironmentTemplate specified in the parent Agent Engine resource that this SandboxEnvironment is created from.

`connectionInfo` `object ( `[`ConnectionInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#ConnectionInfo)` )`

Output only. The connection information of the SandboxEnvironment.

`latestSandboxEnvironmentSnapshot` `string`

Output only. The resource name of the latest snapshot taken for this SandboxEnvironment.

`owner` `string`

Optional. owner information for this sandbox environment. A Sandbox can only be restored from a snapshot that belongs to the same owner. If not set, sandbox will be created as the default owner.

`sandboxEnvironmentSnapshot` `string`

Optional. The resource name of the SandboxEnvironmentSnapshot to use for creating this SandboxEnvironment. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sandboxEnvironmentSnapshots/{sandboxEnvironmentSnapshot}`

`expiration` `Union type`

The expiration of the SandboxEnvironment. If not set, the SandboxEnvironment will not be automatically deleted. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`expireTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Optional. timestamp in UTC of when this SandboxEnvironment is considered expired. This is *always* provided on output, regardless of what `expiration` was sent on input.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`ttl` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. Input only. The TTL for the sandbox environment. The expiration time is computed: now + TTL.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "createTime": string,
  "updateTime": string,
  "state": enum (State),
  "spec": {
    object (SandboxEnvironmentSpec)
  },
  "sandboxEnvironmentTemplate": string,
  "connectionInfo": {
    object (ConnectionInfo)
  },
  "latestSandboxEnvironmentSnapshot": string,
  "owner": string,
  "sandboxEnvironmentSnapshot": string,

  // expiration
  "expireTime": string,
  "ttl": string
  // Union type
}
```

## State

The state of the SandboxEnvironment.

| Enums                  |                                                                    |
|------------------------|--------------------------------------------------------------------|
| `STATE_UNSPECIFIED`    | The default value. This value is unused.                           |
| `STATE_PROVISIONING`   | Runtime resources are being allocated for the sandbox environment. |
| `STATE_RUNNING`        | Sandbox runtime is ready for serving.                              |
| `STATE_DEPROVISIONING` | Sandbox runtime is halted, performing tear down tasks.             |
| `STATE_TERMINATED`     | Sandbox has terminated with underlying runtime failure.            |
| `STATE_DELETED`        | Sandbox runtime has been deleted.                                  |
| `STATE_PAUSED`         | Sandbox runtime is paused.                                         |
| `STATE_PAUSING`        | Sandbox runtime is pausing.                                        |
| `STATE_RESUMING`       | Sandbox runtime is resuming.                                       |
| `STATE_STOPPING`       | Sandbox runtime is stopping.                                       |

## SandboxEnvironmentSpec

The specification of a SandboxEnvironment.

Fields

`useGkeTd` `boolean`

Optional. Immutable. Whether to provision the SandboxEnvironment via the GKE TD pool. Immutable.

`sandbox_environment_category` `Union type`

The supported sandbox runtime environment categories. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`computerUseEnvironment` `object ( `[`ComputerUseEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#ComputerUseEnvironment)` )`

Optional. The computer use environment.

`codeExecutionEnvironment` `object ( `[`CodeExecutionEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#CodeExecutionEnvironment)` )`

Optional. The code execution environment.

`shellEnvironment` `object ( `[`ShellEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#ShellEnvironment)` )`

Optional. The shell environment for executing shell commands and scripts.

End of mutually exclusive fields.

**JSON representation**

```
{
  "useGkeTd": boolean,

  // sandbox_environment_category
  "computerUseEnvironment": {
    object (ComputerUseEnvironment)
  },
  "codeExecutionEnvironment": {
    object (CodeExecutionEnvironment)
  },
  "shellEnvironment": {
    object (ShellEnvironment)
  }
  // Union type
}
```

## ComputerUseEnvironment

This type has no fields.

The computer use environment with customized settings.

## CodeExecutionEnvironment

The code execution environment with customized settings.

Fields

`machineConfig` `enum ( `[`MachineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#MachineConfig)` )`

The machine config of the code execution environment.

`codeLanguage` `enum ( `[`Language`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#Language)` )`

The coding language supported in this environment.

**JSON representation**

```
{
  "machineConfig": enum (MachineConfig),
  "codeLanguage": enum (Language)
}
```

## MachineConfig

The machine config of the code execution environment.

| Enums                          |                                                 |
|--------------------------------|-------------------------------------------------|
| `MACHINE_CONFIG_UNSPECIFIED`   | The default value: milligcu 2000, memory 1.5Gib |
| `MACHINE_CONFIG_VCPU4_RAM4GIB` | The default value: milligcu 4000, memory 4 Gib  |

## Language

The coding language supported by the code execution environment.

| Enums                  |                                          |
|------------------------|------------------------------------------|
| `LANGUAGE_UNSPECIFIED` | The default value. This value is unused. |
| `LANGUAGE_PYTHON`      | The coding language is Python.           |
| `LANGUAGE_JAVASCRIPT`  | The coding language is JavaScript.       |

## ShellEnvironment

This type has no fields.

The shell environment.

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

`serviceAttachment` `string`

Output only. The name of the PSC-E service attachment created for private ingress to this SandboxEnvironment. Only populated when the template enables private ingress (see SandboxEnvironmentTemplate.ingress_control_config). VPC-SC customers use this to create a PSC endpoint in their VPC.

**JSON representation**

```
{
  "loadBalancerIp": string,
  "loadBalancerHostname": string,
  "sandboxInternalIp": string,
  "routingToken": string,
  "serviceAttachment": string
}
```

| Methods                                                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`authorizeAccess`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/authorizeAccess) | Checks whether the caller is authorized to access the sandbox environment.                                                                                                                                                                                                                                                                                                                                                                                        |
| [`bidiExecute`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/bidiExecute)         | Executes using a sandbox environment with bidirectional streaming.                                                                                                                                                                                                                                                                                                                                                                                                |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/create)                   | Creates a [`SandboxEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#SandboxEnvironment) in a given reasoning engine.                                                                                                                                                                                                                                   |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/delete)                   | Deletes the specific [`SandboxEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#SandboxEnvironment) .                                                                                                                                                                                                                                                   |
| [`execute`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/execute)                 | Executes using a sandbox environment.                                                                                                                                                                                                                                                                                                                                                                                                                             |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/get)                         | Gets details of the specific [`SandboxEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#SandboxEnvironment) .                                                                                                                                                                                                                                           |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/list)                       | Lists [`SandboxEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#SandboxEnvironment) s in a given reasoning engine.                                                                                                                                                                                                                                     |
| [`pause`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/pause)                     | Pauses the specific [`SandboxEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#SandboxEnvironment) .                                                                                                                                                                                                                                                    |
| [`resume`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/resume)                   | Resumes the specific [`SandboxEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#SandboxEnvironment) .                                                                                                                                                                                                                                                   |
| [`snapshot`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/snapshot)               | Snapshots the specific [`SandboxEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments#SandboxEnvironment) resource and creates a [`SandboxEnvironmentSnapshot`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentSnapshots#SandboxEnvironmentSnapshot) resource. |
