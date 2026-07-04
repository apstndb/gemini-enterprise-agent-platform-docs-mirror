---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.semanticGovernancePolicies/delete
title: 'Method: semanticGovernancePolicies.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.semanticGovernancePolicies.delete

Deletes a SemanticGovernancePolicy.

### Endpoint

delete `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the SemanticGovernancePolicy resource to be deleted. Format: `projects/{project}/locations/{location}/semanticGovernancePolicies/{semanticGovernancePolicy}`

### Query parameters

`etag` `string`

Optional. The etag of the SemanticGovernancePolicy. If an etag is provided and does not match the current etag of the SemanticGovernancePolicy, deletion will be blocked and an ABORTED error will be returned.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
