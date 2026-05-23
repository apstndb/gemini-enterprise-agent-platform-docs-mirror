---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/evaluateDataset
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/evaluateDataset
title: 'Method: locations.evaluateDataset'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.evaluateDataset

Evaluates a dataset based on a set of given metrics.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{location}:evaluateDataset`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`location` `string`

Required. The resource name of the Location to evaluate the dataset. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`dataset` ` object ( EvaluationDataset  ` )

Required. The dataset used for evaluation.

`metrics[]` ` object ( Metric  ` )

Required. The metrics used for evaluation.

`outputConfig` ` object ( OutputConfig  ` )

Required. Config for evaluation output.

`autoraterConfig` ` object ( AutoraterConfig  ` )

Optional. Autorater config used for evaluation. Currently only publisher Gemini models are supported. Format: `projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL}.`

### Response body

If successful, the response body contains an instance of `  Operation  ` .
