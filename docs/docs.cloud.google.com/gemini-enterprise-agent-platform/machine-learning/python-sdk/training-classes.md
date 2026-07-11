---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/training-classes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/training-classes
title: Training classes
description: Learn about the Vertex AI SDK classes that you use to create, train, and return your model.
data_source: docs.cloud.google.com
---

The Vertex AI SDK includes several classes that you use when you train your model. Most of the training classes are used to create, train, and return your model. Use the [`HyperparameterTuningJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob) to tune the training job's hyperparameters. Use the [`PipelineJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob) manage your machine learning (ML) workflow so you can automate and monitor your ML systems.

The following topics provide a high-level description of each training-related class in the Vertex AI SDK.

## AutoML training classes for structured data

Vertex AI SDK includes the following classes that are used to train a structured AutoML model.

### [`AutoMLForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLForecastingTrainingJob)

The [`AutoMLForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLForecastingTrainingJob) class uses the `AutoML` training method to train and run a forecasting model. The `AutoML` training method is a good choice for most forecasting use cases. If your use case doesn't benefit from the `Seq2seq` or the `Temporal fusion transformer` training method that the [`SequenceToSequencePlusForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob) and [`TemporalFusionTransformerForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob) classes offer respectively, then `AutoML` is likely the best training method for your forecasting predictions.

For sample code that shows you how to use [`AutoMLForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLForecastingTrainingJob) , see the [Create a training pipeline forecasting sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_sample.py) on GitHub.

### [`AutoMLTabularTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTabularTrainingJob)

The [`AutoMLTabularTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTabularTrainingJob) class represents a job that creates, trains, and returns an `AutoML` tabular model. For more information about training tabular models and Gemini Enterprise Agent Platform, see [Tabular data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview#tabular_data) and [Tabular data overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview) .

The following sample code snippet shows how you might use the Vertex AI SDK to create and run an `AutoML` tabular model:

    dataset = aiplatform.TabularDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
    
    job = aiplatform.AutoMLTabularTrainingJob(
      display_name="train-automl",
      optimization_prediction_type="regression",
      optimization_objective="minimize-rmse",
    )
    
    model = job.run(
        dataset=dataset,
        target_column="target_column_name",
        training_fraction_split=0.6,
        validation_fraction_split=0.2,
        test_fraction_split=0.2,
        budget_milli_node_hours=1000,
        model_display_name="my-automl-model",
        disable_early_stopping=False,
    )

### [`SequenceToSequencePlusForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob)

The [`SequenceToSequencePlusForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob) class uses the `Seq2seq+` training method to train and run a forecasting model. The `Seq2seq+` training method is a good choice for experimentation. Its algorithm is simpler and uses a smaller search space than the `AutoML` option. `Seq2seq+` is a good option if you want fast results and your datasets are smaller than 1 GB.

For sample code that shows you how to use [`SequenceToSequencePlusForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob) , see the [Create a training pipeline forecasting Seq2seq sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_seq2seq_sample.py) on GitHub.

### [`TemporalFusionTransformerForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob)

The [`TemporalFusionTransformerForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob) class uses the Temporal Fusion Transformer (TFT) training method to train and run a forecasting model. The TFT training method implements an attention-based deep neural network (DNN) model that uses a multi-horizon forecasting task to produce predictions.

For sample code that shows you how to use [`TemporalFusionTransformerForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob) , see the [Create a training pipeline forecasting temporal fusion transformer sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_tft_sample.py) on GitHub.

### [`TimeSeriesDenseEncoderForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDenseEncoderForecastingTrainingJob)

The [`TimeSeriesDenseEncoderForecastingTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDenseEncoderForecastingTrainingJob) class uses the Time-series Dense Encoder (TiDE) training method to train and run a forecasting model. TiDE uses a [multi-layer perceptron](https://arxiv.org/abs/2304.08424) (MLP) to provide the speed of forecasting linear models with covariates and non-linear dependencies. For more information about TiDE, see [Recent advances in deep long-horizon forecasting](https://research.google/blog/recent-advances-in-deep-long-horizon-forecasting/) and this [TiDE blog post](https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-forecasting) .

## AutoML training classes for unstructured data

The Vertex AI SDK includes the following classes to train unstructured image models:

### [`AutoMLImageTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLImageTrainingJob)

