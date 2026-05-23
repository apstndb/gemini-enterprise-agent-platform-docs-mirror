---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.onlineEvaluators/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.onlineEvaluators/create
title: 'Method: onlineEvaluators.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.onlineEvaluators.create

Creates an OnlineEvaluator in the given project and location.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /onlineEvaluators`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent resource where the OnlineEvaluator will be created. Format: projects/{project}/locations/{location}.

### Request body

The request body contains an instance of `  OnlineEvaluator  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
