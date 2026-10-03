---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines
title: 'REST Resource: projects.locations.reasoningEngines'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ReasoningEngine

ReasoningEngine provides a customizable runtime for models to determine which actions to take and in which order.

Fields

`name` `string`

Identifier. The resource name of the ReasoningEngine. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

`displayName` `string`

Required. The display name of the ReasoningEngine.

`description` `string`

Optional. The description of the ReasoningEngine.

`spec` `object ( `[`ReasoningEngineSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#ReasoningEngineSpec)` )`

Optional. Configurations of the ReasoningEngine

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ReasoningEngine was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ReasoningEngine was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec)` )`

Customer-managed encryption key spec for a ReasoningEngine. If set, this ReasoningEngine and all sub-resources of this ReasoningEngine will be secured by this key.

`labels` `map (key: string, value: string)`

Labels for the ReasoningEngine.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "spec": {
    object (ReasoningEngineSpec)
  },
  "createTime": string,
  "updateTime": string,
  "etag": string,
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "labels": {
    string: string,
    ...
  }
}
```

## ReasoningEngineSpec

ReasoningEngine configurations

Fields

`packageSpec` `object ( `[`PackageSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#PackageSpec)` )`

Optional. user provided package spec of the ReasoningEngine. Ignored when users directly specify a deployment image through `deploymentSpec.first_party_image_override` , but keeping the field_behavior to avoid introducing breaking changes. The `deployment_source` field should not be set if `packageSpec` is specified.

`deploymentSpec` `object ( `[`DeploymentSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#DeploymentSpec)` )`

Optional. The specification of a Reasoning Engine deployment.

`classMethods[]` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. Declarations for object class methods in OpenAPI specification format.

`agentFramework` `string`

Optional. The OSS agent framework used to develop the agent. Currently supported values: "google-adk", "langchain", "langgraph", "ag2", "llama-index", "custom".

`identityType` `enum ( `[`IdentityType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#IdentityType)` )`

Optional. The identity type to use for the Reasoning Engine. If not specified, the `serviceAccount` field will be used if set, otherwise the default Agent Platform Reasoning Engine service Agent in the project will be used.

`deployment_source` `Union type`

Defines the source for the deployment. The `package_spec` field should not be set if `deployment_source` is specified. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`sourceCodeSpec` `object ( `[`SourceCodeSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#SourceCodeSpec)` )`

Deploy from source code files with a defined entrypoint.

`containerSpec` `object ( `[`ContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#ContainerSpec)` )`

Deploy from a container image with a defined entrypoint and commands.

End of mutually exclusive fields.

`serviceAccount` `string`

Optional. The service account that the Reasoning Engine artifact runs as. It should have "roles/storage.objectViewer" for reading the user project's Cloud Storage and "roles/aiplatform.user" for using Vertex extensions. If not specified, the Agent Platform Reasoning Engine service Agent in the project will be used.

**JSON representation**

```
{
  "packageSpec": {
    object (PackageSpec)
  },
  "deploymentSpec": {
    object (DeploymentSpec)
  },
  "classMethods": [
    {
      object
    }
  ],
  "agentFramework": string,
  "identityType": enum (IdentityType),

  // deployment_source
  "sourceCodeSpec": {
    object (SourceCodeSpec)
  },
  "containerSpec": {
    object (ContainerSpec)
  }
  // Union type
  "serviceAccount": string
}
```

## SourceCodeSpec

Specification for deploying from source code.

Fields

`source` `Union type`

Specifies where the source code is located. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`inlineSource` `object ( `[`InlineSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#InlineSource)` )`

Source code is provided directly in the request.

`developerConnectSource` `object ( `[`DeveloperConnectSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#DeveloperConnectSource)` )`

Source code is in a Git repository managed by Developer Connect.

`agentConfigSource` `object ( `[`AgentConfigSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#AgentConfigSource)` )`

Source code is generated from the agent config.

End of mutually exclusive fields.

`language_spec` `Union type`

Specifies the language-specific configuration for building and running the code. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`pythonSpec` `object ( `[`PythonSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#PythonSpec)` )`

Configuration for a Python application.

`imageSpec` `object ( `[`ImageSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#ImageSpec)` )`

Optional. Configuration for building an image with custom config file.

End of mutually exclusive fields.

**JSON representation**

```
{

  // source
  "inlineSource": {
    object (InlineSource)
  },
  "developerConnectSource": {
    object (DeveloperConnectSource)
  },
  "agentConfigSource": {
    object (AgentConfigSource)
  }
  // Union type

  // language_spec
  "pythonSpec": {
    object (PythonSpec)
  },
  "imageSpec": {
    object (ImageSpec)
  }
  // Union type
}
```

## InlineSource

Specifies source code provided as a byte stream.

Fields

`sourceArchive` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

Required. Input only. The application source code archive. It must be a compressed tarball (.tar.gz) file.

A base64-encoded string.

**JSON representation**

```
{
  "sourceArchive": string
}
```

## DeveloperConnectSource

Specifies source code to be fetched from a Git repository managed through the Developer Connect service.

Fields

`config` `object ( `[`DeveloperConnectConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#DeveloperConnectConfig)` )`

Required. The Developer Connect configuration that defines the specific repository, revision, and directory to use as the source code root.

**JSON representation**

```
{
  "config": {
    object (DeveloperConnectConfig)
  }
}
```

## DeveloperConnectConfig

Specifies the configuration for fetching source code from a Git repository that is managed by Developer Connect. This includes the repository, revision, and directory to use.

Fields

`gitRepositoryLink` `string`

Required. The Developer Connect Git repository link, formatted as `projects/*/locations/*/connections/*/gitRepositoryLink/*` .

`dir` `string`

Required. Directory, relative to the source root, in which to run the build.

`revision` `string`

Required. The revision to fetch from the Git repository such as a branch, a tag, a commit SHA, or any Git ref.

**JSON representation**

```
{
  "gitRepositoryLink": string,
  "dir": string,
  "revision": string
}
```

## AgentConfigSource

Specification for the deploying from agent config.

Fields

`adkConfig` `object ( `[`AdkConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#AdkConfig)` )`

Required. The ADK configuration.

`inlineSource` `object ( `[`InlineSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#InlineSource)` )`

Optional. Any additional files needed to interpret the config. If a `requirements.txt` file is present in the `inlineSource` , the corresponding packages will be installed. If no `requirements.txt` file is present in `inlineSource` , then the latest version of `google-adk` will be installed for interpreting the ADK config.

**JSON representation**

```
{
  "adkConfig": {
    object (AdkConfig)
  },
  "inlineSource": {
    object (InlineSource)
  }
}
```

## AdkConfig

Configuration for the Agent Development Kit (ADK).

Fields

`jsonConfig` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Required. The value of the ADK config in JSON format.

**JSON representation**

```
{
  "jsonConfig": {
    object
  }
}
```

## PythonSpec

Specification for running a Python application from source.

Fields

`version` `string`

Optional. The version of Python to use. Supported versions include 3.10, 3.11, 3.12, 3.13, 3.14. If not specified, default value is 3.10.

`entrypointModule` `string`

Optional. The Python module to load as the entrypoint, specified as a fully qualified module name. For example: path.to.agent. If not specified, defaults to "agent".

The project root will be added to Python sys.path, allowing imports to be specified relative to the root.

This field should not be set if the source is `agentConfigSource` .

`entrypointObject` `string`

Optional. The name of the callable object within the `entrypointModule` to use as the application If not specified, defaults to "root_agent".

This field should not be set if the source is `agentConfigSource` .

`requirementsFile` `string`

Optional. The path to the requirements file, relative to the source root. If not specified, defaults to "requirements.txt".

**JSON representation**

```
{
  "version": string,
  "entrypointModule": string,
  "entrypointObject": string,
  "requirementsFile": string
}
```

## ImageSpec

The image spec for building an image (within a single build step), based on the config file (i.e. Dockerfile) in the source directory.

Fields

`buildArgs` `map (key: string, value: string)`

Optional. Build arguments to be used. They will be passed through --build-arg flags.

**JSON representation**

```
{
  "buildArgs": {
    string: string,
    ...
  }
}
```

## ContainerSpec

Specification for deploying from a container image.

Fields

`imageUri` `string`

Required. The Artifact Registry Docker image URI (e.g., us-central1-docker.pkg.dev/my-project/my-repo/my-image:tag) of the container image that is to be run on each worker replica.

`port` `integer`

Optional. The port the container listens on. Defaults to 8080 if unset.

**JSON representation**

```
{
  "imageUri": string,
  "port": integer
}
```

## PackageSpec

user-provided package specification, containing pickled object and package requirements.

Fields

`pickleObjectGcsUri` `string`

Optional. The Cloud Storage URI of the pickled python object.

`dependencyFilesGcsUri` `string`

Optional. The Cloud Storage URI of the dependency files in tar.gz format.

`requirementsGcsUri` `string`

Optional. The Cloud Storage URI of the `requirements.txt` file

`pythonVersion` `string`

Optional. The Python version. Supported values are 3.10, 3.11, 3.12, 3.13, 3.14. If not specified, the default value is 3.10.

**JSON representation**

```
{
  "pickleObjectGcsUri": string,
  "dependencyFilesGcsUri": string,
  "requirementsGcsUri": string,
  "pythonVersion": string
}
```

## DeploymentSpec

The specification of a Reasoning Engine deployment.

Fields

`env[]` `object ( `[`EnvVar`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/EnvVar)` )`

Optional. Environment variables to be set with the Reasoning Engine deployment. The environment variables can be updated through the reasoningEngines.patch API.

`secretEnv[]` `object ( `[`SecretEnvVar`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#SecretEnvVar)` )`

Optional. Environment variables where the value is a secret in Cloud Secret Manager. To use this feature, add 'Secret Manager Secret Accessor' role (roles/secretmanager.secretAccessor) to AI Platform Reasoning Engine service Agent.

`pscInterfaceConfig` `object ( `[`PscInterfaceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec#PscInterfaceConfig)` )`

Optional. Configuration for PSC-I.

`resourceLimits` `map (key: string, value: string)`

Optional. Resource limits for each container. Only 'cpu' and 'memory' keys are supported. Defaults to {"cpu": "4", "memory": "4Gi"}.

- The only supported values for CPU are '1', '2', '4', '6' and '8'. For more information, go to <https://cloud.google.com/run/docs/configuring/cpu> .
- The only supported values for memory are '1Gi', '2Gi', ... '32 Gi'.
- For required cpu on different memory values, go to <https://cloud.google.com/run/docs/configuring/memory-limits>

`keepAliveProbe` `object ( `[`KeepAliveProbe`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#KeepAliveProbe)` )`

Optional. Specifies the configuration for keep-alive probe. Contains configuration on a specified endpoint that a deployment host should use to keep the container alive based on the probe settings.

`minInstances` `integer`

Optional. The minimum number of application instances that will be kept running at all times. Defaults to 1. Range: \[0, 75\].

`maxInstances` `integer`

Optional. The maximum number of application instances that can be launched to handle increased traffic. Defaults to 100. Range: \[1, 1000\].

If VPC-SC or PSC-I is enabled, the acceptable range is \[1, 100\].

`containerConcurrency` `integer`

Optional. Concurrency for each container and agent server. Recommended value: 2 \* cpu + 1. Defaults to 9.

**JSON representation**

```
{
  "env": [
    {
      object (EnvVar)
    }
  ],
  "secretEnv": [
    {
      object (SecretEnvVar)
    }
  ],
  "pscInterfaceConfig": {
    object (PscInterfaceConfig)
  },
  "resourceLimits": {
    string: string,
    ...
  },
  "keepAliveProbe": {
    object (KeepAliveProbe)
  },
  "minInstances": integer,
  "maxInstances": integer,
  "containerConcurrency": integer
}
```

## SecretEnvVar

Represents an environment variable where the value is a secret in Cloud Secret Manager.

Fields

`name` `string`

Required. name of the secret environment variable.

`secretRef` `object ( `[`SecretRef`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#SecretRef)` )`

Required. Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable.

**JSON representation**

```
{
  "name": string,
  "secretRef": {
    object (SecretRef)
  }
}
```

## SecretRef

Reference to a secret stored in the Cloud Secret Manager that will provide the value for this environment variable.

Fields

`secret` `string`

Required. The name of the secret in Cloud Secret Manager. Format: {secret_name}.

`version` `string`

The Cloud Secret Manager secret version. Can be 'latest' for the latest version, an integer for a specific version, or a version alias.

**JSON representation**

```
{
  "secret": string,
  "version": string
}
```

## KeepAliveProbe

Represents the configuration for keep-alive probe. Contains configuration on a specified endpoint that a deployment host should use to keep the container alive based on the probe settings.

Fields

`httpGet` `object ( `[`HttpGet`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines#HttpGet)` )`

Optional. Specifies the HTTP GET configuration for the probe.

`maxSeconds` `integer`

Optional. Specifies the maximum duration (in seconds) to keep the instance alive via this probe. Can be a maximum of 3600 seconds (1 hour).

**JSON representation**

```
{
  "httpGet": {
    object (HttpGet)
  },
  "maxSeconds": integer
}
```

## HttpGet

Specifies the HTTP GET configuration for the probe.

Fields

`path` `string`

Required. Specifies the path of the HTTP GET request (e.g., `"/is_busy"` ).

`port` `integer`

Optional. Specifies the port number on the container to which the request is sent.

**JSON representation**

```
{
  "path": string,
  "port": integer
}
```

## IdentityType

The identity type to use for the Reasoning Engine.

| Enums                       |                                                                                                                                                                                                             |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `IDENTITY_TYPE_UNSPECIFIED` | Default value. Use a custom service account if the `serviceAccount` field is set, otherwise use the default Agent Platform Reasoning Engine service Agent in the project. Same behavior as SERVICE_ACCOUNT. |
| `SERVICE_ACCOUNT`           | Use a custom service account if the `serviceAccount` field is set, otherwise use the default Agent Platform Reasoning Engine service Agent in the project.                                                  |
| `AGENT_IDENTITY`            | Use Agent Identity. The `serviceAccount` field must not be set.                                                                                                                                             |

| Methods                                                                                                                                                         |                                                                  |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| [`asyncQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/asyncQuery)                 | Async query using a reasoning engine.                            |
| [`cancelAsyncQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/cancelAsyncQuery)     | Cancels an AsyncQueryReasoningEngine operation.                  |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/create)                         | Creates a reasoning engine.                                      |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/delete)                         | Deletes a reasoning engine.                                      |
| [`executeCode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/executeCode)               | Executes code statelessly.                                       |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/get)                               | Gets a reasoning engine.                                         |
| [`getIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/getIamPolicy)             | Gets the access control policy for a resource.                   |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/list)                             | Lists reasoning engines in a location.                           |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/patch)                           | Updates a reasoning engine.                                      |
| [`query`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/query)                           | Queries using a reasoning engine.                                |
| [`setIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/setIamPolicy)             | Sets the access control policy on the specified resource.        |
| [`streamQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/streamQuery)               | Streams queries using a reasoning engine.                        |
| [`testIamPermissions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/testIamPermissions) | Returns permissions that a caller has on the specified resource. |