Use the [`AutoMLImageTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLImageTrainingJob) class to create, train, and return an image model. For more information about working with image data models in Gemini Enterprise Agent Platform, see [Image data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview#image_data) .

For an example of how to use the [`AutoMLImageTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLImageTrainingJob) class, see the tutorial in the [AutoML image classification](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-automl-text-classification-batch-prediction.ipynb) notebook.

## Custom data training classes

You can use the Vertex AI SDK to automate a custom training workflow. For information about using Gemini Enterprise Agent Platform to run custom training applications, see [Custom training overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) .

The Vertex AI SDK includes three classes that create a custom training pipeline. A training pipeline accepts an input Gemini Enterprise Agent Platform managed dataset that it uses to train a model. Next, it returns the model after the training job completes. Each of the three custom training pipeline classes creates a training pipeline differently. [`CustomTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob) uses a Python script, [`CustomContainerTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob) uses a custom container, and [`CustomPythonPackageTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob) uses a Python package and a prebuilt container.

The [`CustomJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob) class creates a custom training job but is not a pipeline. Unlike a custom training pipeline, the [`CustomJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob) class can use a dataset that's not a Gemini Enterprise Agent Platform managed dataset to train a model, and it doesn't return the trained model. Because the class accepts different types of datasets and doesn't return a trained model, it's less automated and more flexible than a custom training pipeline.

### [`CustomContainerTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob)

Use the [`CustomContainerTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob) class to use a container to launch a custom training pipeline in Gemini Enterprise Agent Platform.

For an example of how to use the [`CustomContainerTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob) class, see the tutorial in the [PyTorch Image Classification Multi-Node Distributed Data Parallel Training on GPU using Gemini Enterprise Agent Platform Training with Custom Container](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/multi_node_ddp_nccl_vertex_training_with_custom_container.ipynb) notebook.

### [`CustomJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob)

