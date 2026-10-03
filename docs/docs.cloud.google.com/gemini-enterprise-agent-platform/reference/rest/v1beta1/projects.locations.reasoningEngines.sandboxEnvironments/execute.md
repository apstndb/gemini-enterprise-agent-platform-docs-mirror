---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/execute
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironments/execute
title: 'Method: sandboxEnvironments.execute'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.sandboxEnvironments.execute

Executes using a sandbox environment.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:execute`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the sandbox environment to execute. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sandboxEnvironments/{sandboxEnvironment}`

### Request body

The request body contains data with the following structure:

Fields

`inputs[]` `object ( `[`Chunk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Chunk)` )`

Required. The inputs to the sandbox environment.

### Response body

Response message for \[SandboxEnvironmentExecutionService.Execute\]\[\].

If successful, the response body contains data with the following structure:

Fields

`outputs[]` `object ( `[`Chunk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Chunk)` )`

The outputs from the sandbox environment.

**JSON representation**

```
{
  "outputs": [
    {
      object (Chunk)
    }
  ]
}
```
