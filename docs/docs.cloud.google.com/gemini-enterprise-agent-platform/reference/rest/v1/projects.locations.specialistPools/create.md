---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.specialistPools/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.specialistPools/create
title: 'Method: specialistPools.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.specialistPools.create

Creates a SpecialistPool.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /specialistPools`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent Project name for the new SpecialistPool. The form is `projects/{project}/locations/{location}` .

### Request body

The request body contains an instance of `  SpecialistPool  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
