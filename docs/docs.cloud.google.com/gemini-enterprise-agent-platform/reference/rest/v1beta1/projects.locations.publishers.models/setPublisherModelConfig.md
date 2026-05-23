---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.publishers.models/setPublisherModelConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.publishers.models/setPublisherModelConfig
title: 'Method: models.setPublisherModelConfig'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.publishers.models.setPublisherModelConfig

Sets (creates or updates) configs of publisher models. For example, sets the request/response logging config.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:setPublisherModelConfig`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the publisher model, in the format of `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}` .

### Request body

The request body contains data with the following structure:

Fields

`publisherModelConfig` ` object ( PublisherModelConfig  ` )

Required. The publisher model config.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
