---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates/create
title: 'Method: notebookRuntimeTemplates.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.notebookRuntimeTemplates.create

Creates a NotebookRuntimeTemplate.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /notebookRuntimeTemplates`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: `projects/{project}/locations/{location}`

### Query parameters

`notebookRuntimeTemplateId` `string`

Optional. user specified id for the notebook runtime template.

### Request body

The request body contains an instance of `  NotebookRuntimeTemplate  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
