---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/import
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/import
title: 'Method: extensions.import'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.extensions.import

Imports an Extension.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /extensions:import`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to import the Extension in. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains an instance of `  Extension  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
