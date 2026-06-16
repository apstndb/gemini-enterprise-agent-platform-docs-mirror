---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements
title: Prepare training code
description: Learn about best practices to consider when writing code for Gemini Enterprise Agent Platform serverless training.
data_source: docs.cloud.google.com
---

Perform serverless training on Gemini Enterprise Agent Platform to run your own machine learning (ML) training code in the cloud, instead of using AutoML. This document describes best practices to consider as you write training code.

> **Note:** This document describes training code best practices specific to Agent Platform, but it doesn't comprehensively explain how to design an ML model or write ML training code. These details vary depending on the purpose of your model and the ML framework that you use for training. If you are new to creating custom ML models, we recommend working through Google's [Machine Learning Crash Course with TensorFlow APIs.](https://developers.google.com/machine-learning/crash-course)

## Choose a training code structure

First, determine what structure you want your ML training code to take. You can provide training code to Agent Platform in one of the following forms:

  - **A Python script to use with a prebuilt container.** Use the [Vertex AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) to [create a custom job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob#google_cloud_aiplatform_CustomJob_from_local_script) . This method lets you provide your training application as a single Python script.

  - **A Python training application to use with a prebuilt container.** Create a [Python source distribution](https://packaging.python.org/en/latest/overview/#python-source-distributions) with code that trains an ML model and exports it to Cloud Storage. This training application can use any of the dependencies included in the prebuilt container that you plan to use it with.
    
    > **Note:** If you use the [Agent Platform SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) to [create a `TrainingPipeline` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline#custom-job-model-upload) , then you can provide your training application as a single Python script, rather than as a Python source distribution.
    
    Use this option if one of the Agent Platform [prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) includes all the dependencies that you need for training. For example, if you want to train with PyTorch, scikit-learn, TensorFlow, or XGBoost, then this is likely the better option.
    
    To learn about best practices specific to this option, read the guide to [creating a Python training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) .

  - **A custom container image.** Create a [Docker container image](https://docs.docker.com/get-started/overview/#docker-objects) with code that trains an ML model and exports it to Cloud Storage. Include any dependencies required by your code in the container image.
    
    Use this option if you want to use dependencies that are not included in one of the Agent Platform [prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) . For example, if you want to train using a Python ML framework that is not available in a prebuilt container, or if you want to train using a programming language other than Python, then this is the better option.
    
    To learn about best practices specific to this option, read the guide to [creating a custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .

The rest of this document describes best practices relevant to both training code structures.

## Best practices for all serverless training code

When you write serverless training code for Agent Platform, keep in mind that the code will run on one or more virtual machine (VM) instances managed by Google Cloud. This section describes best practices applicable to all custom training code.

### Access Google Cloud services in your code

Several of the following sections describe accessing other Google Cloud services from your code. To access Google Cloud services, write your training code to use [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication#adc) . Many Google Cloud client libraries authenticate with ADC by default. You don't need to configure any environment variables; Agent Platform automatically configures ADC to authenticate as either the [Gemini Enterprise Agent Platform Custom Code Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) for your project (by default) or a [custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) (if you have configured one).

> **Note:** If you want to run your training code in your local environment before you run it on Agent Platform, you might want to configure your local environment for ADC. You can do this by [downloading a service account key](https://docs.cloud.google.com/docs/authentication/production#manually) or by using the [`gcloud auth application-default login` command](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) .

However, when you use a Google Cloud client library in your code, Agent Platform might not always connect to the correct Google Cloud project by default. If you encounter permission errors, connecting to the wrong project might be the problem.

This problem occurs because Agent Platform does not run your code directly in your Google Cloud project. Instead, Agent Platform runs your code in one of several separate projects managed by Google. Agent Platform uses these projects exclusively for operations related to your project. Therefore, don't try to infer a project ID from the environment in your training or inference code; specify project IDs explicitly.

If you don't want to hardcode a project ID in your training code, you can reference the `CLOUD_ML_PROJECT_ID` environment variable: Agent Platform sets this environment variable in every serverless training container to contain the [project number](https://docs.cloud.google.com/docs/overview#projects) of the project where you initiated serverless training. Many Google Cloud tools can accept a project number wherever they take a project ID.

For example, if you want to use the [Python Client for Google BigQuery](https://github.com/googleapis/python-bigquery) to access a BigQuery table in the same project, then don't try to infer the project in your training code:

Implicit project selection

    from google.cloud import bigquery
    
    client = bigquery.Client()

Instead use code that explicitly selects a project:

Explicit project selection

    import os
    
    from google.cloud import bigquery
    
    project_number = os.environ["CLOUD_ML_PROJECT_ID"]
    
    client = bigquery.Client(project=project_number)

If you encounter permission errors after configuring your code in this way, then read the following section about [which resources your code can access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#which-resources) to adjust the permissions available to your training code.

#### Which resources your code can access

By default, your training application can access any Google Cloud resources that are available to the [Gemini Enterprise Agent Platform Custom Code Service Agent (CCSA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) of your project. You can grant the CCSA, and thereby your training application, access to a limited number of other resources by following the instructions in [Grant Gemini Enterprise Agent Platform service agents access to other resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#grant_service_agents_access_to_other_resources) . If your training application needs more than read-level access to Google Cloud resources that are not listed in that page, it needs to acquire an OAuth 2.0 access token with the <https://www.googleapis.com/auth/cloud-platform> scope, which can only be done by using a [custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) .

For example, consider your training code's access to Cloud Storage resources:

By default, Agent Platform can access any Cloud Storage bucket in the Google Cloud project where you're performing serverless training. You can also [grant Agent Platform access to Cloud Storage buckets in other projects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#different-project) , or you can precisely customize what buckets a specific job can access by [using a custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) .

#### Read and write Cloud Storage files with Cloud Storage FUSE

In all serverless training jobs, Agent Platform mounts Cloud Storage buckets that you have access to in the `/gcs/` directory of each training node's file system. As a convenient alternative to using the Python Client for Cloud Storage or another library to access Cloud Storage, you can read and write directly to the local file system in order to read data from Cloud Storage or write data to Cloud Storage. For example, to load data from `gs:// BUCKET /data.csv` , you can use the following Python code:

    file = open('/gcs/BUCKET/data.csv', 'r')

Agent Platform uses [Cloud Storage FUSE](https://docs.cloud.google.com/storage/docs/gcs-fuse) to mount the storage buckets. Note that [directories mounted by Cloud Storage FUSE are not POSIX compliant](https://docs.cloud.google.com/storage/docs/gcs-fuse#notes) .

The credentials that you're using for serverless training determine which buckets you can access in this way. The preceding section about [which resources your code can access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#which-resources) describes exactly which buckets you can access by default and how to customize this access.

### Load input data

ML code usually operates on training data in order to train a model. Don't store training data together with your code, whether you create a Python training application or a custom container image. Storing data with code can lead to a poorly organized project, make it difficult to reuse code on different datasets, and cause errors for large datasets.

You can load data from a [Agent Platform managed dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-managed-datasets) or write your own code to load data from a source outside of Agent Platform, such as BigQuery or Cloud Storage.

For best performance when you load data from Cloud Storage, use a bucket in the [region where you're performing serverless training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) . To learn how to store data in Cloud Storage, read [Creating storage buckets](https://docs.cloud.google.com/storage/docs/creating-buckets) and [Uploading objects](https://docs.cloud.google.com/storage/docs/uploading-objects) .

To learn about which Cloud Storage buckets you can load data from, read the previous section about [which resources your code can access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#which-resources) .

To load data from Cloud Storage in your training code, use the [Cloud Storage FUSE feature described in the preceding section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#fuse) , or use any library that supports ADC. You don't need to explicitly provide any authentication credentials in your code.

For example, you can use one of the client libraries demonstrated in the Cloud Storage guide to [Downloading objects](https://docs.cloud.google.com/storage/docs/downloading-objects#storage-download-object-python) . The [Python Client for Cloud Storage](https://docs.cloud.google.com/python/docs/reference/storage/latest) , in particular, is included in prebuilt containers. TensorFlow's [`tf.io.gfile.GFile` class](https://www.tensorflow.org/api_docs/python/tf/io/gfile/GFile) also supports ADC.

#### Load a large dataset

Depending on which [machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_machine_types) you plan to use during serverless training, your VMs might not be able to load the entirety of a large dataset into memory.

If you need to read data that is too large to fit in memory, stream the data or read it incrementally. Different ML frameworks have different best practices for doing this. For example, TensorFlow's [`tf.data.Dataset` class](https://www.tensorflow.org/api_docs/python/tf/data/Dataset) can stream TFRecord or text data from Cloud Storage.

Performing serverless training on multiple VMs with data parallelism is another way to reduce the amount of data each VM loads into memory. See the [Writing code for distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#distributed) section of this document.

### Export a trained ML model

ML code usually exports a trained model at the end of training in the form of one or more model artifacts. You can then use the model artifacts to get inferences.

After serverless training completes, you can no longer access the VMs that ran your training code. Therefore, your training code must export model artifacts to a location outside of Agent Platform.

We recommend that you export model artifacts to a Cloud Storage bucket. As described in the previous section about [which resources your code can access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#which-resources) , Agent Platform can access any Cloud Storage bucket in the Google Cloud project where you are performing serverless training. Use a library that supports ADC to export your model artifacts. For example, the [TensorFlow APIs for saving Keras models](https://www.tensorflow.org/guide/keras/serialization_and_saving) can export artifacts directly to a Cloud Storage path.

> **Note:** You can't export model artifacts from your training code in a way that directly creates a [`Model` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) . However, if you perform serverless training by creating a [`TrainingPipeline` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines) , the `TrainingPipeline` can export model artifacts to Cloud Storage. The `TrainingPipeline` can then immediately import those same model artifacts back into Agent Platform as a `Model` . Learn more in the [guide to creating training pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) .

If you want to use your trained model to serve inferences on Agent Platform, then your code must export model artifacts in a format compatible with one of the [prebuilt containers for inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/pre-built-containers) . Learn more in the [guide to exporting model artifacts for inference and explanation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts) .

### Environment variables for special Cloud Storage directories

> To see an example of using `AIP_MODEL_DIR` to export model artifacts as part of a more comprehensive workflow, run the "Custom training and online prediction" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb)

If you specify the [`baseOutputDirectory` API field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#FIELDS.base_output_directory) , Agent Platform sets the following environment variables when it runs your training code:

  - `AIP_MODEL_DIR` : a Cloud Storage URI of a directory intended for [saving model artifacts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#export) .
  - `AIP_CHECKPOINT_DIR` : a Cloud Storage URI of a directory intended for [saving checkpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#resilience) .
  - `AIP_TENSORBOARD_LOG_DIR` : a Cloud Storage URI of a directory intended for saving [TensorBoard](https://www.tensorflow.org/tensorboard) logs. See [Using Vertex AI TensorBoard with custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-training) .

The values of these environment variables differ slightly depending on whether you are using hyperparameter tuning. To learn more, see the [API reference for `baseOutputDirectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#FIELDS.base_output_directory) .

Using these environment variables makes it easier to reuse the same training code multiple times—for example with different data or configuration options—and save model artifacts and checkpoints to different locations, just by changing the `baseOutputDirectory` API field. However, you are not required to use the environment variables in your code if you don't want to. For example, you can alternatively hardcode locations for saving checkpoints and exporting model artifacts.

Additionally, if you [use a `TrainingPipeline` for custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) and don't specify the [`modelToUpload.artifactUri` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.artifact_uri) , then Agent Platform uses the value of the `AIP_MODEL_DIR` environment variable for `modelToUpload.artifactUri` . (For hyperparameter tuning, Agent Platform uses the value of the `AIP_MODEL_DIR` environment variable from the best trial.)

### Ensure resilience to restarts

The VMs that run your training code restart occasionally. For example, Google Cloud might need to restart a VM for maintenance reasons. When a VM restarts, Agent Platform starts running your code again from its start.

If you expect your training code to run for more than four hours, add several behaviors to your code to make it resilient to restarts:

  - Frequently export your training progress to Cloud Storage, at least once every four hours, so that you don't lose progress if your VMs restart.

  - At the start of your training code, check whether any training progress already exists in your export location. If so, load the saved training state instead of starting training from scratch.

Four hours is a guideline, not a hard limit. If ensuring resilience is a priority, consider adding these behaviors to your code even if you don't expect it to run for that long.

How to accomplish these behaviors depends on which ML framework you use. For example, if you use TensorFlow Keras, [learn how to use the `ModelCheckpoint` callback for this purpose](https://www.tensorflow.org/guide/keras/writing_your_own_callbacks) .

To learn more about how Agent Platform manages VMs, see [Understand the custom training service](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/understanding-training-service) .

## Best practices for optional serverless training features

If you want to use certain optional serverless training features, you might need to make additional changes to your training code. This section describes code best practices for hyperparameter tuning, GPUs, distributed training, and Vertex AI TensorBoard.

### Write code to enable autologging

You can enable autologging using the Agent Platform SDK for Python to automatically capture parameters and performance metrics when submitting the custom job. For details, see [Run training job with experiment tracking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/run-training-job-experiments) .

> To see an example of how to create a custom job with autologging enabled, run the " Experiments: Autologging" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments_autologging.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_vertex_experiments_autologging.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_vertex_experiments_autologging.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments_autologging.ipynb)

### Write code to return container logs

When you write logs from your service or job, they will be picked up automatically by Cloud Logging so long as the logs are written to any of these locations:

  - [Standard output ( `stdout` ) or standard error ( `stderr` ) streams](https://en.wikipedia.org/wiki/Standard_streams)
  - Log files in `/var/log-storage/` that follow the `output*.log` naming convention.
  - syslog ( `/dev/log` )
  - Logs written using [Cloud Logging client libraries](https://docs.cloud.google.com/logging/docs/reference/libraries) , which are available for many popular languages

Most developers are expected to write logs using standard output and standard error.

The container logs written to these supported locations are automatically associated with the Gemini Enterprise Agent Platform serverless training service, revision, and location, or with the serverless training job. Exceptions contained in these logs are captured by and reported in [Error Reporting](https://docs.cloud.google.com/run/docs/error-reporting) .

#### Use plain text versus structured JSON in logs

When you write logs, you can send a plain text string or send a single line of serialized JSON, also called "structured" data. This is picked up and parsed by Cloud Logging and is placed into `jsonPayload` . In contrast, the plain text message is placed in `textPayload` .

#### Write structured logs

You can pass structured JSON logs in multiple ways. The most common ways are by using the [Python Logging library](https://docs.python.org/3/library/logging.html) or by passing raw JSON using `print` .

### Python logging library

    import json
    import logging
    from pythonjsonlogger import jsonlogger
    
    class CustomJsonFormatter(jsonlogger.JsonFormatter):
     """Formats log lines in JSON."""
      def process_log_record(self, log_record):
        """Modifies fields in the log_record to match Cloud Logging's expectations."""
        log_record['severity'] = log_record['levelname']
        log_record['timestampSeconds'] = int(log_record['created'])
        log_record['timestampNanos'] = int(
            (log_record['created'] % 1) * 1000 * 1000 * 1000)
    
        return log_record
    
    def configure_logger():
      """Configures python logger to format logs as JSON."""
      formatter = CustomJsonFormatter(
            '%(name)s|%(levelname)s|%(message)s|%(created)f'
            '|%(lineno)d|%(pathname)s', '%Y-%m-%dT%H:%M:%S')
      root_logger = logging.getLogger()
      handler = logging.StreamHandler()
      handler.setFormatter(formatter)
      root_logger.addHandler(handler)
      root_logger.setLevel(logging.WARNING)
    
    logging.warning("This is a warning log")

### Raw JSON

    import json
    
    def log(severity, message):
      global_extras = {"debug_key": "debug_value"}
      structured_log = {"severity": severity, "message": message, **global_extras}
      print(json.dumps(structured_log))
    
    def main(args):
      log("DEBUG", "Debugging the application.")
      log("INFO", "Info.")
      log("WARNING", "Warning.")
      log("ERROR", "Error.")
      log("CRITICAL", "Critical.")

#### Special JSON fields in messages

When you provide a structured log as a JSON dictionary, some special fields are stripped from the `jsonPayload` and are written to the corresponding field in the generated [LogEntry](https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/LogEntry) as described in the documentation for [special fields](https://docs.cloud.google.com/logging/docs/agent/configuration#special-fields) .

For example, if your JSON includes a `severity` property, it is removed from the `jsonPayload` and appears instead as the log entry's `severity` . The `message` property is used as the main display text of the log entry if present.

#### Correlate your container logs with a request log (services only)

In the Logs Explorer, logs correlated by the same `trace` are viewable in "parent-child" format: when you click the triangle icon at the left of the request log entry, the container logs related to that request show up nested under the request log.

Container logs are not automatically correlated to request logs unless you use a [Cloud Logging client library](https://docs.cloud.google.com/logging/docs/reference/libraries) . To correlate container logs with request logs without using a client library, you can use a structured JSON log line that contains a `logging.googleapis.com/trace` field with the trace identifier extracted from the `X-Cloud-Trace-Context` header.

#### View logs

To view your container logs in the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Gemini Enterprise Agent Platform custom jobs** page.

2.  Click the name of the custom job that you want to see logs for.

3.  Click **View logs** .

### Write code for hyperparameter tuning

Agent Platform can perform hyperparameter tuning on your ML training code. Learn more about [how hyperparameter tuning on Agent Platform works](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) and [how to configure a `HyperparameterTuningJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) .

If you want to use hyperparameter tuning, your training code must do the following:

  - Parse command-line arguments representing the hyperparameters that you want to tune, and use the parsed values to set the hyperparameters for training.

  - Intermittently report the hyperparameter tuning metric to Agent Platform.

#### Parse command-line arguments

For hyperparameter tuning, Agent Platform runs your training code multiple times, with different command-line arguments each time. Your training code must parse these command-line arguments and use them as hyperparameters for training. For example, to tune your optimizer's [learning rate](https://developers.google.com/machine-learning/glossary#learning-rate) , you might want to parse a command-line argument named `--learning_rate` . Learn [how to configure which command-line arguments Agent Platform provides](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#command-line-arguments) .

We recommend that you use Python's [`argparse` library](https://docs.python.org/3/library/argparse.html) to parse command-line arguments.

#### Report the hyperparameter tuning metric

Your training code must intermittently report the hyperparameter metric that you are trying to optimize to Agent Platform. For example, if you want to maximize your model's accuracy, you might want to report this metric at the end of every training epoch. Agent Platform uses this information to decide what hyperparameters to use for the next training trial. Learn more about [selecting and specifying a hyperparameter tuning metric](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview#what_hyperparameter_tuning_optimizes) .

Use the `cloudml-hypertune` Python library to report the hyperparameter tuning metric. This library is included in all [prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) , and you can use `pip` to install it in a custom container.

To learn how to install and use this library, see [the `cloudml-hypertune` GitHub repository](https://github.com/GoogleCloudPlatform/cloudml-hypertune) , or refer to the [Agent Platform: Hyperparameter Tuning codelab](https://codelabs.developers.google.com/vertex_hyperparameter_tuning#0) .

### Write code for GPUs

You can select VMs with graphics processing units (GPUs) to run your custom training code. Learn more about [configuring serverless training to use GPU-enabled VMs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_gpus) .

If you want to train with GPUs, make sure your training code can take advantage of them. Depending on which ML framework you use, this might require changes to your code. For example, if you use TensorFlow Keras, [you only need to adjust your code if you want to use more than one GPU](https://www.tensorflow.org/guide/gpu) . Some ML frameworks can't use GPUs at all.

In addition, make sure that your container supports GPUs: Select a [prebuilt container for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) that supports GPUs, or install the [NVIDIA CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit) and [NVIDIA cuDNN](https://developer.nvidia.com/cudnn) on your custom container. One way to do this is to use base image from the [`nvidia/cuda` Docker repository](https://hub.docker.com/r/nvidia/cuda/) ; another way is to [use a Deep Learning Containers instance as your base image](https://docs.cloud.google.com/deep-learning-containers/docs/derivative-container) .

### Write code for distributed training

To train on large datasets, you can run your code on multiple VMs in a distributed cluster managed by Agent Platform. Learn how to [configure multiple VMs for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) .

Some ML frameworks, like [TensorFlow](https://www.tensorflow.org/guide/distributed_training#multiworkermirroredstrategy) and [PyTorch](https://pytorch.org/tutorials/intermediate/ddp_tutorial.html) , let you run identical training code on multiple machines which automatically coordinate how to divide the work based on environment variables set on each machine. Find out if Agent Platform [sets environment variables to make this possible for your ML framework](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training#cluster-variables) .

Alternatively, you can run a different container on each of several *worker pools* . A worker pool is a group of VMs that you configure to use the same compute options and container. In this case, you still probably want to rely on the environment variables set by Agent Platform to coordinate communication between the VMs. You can customize the training code of each worker pool to perform whatever arbitrary tasks you want; how you do this depends on your goal and which ML framework you use.

### Track and visualize serverless training experiments using Vertex AI TensorBoard

[Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction) is a managed version of [TensorBoard](https://www.tensorflow.org/tensorboard/get_started) , a Google open source project for visualizing machine learning experiments. With Vertex AI TensorBoard you can track, visualize, and compare ML experiments and then share them with your team. You can also use [Cloud Profiler](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler) to pinpoint and fix performance bottlenecks to train models faster and cheaper.

To use Vertex AI TensorBoard with serverless training, you must do the following:

  - Create a Vertex AI TensorBoard instance in your project to store your experiments (see [Create a TensorBoard instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-setup#create-tensorboard-instance) ).

  - Configure a service account to run the serverless training job with appropriate permissions.

  - Adjust your serverless training code to write out TensorBoard compatible logs to Cloud Storage (see [Changes to your training script](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-training#script_changes) )

For a step-by-step guide, see [Using Vertex AI TensorBoard with serverless training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-training) .

## What's next

  - Learn the details of [creating a Python training application to use with a prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) or [creating a custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .

  - If you aren't sure that you want to perform serverless training, read a [comparison of serverless training and AutoML](https://docs.cloud.google.com/vertex-ai/docs/start/training-methods) .
