---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimes/stop
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimes/stop
title: 'Method: notebookRuntimes.stop'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.notebookRuntimes.stop

Stops a NotebookRuntime.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:stop`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
