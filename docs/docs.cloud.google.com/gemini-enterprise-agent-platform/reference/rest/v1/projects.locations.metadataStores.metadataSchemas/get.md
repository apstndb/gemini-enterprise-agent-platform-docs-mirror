---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.metadataSchemas/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.metadataSchemas/get
title: 'Method: metadataSchemas.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.metadataSchemas.get

Retrieves a specific MetadataSchema.

### Endpoint

get `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the MetadataSchema to retrieve. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/metadataSchemas/{metadataschema}`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  MetadataSchema  ` .
