---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployModelOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployModelOperationMetadata
title: DeployModelOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation information for [`EndpointService.DeployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel#google.cloud.aiplatform.v1.EndpointService.DeployModel) .

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenericOperationMetadata)` )`

The operation generic information.

`deploymentStage` `enum ( `[`DeploymentStage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeploymentStage)` )`

Output only. The deployment stage of the model.

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "deploymentStage": enum (DeploymentStage)
}
```
