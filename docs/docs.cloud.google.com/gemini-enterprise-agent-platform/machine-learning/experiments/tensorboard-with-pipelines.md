---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-with-pipelines
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-with-pipelines
title: Use Vertex AI TensorBoard with Gemini Enterprise Agent Platform Pipelines
description: Use the Agent Platform SDK for Python or {{dynamic_data.site_values.cloud_name_short}} console to either create or delete an experiment.
data_source: docs.cloud.google.com
---

> To see an example of TensorBoard integration with pipelines, run the " TensorBoard integration with Pipelines" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_vertex_ai_pipelines_integration.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_vertex_ai_pipelines_integration.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_vertex_ai_pipelines_integration.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_vertex_ai_pipelines_integration.ipynb)

Your training code can be packaged into a custom training component and run in a pipeline job. TensorBoard logs are automatically streamed to your Vertex AI TensorBoard experiment. You can use this integration to monitor your training in near real time as Vertex AI TensorBoard streams in Vertex AI TensorBoard logs as they are written to Cloud Storage.

For initial setup see [Set up for Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-setup) .

### Changes to your training script

Your training script must be configured to write TensorBoard logs to the Cloud Storage bucket, the location of which the Gemini Enterprise Agent Platform Training Service will automatically make available through a predefined environment variable `  AIP_TENSORBOARD_LOG_DIR  ` .

This can usually be done by providing `os.environ['AIP_TENSORBOARD_LOG_DIR']` as the log directory to the open source TensorBoard log writing APIs. The location of the `AIP_TENSORBOARD_LOG_DIR` is typically set with the `staging_bucket` variable.

To configure your training script in TensorFlow 2.x, create a TensorBoard callback and set the `log_dir` variable to `os.environ['AIP_TENSORBOARD_LOG_DIR']` The TensorBoard callback is then included in the TensorFlow `model.fit` callbacks list.

``` 
  tensorboard_callback = tf.keras.callbacks.TensorBoard(
       log_dir=os.environ['AIP_TENSORBOARD_LOG_DIR'],
       histogram_freq=1
  )
  
  model.fit(
       x=x_train,
       y=y_train,
       epochs=epochs,
       validation_data=(x_test, y_test),
       callbacks=[tensorboard_callback],
  )
  
```

Learn more about [how Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#environment-variables) sets environment variables in your custom training environment.

### Build and run a pipeline

The following example shows how to build and run a pipeline using Kubeflow Pipelines DSL package. For more examples and additional details, see [Agent Platform Pipelines documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines) .

#### Create a training component

Package your training code into a custom component, making sure that the code is configured to write TensorBoard logs to a Cloud Storage bucket. For more examples see [Build your own pipeline components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-own-components) .

    from kfp.v2.dsl import component
    
    @component(
        base_image="tensorflow/tensorflow:latest",
        packages_to_install=["tensorflow_datasets"],
    )
    def train_tensorflow_model_with_tensorboard():
        import datetime, os
        import tensorflow as tf
    
        (x_train, y_train), (x_test, y_test) = tf.keras.datasets.mnist.load_data()
        x_train, x_test = x_train / 255.0, x_test / 255.0
    
        def create_model():
            return tf.keras.models.Sequential(
                [
                    tf.keras.layers.Flatten(input_shape=(28, 28)),
                    tf.keras.layers.Dense(512, activation="relu"),
                ]
            )
    
        model = create_model()
        model.compile(
            optimizer="adam",
            loss="sparse_categorical_crossentropy",
            metrics=["accuracy"]
        )
    
        tensorboard_callback = tf.keras.callbacks.TensorBoard(
            log_dir=os.environ['AIP_TENSORBOARD_LOG_DIR'],
            histogram_freq=1
        )
    
        model.fit(
            x=x_train,
            y=y_train,
            epochs=5,
            validation_data=(x_test, y_test),
            callbacks=[tensorboard_callback],
        )

#### Build and compile a pipeline

Create a custom training job from the component you've created by specifying the component spec in `create_custom_training_job_op_from_component` . Set the `tensorboard_resource_name` to your TensorBoard instance, and the `staging_bucket` to the location to stage artifacts during API calls (including TensorBoard logs).

Then, build a pipeline to include this job and compile the pipeline to a JSON file.

For more examples and information, see [Custom job components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/customjob-component) and [Build a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline) .

    from kfp.v2 import compiler
    from google_cloud_pipeline_components.v1.custom_job.utils import \
        create_custom_training_job_op_from_component
    from kfp.v2 import dsl
    
    def create_tensorboard_pipeline_sample(
        project, location, staging_bucket, display_name, service_account, experiment, tensorboard_resource_name
    ):
    
        @dsl.pipeline(
            pipeline_root=f"{staging_bucket}/pipeline_root",
            name=display_name,
        )
        def pipeline():
            custom_job_op = create_custom_training_job_op_from_component(
                component_spec=train_tensorflow_model_with_tensorboard,
                tensorboard=tensorboard_resource_name,
                base_output_directory=staging_bucket,
                service_account=service_account,
            )
            custom_job_op(project=project, location=location)
    
        compiler.Compiler().compile(
            pipeline_func=pipeline, package_path=f"{display_name}.json"
        )

#### Submit a Gemini Enterprise Agent Platform pipeline

Submit your pipeline using the Agent Platform SDK for Python. For more information, see [Run a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline#vertex-ai-sdk-for-python) .

### Python

    from typing import Any, Dict, Optional
    
    from google.cloud import aiplatform
    
    
    def log_pipeline_job_to_experiment_sample(
        experiment_name: str,
        pipeline_job_display_name: str,
        template_path: str,
        pipeline_root: str,
        project: str,
        location: str,
        parameter_values: Optional[Dict[str, Any]] = None,
    ):
        aiplatform.init(project=project, location=location)
    
        pipeline_job = aiplatform.PipelineJob(
            display_name=pipeline_job_display_name,
            template_path=template_path,
            pipeline_root=pipeline_root,
            parameter_values=parameter_values,
        )
    
        pipeline_job.submit(experiment=experiment_name)

  - `experiment_name` : Provide a name for your experiment.
  - `pipeline_job_display_name` : The display name for the pipeline job.
  - `template_path` : The path to the compiled pipeline template.
  - `pipeline_root` : Specify a Cloud Storage URI that your pipelines service account can access. The artifacts of your pipeline runs are stored within the pipeline root.
  - `parameter_values` : The pipeline parameters to pass to this run. For example, create a `dict()` with the parameter names as the dictionary keys and the parameter values as the dictionary values.
  - `project` : . The Google Cloud project to run the pipeline in. You can find your IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.  
  - `location` : The location to run the pipeline in. This should be the same location as the TensorBoard instance you're using.

## What's next

  - View your results: [View TensorBoard for Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-view#vertex-ai-pipelines) .
  - Learn how to optimize the performance of your custom training jobs using [Cloud Profiler](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler) .
