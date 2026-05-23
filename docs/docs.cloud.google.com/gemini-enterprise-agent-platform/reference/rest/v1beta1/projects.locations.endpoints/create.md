---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/create
title: 'Method: endpoints.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.create

Creates an Endpoint.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /endpoints`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to create the Endpoint in. Format: `projects/{project}/locations/{location}`

### Query parameters

`endpointId` `string`

Immutable. The id to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Agent Platform will generate a value for this id.

If the first character is a letter, this value may be up to 63 characters, and valid characters are `[a-z0-9-]` . The last character must be a letter or number.

If the first character is a number, this value may be up to 9 characters, and valid characters are `[0-9]` with no leading zeros.

When using HTTP/JSON, this field is populated based on a query string argument, such as `?endpointId=12345` . This is the fallback for fields that are not included in either the URI or the body.

### Request body

The request body contains an instance of `  Endpoint  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
