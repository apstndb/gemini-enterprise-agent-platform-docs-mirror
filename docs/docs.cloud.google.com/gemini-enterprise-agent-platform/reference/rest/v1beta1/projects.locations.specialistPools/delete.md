---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools/delete
title: 'Method: specialistPools.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.specialistPools.delete

Deletes a SpecialistPool as well as all Specialists in the pool.

### Endpoint

delete `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the SpecialistPool to delete. Format: `projects/{project}/locations/{location}/specialistPools/{specialistPool}`

### Query parameters

`force` `boolean`

If set to true, any specialist managers in this SpecialistPool will also be deleted. (Otherwise, the request will only work if the SpecialistPool has no specialist managers.)

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
