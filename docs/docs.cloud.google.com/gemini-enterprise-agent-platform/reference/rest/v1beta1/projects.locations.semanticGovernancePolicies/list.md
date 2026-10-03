---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.semanticGovernancePolicies/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.semanticGovernancePolicies/list
title: 'Method: semanticGovernancePolicies.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.semanticGovernancePolicies.list

Lists SemanticGovernancePolicies in a given location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /semanticGovernancePolicies`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to list the SemanticGovernancePolicies. Format: `projects/{project}/locations/{location}`

### Query parameters

`pageSize` `integer`

Optional. The list page size. If zero, a default page size of 10 is used.

`pageToken` `string`

Optional. The standard list page token.

### Request body

The request body must be empty.

### Response body

Response message for SemanticGovernancePolicyService.ListSemanticGovernancePolicies.

If successful, the response body contains data with the following structure:

Fields

`semanticGovernancePolicies[]` `object ( `[`SemanticGovernancePolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.semanticGovernancePolicies#SemanticGovernancePolicy)` )`

The list of SemanticGovernancePolicies.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to [`ListSemanticGovernancePoliciesRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.semanticGovernancePolicies/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "semanticGovernancePolicies": [
    {
      object (SemanticGovernancePolicy)
    }
  ],
  "nextPageToken": string
}
```
