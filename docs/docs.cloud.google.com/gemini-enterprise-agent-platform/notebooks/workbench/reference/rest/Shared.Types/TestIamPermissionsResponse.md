---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/TestIamPermissionsResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/TestIamPermissionsResponse
title: TestIamPermissionsResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `instances.testIamPermissions` method.

**JSON representation**

```
{
  "permissions": [
    string
  ]
}
```

| Fields          |                                                                                       |
|-----------------|---------------------------------------------------------------------------------------|
| `permissions[]` | `string` A subset of `TestPermissionsRequest.permissions` that the caller is allowed. |
