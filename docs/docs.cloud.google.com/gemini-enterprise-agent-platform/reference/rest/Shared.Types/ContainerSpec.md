---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ContainerSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ContainerSpec
title: ContainerSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The spec of a Container.

Fields

`imageUri` `string`

Required. The URI of a container image in the Artifact Registry that is to be run on each worker replica.

`command[]` `string`

The command to be invoked when the container is started. It overrides the entrypoint instruction in Dockerfile when provided.

`args[]` `string`

The arguments to be passed when starting the container.

`env[]` `object ( `[`EnvVar`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/EnvVar)` )`

Environment variables to be passed to the container. Maximum limit is 100.

**JSON representation**

```
{
  "imageUri": string,
  "command": [
    string
  ],
  "args": [
    string
  ],
  "env": [
    {
      object (EnvVar)
    }
  ]
}
```
