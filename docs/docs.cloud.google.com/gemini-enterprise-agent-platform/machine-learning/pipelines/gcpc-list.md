---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/gcpc-list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/gcpc-list
title: Google Cloud Pipeline Components list
description: Explore a list of {{dynamic_data.site_values.cloud_name}} Pipeline Components available for use with your ML workflows in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

Google Cloud Pipeline Components are released in two stages:

  - Generally available (v1.0 and later)

  - Preview

For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

## Generally available (1.0 and later) components

Generally available (GA) Google Cloud Pipeline Components are available in the `v1` namespace of the Google Cloud Pipeline Components SDK. These components have a stable interface and are ready to be used in a production environment.

### AutoML components

#### AutoML Forecasting components

The Google Cloud SDK includes the following operators related to AutoML forecasting:

  - [`ProphetTrainerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/forecasting.html#v1.automl.forecasting.ProphetTrainerOp)

#### AutoML Tabular components

The Google Cloud SDK includes the following operators related to AutoML tabular:

  - [`CvTrainerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.CvTrainerOp)
  - [`EnsembleOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.EnsembleOp)
  - [`FinalizerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.FinalizerOp)
  - [`InfraValidatorOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.InfraValidatorOp)
  - [`SplitMaterializedDataOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.SplitMaterializedDataOp)
  - [`Stage1TunerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.Stage1TunerOp)
  - [`StatsAndExampleGenOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.StatsAndExampleGenOp)
  - [`TrainingConfiguratorAndValidatorOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.TrainingConfiguratorAndValidatorOp)
  - [`TransformOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.TransformOp)

#### AutoML Training Job components

The Google Cloud SDK includes the following operators related to AutoML training jobs:

  - [`AutoMLForecastingTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLForecastingTrainingJobRunOp)
  - [`AutoMLImageTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLImageTrainingJobRunOp)
  - [`AutoMLTabularTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLTabularTrainingJobRunOp)
  - [`AutoMLTextTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLTextTrainingJobRunOp)

### Batch Prediction components

The Google Cloud SDK includes the following operators related to Batch Prediction:

  - [`ModelBatchPredictOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/batch_predict_job.html#v1.batch_predict_job.ModelBatchPredictOp)

### BigQuery ML components

The Google Cloud SDK includes the following operators for creating and executing machine learning models using BigQuery:

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

### Custom Job components

The Google Cloud SDK includes the following operators for running KFP components as Gemini Enterprise Custom Training jobs:

  - [`CustomTrainingJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.CustomTrainingJobOp)

### Dataflow components

