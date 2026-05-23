---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/assign
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/assign
title: 'Method: notebookRuntimes.assign'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.notebookRuntimes.assign

Assigns a NotebookRuntime to a user for a particular Notebook file. This method will either returns an existing assignment or generates a new one.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /notebookRuntimes:assign`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to get the NotebookRuntime assignment. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`notebookRuntimeTemplate` `string`

Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one).

`notebookRuntime` ` object ( NotebookRuntime  ` )

Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment.

`notebookRuntimeId` `string`

Optional. user specified id for the notebook runtime.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
