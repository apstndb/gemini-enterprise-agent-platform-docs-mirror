---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.interactionsHttp/cancel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.interactionsHttp/cancel
title: 'Method: interactionsHttp.cancel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.interactionsHttp.cancel

Cancels an interaction by id. This only applies to background interactions that are still running.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name} /cancel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the interaction to cancel. Format: `interactions/{interaction}` .

### Request body

The request body must be empty.

### Response body

If successful, the response is a generic HTTP response whose format is defined by the method.
