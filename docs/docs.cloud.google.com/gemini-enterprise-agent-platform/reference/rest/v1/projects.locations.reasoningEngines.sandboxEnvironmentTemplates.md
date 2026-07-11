---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates
title: 'REST Resource: projects.locations.reasoningEngines.sandboxEnvironmentTemplates'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: SandboxEnvironmentTemplate

The specification of a SandboxEnvironmentTemplate. A SandboxEnvironmentTemplate defines a template for creating SandboxEnvironments.

Fields

`name` `string`

Identifier. The resource name of the SandboxEnvironmentTemplate. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sandboxEnvironmentTemplates/{sandboxEnvironmentTemplate}`

`displayName` `string`

Required. The display name of the SandboxEnvironmentTemplate.

`createTime` ` string ( Timestamp  ` format)

Output only. The timestamp when this SandboxEnvironmentTemplate was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. The timestamp when this SandboxEnvironmentTemplate was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state` ` enum ( State  ` )

Output only. The state of the sandbox environment template.

`egressControlConfig` ` object ( EgressControlConfig  ` )

Optional. The configuration for egress control of this template.

`sandbox_environment_category` `Union type`

The supported sandbox environment template categories. `sandbox_environment_category` can be only one of the following:

`customContainerEnvironment` ` object ( CustomContainerEnvironment  ` )

The sandbox environment for custom container workloads.

`defaultContainerEnvironment` ` object ( DefaultContainerEnvironment  ` )

The sandbox environment for default container workloads.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;state&quot;: enum (State),&quot;egressControlConfig&quot;: {object (EgressControlConfig)},// sandbox_environment_category&quot;customContainerEnvironment&quot;: {object (CustomContainerEnvironment)},&quot;defaultContainerEnvironment&quot;: {object (DefaultContainerEnvironment)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## CustomContainerEnvironment

The customized sandbox runtime environment for BYOC.

Fields

`customContainerSpec` ` object ( CustomContainerSpec  ` )

The specification of the custom container environment.

`ports[]` ` object ( NetworkPort  ` )

Ports to expose from the container.

`resources` ` object ( ResourceRequirements  ` )

Resource requests and limits for the container.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;customContainerSpec&quot;: {object (CustomContainerSpec)},&quot;ports&quot;: [{object (NetworkPort)}],&quot;resources&quot;: {object (ResourceRequirements)}}</code></pre></td>
</tr>
</tbody>
</table>

## CustomContainerSpec

Specification for deploying from a custom container image.

Fields

`imageUri` `string`

Required. The Artifact Registry Docker image URI (e.g., us-central1-docker.pkg.dev/my-project/my-repo/my-image:tag) of the container image that is to be run on each worker replica.

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
  &quot;imageUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## NetworkPort

Represents a network port in a container.

Fields

`port` `integer`

Optional. Port number to expose. This must be a valid port number, between 1 and 65535.

`protocol` ` enum ( Protocol  ` )

Optional. protocol for port. Defaults to TCP if not specified.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;port&quot;: integer,&quot;protocol&quot;: enum (Protocol)}</code></pre></td>
</tr>
</tbody>
</table>

## Protocol

The protocol for the port.

Enums

`PROTOCOL_UNSPECIFIED`

Unspecified protocol. Defaults to TCP.

`TCP`

TCP protocol.

`UDP`

UDP protocol.

## ResourceRequirements

message to define resource requests and limits (mirroring Kubernetes) for each sandbox instance created from this template.

Fields

`requests` `map (key: string, value: string)`

Optional. The requested amounts of compute resources. Keys are resource names (e.g., "cpu", "memory"). Values are quantities (e.g., "250m", "512Mi").

`limits` `map (key: string, value: string)`

Optional. The maximum amounts of compute resources allowed. Keys are resource names (e.g., "cpu", "memory"). Values are quantities (e.g., "500m", "1Gi").

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
  &quot;requests&quot;: {
    string: string,
    ...
  },
  &quot;limits&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

## DefaultContainerEnvironment

The default sandbox runtime environment for default container workloads.

Fields

`defaultContainerCategory` ` enum ( DefaultContainerCategory  ` )

Required. The category of the default container image.

`resources` ` object ( ResourceRequirements  ` )

Optional. Resource requests and limits for the default container.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;defaultContainerCategory&quot;: enum (DefaultContainerCategory),&quot;resources&quot;: {object (ResourceRequirements)}}</code></pre></td>
</tr>
</tbody>
</table>

## DefaultContainerCategory

The category of the default container image.

Enums

`DEFAULT_CONTAINER_CATEGORY_UNSPECIFIED`

The default value. This value is unused.

`DEFAULT_CONTAINER_CATEGORY_COMPUTER_USE`

The default container image for Computer Use.

## State

Represents the state of a sandbox environment template.

Enums

`UNSPECIFIED`

The default value. This value is unused.

`PROVISIONING`

Runtime resources are being allocated for the sandbox environment.

`ACTIVE`

Sandbox runtime is ready for serving.

`DEPROVISIONING`

Sandbox runtime is halted, performing tear down tasks.

`DELETED`

Sandbox has terminated with underlying runtime failure.

`FAILED`

Sandbox has failed to provision.

## EgressControlConfig

Configuration for egress control of sandbox instances.

Fields

`internetAccess` `boolean`

Optional. Whether to allow internet access.

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
  &quot;internetAccess&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates a `  SandboxEnvironmentTemplate  ` in a given reasoning engine.

### `            delete           `

Deletes the specific `  SandboxEnvironmentTemplate  ` .

### `            get           `

Gets details of the specific `  SandboxEnvironmentTemplate  ` .

### `            list           `

Lists `  SandboxEnvironmentTemplate  ` s in a given reasoning engine.
