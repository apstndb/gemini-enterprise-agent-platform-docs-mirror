---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/VmImage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/VmImage
title: VmImage
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Definition of a custom Compute Engine virtual machine image for starting a notebook instance with the environment installed directly on the VM.

**JSON representation**

```
{
  "project": string,

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "imageName": string,
  "imageFamily": string
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                                           |                                                                                                              |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| `project`                                                                                                                                                        | `string` Required. The name of the Google Cloud project that this VM image belongs to. Format: `{projectId}` |
| The reference to an external Compute Engine VM image. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                              |
| `imageName`                                                                                                                                                      | `string` Use VM image name to find the image.                                                                |
| `imageFamily`                                                                                                                                                    | `string` Use this VM image family to find the image; the newest image in this family will be used.           |
| End of mutually exclusive fields.                                                                                                                                |                                                                                                              |
