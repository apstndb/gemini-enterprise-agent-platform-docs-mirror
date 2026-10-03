---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutoraterConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutoraterConfig
title: AutoraterConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The configs for autorater. This is applicable to both EvaluateInstances and EvaluateDataset.

Fields

`autoraterModel` `string`

Optional. The fully qualified name of the publisher model or tuned autorater endpoint to use.

Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`

Tuned model endpoint format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

`generationConfig` `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#GenerationConfig)` )`

Optional. Configuration options for model generation and outputs.

`samplingCount` `integer`

Optional. Number of samples for each instance in the dataset. If not specified, the default is 4. Minimum value is 1, maximum value is 32.

`flipEnabled` `boolean`

Optional. Default is true. Whether to flip the candidate and baseline responses. This is only applicable to the pairwise metric. If enabled, also provide PairwiseMetricSpec.candidate_response_field_name and PairwiseMetricSpec.baseline_response_field_name. When rendering PairwiseMetricSpec.metric_prompt_template, the candidate and baseline fields will be flipped for half of the samples to reduce bias.

**JSON representation**

```
{
  "autoraterModel": string,
  "generationConfig": {
    object (GenerationConfig)
  },
  "samplingCount": integer,
  "flipEnabled": boolean
}
```
