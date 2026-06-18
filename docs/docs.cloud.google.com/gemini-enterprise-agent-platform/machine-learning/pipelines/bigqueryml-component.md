---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/bigqueryml-component
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/bigqueryml-component
title: BigQuery ML components
description: Learn how to use BigQuery components to orchestrate BigQuery operations within Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

BigQuery ML components orchestrate tasks associated with BigQuery ML operations. See [BigQuery ML documentation](https://docs.cloud.google.com/bigquery/docs/bqml-introduction) .

## BigQuery ML operators

The Google Cloud SDK includes the following operators related to BigQuery ML resources:

  - [`BigqueryCreateModelJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryCreateModelJobOp)
  - [`BigqueryDetectAnomaliesModelJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryDetectAnomaliesModelJobOp)
  - [`BigqueryDropModelJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryDropModelJobOp)
  - [`BigqueryEvaluateModelJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryEvaluateModelJobOp)
  - [`BigqueryExplainForecastModelJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryExplainForecastModelJobOp)
  - [`BigqueryExplainPredictModelJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryExplainPredictModelJobOp)
  - [`BigqueryExportModelJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryExportModelJobOp)
  - [`BigqueryForecastModelJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryForecastModelJobOp)
  - [`BigqueryMLAdvancedWeightsJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLAdvancedWeightsJobOp)
  - [`BigqueryMLArimaCoefficientsJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLArimaCoefficientsJobOp)
  - [`BigqueryMLArimaEvaluateJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLArimaEvaluateJobOp)
  - [`BigqueryMLCentroidsJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLCentroidsJobOp)
  - [`BigqueryMLConfusionMatrixJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLConfusionMatrixJobOp)
  - [`BigqueryMLFeatureImportanceJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLFeatureImportanceJobOp)
  - [`BigqueryMLFeatureInfoJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLFeatureInfoJobOp)
  - [`BigqueryMLGlobalExplainJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLGlobalExplainJobOp)
  - [`BigqueryMLPrincipalComponentInfoJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLPrincipalComponentInfoJobOp)
  - [`BigqueryMLPrincipalComponentsJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLPrincipalComponentsJobOp)
  - [`BigqueryMLRecommendJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLRecommendJobOp)
  - [`BigqueryMLReconstructionLossJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLReconstructionLossJobOp)
  - [`BigqueryMLRocCurveJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLRocCurveJobOp)
  - [`BigqueryMLTrainingInfoJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLTrainingInfoJobOp)
  - [`BigqueryMLTrialInfoJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLTrialInfoJobOp)
  - [`BigqueryMLWeightsJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryMLWeightsJobOp)
  - [`BigqueryPredictModelJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryPredictModelJobOp)
  - [`BigqueryQueryJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html#v1.bigquery.BigqueryQueryJobOp)

## API reference

  - For component reference, see the [Google Cloud SDK reference for BigQuery ML components](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/bigquery.html) .

  - [BigQuery ML API reference](https://docs.cloud.google.com/bigquery/docs/reference/rest)

## Tutorial

  - [Get started with BigQuery ML pipeline components](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/ml_ops/stage3/get_started_with_bqml_pipeline_components.ipynb)
  - [Train and evaluate a demand forecasting model](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/pipelines/google_cloud_pipeline_components_bqml_pipeline_demand_forecasting.ipynb)

## Version history and release notes

To learn more about the version history and changes to the Google Cloud Pipeline Components SDK, see the [Google Cloud Pipeline Components SDK Release Notes](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/release.html) .

## Technical support contacts

If you have any questions, reach out to [bqml-feedback@google.com](mailto:%20bqml-feedback@google.com) .
