---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates
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

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. The timestamp when this SandboxEnvironmentTemplate was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. The timestamp when this SandboxEnvironmentTemplate was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state` `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#State)` )`

Output only. The state of the sandbox environment template.

`egressControlConfig` `object ( `[`EgressControlConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#EgressControlConfig)` )`

Optional. The configuration for egress control of this template.

`ingressControlConfig` `object ( `[`PrivateServiceConnectConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PrivateServiceConnectConfig)` )`

Optional. The configuration for private ingress (PSC-E) of this template. When set, the sandbox router is exposed privately via a PSC service attachment so VPC-SC customers can connect from their VPC over a private endpoint instead of the public internet. The resulting service attachment is surfaced on `SandboxEnvironment.connection_info.service_attachment` .

Only the PSC-E (service-attachment/ingress) portion of `PrivateServiceConnectConfig` applies here: `enablePrivateServiceConnect` and `projectAllowlist` (the consumer projects allowed to connect). The nested `pscInterfaceConfig` (PSC-I / egress) is not used for sandbox ingress; sandbox egress is configured via `egressControlConfig` instead.

`useGkeTd` `boolean`

Optional. Immutable. Whether to provision the SandboxEnvironmentTemplate via the GKE TD pool.

`sandbox_environment_category` `Union type`

