---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ContainerImage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ContainerImage
title: ContainerImage
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Definition of a container image for starting a notebook instance with the environment installed in a container.

**JSON representation**

```
{
  "repository": string,
  "tag": string
}
```

| Fields       |                                                                                                              |
|--------------|--------------------------------------------------------------------------------------------------------------|
| `repository` | `string` Required. The path to the container image repository. For example: `gcr.io/{projectId}/{imageName}` |
| `tag`        | `string` The tag of the container image. If not specified, this defaults to the latest tag.                  |
