---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts/queryContextLineageSubgraph
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts/queryContextLineageSubgraph
title: 'Method: contexts.queryContextLineageSubgraph'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.contexts.queryContextLineageSubgraph

Retrieves Artifacts and Executions within the specified Context, connected by Event edges and returned as a LineageSubgraph.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{context}:queryContextLineageSubgraph`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`context` `string`

Required. The resource name of the Context whose Artifacts and Executions should be retrieved as a LineageSubgraph. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`

The request may error with FAILED\_PRECONDITION if the number of Artifacts, the number of Executions, or the number of events that would be returned for the Context exceeds 1000.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  LineageSubgraph  ` .