The supported sandbox environment template categories. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`customContainerEnvironment` `object ( `[`CustomContainerEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#CustomContainerEnvironment)` )`

The sandbox environment for custom container workloads.

`defaultContainerEnvironment` `object ( `[`DefaultContainerEnvironment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#DefaultContainerEnvironment)` )`

The sandbox environment for default container workloads.

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "createTime": string,
  "updateTime": string,
  "state": enum (State),
  "egressControlConfig": {
    object (EgressControlConfig)
  },
  "ingressControlConfig": {
    object (PrivateServiceConnectConfig)
  },
  "useGkeTd": boolean,

  // sandbox_environment_category
  "customContainerEnvironment": {
    object (CustomContainerEnvironment)
  },
  "defaultContainerEnvironment": {
    object (DefaultContainerEnvironment)
  }
  // Union type
}
```

## CustomContainerEnvironment

The customized sandbox runtime environment for BYOC.

Fields

`customContainerSpec` `object ( `[`CustomContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#CustomContainerSpec)` )`

The specification of the custom container environment.

`ports[]` `object ( `[`NetworkPort`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#NetworkPort)` )`

Ports to expose from the container.

`resources` `object ( `[`ResourceRequirements`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#ResourceRequirements)` )`

Resource requests and limits for the container.

**JSON representation**

```
{
  "customContainerSpec": {
    object (CustomContainerSpec)
  },
  "ports": [
    {
      object (NetworkPort)
    }
  ],
  "resources": {
    object (ResourceRequirements)
  }
}
```

## CustomContainerSpec

Specification for deploying from a custom container image.

Fields

`imageUri` `string`

Required. The Artifact Registry Docker image URI (e.g., us-central1-docker.pkg.dev/my-project/my-repo/my-image:tag) of the container image that is to be run on each worker replica.

**JSON representation**

```
{
  "imageUri": string
}
```

## NetworkPort

Represents a network port in a container.

Fields

`port` `integer`

Optional. Port number to expose. This must be a valid port number, between 1 and 65535.

`protocol` `enum ( `[`Protocol`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#Protocol)` )`

Optional. protocol for port. Defaults to TCP if not specified.

**JSON representation**

```
{
  "port": integer,
  "protocol": enum (Protocol)
}
```

## Protocol

The protocol for the port.

| Enums                  |                                        |
|------------------------|----------------------------------------|
| `PROTOCOL_UNSPECIFIED` | Unspecified protocol. Defaults to TCP. |
| `TCP`                  | TCP protocol.                          |
| `UDP`                  | UDP protocol.                          |

## ResourceRequirements

message to define resource requests and limits (mirroring Kubernetes) for each sandbox instance created from this template.

Fields

`requests` `map (key: string, value: string)`

Optional. The requested amounts of compute resources. Keys are resource names (e.g., "cpu", "memory"). Values are quantities (e.g., "250m", "512Mi").

`limits` `map (key: string, value: string)`

Optional. The maximum amounts of compute resources allowed. Keys are resource names (e.g., "cpu", "memory"). Values are quantities (e.g., "500m", "1Gi").

**JSON representation**

```
{
  "requests": {
    string: string,
    ...
  },
  "limits": {
    string: string,
    ...
  }
}
```

## DefaultContainerEnvironment

The default sandbox runtime environment for default container workloads.

Fields

`defaultContainerCategory` `enum ( `[`DefaultContainerCategory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#DefaultContainerCategory)` )`

Required. The category of the default container image.

`resources` `object ( `[`ResourceRequirements`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#ResourceRequirements)` )`

Optional. Resource requests and limits for the default container.

**JSON representation**

```
{
  "defaultContainerCategory": enum (DefaultContainerCategory),
  "resources": {
    object (ResourceRequirements)
  }
}
```

## DefaultContainerCategory

The category of the default container image.

| Enums                                      |                                                |
|--------------------------------------------|------------------------------------------------|
| `DEFAULT_CONTAINER_CATEGORY_UNSPECIFIED`   | The default value. This value is unused.       |
| `DEFAULT_CONTAINER_CATEGORY_COMPUTER_USE`  | The default container image for Computer Use.  |
| `DEFAULT_CONTAINER_CATEGORY_SHELL_SANDBOX` | The default container image for Shell Sandbox. |

## State

Represents the state of a sandbox environment template.

| Enums            |                                                                    |
|------------------|--------------------------------------------------------------------|
| `UNSPECIFIED`    | The default value. This value is unused.                           |
| `PROVISIONING`   | Runtime resources are being allocated for the sandbox environment. |
| `ACTIVE`         | Sandbox runtime is ready for serving.                              |
| `DEPROVISIONING` | Sandbox runtime is halted, performing tear down tasks.             |
| `DELETED`        | Sandbox has terminated with underlying runtime failure.            |
| `FAILED`         | Sandbox has failed to provision.                                   |

## EgressControlConfig

Configuration for egress control of sandbox instances.

Fields

`internetAccess` `boolean`

Optional. Whether to allow internet access.

`networkAttachment` `string`

Optional. The name of the customer VPC `NetworkAttachment` used to draw a PSC interface IP into the customer VPC for sandbox egress.

`dnsPeeringConfigs[]` `object ( `[`DnsPeeringConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#DnsPeeringConfig)` )`

Optional. DNS peering configurations that allow sandbox egress to resolve customer-internal domains via the customer VPC.

**JSON representation**

```
{
  "internetAccess": boolean,
  "networkAttachment": string,
  "dnsPeeringConfigs": [
    {
      object (DnsPeeringConfig)
    }
  ]
}
```

## DnsPeeringConfig

Configuration for peering a customer's private DNS zone so that sandbox egress can resolve customer-internal domains via the customer VPC.

Fields

`domain` `string`

Required. The DNS name suffix of the zone being peered to, e.g., "my-internal-domain.corp.". Must end with a dot.

`targetProject` `string`

Required. The project id hosting the Cloud DNS managed zone that contains the `domain` . The Agent Platform service Agent requires the dns.peer role on this project.

`targetNetwork` `string`

Required. The VPC network name in the targetProject where the DNS zone specified by `domain` is visible.

**JSON representation**

```
{
  "domain": string,
  "targetProject": string,
  "targetNetwork": string
}
```

| Methods                                                                                                                                                                  |                                                                                                                                                                                                                                                         |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates/create) | Creates a [`SandboxEnvironmentTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#SandboxEnvironmentTemplate) in a given reasoning engine. |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates/delete) | Deletes the specific [`SandboxEnvironmentTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#SandboxEnvironmentTemplate) .                 |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates/get)       | Gets details of the specific [`SandboxEnvironmentTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#SandboxEnvironmentTemplate) .         |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates/list)     | Lists [`SandboxEnvironmentTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#SandboxEnvironmentTemplate) s in a given reasoning engine.   |
