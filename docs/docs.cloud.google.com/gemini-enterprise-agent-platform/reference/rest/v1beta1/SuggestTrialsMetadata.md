---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SuggestTrialsMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SuggestTrialsMetadata
title: SuggestTrialsMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Details of operations that perform Trials suggestion.

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenericOperationMetadata)` )`

Operation metadata for suggesting Trials.

`clientId` `string`

The identifier of the client that is requesting the suggestion.

If multiple SuggestTrialsRequests have the same `clientId` , the service will return the identical suggested Trial if the Trial is pending, and provide a new Trial if the last suggested Trial was completed.

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "clientId": string
}
```
