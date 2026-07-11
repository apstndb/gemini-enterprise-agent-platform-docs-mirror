---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/create
title: 'Method: sandboxEnvironments.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.sandboxEnvironments.create

Creates a `  SandboxEnvironment  ` in a given reasoning engine.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /sandboxEnvironments`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the reasoning engine to create the SandboxEnvironment in. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}` .

### Request body

The request body contains an instance of `  SandboxEnvironment  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
