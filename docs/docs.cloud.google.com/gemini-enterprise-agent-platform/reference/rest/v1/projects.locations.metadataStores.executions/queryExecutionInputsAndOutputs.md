---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/queryExecutionInputsAndOutputs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions/queryExecutionInputsAndOutputs
title: 'Method: executions.queryExecutionInputsAndOutputs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.executions.queryExecutionInputsAndOutputs

Obtains the set of input and output Artifacts for this Execution, in the form of LineageSubgraph that also contains the Execution and connecting events.

### Endpoint

get `https: / /{service-endpoint} /v1 /{execution}:queryExecutionInputsAndOutputs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`execution` `string`

Required. The resource name of the Execution whose input and output Artifacts should be retrieved as a LineageSubgraph. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  LineageSubgraph  ` .
