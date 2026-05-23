---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.persistentResources/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.persistentResources/patch
title: 'Method: persistentResources.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.persistentResources.patch

Updates a PersistentResource.

### Endpoint

patch `https: / /{service-endpoint} /v1 /{persistentResource.name}`  

`PATCH https://{service-endpoint}/v1/{persistentResource.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`persistentResource.name` `string`

Immutable. Resource name of a PersistentResource.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. Specify the fields to be overwritten in the PersistentResource by the update method.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  PersistentResource  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
