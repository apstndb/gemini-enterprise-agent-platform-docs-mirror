---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.semanticGovernancePolicies/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.semanticGovernancePolicies/patch
title: 'Method: semanticGovernancePolicies.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.semanticGovernancePolicies.patch

Updates a SemanticGovernancePolicy.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{semanticGovernancePolicy.name}`  

`PATCH https://{service-endpoint}/v1beta1/{semanticGovernancePolicy.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`semanticGovernancePolicy.name` `string`

Identifier. Resource name of the SemanticGovernancePolicy.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Optional. `updateMask` is used to specify the fields to be overwritten in the SemanticGovernancePolicy resource by the update. The fields specified in the `updateMask` are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the mask is not present, then all fields that are populated in the request message will be overwritten. Set the `updateMask` to `*` to override all fields.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  SemanticGovernancePolicy  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
