---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicyEngine/deprovision
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicyEngine/deprovision
title: 'Method: semanticGovernancePolicyEngine.deprovision'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.semanticGovernancePolicyEngine.deprovision

Deprovisions the SemanticGovernancePolicyEngine, tearing down the associated tenant project, GKE cluster, and PSC service attachments. This operation is irreversible.

Returns a long-running operation; poll for completion. The response contains the SemanticGovernancePolicyEngine in DEPROVISIONING state.

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:deprovision`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the SemanticGovernancePolicyEngine to deprovision. Format: projects/{project}/locations/{location}/semanticGovernancePolicyEngine

### Request body

The request body contains data with the following structure:

Fields

`force` `boolean`

Optional. If true, the operation bypass checks on current state and force the deprovisioning operation.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
