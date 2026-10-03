---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/generateInstanceRubrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations/generateInstanceRubrics
title: 'Method: locations.generateInstanceRubrics'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.generateInstanceRubrics

Generates rubrics for a given prompt. A rubric represents a single testable criterion for evaluation. One input prompt could have multiple rubrics This RPC allows users to get suggested rubrics based on provided prompt, which can then be reviewed and used for subsequent evaluations.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{location}:generateInstanceRubrics`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`location` `string`

Required. The resource name of the Location to generate rubrics from. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`contents[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content)` )`

Required. The prompt to generate rubrics from. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request.

`predefinedRubricGenerationSpec` `object ( `[`PredefinedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#PredefinedMetricSpec)` )`

Optional. Specification for using the rubric generation configs of a pre-defined metric, e.g. "generic_quality_v1" and "instruction_following_v1". Some of the configs may be only used in rubric generation and not supporting evaluation, e.g. "fully_customized_generic_quality_v1". If this field is set, the `rubricGenerationSpec` field will be ignored.

`rubricGenerationSpec` `object ( `[`RubricGenerationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#RubricGenerationSpec)` )`

Optional. Specification for how the rubrics should be generated.

`agentConfig` `object ( `[`DeprecatedAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DeprecatedAgentConfig)` )`

Optional. Agent configuration, required for agent-based rubric generation.

`metricResourceName` `string`

Optional. The resource name of a registered metric. Rubric generation using predefined metric spec or LLMBasedMetricSpec is supported. If this field is set, the configuration provided in this field is used for rubric generation. The `predefinedRubricGenerationSpec` and `rubricGenerationSpec` fields will be ignored.

### Response body

Response message for EvaluationService.GenerateInstanceRubrics.

If successful, the response body contains data with the following structure:

Fields

`generatedRubrics[]` `object ( `[`Rubric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Rubric)` )`

Output only. A list of generated rubrics.

**JSON representation**

```
{
  "generatedRubrics": [
    {
      object (Rubric)
    }
  ]
}
```
