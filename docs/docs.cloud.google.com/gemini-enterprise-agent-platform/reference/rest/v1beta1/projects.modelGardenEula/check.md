---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.modelGardenEula/check
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.modelGardenEula/check
title: 'Method: modelGardenEula.check'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.modelGardenEula.check

Checks the EULA acceptance status of a publisher model.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /modelGardenEula:check`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The project requesting access for named model. The format is `projects/{project}` .

### Request body

The request body contains data with the following structure:

Fields

`publisherModel` `string`

Required. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisherModel}` , or `publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}`

### Response body

If successful, the response body contains an instance of `  PublisherModelEulaAcceptance  ` .
