---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/CreateIndexOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/CreateIndexOperationMetadata
title: CreateIndexOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation information for [`IndexService.CreateIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexes/create#google.cloud.aiplatform.v1beta1.IndexService.CreateIndex) .

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenericOperationMetadata)` )`

The operation generic information.

`nearestNeighborSearchOperationMetadata` `object ( `[`NearestNeighborSearchOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NearestNeighborSearchOperationMetadata)` )`

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
