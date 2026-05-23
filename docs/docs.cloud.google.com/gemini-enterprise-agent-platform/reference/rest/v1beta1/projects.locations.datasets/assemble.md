---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assemble
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assemble
title: 'Method: datasets.assemble'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.assemble

Assembles each row of a multimodal dataset and writes the result into a BigQuery table.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:assemble`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the Dataset resource (used only for MULTIMODAL datasets). Format: `projects/{project}/locations/{location}/datasets/{dataset}`

### Request body

The request body contains data with the following structure:

Fields

`geminiRequestReadConfig` ` object ( GeminiRequestReadConfig  ` )

Optional. The read config for the dataset.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
