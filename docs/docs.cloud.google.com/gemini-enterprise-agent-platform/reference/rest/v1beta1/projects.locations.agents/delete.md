---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.agents/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.agents/delete
title: 'Method: agents.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.agents.delete

Deletes an agent.

### Endpoint

delete `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the agent to delete. Format: `projects/{project}/locations/{location}/agents/{agent}` .

### Query parameters

`force` `boolean`

Optional. If true, any `Task` belonging to this agent is deleted along with it. If false or unset and the agent still has at least one `Task` , the request fails with `FAILED_PRECONDITION` and nothing is deleted.

This governs `Task` and nothing else. Resources the agent owns but a caller never named -- its AI Application and the tenant project bound to it, its Workspace identity, its service-extension binding -- are torn down with the agent on every delete, whatever this field says.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
