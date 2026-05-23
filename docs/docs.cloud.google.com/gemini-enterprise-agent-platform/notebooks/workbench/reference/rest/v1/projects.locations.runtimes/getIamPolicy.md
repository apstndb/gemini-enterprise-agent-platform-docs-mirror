---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/getIamPolicy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/getIamPolicy
title: 'Method: projects.locations.runtimes.getIamPolicy'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Gets the access control policy for a resource. Returns an empty policy if the resource exists and does not have a policy set.

### HTTP request

`GET https://notebooks.googleapis.com/v1/{resource}:getIamPolicy`

### Path parameters

Parameters

`resource`

`string`

REQUIRED: The resource for which the policy is being requested. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.

### Query parameters

Parameters

`options`

` object ( GetPolicyOptions  ` )

OPTIONAL: A `GetPolicyOptions` object for specifying options to `runtimes.getIamPolicy` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Policy  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
