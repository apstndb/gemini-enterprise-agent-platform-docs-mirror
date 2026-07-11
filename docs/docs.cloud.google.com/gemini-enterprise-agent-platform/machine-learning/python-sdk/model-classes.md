---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/model-classes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/model-classes
title: Model classes
description: Learn about the model class, which represents a trained model that is registered in the Gemini Enterprise Agent Platform Model Registry.
data_source: docs.cloud.google.com
---

The Vertex AI SDK includes the [`Model`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model) class to work with a model that you train and then use for predictions. The SDK also includes the [`ModelEvaluation`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelEvaluation) class to evaluate metrics on trained AutoML models. For more information about models, see [Train and use your own models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview) .

### [`Model`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model)

The [`Model`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model) class represents a trained model that is registered in the Gemini Enterprise Agent Platform Model Registry. You use a trained model to generate predictions.

Use the [`aiplatform.Model()`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#parameters) method to find and return a reference to a model. You can specify a model using its name or ID. Because more than one model in a project can share the same name, we recommend specifying a model with its model ID. The following code sample shows how to use a model ID to find and return a reference to an existing model:

    MODEL_ID="my-sample-model-ID"
    model = aiplatform.Model(model_name=MODEL_ID)

After you have a reference to a trained model, you can use the [properties](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#properties) and [methods](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#methods) of the [`Model`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model) to work with it and get predictions.

#### Create a registered model

To create a model resource that's registered in the Gemini Enterprise Agent Platform Model Registry, call the `run` method on a training job class. The following methods create a model, train the model, register the model in the Gemini Enterprise Agent Platform Model Registry, then return a reference to the model.

  - [`AutoMLForecastingTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLForecastingTrainingJob#google_cloud_aiplatform_AutoMLForecastingTrainingJob_run)
  - [`AutoMLImageTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLImageTrainingJob#google_cloud_aiplatform_AutoMLImageTrainingJob_run)
  - [`AutoMLTabularTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTabularTrainingJob#google_cloud_aiplatform_AutoMLTabularTrainingJob_run)
  - [`AutoMLTextTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTextTrainingJob#google_cloud_aiplatform_AutoMLTextTrainingJob_run)
  - [`AutoMLVideoTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLVideoTrainingJob#google_cloud_aiplatform_AutoMLVideoTrainingJob_run)
  - [`CustomContainerTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob#google_cloud_aiplatform_CustomContainerTrainingJob_run)
  - [`CustomPythonPackageTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob#google_cloud_aiplatform_CustomPythonPackageTrainingJob_run)
  - [`CustomTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob#google_cloud_aiplatform_CustomTrainingJob_run)

The following sample code shows you how to create a `CustomTrainingJob` resource and then use its `run` method to create a model, train the model, register the model in the Gemini Enterprise Agent Platform Model Registry, and return a reference to the model:

    # Create a custom training job using a script
    job = aiplatform.CustomTrainingJob(
        display_name="my-training-job",
        script_path="task.py",
        container_uri="us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-8:latest",
        requirements=["google-cloud-bigquery>=2.20.0", "db-dtypes", "protobuf<3.20.0"],
        model_serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-8:latest",
    )
    
    # Create and train your model using a BigQuery dataset. The method
    # returns a reference to the trained model.
    model = job.run(
        dataset=dataset,
        model_display_name="my-model-name",
        bigquery_destination=f"bq://{project_id}",
        args=CMDARGS,
    )

#### Create an unregistered model

To create a model that's not registered to the Gemini Enterprise Agent Platform Model Registry, use the [`CustomJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob) class and its `run` method. The [`CustomJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob#google_cloud_aiplatform_CustomJob_run) method trains a model, but it doesn't register the model in the Gemini Enterprise Agent Platform Model Registry and it doesn't return a reference to the model.

If you use the `CustomJob` class, you need to use a script to write your model to a location such as a Cloud Storage bucket. For more information, see [Export a trained ML model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#export) .

#### Register a model

If you have a model that isn't registered with the Gemini Enterprise Agent Platform Model Registry, then you need to register it so you can manage your model's lifecycle. Gemini Enterprise Agent Platform Model Registry is a central repository that provides an overview of your models so you can manage them. For more information, see [Introduction to Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction) .

The Vertex AI SDK includes the following methods to import a model to the Gemini Enterprise Agent Platform Model Registry. Click one of the methods to learn more about it in the Vertex AI SDK reference guide.

  - [`Model.upload`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#google_cloud_aiplatform_Model_upload)
  - [`Model.upload_scikit_learn_model_file`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#google_cloud_aiplatform_Model_upload_scikit_learn_model_file)
  - [`Model.upload_tensorflow_saved_model`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#google_cloud_aiplatform_Model_upload_tensorflow_saved_model)
  - [`Model.upload_xgboost_model_file`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#google_cloud_aiplatform_Model_upload_xgboost_model_file)

#### Deploy a model

After you register a model, you need to deploy the model to an endpoint before you can use it for predictions. Use the [`Model.deploy`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model#google_cloud_aiplatform_Model_deploy) method to deploy your model to an [`Endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/prediction-classes#endpoint) . For more information, see [Deploy a model to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) .

### [`ModelEvaluation`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelEvaluation)

Use the [`ModelEvaluation`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelEvaluation) class to get evaluation metrics for AutoML models, such as precision and recall, to help determine the performance of your models. For more information, see [Model evaluation in Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/evaluation/introduction) .

The following code sample shows how to list all evaluations for a model with model ID `model-id` that's in a project with a project ID of `my-project` and that's in the `us-central1` region:

    model = aiplatform.Model('projects/my-project/locations/us-central1/models/{model-id}')
    
    evaluations = model.list_model_evaluations()

The following code sample shows how to get the model evaluation for a model with model ID `model-id` that's in a project with a project ID of `my-project` and that's in the `us-central1` region:

    model = aiplatform.Model('projects/my-project/locations/us-central1/models/{model-id}')
    
    # Return the first evaluation with no arguments. You can also specify a model
    # using its model ID.
    evaluation = model.get_model_evaluation()
    
    eval_metrics = evaluation.metrics

To create a reference to a model evaluation, use its resource name or model ID and the evaluation ID. The following code sample shows how to create a reference to a model evaluation using its resource name:

    evaluation = aiplatform.ModelEvaluation(
      evaluation_name='projects/my-project/locations/us-central1/
        models/{model-id}/evaluations/{evaluation-id}')
    
    eval_metrics = evaluation.metrics

The following code sample shows how to create a reference to a model evaluation using the model ID and the evaluation ID:

    evaluation.metrics = aiplatform.ModelEvaluation(
      evaluation_name={evaluation-id},
      model_id={model-id})
    
    eval_metrics = evaluation.metrics

## What's next

  - Learn about the [Vertex AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) .
