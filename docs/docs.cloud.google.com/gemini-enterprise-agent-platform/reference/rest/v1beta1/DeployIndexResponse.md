---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeployIndexResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeployIndexResponse
title: DeployIndexResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`IndexEndpointService.DeployIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexEndpoints/deployIndex#google.cloud.aiplatform.v1beta1.IndexEndpointService.DeployIndex) .

Fields

`deployedIndex` `object ( `[`DeployedIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexEndpoints#DeployedIndex)` )`

The DeployedIndex that had been deployed in the IndexEndpoint.

**JSON representation**

```
{
  "deployedIndex": {
    object (DeployedIndex)
  }
}
```
