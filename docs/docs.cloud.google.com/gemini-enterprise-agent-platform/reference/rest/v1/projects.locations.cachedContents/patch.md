---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.cachedContents/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.cachedContents/patch
title: 'Method: cachedContents.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.cachedContents.patch

Updates cached content configurations

### Endpoint

patch `https: / /{service-endpoint} /v1 /{cachedContent.name}`  

`PATCH https://{service-endpoint}/v1/{cachedContent.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`cachedContent.name` `string`

Immutable. Identifier. The server-generated resource name of the cached content Format: projects/{project}/locations/{location}/cachedContents/{cachedContent}

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. The list of fields to update.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  CachedContent  ` .

### Response body

If successful, the response body contains an instance of `  CachedContent  ` .
