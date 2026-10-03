---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/SetIamPolicyRequest
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/SetIamPolicyRequest
title: SetIamPolicyRequest
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Request message for `instances.setIamPolicy` method.

**JSON representation**

```
{
  "resource": string,
  "policy": {
    object (Policy)
  }
}
```

| Fields     |                                                                                                                                                                                                                                                                                                                                                                                  |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resource` | `string` REQUIRED: The resource for which the policy is being specified. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.                                                                                                                                                                                     |
| `policy`   | `object ( `[`Policy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/Policy)` )` REQUIRED: The complete policy to be applied to the `resource` . The size of the policy is limited to a few 10s of KB. An empty policy is a valid policy but certain Google Cloud services (such as Projects) might reject them. |
