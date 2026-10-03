---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeployIndexOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeployIndexOperationMetadata
title: DeployIndexOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation information for [`IndexEndpointService.DeployIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexEndpoints/deployIndex#google.cloud.aiplatform.v1beta1.IndexEndpointService.DeployIndex) .

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenericOperationMetadata)` )`

The operation generic information.

`deployedIndexId` `string`

The unique index id specified by user

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "deployedIndexId": string
}
```
