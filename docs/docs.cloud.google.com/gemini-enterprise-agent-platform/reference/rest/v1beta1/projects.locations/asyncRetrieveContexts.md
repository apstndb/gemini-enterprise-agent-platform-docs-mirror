---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/asyncRetrieveContexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/asyncRetrieveContexts
title: 'Method: locations.asyncRetrieveContexts'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.asyncRetrieveContexts

Asynchronous API to retrieves relevant contexts for a query.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent}:asyncRetrieveContexts`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .

### Request body

The request body contains data with the following structure:

Fields

`query` ` object ( RagQuery  ` )

Required. Single RAG retrieve query.

`tools[]` ` object ( Tool  ` )

Optional. The tools to use for locations.askContexts.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
