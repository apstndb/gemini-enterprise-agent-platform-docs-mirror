---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CheckTrialEarlyStoppingStateMetatdata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CheckTrialEarlyStoppingStateMetatdata
title: CheckTrialEarlyStoppingStateMetatdata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenericOperationMetadata)` )`

Operation metadata for suggesting Trials.

`study` `string`

The name of the Study that the Trial belongs to.

`trial` `string`

The Trial name.

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "study": string,
  "trial": string
}
```
