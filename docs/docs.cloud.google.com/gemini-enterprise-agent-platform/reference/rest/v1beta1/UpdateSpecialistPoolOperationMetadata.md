---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UpdateSpecialistPoolOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UpdateSpecialistPoolOperationMetadata
title: UpdateSpecialistPoolOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation metadata for [`SpecialistPoolService.UpdateSpecialistPool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools/patch#google.cloud.aiplatform.v1beta1.SpecialistPoolService.UpdateSpecialistPool) .

Fields

`specialistPool` `string`

Output only. The name of the SpecialistPool to which the specialists are being added. Format: `projects/{projectId}/locations/{locationId}/specialistPools/{specialistPool}`

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenericOperationMetadata)` )`

The operation generic information.

**JSON representation**

```
{
  "specialistPool": string,
  "genericMetadata": {
    object (GenericOperationMetadata)
  }
}
```
