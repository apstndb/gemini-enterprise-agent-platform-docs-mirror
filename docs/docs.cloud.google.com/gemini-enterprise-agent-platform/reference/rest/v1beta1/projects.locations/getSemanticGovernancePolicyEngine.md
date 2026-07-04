---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/getSemanticGovernancePolicyEngine
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/getSemanticGovernancePolicyEngine
title: 'Method: locations.getSemanticGovernancePolicyEngine'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.getSemanticGovernancePolicyEngine

Gets a SemanticGovernancePolicyEngine.

A SemanticGovernancePolicyEngine is a singleton resource that is created when its parent is created, and deleted when its parent is deleted. This method retrieves the current state of the Semantic Governance Policy Engine.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the SemanticGovernancePolicyEngine to retrieve. Format: projects/{project}/locations/{location}/semanticGovernancePolicyEngine

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  SemanticGovernancePolicyEngine  ` .