Use the [`CustomJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob) class to use a script to launch a custom training job in Gemini Enterprise Agent Platform.

A training job is more flexible than a training pipeline because you aren't restricted to loading your data in a Gemini Enterprise Agent Platform managed dataset and a reference to your model isn't registered after the training job completes. For example, you might want to use the [`CustomJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob) class, its [`from_local_script`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob#google_cloud_aiplatform_CustomJob_from_local_script) method, and a script to load a dataset from [scikit-learn](https://scikit-learn.org/) or [TensorFlow](https://www.tensorflow.org/) . Or, you might want to analyze or test your trained model before you register it to Gemini Enterprise Agent Platform.

For more information about custom training jobs, including requirements before submitting a custom training job, what a custom job includes, and a Python code sample, see [Create custom training jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#create_custom_job-python) .

Because the [`CustomJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob#google_cloud_aiplatform_CustomJob_run) doesn't return the trained model, you need to use a script to write the model artifact to a location, such as a Cloud Storage bucket. For more information, see [Export a trained ML model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#export) .

The following sample code demonstrates how to create and run a custom job using a sample worker pool specification. The code writes the trained model to a Cloud Storage bucket named *artifact-bucket* .

    # Create a worker pool spec that specifies a TensorFlow cassava dataset and
    # includes the machine type and Docker image. The Google Cloud project ID
    # is 'project-id'.
    worker_pool_specs=[
         {
            "replica_count": 1,
            "machine_spec": { "machine_type": "n1-standard-8",
                              "accelerator_type": "NVIDIA_TESLA_V100",
                              "accelerator_count": 1
            },
            "container_spec": {"image_uri": "gcr.io/{project-id}/multiworker:cassava"}
          },
          {
            "replica_count": 1,
            "machine_spec": { "machine_type": "n1-standard-8",
                              "accelerator_type": "NVIDIA_TESLA_V100",
                              "accelerator_count": 1
            },
            "container_spec": {"image_uri": "gcr.io/{project-id}/multiworker:cassava"}
          }
    ]
    
    # Use the worker pool spec to create a custom training job. The custom training
    # job artifacts are stored in the Cloud Storage bucket
    # named 'artifact-bucket'.
    your_custom_training_job = aiplatform.CustomJob(
                                          display_name='multiworker-cassava-sdk',
                                          worker_pool_specs=worker_pool_specs,
                                          staging_bucket='gs://{artifact-bucket}')
    
    # Run the training job. This method doesn't return the trained model.
    my_multiworker_job.run()

### [`CustomPythonPackageTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob)

Use the [`CustomPythonPackageTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob) class to use a Python package to launch a custom training pipeline in Gemini Enterprise Agent Platform.

For an example of how to use the [`CustomPythonPackageTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob) class, see the tutorial in the [Custom training using Python package, managed text dataset, and TensorFlow serving container](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/sdk/SDK_Custom_Training_Python_Package_Managed_Text_Dataset_Tensorflow_Serving_Container.ipynb) notebook.

### [`CustomTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob)

Use the [`CustomTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob) class to launch a custom training pipeline in Gemini Enterprise Agent Platform with a script.

For an example of how to use the [`CustomTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob) class, see the tutorial in the [Custom training image classification model for online prediction with explainability](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/explainable_ai/sdk_custom_image_classification_online_explain.ipynb) notebook.

## Hyperparameter training class

The Vertex AI SDK includes a class for hyperparameter tuning. Hyperparameter tuning maximizes your model's predictive accuracy by optimizing variables (known as *hyperparameters* ) that govern the training process. For more information, see [Overview of hyperparameter tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) .

### [`HyperparameterTuningJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob)

Use the [`HyperparameterTuningJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob) class to automate hyperparameter tuning on a training application.

To learn how to use the [`HyperparameterTuningJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob) class to create and tune a custom trained model, see the [Hyperparameter tuning](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-hyperparameter-tuning.ipynb) tutorial on GitHub.

To learn how to use the [`HyperparameterTuningJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob) class to run a Gemini Enterprise Agent Platform hyperparameter tuning job for a TensorFlow model, see the [Run hyperparameter tuning for a TensorFlow model](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/hyperparameter_tuning_tensorflow.ipynb) tutorial on GitHub.

## Pipeline training class

A pipeline orchestrates your ML workflow in Gemini Enterprise Agent Platform. You can use a pipeline to automate, monitor, and govern your machine learning systems. To learn more about pipelines in Gemini Enterprise Agent Platform, see [Introduction to Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction) .

### [`PipelineJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob)

An instance of the [`PipelineJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob) class represents a Gemini Enterprise Agent Platform pipeline.

There are several tutorial notebooks that demonstrate how to use the [`PipelineJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob) class:

  - To learn how to run a [Kubeflow Pipelines (KFP)](https://www.kubeflow.org/docs/components/pipelines/) pipeline, see the [Pipeline control structures using the KFP SDK](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/control_flow_kfp.ipynb) tutorial on GitHub.

  - To learn how to train a [scikit-learn](https://scikit-learn.org/stable/) tabular classification model and create a batch prediction job with a Gemini Enterprise Agent Platform pipeline, see the [Training and batch prediction with BigQuery source and destination for a custom tabular classification model](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/custom_tabular_train_batch_pred_bq_pipeline.ipynb) tutorial on GitHub.

  - To learn how to build an AutoML image classification model and use a Gemini Enterprise Agent Platform pipeline, see the [AutoML image classification pipelines using google-cloud-pipeline-components](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/google_cloud_pipeline_components_automl_images.ipynb) tutorial on GitHub.

For more tutorial notebooks, see [Gemini Enterprise Agent Platform notebook tutorials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/jupyter-notebooks) .

## What's next

  - Learn about the [Vertex AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) .
