---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookSoftwareConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookSoftwareConfig
title: NotebookSoftwareConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

Fields

`env[]` `object ( ``EnvVar`` )`

Optional. Environment variables to be passed to the container. Maximum limit is 100.

`postStartupScriptConfig` `object ( `[`PostStartupScriptConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookSoftwareConfig#PostStartupScriptConfig)` )`

Optional. Post startup script config.

`runtime_image` `Union type`

The image to be used by the notebook runtime. Can be one of release name, or custom container image. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`colabImage` `object ( `[`ColabImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookSoftwareConfig#ColabImage)` )`

Optional. Google-managed NotebookRuntime colab image.

End of mutually exclusive fields.

**JSON representation**

```
{
  "env": [
    {
      object (EnvVar)
    }
  ],
  "postStartupScriptConfig": {
    object (PostStartupScriptConfig)
  },

  // runtime_image
  "colabImage": {
    object (ColabImage)
  }
  // Union type
}
```

## ColabImage

Colab image of the runtime.

Fields

`releaseName` `string`

Optional. The release name of the NotebookRuntime Colab image, e.g. "py310". If not specified, detault to the latest release.

`description` `string`

Output only. A human-readable description of the specified colab image release, populated by the system. Example: "Python 3.10", "Latest - current Python 3.11"

**JSON representation**

```
{
  "releaseName": string,
  "description": string
}
```

## PostStartupScriptConfig

Post startup script config.

Fields

`postStartupScript` `string`

Optional. Post startup script to run after runtime is started.

`postStartupScriptUrl` `string`

Optional. Post startup script url to download. Example: `gs://bucket/script.sh`

`postStartupScriptBehavior` `enum ( `[`PostStartupScriptBehavior`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookSoftwareConfig#PostStartupScriptBehavior)` )`

Optional. Post startup script behavior that defines download and execution behavior.

**JSON representation**

```
{
  "postStartupScript": string,
  "postStartupScriptUrl": string,
  "postStartupScriptBehavior": enum (PostStartupScriptBehavior)
}
```

## PostStartupScriptBehavior

Represents a notebook runtime post startup script behavior.

| Enums                                      |                                                                     |
|--------------------------------------------|---------------------------------------------------------------------|
| `POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED` | Unspecified post startup script behavior.                           |
| `RUN_ONCE`                                 | Run post startup script after runtime is started.                   |
| `RUN_EVERY_START`                          | Run post startup script after runtime is stopped.                   |
| `DOWNLOAD_AND_RUN_EVERY_START`             | Download and run post startup script every time runtime is started. |
