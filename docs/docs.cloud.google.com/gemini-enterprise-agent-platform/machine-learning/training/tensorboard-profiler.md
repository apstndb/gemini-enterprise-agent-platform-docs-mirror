---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler
title: Enable Cloud Profiler for debugging model training performance debugging
description: Enable Cloud Profiler for debugging model training performance.
data_source: docs.cloud.google.com
---

> To see an example of how to profile model training performance, run the "Profile model training performance using Cloud Profiler in custom training with prebuilt container" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training_with_prebuilt_container.ipynb)

This page shows you how to enable [Cloud Profiler](https://github.com/googleapis/python-aiplatform/tree/main/google/cloud/aiplatform/training_utils/cloud_profiler) so you can debug model training performance for your serverless training jobs.

Training models can be computationally expensive. Profiler lets you monitor and optimize your model training performance by helping you understand the resource consumption of training operations. With this information, you can pinpoint and fix performance bottlenecks to train models faster and cheaper.

## Before you begin

  - Ensure that you're using TensorFlow 2.4 or a later version.

  - Install the [Agent Platform SDK](https://github.com/googleapis/python-aiplatform) with the `cloud_profiler` plugin. From your local Docker container, run:
    
        pip install google-cloud-aiplatform[cloud_profiler]

  - You must have a Vertex AI TensorBoard instance. See [Create a Vertex AI TensorBoard instance](https://docs.cloud.google.com/vertex-ai/docs/experiments/tensorboard-setup#create-tensorboard-instance) for instructions.

  - You must have a service account with `roles/storage.admin` and `roles/aiplatform.user` roles. See [Create a service account with required permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-training#create_a_service_account_with_required_permissions) for instructions.

  - You must have a Cloud Storage bucket to store Vertex AI TensorBoard logs. See [Create a Cloud Storage bucket to store Vertex AI TensorBoard logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-training#create_a_bucket_to_store_logs) for instructions.

## Enable Profiler

To enable Profiler for your training job, add the following to your training script:

1.  Add the `cloud_profiler` import at your top level imports:
    
        from google.cloud.aiplatform.training_utils import cloud_profiler

2.  Initialize the `cloud_profiler` plugin by adding:
    
        cloud_profiler.init()

#### Example

Here's a sample training script:

    #!/usr/bin/env python
    
    import tensorflow as tf
    import argparse
    import os
    from google.cloud.aiplatform.training_utils import cloud_profiler
    import time
    
    """Train an mnist model and use cloud_profiler for profiling."""
    
    def _create_model():
        model = tf.keras.models.Sequential(
            [
                tf.keras.layers.Flatten(input_shape=(28, 28)),
                tf.keras.layers.Dense(128, activation="relu"),
                tf.keras.layers.Dropout(0.2),
                tf.keras.layers.Dense(10),
            ]
        )
        return model
    
    def main(args):
        strategy = None
        if args.distributed:
            strategy = tf.distribute.MultiWorkerMirroredStrategy()
    
        mnist = tf.keras.datasets.mnist
    
        (x_train, y_train), (x_test, y_test) = mnist.load_data()
        x_train, x_test = x_train / 255.0, x_test / 255.0
    
        if args.distributed:
            strategy = tf.distribute.MultiWorkerMirroredStrategy()
            with strategy.scope():
                model = _create_model()
                model.compile(
                    optimizer="adam",
                    loss=tf.keras.losses.sparse_categorical_crossentropy,
                    metrics=["accuracy"],
                )
        else:
            model = _create_model()
            model.compile(
                optimizer="adam",
                loss=tf.keras.losses.sparse_categorical_crossentropy,
                metrics=["accuracy"],
            )
    
        # Initialize the profiler.
        cloud_profiler.init()
    
        # Use AIP_TENSORBOARD_LOG_DIR to update where logs are written to.
        tensorboard_callback = tf.keras.callbacks.TensorBoard(
            log_dir=os.environ["AIP_TENSORBOARD_LOG_DIR"], histogram_freq=1
        )
    
        model.fit(
            x_train,
            y_train,
            epochs=args.epochs,
            verbose=0,
            callbacks=[tensorboard_callback],
        )
    if __name__ == "__main__":
        parser = argparse.ArgumentParser()
        parser.add_argument(
            "--epochs", type=int, default=100, help="Number of epochs to run model."
        )
        parser.add_argument(
            "--distributed", action="store_true", help="Use MultiWorkerMirroredStrategy"
        )
        args = parser.parse_args()
        main(args)

## Access the Profiler dashboard

Once you have configured your training script to enable Profiler, [run the training script with a Vertex AI TensorBoard instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-training#create_a_custom_training_job) .

In your training script, ensure the following configurations:

  - Set `BASE_OUTPUT_DIR:` to the Cloud Storage bucket where you want to store the Vertex AI TensorBoard logs that's generated by your training script.

  - Set `'serviceAccount':` to the service account that you created with `roles/storage.admin` and `roles/aiplatform.user` roles.

  - Set `'tensorboard':` to the fully qualified name of the Vertex AI TensorBoard instance that you want to use with this training job. The fully qualified name has the following format:
    
        projects/PROJECT_NUMBER_OR_ID/locations/REGION/tensorboards/TENSORBOARD_INSTANCE_ID

There are two ways to access the Profiler dashboard from the Google Cloud console:

  - From the Custom jobs page.
  - From the Experiments page.

#### Access the Profiler dashboard through the Custom jobs page

You can use this method to access the Profiler dashboard even if the training job is in the **Finished** state.

1.  In the Google Cloud console, go to the **Custom jobs** tab on the **Training** page.

2.  Click the name of the training job you just created to go to the job details page.

3.  Click **Open TensorBoard** .

4.  Click the **Profile** tab.

#### Access the Profiler dashboard through the Experiments page

You can use this method to access the Profiler dashboard only when the training job is in the **Running** state.

1.  In the Google Cloud console, go to the Vertex AI Experiments page.

2.  Select the region of the training job that you just created.

3.  Click **Open TensorBoard** next to the name of the training job.

4.  Click the **Profile** tab.

## Capture a profiling session

To capture a profiling session, your training job must be in the **Running** state. From the **Profile** tab in the Vertex AI TensorBoard instance, perform the following steps:

1.  Click **Capture profile** .

2.  In the **Profile Service URL(s) or TPU name** field, enter:
    
        workerpool0-0

3.  For **Address type** , select **IP address** .

4.  Click **Capture** .

## Notebook

> To see examples of how to profile model training performance, run the following notebooks in the environment of your choice:
> 
>   - "Profile model training performance using Cloud Profiler":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training.ipynb)
> 
>   - "Profile model training performance using Cloud Profiler in custom training with prebuilt container":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training_with_prebuilt_container.ipynb)

## What's next

  - See the [Tensorflow Profiler documentation](https://www.tensorflow.org/guide/profiler) to learn about the profiler tools and how to use them to optimize model performance.
