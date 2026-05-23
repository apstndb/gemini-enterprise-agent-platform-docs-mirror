---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.executions/addExecutionEvents
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.executions/addExecutionEvents
title: 'Method: executions.addExecutionEvents'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.executions.addExecutionEvents

Adds events to the specified Execution. An Event indicates whether an Artifact was used as an input or output for an Execution. If an Event already exists between the Execution and the Artifact, the Event is skipped.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{execution}:addExecutionEvents`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`execution` `string`

Required. The resource name of the Execution that the events connect Artifacts with. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`

### Request body

The request body contains data with the following structure:

Fields

`events[]` ` object ( Event  ` )

The events to create and add.

### Response body

If successful, the response body is empty.