The Google Cloud SDK includes the following operators related to Dataflow:

  - [`DataflowFlexTemplateJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html#preview.dataflow.DataflowFlexTemplateJobOp)
  - [`DataflowPythonJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html#v1.dataflow.DataflowPythonJobOp)

### Managed Service for Apache Spark components

The Google Cloud SDK includes the following operators related to Managed Service for Apache Spark:

  - [`DataprocPySparkBatchOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataproc.html#v1.dataproc.DataprocPySparkBatchOp)
  - [`DataprocSparkBatchOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataproc.html#v1.dataproc.DataprocSparkBatchOp)
  - [`DataprocSparkRBatchOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataproc.html#v1.dataproc.DataprocSparkRBatchOp)
  - [`DataprocSparkSqlBatchOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataproc.html#v1.dataproc.DataprocSparkSqlBatchOp)

### Dataset components

The Google Cloud SDK includes the following operators for AutoML `dataset` resource management:

  - [`GetVertexDatasetOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.GetVertexDatasetOp)
  - [`ImageDatasetCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.ImageDatasetCreateOp)
  - [`ImageDatasetExportDataOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.ImageDatasetExportDataOp)
  - [`ImageDatasetImportDataOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.ImageDatasetImportDataOp)
  - [`TabularDatasetCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.TabularDatasetCreateOp)
  - [`TabularDatasetExportDataOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.TabularDatasetExportDataOp)
  - [`TextDatasetCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.TextDatasetCreateOp)
  - [`TextDatasetExportDataOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.TextDatasetExportDataOp)
  - [`TextDatasetImportDataOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.TextDatasetImportDataOp)
  - [`TimeSeriesDatasetCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.TimeSeriesDatasetCreateOp)
  - [`TimeSeriesDatasetExportDataOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.TimeSeriesDatasetExportDataOp)

### Endpoint components

The Google Cloud SDK includes the following operators related to model serving endpoints:

  - [`EndpointCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/endpoint.html#v1.endpoint.EndpointCreateOp)
  - [`EndpointDeleteOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/endpoint.html#v1.endpoint.EndpointDeleteOp)
  - [`ModelDeployOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/endpoint.html#v1.endpoint.ModelDeployOp)
  - [`ModelUndeployOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/endpoint.html#v1.endpoint.ModelUndeployOp)

### Forecasting components

The Google Cloud SDK includes the following operators related to forecasting:

  - [`ForecastingPrepareDataForTrainOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/forecasting.html#v1.forecasting.ForecastingPrepareDataForTrainOp)
  - [`ForecastingPreprocessingOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/forecasting.html#v1.forecasting.ForecastingPreprocessingOp)
  - [`ForecastingValidationOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/forecasting.html#v1.forecasting.ForecastingValidationOp)

### Hyperparameter Tuning components

The Google Cloud SDK includes the following operators related to hyperparameter tuning jobs:

  - [`HyperparameterTuningJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/hyperparameter_tuning_job.html#v1.hyperparameter_tuning_job.HyperparameterTuningJobRunOp)

### Model components

The Google Cloud SDK includes the following operators for managing models through the Gemini Enterprise Agent Platform Model Registry:

  - [`ModelDeleteOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model.html#v1.model.ModelDeleteOp)
  - [`ModelExportOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model.html#v1.model.ModelExportOp)
  - [`ModelUploadOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model.html#v1.model.ModelUploadOp)

### Model evaluation components

The Google Cloud SDK includes the following operators related to model evaluation:

  - [`ModelEvaluationClassificationOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model_evaluation.html#v1.model_evaluation.ModelEvaluationClassificationOp)
  - [`ModelEvaluationForecastingOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model_evaluation.html#v1.model_evaluation.ModelEvaluationForecastingOp)
  - [`ModelEvaluationRegressionOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/model_evaluation.html#v1.model_evaluation.ModelEvaluationRegressionOp)

### Email notification components

The Google Cloud SDK includes the following operators for managing email notifications:

  - [`VertexNotificationEmailOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/vertex_notification_email.html#v1.vertex_notification_email.VertexNotificationEmailOp)

### Components related to wait on resources

The Google Cloud SDK includes the following operator related to waiting on resource creation:

  - [`WaitGcpResourcesOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/wait_gcp_resources.html#v1.wait_gcp_resources.WaitGcpResourcesOp)

## Preview components

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Google Cloud Pipeline Components in the Preview stage are available in the `preview` namespace of the Google Cloud Pipeline Components SDK.

### AutoML components

#### AutoML Forecasting components

The Google Cloud SDK includes the following preview operators related to AutoML forecasting:

  - [`ForecastingEnsembleOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/forecasting.html#preview.automl.forecasting.ForecastingEnsembleOp)
  - [`ForecastingStage1TunerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/forecasting.html#preview.automl.forecasting.ForecastingStage1TunerOp)
  - [`ForecastingStage2TunerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/forecasting.html#preview.automl.forecasting.ForecastingStage2TunerOp)

#### AutoML Tabular components

The Google Cloud SDK includes the following preview operators related to AutoML tabular:

  - [`AutoFeatureEngineeringOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/tabular.html#preview.automl.tabular.AutoFeatureEngineeringOp)
  - [`DistillationStageFeatureTransformEngineOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/tabular.html#preview.automl.tabular.DistillationStageFeatureTransformEngineOp)
  - [`FeatureSelectionOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/tabular.html#preview.automl.tabular.FeatureSelectionOp)
  - [`FeatureTransformEngineOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/tabular.html#preview.automl.tabular.FeatureTransformEngineOp)
  - [`WideAndDeepHyperparameterTuningJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/tabular.html#preview.automl.tabular.WideAndDeepHyperparameterTuningJobOp)
  - [`WideAndDeepTrainerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/tabular.html#preview.automl.tabular.WideAndDeepTrainerOp)
  - [`XGBoostHyperparameterTuningJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/tabular.html#preview.automl.tabular.XGBoostHyperparameterTuningJobOp)
  - [`XGBoostTrainerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/automl/tabular.html#preview.automl.tabular.XGBoostTrainerOp)

### Custom Job components

The Google Cloud SDK includes the following preview operators for running KFP components as Gemini Enterprise API Custom Training jobs:

  - [`CustomTrainingJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/custom_job.html#preview.custom_job.CustomTrainingJobOp)

### Dataflow components

The Google Cloud SDK includes the following preview operators related to Dataflow:

  - [`DataflowFlexTemplateJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/dataflow.html#preview.dataflow.DataflowFlexTemplateJobOp)

### Large-language model (LLM) components

The Google Cloud SDK includes the following preview operators related to LLMs:

  - [`infer_pipeline`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/llm.html#preview.llm.infer_pipeline)
  - [`rlhf_pipeline`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/llm.html#preview.llm.rlhf_pipeline)

### Model evaluation components

The Google Cloud SDK includes the following preview operators related to model evaluation:

  - [`DetectDataBiasOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/model_evaluation.html#preview.model_evaluation.DetectDataBiasOp)
  - [`DetectModelBiasOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/model_evaluation.html#preview.model_evaluation.DetectModelBiasOp)
  - [`ModelEvaluationFeatureAttributionOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/preview/model_evaluation.html#preview.model_evaluation.ModelEvaluationFeatureAttributionOp)

## What's next

  - See the following reference pages for specific Google Cloud Pipeline Components information:
    
      - [Dataflow components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/dataflow-component)
    
      - [Managed Service for Apache Spark components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/dataproc-component)
    
      - [CustomJob components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/customjob-component)
    
      - [Batch prediction component](https://docs.cloud.google.com/vertex-ai/docs/pipelines/batchprediction-component)
    
      - [Model and endpoint components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/model-endpoint-component)
    
      - [Model evaluation component](https://docs.cloud.google.com/vertex-ai/docs/pipelines/model-evaluation-component)
    
      - [Gemini Enterprise Agent Platform (aiplatform) AutoML components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/vertex-automl-component)
