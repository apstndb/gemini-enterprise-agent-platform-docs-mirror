---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects/fetchPublisherModelConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects/fetchPublisherModelConfig
title: 'Method: projects.fetchPublisherModelConfig'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.fetchPublisherModelConfig

Fetches the configs of publisher models.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{name}:fetchPublisherModelConfig`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the publisher model, in the format of `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}` .

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  PublisherModelConfig  ` .
