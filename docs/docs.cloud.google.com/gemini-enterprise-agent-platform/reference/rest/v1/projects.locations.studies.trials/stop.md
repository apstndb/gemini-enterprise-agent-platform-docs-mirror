---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/stop
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/stop
title: 'Method: trials.stop'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.trials.stop

Stops a Trial.

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:stop`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Trial  ` .
