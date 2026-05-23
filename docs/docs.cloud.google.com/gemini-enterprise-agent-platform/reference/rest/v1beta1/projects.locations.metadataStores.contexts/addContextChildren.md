---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts/addContextChildren
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.metadataStores.contexts/addContextChildren
title: 'Method: contexts.addContextChildren'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.contexts.addContextChildren

Adds a set of Contexts as children to a parent Context. If any of the child Contexts have already been added to the parent Context, they are simply skipped. If this call would create a cycle or cause any Context to have more than 10 parents, the request will fail with an INVALID\_ARGUMENT error.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{context}:addContextChildren`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`context` `string`

Required. The resource name of the parent Context.

Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`

### Request body

The request body contains data with the following structure:

Fields

`childContexts[]` `string`

The resource names of the child Contexts.

### Response body

If successful, the response body is empty.
