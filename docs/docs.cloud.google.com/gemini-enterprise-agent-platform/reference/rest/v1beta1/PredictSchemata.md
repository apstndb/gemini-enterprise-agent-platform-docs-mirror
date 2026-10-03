---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata
title: PredictSchemata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Contains the schemata used in Model's predictions and explanations via [`PredictionService.Predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/predict#google.cloud.aiplatform.v1beta1.PredictionService.Predict) , [`PredictionService.Explain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/explain#google.cloud.aiplatform.v1beta1.PredictionService.Explain) and [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob) .

Fields

`instanceSchemaUri` `string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in [`PredictRequest.instances`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/predict#body.request_body.FIELDS.instances) , [`ExplainRequest.instances`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/explain#body.request_body.FIELDS.instances) and [`BatchPredictionJob.input_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.input_config) . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`parametersSchemaUri` `string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via [`PredictRequest.parameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/predict#body.request_body.FIELDS.parameters) , [`ExplainRequest.parameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/explain#body.request_body.FIELDS.parameters) and [`BatchPredictionJob.model_parameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.model_parameters) . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform, if no parameters are supported, then it is set to an empty string. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`predictionSchemaUri` `string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via [`PredictResponse.predictions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictResponse#FIELDS.predictions) , [`ExplainResponse.explanations`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/explain#body.ExplainResponse.FIELDS.explanations) , and [`BatchPredictionJob.output_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.output_config) . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

**JSON representation**

```
{
  "instanceSchemaUri": string,
  "parametersSchemaUri": string,
  "predictionSchemaUri": string
}
```
