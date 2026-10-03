---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployModelResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployModelResponse
title: DeployModelResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`EndpointService.DeployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel#google.cloud.aiplatform.v1.EndpointService.DeployModel) .

Fields

`deployedModel` `object ( `[`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel)` )`

The DeployedModel that had been deployed in the Endpoint.

**JSON representation**

```
{
  "deployedModel": {
    object (DeployedModel)
  }
}
```
