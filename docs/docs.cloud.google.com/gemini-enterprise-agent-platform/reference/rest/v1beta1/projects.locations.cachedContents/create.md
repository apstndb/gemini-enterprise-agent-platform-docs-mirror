---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.cachedContents/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.cachedContents/create
title: 'Method: cachedContents.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.cachedContents.create

Creates cached content, this call will initialize the cached content in the data storage, and users need to pay for the cache data storage.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /cachedContents`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent resource where the cached content will be created

### Request body

The request body contains an instance of `  CachedContent  ` .

### Response body

If successful, the response body contains a newly created instance of `  CachedContent  ` .
