---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/tracking-classes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/tracking-classes
title: Tracking classes
description: Learn about the Vertex AI SDK classes that help with visualization, measurements, and tracking.
data_source: docs.cloud.google.com
---

The Agent Platform SDK for Python includes classes to help with visualization, measurements, and tracking. These classes can be grouped into three types:

  - Classes that use metadata to track resources in your machine learning (ML) workflow
  - Classes that are used for Vertex AI Experiments
  - Classes that are used for a Vertex AI TensorBoard

The following topics provide an overview of the classes related to tracking and monitoring an ML workflow in Agent Platform SDK for Python.

## Metadata classes

You can use the Agent Platform SDK for Python to create Vertex ML Metadata to help you track and analyze the metadata in your ML workflow. For more information, see [Introduction to Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction) .

### [`Artifact`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Artifact)

The [`Artifact`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Artifact) class represents the metadata in an artifact in Gemini Enterprise Agent Platform. An artifact is a discrete entity or piece of data that's produced by an ML workflow. Examples of an artifact are a [dataset](https://docs.cloud.google.com/vertex-ai/docs/datasets/overview) , a [model](https://docs.cloud.google.com/vertex-ai/docs/training-overview) , and an [input file](https://docs.cloud.google.com/vertex-ai/docs/video-data/classification/prepare-data#input-files) . For more information, see [Track executions and artifacts](https://docs.cloud.google.com/vertex-ai/docs/experiments/track-executions-artifacts) .

