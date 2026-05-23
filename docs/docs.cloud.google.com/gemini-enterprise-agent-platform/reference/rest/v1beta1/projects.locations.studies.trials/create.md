---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials/create
title: 'Method: trials.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.trials.create

Adds a user provided Trial to a Study.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /trials`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Study to create the Trial in. Format: `projects/{project}/locations/{location}/studies/{study}`

### Request body

The request body contains an instance of `  Trial  ` .

### Response body

If successful, the response body contains a newly created instance of `  Trial  ` .
