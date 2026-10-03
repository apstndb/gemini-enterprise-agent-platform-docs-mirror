---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess
title: 'Method: datasets.assess'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.assess

Assesses the state or validity of the dataset with respect to a given use case.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:assess`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the Dataset resource. Used only for MULTIMODAL datasets. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

### Request body

The request body contains data with the following structure:

Fields

`geminiRequestReadConfig` `object ( `[`GeminiRequestReadConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiRequestReadConfig)` )`

Optional. The Gemini request read config for the dataset.

`assessment_config` `Union type`

The assessment type. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`tuningValidationAssessmentConfig` `object ( `[`TuningValidationAssessmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess#TuningValidationAssessmentConfig)` )`

Optional. Configuration for the tuning validation assessment.

`tuningResourceUsageAssessmentConfig` `object ( `[`TuningResourceUsageAssessmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess#TuningResourceUsageAssessmentConfig)` )`

Optional. Configuration for the tuning resource usage assessment.

`batchPredictionValidationAssessmentConfig` `object ( `[`BatchPredictionValidationAssessmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess#BatchPredictionValidationAssessmentConfig)` )`

Optional. Configuration for the batch prediction validation assessment.

`batchPredictionResourceUsageAssessmentConfig` `object ( `[`BatchPredictionResourceUsageAssessmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess#BatchPredictionResourceUsageAssessmentConfig)` )`

Optional. Configuration for the batch prediction resource usage assessment.

End of mutually exclusive fields.

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

## TuningValidationAssessmentConfig

Configuration for the tuning validation assessment.

Fields

`modelName` `string`

Required. The name of the model used for tuning.

`datasetUsage` `enum ( `[`DatasetUsage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess#DatasetUsage)` )`

Required. The dataset usage (e.g. training/validation).

**JSON representation**

```
{
  "modelName": string,
  "datasetUsage": enum (DatasetUsage)
}
```

## DatasetUsage

The dataset usage (e.g. training/validation).

| Enums                       |                                            |
|-----------------------------|--------------------------------------------|
| `DATASET_USAGE_UNSPECIFIED` | Default value. Should not be used.         |
| `SFT_TRAINING`              | Supervised fine-tuning training dataset.   |
| `SFT_VALIDATION`            | Supervised fine-tuning validation dataset. |

## TuningResourceUsageAssessmentConfig

Configuration for the tuning resource usage assessment.

Fields

`modelName` `string`

Required. The name of the model used for tuning.

**JSON representation**

```
{
  "modelName": string
}
```

## BatchPredictionValidationAssessmentConfig

Configuration for the batch prediction validation assessment.

Fields

`modelName` `string`

Required. The name of the model used for batch prediction.

**JSON representation**

```
{
  "modelName": string
}
```

## BatchPredictionResourceUsageAssessmentConfig

Configuration for the batch prediction resource usage assessment.

Fields

`modelName` `string`

Required. The name of the model used for batch prediction.

**JSON representation**

```
{
  "modelName": string
}
```
