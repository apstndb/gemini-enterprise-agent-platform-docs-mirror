---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies/create
title: 'Method: semanticGovernancePolicies.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.semanticGovernancePolicies.create

Creates a SemanticGovernancePolicy.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /semanticGovernancePolicies`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location into which to create the SemanticGovernancePolicy. Format: `projects/{project}/locations/{location}`

### Query parameters

`semanticGovernancePolicyId` `string`

Required. The id to use for the SemanticGovernancePolicy, which will become the final component of the SemanticGovernancePolicy's resource name.

This value may be up to 63 characters, and valid characters are `[a-z0-9-]` . The first character cannot be a number or hyphen. The last character must be a letter or a number.

### Request body

The request body contains an instance of `  SemanticGovernancePolicy  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
