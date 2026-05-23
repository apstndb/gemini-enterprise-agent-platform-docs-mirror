---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.specialistPools/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.specialistPools/get
title: 'Method: specialistPools.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.specialistPools.get

Gets a SpecialistPool.

### Endpoint

get `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the SpecialistPool resource. The form is `projects/{project}/locations/{location}/specialistPools/{specialistPool}` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  SpecialistPool  ` .
