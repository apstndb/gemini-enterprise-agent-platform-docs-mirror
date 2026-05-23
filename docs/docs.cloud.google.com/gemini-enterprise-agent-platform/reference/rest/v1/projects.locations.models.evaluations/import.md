---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations/import
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations/import
title: 'Method: evaluations.import'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.evaluations.import

Imports an externally generated ModelEvaluation.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /evaluations:import`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the parent model resource. Format: `projects/{project}/locations/{location}/models/{model}`

### Request body

The request body contains data with the following structure:

Fields

`modelEvaluation` ` object ( ModelEvaluation  ` )

Required. Model evaluation resource to be imported.

### Response body

If successful, the response body contains an instance of `  ModelEvaluation  ` .