When you create an [`Artifact`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Artifact) resource, you need to specify its schema. Each type of an artifact has a unique schema. For example, the `system.Dataset` schema represents a dataset and the `system.Metrics` schema represents evaluation metrics. For more information, see [How to use system schemas](https://docs.cloud.google.com/vertex-ai/docs/ml-metadata/system-schemas#how_to_use_system_schemas) .

The following sample code shows how to create an [`Artifact`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Artifact) resource that represents a model:

    model_artifact = aiplatform.Artifact.create(
            schema_title="system.Model",
            display_name=PREPROCESSED_DATASET_NAME,
            uri=PREPROCESSED_DATASET_URI,

### [`Execution`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Execution)

The [`Execution`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Execution) class represents the metadata in an execution in Gemini Enterprise Agent Platform. An execution is a step in an ML workflow. Examples of an execution are data processing, training, and model evaluation. An execution can consume artifacts, such as a dataset, and produce an artifact, such as a model.

Use [`aiplatform.start_execution`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_start_execution) to create an [`Execution`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Execution) resource. After you create an [`Execution`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Execution) resource, use the same [`aiplatform.start_execution`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_start_execution) method with its `resume` parameter set to `True` to resume it.

The following sample code shows how to create an [`Execution`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Execution) resource:

    with aiplatform.start_execution(schema_title='system.ContainerExecution',
                                    display_name='trainer') as execution:
        execution.assign_input_artifacts([my_artifact])
        model = aiplatform.Artifact.create(uri='gs://my-uri', schema_title='system.Model')
        execution.assign_output_artifacts([model])

## Vertex AI Experiments classes

You can use the Agent Platform SDK for Python to create and run Vertex AI Experiments. Use Vertex AI Experiments to track logged metrics and parameters to help you analyze and optimize your ML workflow. For more information, see [Introduction to Vertex AI Experiments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/intro-vertex-ai-experiments) .

To learn more about how to use the [`Experiment`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment) and [`ExperimentRun`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun) classes, try one of the following tutorials:

  - [Build Vertex AI Experiments lineage for custom training](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/build_model_experimentation_lineage_with_prebuild_code.ipynb)
  - [Track parameters and metrics for locally trained models](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/comparing_local_trained_models.ipynb)
  - [Compare pipeline runs with Vertex AI Experiments](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/comparing_pipeline_runs.ipynb)
  - [Get started with Vertex AI Experiments](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments.ipynb)

### [`Experiment`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment)

The [`Experiment`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment) class represents an experiment in Gemini Enterprise Agent Platform. Use an experiment to analyze its [*experiment runs*](https://docs.cloud.google.com/vertex-ai/docs/experiments/create-manage-exp-run) and [*pipeline runs*](https://docs.cloud.google.com/vertex-ai/docs/pipelines/run-pipeline) with different configurations, such as multiple input artifacts and hyperparameters.

There are two ways to create an [`Experiment`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment) resource:

1.  The preferred way to create an [`Experiment`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment) is by specifying a name for your experiment as a parameter when you call [`aiplatform.init`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_init) :
    
        # In a real world scenario it's likely you would specify more parameters
        # when you call aiplatform.init. This sample shows only how to use the
        # parameter used to create an Experiment.
        
        # Specify a name for the experiment
        EXPERIMENT_NAME = "your-experiment-name"
        
        # Create the experiment
        aiplatform.init(experiment=EXPERIMENT_NAME)

2.  You can also create an [`Experiment`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment) by calling [`aiplatform.Experiment.create`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment#google_cloud_aiplatform_Experiment_create) . [`aiplatform.Experiment.create`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment#google_cloud_aiplatform_Experiment_create) creates the [`Experiment`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment) resource but doesn't set it to a global environment. Because of this, you can't run the experiment with [`aiplatform.start_run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform#google_cloud_aiplatform_start_run) . The following sample code shows how to use [`aiplatform.Experiment.create`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment#google_cloud_aiplatform_Experiment_create) to create an experiment and then run the experiment:
    
        # Specify a name for the experiment
        EXPERIMENT_NAME = "your-experiment-name"
        EXPERIMENT_RUN_NAME = "your-run"
        
        # Create the experiment
        experiment = aiplatform.Experiment.create(experiment_name=EXPERIMENT_NAME)
        experiment_run = aiplatform.ExperimentRun.create(EXPERIMENT_RUN_NAME, experiment=EXPERIMENT_NAME)

### [`ExperimentRun`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun)

The [`ExperimentRun`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun) class represents a run of an experiment.

The following sample code shows how to create and start an experiment run, then use it to get information about your experiment. To delete the experiment run, get a reference to the [`ExperimentRun`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun) instance and call its [`delete`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun#google_cloud_aiplatform_ExperimentRun_delete) method.

    # Specify your project name, location, experiment name, and run name
    PROJECT_NAME = "my-project"
    LOCATION = "us-central1"
    EXPERIMENT_NAME = "experiment-1"
    RUN_NAME = "run-1"
    
    # Create the experiment to run
    aiplatform.init(experiment=EXPERIMENT_NAME,
                    project=PROJECT_NAME,
                    location=LOCATION)
    
    # Create and run an ExperimentRun resource. Next, you can use it to get
    # information about your experiment. For example, you can log parameters and
    # metrics with specified key-value pairs.
    with aiplatform.start_run(RUN_NAME):
         aiplatform.log_params({'learning_rate': 0.1, 'dropout_rate': 0.2})
         aiplatform.log_metrics({'accuracy': 0.9, 'recall': 0.8})
    
    # Get a reference to the ExperimentRun resource, get the parameters logged to 
    # the run, get the summary metrics logged to the run, then delete it.
    with aiplatform.start_run(RUN_NAME, resume=True) as run:
         run.get_params()
         run.get_metrics()
         run.delete()

## Vertex AI TensorBoard classes

The Agent Platform SDK for Python includes classes to work with a managed version of the open source [Vertex AI TensorBoard](https://www.tensorflow.org/tensorboard/get_started) . Vertex AI TensorBoard is a tool used to monitor measurements and visualizations during your ML workflow. For more information, see [Get started with Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction) .

To learn more about using the Agent Platform SDK for Python to work with Vertex AI TensorBoard, try one of the following notebook tutorials:

  - [Profile model training performance using Cloud Profiler](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/custom_training_tensorboard_profiler.ipynb)
  - [Vertex AI TensorBoard custom training with a custom container.](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_custom_container.ipynb)
  - [Vertex AI TensorBoard custom training with prebuilt container](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_prebuilt_container.ipynb)
  - [Vertex AI TensorBoard hyperparameter tuning with the HParams Dashboard](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_hyperparameter_tuning_with_hparams.ipynb)
  - [Profile a model's training performance using Cloud Profiler](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training.ipynb)
  - [Profile a model's training performance using Cloud Profiler in custom training with a prebuilt container](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training_with_prebuilt_container.ipynb)

### [`Tensorboard`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Tensorboard)

The [`Tensorboard`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Tensorboard) class represents a managed resource that stores Vertex AI TensorBoard experiments. You need to create a [`Tensorboard`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Tensorboard) instance before the experiments can be visualized. You can create more than one [`Tensorboard`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Tensorboard) instance in a Google Cloud project.

The following sample code shows how to create a [`Tensorboard`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Tensorboard) instance:

    # Specify your project name, location, and the name of your Tensorboard
    PROJECT_NAME = "my-project"
    LOCATION = "us-central1"
    TENSORBOARD_NAME = "my-tensorboard"
    
    aiplatform.init(project=PROJECT_NAME, location=LOCATION)
    
    tensorboard = aiplatform.Tensorboard.create(
        display_name=TENSORBOARD_NAME,
        project=PROJECT_NAME,
        location=LOCATION,
    )

### [`TensorboardExperiment`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardExperiment)

The [`TensorboardExperiment`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardExperiment) represents a group of [`TensorboardRun`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardRun) objects. A [`TensorboardRun`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardRun) instance represents the results of a training job run in a Tensorboard.

### [`TensorboardRun`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardRun)

An instance of the [`TensorboardRun`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardRun) class maps to a training job run in a Tensorboard with a specified set of hyperparameters, a model definition, a dataset, and more.

### [`TensorboardTimeSeries`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardTimeSeries)

The [`TensorboardTimeSeries`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardTimeSeries) class represents a series produced in training runs.

## What's next

  - Learn about the [Vertex AI SDK](https://docs.cloud.google.com/vertex-ai/docs/python-sdk/use-vertex-ai-python-sdk) .
