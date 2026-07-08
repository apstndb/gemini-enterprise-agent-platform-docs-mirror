---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/vertex-automl-component
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/vertex-automl-component
title: Gemini Enterprise Agent Platform AutoML components
description: Use dedicated AutoML components within your ML pipelines for automated model training.
data_source: docs.cloud.google.com
---

The AutoML `TrainingPipeline` resource orchestrates tasks associated with training an AutoML model. This resource always executes the training task, and optionally may also export data from a Gemini Enterprise Agent Platform `Dataset` which becomes the training input, upload the Model to Gemini Enterprise Agent Platform, and evaluate the Model. For information about AutoML training in Agent Platform, see the [AutoML training documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/training-overview#automl) . For information about Google Cloud Pipeline Components related to datasets, see [Dataset components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/dataset-component) .

The Google Cloud SDK includes the following operators related to AutoML models and workflows:

**Operators related to AutoML forecasting**

  - [`ProphetTrainerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/forecasting.html#v1.automl.forecasting.ProphetTrainerOp)

**Operators related to AutoML Tabular models**

  - [`CvTrainerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.CvTrainerOp)
  - [`EnsembleOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.EnsembleOp)
  - [`FinalizerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.FinalizerOp)
  - [`InfraValidatorOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.InfraValidatorOp)
  - [`SplitMaterializedDataOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.SplitMaterializedDataOp)
  - [`Stage1TunerOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.Stage1TunerOp)
  - [`StatsAndExampleGenOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.StatsAndExampleGenOp)
  - [`TrainingConfiguratorAndValidatorOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.TrainingConfiguratorAndValidatorOp)
  - [`TransformOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/tabular.html#v1.automl.tabular.TransformOp)

**Operators related to AutoML `model` resource creation**

  - [`AutoMLForecastingTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLForecastingTrainingJobRunOp)
  - [`AutoMLImageTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLImageTrainingJobRunOp)
  - [`AutoMLTabularTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLTabularTrainingJobRunOp)
  - [`AutoMLTextTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLTextTrainingJobRunOp)

[Learn more about training and using your own AutoML models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/training-overview#automl) .

## API reference

  - For AutoML component reference, see the [Google Cloud SDK reference for AutoML components](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html) .

  - For Agent Platform API reference, see the following API reference pages:
    
      - [`Dataset` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets)
    
      - [`TrainingPipeline` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines)

## Tutorials

  - [Learn how to use the Google Cloud pipeline components to train an image classification model using Gemini Enterprise Agent Platform AutoML.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_automl_images.ipynb)
  - [Learn how to use the Google Cloud pipeline components to train a classification model using tabular data and Gemini Enterprise Agent Platform AutoML.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/automl_tabular_classification_beans.ipynb)
  - [Learn how to use the Google Cloud pipeline components to train a linear regression model using tabular data and Gemini Enterprise Agent Platform AutoML.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_automl_tabular.ipynb)
  - [Learn how to use the Google Cloud pipeline components to train a text classification model using Gemini Enterprise Agent Platform AutoML.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_automl_text.ipynb)
  - [Learn how to use the Google Cloud pipeline components to upload and deploy a model.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_model_train_upload_deploy.ipynb)

## Version history and release notes

To learn more about the version history and changes to the Google Cloud Pipeline Components SDK, see the [Google Cloud Pipeline Components SDK Release Notes](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/release.html) .

### Technical support contacts

If you have any questions, reach out to [kubeflow-pipelines-components@google.com](mailto:%20kubeflow-pipelines-components@google.com) .
