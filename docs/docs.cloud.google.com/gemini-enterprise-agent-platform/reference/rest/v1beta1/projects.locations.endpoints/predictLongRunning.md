---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/predictLongRunning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/predictLongRunning
title: 'Method: endpoints.predictLongRunning'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.predictLongRunning

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint}:predictLongRunning`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` or `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}`

### Request body

The request body contains data with the following structure:

Fields

`instances[]` ` value ( Value  ` format)

Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' `  Model's  ` `  PredictSchemata's  ` `  instanceSchemaUri  ` .

`parameters` ` value ( Value  ` format)

Optional. The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' `  Model's  ` `  PredictSchemata's  ` `  parametersSchemaUri  ` .

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only.

label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. label values are optional. label keys must start with a letter.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
