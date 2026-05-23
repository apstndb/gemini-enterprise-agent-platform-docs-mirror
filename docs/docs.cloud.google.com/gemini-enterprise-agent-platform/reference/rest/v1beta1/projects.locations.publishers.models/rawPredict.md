---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.publishers.models/rawPredict
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.publishers.models/rawPredict
title: 'Method: models.rawPredict'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.publishers.models.rawPredict

Perform an online prediction with an arbitrary HTTP payload.

The response includes the following HTTP headers:

  - `X-Vertex-AI-Endpoint-id` : id of the `  Endpoint  ` that served this prediction.

  - `X-Vertex-AI-Deployed-Model-id` : id of the Endpoint's `  DeployedModel  ` that served this prediction.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint}:rawPredict`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains data with the following structure:

Fields

`httpBody` ` object ( HttpBody  ` )

The prediction input. Supports HTTP headers and arbitrary data payload.

A `  DeployedModel  ` may have an upper limit on the number of instances it supports per request. When this limit it is exceeded for an AutoML model, the `  models.rawPredict  ` method returns an error. When this limit is exceeded for a custom-trained model, the behavior varies depending on the model.

You can specify the schema for each instance in the `  predictSchemata.instance_schema_uri  ` field when you create a `  Model  ` . This schema applies when you deploy the `Model` as a `DeployedModel` to an `  Endpoint  ` and use the `models.rawPredict` method.

### Response body

If successful, the response is a generic HTTP response whose format is defined by the method.
