---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/UpdateIndexOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/UpdateIndexOperationMetadata
title: UpdateIndexOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation information for [`IndexService.UpdateIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/patch#google.cloud.aiplatform.v1.IndexService.UpdateIndex) .

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenericOperationMetadata)` )`

The operation generic information.

`nearestNeighborSearchOperationMetadata` `object ( `[`NearestNeighborSearchOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NearestNeighborSearchOperationMetadata)` )`

The operation metadata with regard to Matching Engine Index operation.

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "nearestNeighborSearchOperationMetadata": {
    object (NearestNeighborSearchOperationMetadata)
  }
}
```
