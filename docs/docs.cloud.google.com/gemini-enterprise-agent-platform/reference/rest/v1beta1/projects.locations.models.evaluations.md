---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations
title: 'REST Resource: projects.locations.models.evaluations'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ModelEvaluation

A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data.

Fields

`name` `string`

Output only. The resource name of the ModelEvaluation.

`displayName` `string`

The display name of the ModelEvaluation.

`metricsSchemaUri` `string`

Points to a YAML file stored on Google Cloud Storage describing the [`metrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations#ModelEvaluation.FIELDS.metrics) of this ModelEvaluation. The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) .

`metrics` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Evaluation metrics of the Model. The schema of the metrics is stored in [`metricsSchemaUri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations#ModelEvaluation.FIELDS.metrics_schema_uri)

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ModelEvaluation was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`sliceDimensions[]` `string`

All possible [`dimensions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices#Slice.FIELDS.dimension) of ModelEvaluationSlices. The dimensions can be used as the filter of the [`ModelService.ListModelEvaluationSlices`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices/list#google.cloud.aiplatform.v1beta1.ModelService.ListModelEvaluationSlices) request, in the form of `slice.dimension = <dimension>` .

`modelExplanation` `object ( `[`ModelExplanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelExplanation)` )`

Aggregated explanation metrics for the Model's prediction output over the data this ModelEvaluation uses. This field is populated only if the Model is evaluated with explanations, and only for AutoML tabular Models.

`explanationSpecs[]` `object ( `[`ModelEvaluationExplanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations#ModelEvaluationExplanationSpec)` )`

Describes the values of [`ExplanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExplanationSpec) that are used for explaining the predicted values on the evaluated data.

`metadata` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

The metadata of the ModelEvaluation. For the ModelEvaluation uploaded from Managed Pipeline, metadata contains a structured value with keys of "pipelineJobId", "evaluation_dataset_type", "evaluation_dataset_path", "row_based_metrics_path".

`biasConfigs` `object ( `[`BiasConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations#BiasConfig)` )`

Specify the configuration for bias detection.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "metricsSchemaUri": string,
  "metrics": value,
  "createTime": string,
  "sliceDimensions": [
    string
  ],
  "modelExplanation": {
    object (ModelExplanation)
  },
  "explanationSpecs": [
    {
      object (ModelEvaluationExplanationSpec)
    }
  ],
  "metadata": value,
  "biasConfigs": {
    object (BiasConfig)
  }
}
```

## ModelEvaluationExplanationSpec

Fields

`explanationType` `string`

Explanation type.

For AutoML Image Classification models, possible values are:

- `image-integrated-gradients`
- `image-xrai`

`explanationSpec` `object ( `[`ExplanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExplanationSpec)` )`

Explanation spec details.

**JSON representation**

```
{
  "explanationType": string,
  "explanationSpec": {
    object (ExplanationSpec)
  }
}
```

## BiasConfig

Configuration for bias detection.

Fields

`biasSlices` `object ( `[`SliceSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SliceSpec)` )`

Specification for how the data should be sliced for bias. It contains a list of slices, with limitation of two slices. The first slice of data will be the slice_a. The second slice in the list (slice_b) will be compared against the first slice. If only a single slice is provided, then slice_a will be compared against "not slice_a". Below are examples with feature "education" with value "low", "medium", "high" in the dataset:

Example 1:

```
biasSlices = [{'education': 'low'}]
```

A single slice provided. In this case, slice_a is the collection of data with 'education' equals 'low', and slice_b is the collection of data with 'education' equals 'medium' or 'high'.

Example 2:

```
biasSlices = [{'education': 'low'},
               {'education': 'high'}]
```

Two slices provided. In this case, slice_a is the collection of data with 'education' equals 'low', and slice_b is the collection of data with 'education' equals 'high'.

`labels[]` `string`

Positive labels selection on the target field.

**JSON representation**

```
{
  "biasSlices": {
    object (SliceSpec)
  },
  "labels": [
    string
  ]
}
```

| Methods                                                                                                                                        |                                                  |
|------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations/get)       | Gets a ModelEvaluation.                          |
| [`import`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations/import) | Imports an externally generated ModelEvaluation. |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations/list)     | Lists ModelEvaluations in a Model.               |
