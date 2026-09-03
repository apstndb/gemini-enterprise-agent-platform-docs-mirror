---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.interactionsHttp/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.interactionsHttp/create
title: 'Method: interactionsHttp.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.interactionsHttp.create

Generates a set of responses from the model.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /interactionsHttp`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent resource where this interaction will be created. Format: `projects/{project}/locations/{location}`

Supported only by the Vertex API only.

### Request body

The request body contains data with the following structure:

Fields

`httpBody` ` object ( HttpBody  ` )

Required. The interaction to create.

### Response body

If successful, the response is a generic HTTP response whose format is defined by the method.
