---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.specialistPools/patch
title: 'Method: specialistPools.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.specialistPools.patch

Updates a SpecialistPool.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{specialistPool.name}`  

`PATCH https://{service-endpoint}/v1beta1/{specialistPool.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`specialistPool.name` `string`

Required. The resource name of the SpecialistPool.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. The update mask applies to the resource.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  SpecialistPool  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
