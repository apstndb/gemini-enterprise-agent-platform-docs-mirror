---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/updateSemanticGovernancePolicyEngine
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/updateSemanticGovernancePolicyEngine
title: 'Method: locations.updateSemanticGovernancePolicyEngine'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.updateSemanticGovernancePolicyEngine

Updates a SemanticGovernancePolicyEngine.

This method performs an upsert operation. If the SemanticGovernancePolicyEngine resource does not exist, it will be created. Otherwise, it will be updated.

### Endpoint

patch `https: / /{service-endpoint} /v1 /{semanticGovernancePolicyEngine.name}`  

`PATCH https://{service-endpoint}/v1/{semanticGovernancePolicyEngine.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`semanticGovernancePolicyEngine.name` `string`

Identifier. The resource name of the SemanticGovernancePolicyEngine. Format: projects/{project}/locations/{location}/semanticGovernancePolicyEngine

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. Specifies the fields to be overwritten in the SemanticGovernancePolicyEngine resource by the update. The fields specified in the updateMask are relative to the resource itself. If no updateMask is provided, all fields are overwritten.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  SemanticGovernancePolicyEngine  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
