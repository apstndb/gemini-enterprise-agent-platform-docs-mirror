---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/delete
title: 'Method: reasoningEngines.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.delete

Deletes a reasoning engine.

### Endpoint

delete `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the ReasoningEngine resource to be deleted. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Query parameters

`force` `boolean`

Optional. If set to true, child resources of this reasoning engine will also be deleted. Otherwise, the request will fail with FAILED\_PRECONDITION error when the reasoning engine has undeleted child resources.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
