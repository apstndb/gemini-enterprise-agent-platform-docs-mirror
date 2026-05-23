---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts/addContextArtifactsAndExecutions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts/addContextArtifactsAndExecutions
title: 'Method: contexts.addContextArtifactsAndExecutions'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.contexts.addContextArtifactsAndExecutions

Adds a set of Artifacts and Executions to a Context. If any of the Artifacts or Executions have already been added to a Context, they are simply skipped.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{context}:addContextArtifactsAndExecutions`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`context` `string`

Required. The resource name of the Context that the Artifacts and Executions belong to. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`

### Request body

The request body contains data with the following structure:

Fields

`artifacts[]` `string`

The resource names of the Artifacts to attribute to the Context.

Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`

`executions[]` `string`

The resource names of the Executions to associate with the Context.

Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`

### Response body

If successful, the response body is empty.
