---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.servingProfiles/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.servingProfiles/create
title: 'Method: servingProfiles.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.servingProfiles.create

Creates a ServingProfile.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /servingProfiles`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to create the ServingProfile in. Format: `projects/{project}/locations/{location}`

### Query parameters

`servingProfileId` `string`

Required. The id to use for the ServingProfile, which will become the final component of the ServingProfile's resource name. This value should be 1-63 characters, and valid characters are `^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$` .

### Request body

The request body contains an instance of `  ServingProfile  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
