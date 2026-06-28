---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning
title: Create a hyperparameter tuning job
description: Create a training application for hyperparameter tuning by accepting hyperparameters as command-line arguments and reporting metric values to Gemini Enterprise Agent Platform
data_source: docs.cloud.google.com
---

> To see an example of how to use hyperparameter tuning in , run the "Run hyperparameter tuning for a TensorFlow model" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/hyperparameter_tuning_tensorflow.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fhyperparameter_tuning_tensorflow.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fhyperparameter_tuning_tensorflow.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/hyperparameter_tuning_tensorflow.ipynb)

Hyperparameters are variables that govern the process of training a model, such as batch size or the number of hidden layers in a deep neural network. Hyperparameter tuning searches for the best combination of hyperparameter values by optimizing metric values across a series of trials. Metrics are scalar summaries that you add to your trainer, such as model accuracy.

[Learn more about hyperparameter tuning on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) . For a step-by-step example, refer to the [Agent Platform: Hyperparameter Tuning codelab](https://codelabs.developers.google.com/vertex_hyperparameter_tuning#0) .

This page shows you how to:

  - Prepare your training application for hyperparameter tuning by updating it to [accept hyperparameters as command-line arguments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#command-line-arguments) , and [report metric values to Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#report-metrics) .

  - [Create your hyperparameter training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#create) . For more information about configuration options, see [understanding hyperparameter tuning configuration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#configuration) .

## Prepare your training application

In a hyperparameter tuning job, Agent Platform creates trials of your training job with different sets of hyperparameters and evaluates the effectiveness of a trial using the metrics you specified. Agent Platform passes hyperparameter values to your training application as command-line arguments. For Agent Platform to evaluate the effectiveness of a trial, your training application must report your metrics to Agent Platform.

The following sections describe:

  - How Agent Platform passes hyperparameters to your training application.
  - Options for passing metrics from your training application to Agent Platform.

To learn more about the requirements for serverless training applications that run on Gemini Enterprise Agent Platform, read [Training code requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) .

### Handle the command-line arguments for the hyperparameters you want to tune

Agent Platform sets command-line arguments when it calls your training application. Make use of the command-line arguments in your code:

1.  Define a name for each hyperparameter argument and parse it using whatever argument parser you prefer, such as [`argparse`](https://docs.python.org/3/library/argparse.html) . Use the same argument names when configuring your hyperparameter training job.
    
    For example, if your training application is a Python module named `my_trainer` and you are tuning a hyperparameter named `learning_rate` , Agent Platform starts each trial with a command like the following:
    
        python3 -m my_trainer --learning_rate learning-rate-in-this-trial
    
    Agent Platform determines the learning-rate-in-this-trial and passes it in using the `learning_rate` argument.

2.  Assign the values from the command-line arguments to the hyperparameters in your training code.

[Learn more about the requirements for parsing command-line arguments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#command-line-arguments) .

### Report your metrics to Agent Platform

To report your metrics to Agent Platform, use the [`cloudml-hypertune` Python package](https://github.com/GoogleCloudPlatform/cloudml-hypertune) . This library provides helper functions for reporting metrics to Agent Platform.

[Learn more about reporting hyperparameter metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#hp-tuning-metric) .

## Create a hyperparameter tuning job

Depending on what tool you want to use to create a `HyperparameterTuningJob` , select one of the following tabs:

### Console

In the Google Cloud console, you can't create a `HyperparameterTuningJob` resource directly. However, you can create a `TrainingPipeline` resource that creates a `HyperparameterTuningJob` .

The following instructions describe how to create a `TrainingPipeline` that creates a `HyperparameterTuningJob` and doesn't do anything else. If you want to use additional `TrainingPipeline` features, like training with a managed dataset, read [Creating training pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) .

1.  In the Google Cloud console, in the Agent Platform section, go to the **Training pipelines** page.

2.  Click **add\_box Create** to open the **Train new model** pane.

3.  On the **Training method** step, specify the following settings:
    
    1.  In the **Dataset** drop-down list, select **No managed dataset.**
    
    2.  Select **Custom training (advanced)** .
    
    Click **Continue** .

4.  On the **Model details** step, choose **Train new model** or **Train new version** . If you select train new model, enter a name of your choice, MODEL\_NAME , for your model. Click **Continue** .

5.  On the **Training container** step, specify the following settings:
    
    1.  Select [whether to use a **Prebuilt container** or a **Custom container**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-training-methods#pre-built-custom) for training.
    
    2.  Depending on your choice, do one of the following:
        
          - If you want to use a prebuilt container for training, then provide Agent Platform with information it needs to use the training package that you have uploaded to Cloud Storage:
            
            1.  Use the **Model framework** and **Model framework version** drop-down lists to specify the [prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) that you want to use.
            
            2.  In the **Package location** field, specify the Cloud Storage URI of the [Python training application that you have created and uploaded](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) . This file usually ends with `.tar.gz` .
            
            3.  In the **Python module** field, enter the [module name of your training application's entry point](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container#python-modules) .
        
          - If you want to use a [custom container for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) , then in the **Container image** field, specify the Artifact Registry or Docker Hub URI of your container image.
    
    3.  In the **Model output directory** field, you may specify the Cloud Storage URI of a directory in a bucket that you have access to. The directory does not need to exist yet.
        
        This value gets passed to Agent Platform in the [`baseOutputDirectory` API field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#FIELDS.base_output_directory) , which sets [several environment variables that your training application can access when it runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#environment-variables) .
    
    4.  **Optional** : In the **Arguments** field, you can specify arguments for Agent Platform to use when it starts running your training code. The maximum length for all arguments combined is 100,000 characters. The behavior of these arguments differs depending on what type of container you are using:
        
          - If you are using a prebuilt container, then Agent Platform passes the arguments as command-line flags to your **Python module** .
        
          - If you are using a custom container, then Agent Platform [overrides your container's `CMD` instruction with the arguments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings#configure) .
    
    Click **Continue** .

6.  On the **Hyperparameter tuning** step, select **Enable hyperparameter tuning** checkbox and specify the following settings:
    
    1.  In the **New Hyperparameter** section, specify the **Parameter name** and **Type** of a hyperparameter that you want to tune. Depending on which type you specify, configure the additional hyperparameter settings that appear.
        
        Learn more about [hyperparameter types and their configurations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview#hyperparameters) .
    
    2.  If you want to tune more than one hyperparameter, click **Add new parameter** and repeat the previous step in the new section that appears.
        
        Repeat this for each hyperparameter that you want to tune.
    
    3.  In the **Metric to optimize** field and the **Goal** drop-down list, specify the name and goal of the [metric that you want to optimize](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview#what_hyperparameter_tuning_optimizes) .
    
    4.  In the **Maximum number of trials** field, specify the [maximum number of trials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#understanding-trials) that you want Agent Platform to run for your hyperparameter tuning job.
    
    5.  In the **Maximum number of parallel trials** field, specify the [maximum number of trials to let Agent Platform run at the same time](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#parallel-trials) .
    
    6.  In the **Search algorithm** drop-down list, specify a [search algorithm](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview#search_algorithms) for Agent Platform to use.
    
    7.  Ignore the **Enable early stopping** toggle, which has no effect.
    
    Click **Continue** .

7.  On the **Compute and pricing** step, specify the following settings:
    
    1.  In the **Region** drop-down list, select a " [region that supports custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) "
    
    2.  In the **Worker pool 0** section, specify [compute resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) to use for training.
        
        If you specify accelerators, [make sure the type of accelerator that you choose is available in your selected region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#region_considerations) .
        
        If you want to perform [distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) , then click **Add more worker pools** and specify an additional set of compute resources for each additional worker pool that you want.
    
    Click **Continue** .

8.  On the **Prediction container** step, select **No prediction container** .

9.  Click **Start training** to start the serverless training pipeline.

### gcloud

The following steps show how to use the Google Cloud CLI to create a `HyperparameterTuningJob` with a relatively minimal configuration. To learn about all the configuration options that you can use for this task, see the reference documentation for the [`gcloud ai hp-tuning-jobs create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/hp-tuning-jobs/create) and the [`HyperparameterTuningJob` API resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs) .

1.  Create a YAML file named `config.yaml` with some API fields that you want to specify for your new `HyerparameterTuningJob` :
    
    ##### `config.yaml`
    
        studySpec:
          metrics:
          - metricId: METRIC_ID
            goal: METRIC_GOAL
          parameters:
          - parameterId: HYPERPARAMETER_ID
            doubleValueSpec:
              minValue: DOUBLE_MIN_VALUE
              maxValue: DOUBLE_MAX_VALUE
        trialJobSpec:
          workerPoolSpecs:
            - machineSpec:
                machineType: MACHINE_TYPE
              replicaCount: 1
              containerSpec:
                imageUri: CUSTOM_CONTAINER_IMAGE_URI
    
    Replace the following:
    
      - `  METRIC_ID  ` : the name of a [hyperparameter metric](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview#what_hyperparameter_tuning_optimizes) to optimize. Your training code must [report this metric](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#report-metrics) when it runs.
    
      - `  METRIC_GOAL  ` : the goal for your hyperparameter metric, either `MAXIMIZE` or `MINIMIZE` .
    
      - `  HYPERPARAMETER_ID  ` : the name of a hyperparameter to tune. Your training code must [parse a command-line flag with this name](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#command-line-arguments) . For this example, the hyperparameter must take floating-point values. Learn about other [hyperparameter data types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview#data-types) .
    
      - `  DOUBLE_MIN_VALUE  ` : The minimum value (a number) that you want Agent Platform to try for this hyperparameter.
    
      - `  DOUBLE_MAX_VALUE  ` : The maximum value (a number) that you want Agent Platform to try for this hyperparameter.
    
      - `  MACHINE_TYPE  ` : the [type of VM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) to use for training.
    
      - `  CUSTOM_CONTAINER_IMAGE_URI  ` : the URI of a Docker container image with your training code. Learn how to [create a custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .
        
        For this example, you must use a custom container. `HyperparameterTuningJob` resources also support [training code in a Python source distribution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) instead of a custom container.

2.  In the same directory as your `config.yaml` file, run the following shell command:
    
        gcloud ai hp-tuning-jobs create \
            --region=LOCATION \
            --display-name=DISPLAY_NAME \
            --max-trial-count=MAX_TRIAL_COUNT \
            --parallel-trial-count=PARALLEL_TRIAL_COUNT \
            --config=config.yaml
    
    Replace the following:
    
      - `  LOCATION  ` : the region where you want to create the `HyperparameterTuningJob` . Use a [region that supports serverless training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .
    
      - `  DISPLAY_NAME  ` : a memorable display name of your choice for the `HyperparameterTuningJob` . See [REST resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs) .
    
      - `  MAX_TRIAL_COUNT  ` : the [maximum number of trials to run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#understanding-trials) .
    
      - `  PARALLEL_TRIAL_COUNT  ` : the [maximum number of trials to run in parallel](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#parallel-trials) .

### REST

Use the following code sample to create a hyperparameter tuning job using the [`create` method of the `hyperparameterTuningJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/create) .

Before using any of the request data, make the following replacements:

  - `  LOCATION  ` : the region where you want to create the `HyperparameterTuningJob` . Use a [region that supports serverless training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .
  - PROJECT : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - `  DISPLAY_NAME  ` : a memorable display name of your choice for the `HyperparameterTuningJob` . See [REST resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs) .
  - Specify your metrics:
      - `  METRIC_ID  ` : the name of a [hyperparameter metric](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview#what_hyperparameter_tuning_optimizes) to optimize. Your training code must [report this metric](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#report-metrics) when it runs.
      - `  METRIC_GOAL  ` : the goal for your hyperparameter metric, either `MAXIMIZE` or `MINIMIZE` .
  - Specify your hyperparameters:
      - `  HYPERPARAMETER_ID  ` : the name of a hyperparameter to tune. Your training code must [parse a command-line flag with this name](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#command-line-arguments) .
      - PARAMETER\_SCALE : (Optional.) How the parameter should be scaled. Leave unset for CATEGORICAL parameters. Can be `UNIT_LINEAR_SCALE` , `UNIT_LOG_SCALE` , `UNIT_REVERSE_LOG_SCALE` , or `SCALE_TYPE_UNSPECIFIED`
      - If this hyperparameter's type is DOUBLE, specify the minimum ( DOUBLE\_MIN\_VALUE ) and maximum ( DOUBLE\_MAX\_VALUE ) values for this hyperparameter.
      - If this hyperparameter's type is INTEGER, specify the minimum ( INTEGER\_MIN\_VALUE ) and maximum ( INTEGER\_MAX\_VALUE ) values for this hyperparameter.
      - If this hyperparameter's type is CATEGORICAL, specify the acceptable values ( CATEGORICAL\_VALUES ) as an array of strings.
      - If this hyperparameter's type is DISCRETE, specify the acceptable values ( DISCRETE\_VALUES ) as an array of numbers.
      - Specify conditional hyperparameters. Conditional hyperparameters are added to a trial when the parent hyperparameter's value matches the condition you specify. Learn more about [conditional hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview#conditional_hyperparameters) .
          - CONDITIONAL\_PARAMETER : The `ParameterSpec` of the conditional parameter. This specification includes the parameter's name, scale, range of values, and any conditional parameters that depend on this hyperparameter.
          - If the parent hyperparameter's type is INTEGER, specify a list of integers as the INTEGERS\_TO\_MATCH . If the parent hyperparameter's value matches one of the values specified, this conditional parameter is added to the trial.
          - If the parent hyperparameter's type is CATEGORICAL, specify a list of categories as the CATEGORIES\_TO\_MATCH . If the parent hyperparameter's value matches one of the values specified, this conditional parameter is added to the trial.
          - If the parent hyperparameter's type is DISCRETE, specify a list of integers as the DISCRETE\_VALUES\_TO\_MATCH . If the parent hyperparameter's value matches one of the values specified, this conditional parameter is added to the trial.
  - ALGORITHM : (Optional.) The search algorithm to use in this hyperparameter tuning job. Can be `ALGORITHM_UNSPECIFIED` , `GRID_SEARCH` , or `RANDOM_SEARCH` .
  - `  MAX_TRIAL_COUNT  ` : the [maximum number of trials to run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#understanding-trials) .
  - `  PARALLEL_TRIAL_COUNT  ` : the [maximum number of trials to run in parallel](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#parallel-trials) .
  - MAX\_FAILED\_TRIAL\_COUNT : The number of jobs that can fail before the hyperparameter tuning job fails.
  - Define the trial custom training job:
      - `  MACHINE_TYPE  ` : the [type of VM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) to use for training.
      - ACCELERATOR\_TYPE : (Optional.) The type of accelerator to attach to each trial.
      - ACCELERATOR\_COUNT : (Optional.) The number of accelerators to attach to each trial.
      - REPLICA\_COUNT : The number of worker replicas to use for each trial.
      - If your training application runs in a custom container, specify the following:
          - `  CUSTOM_CONTAINER_IMAGE_URI  ` : the URI of a Docker container image with your training code. Learn how to [create a custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .
          - CUSTOM\_CONTAINER\_COMMAND : (Optional.) The command to be invoked when the container is started. This command overrides the container's default entrypoint.
          - CUSTOM\_CONTAINER\_ARGS : (Optional.) The arguments to be passed when starting the container.
      - If your training application is a Python package that runs in a prebuilt container, specify the following:
          - PYTHON\_PACKAGE\_EXECUTOR\_IMAGE\_URI : The URI of the container image that runs the provided python package. Learn more about [prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) .
          - PYTHON\_PACKAGE\_URIS : The Cloud Storage location of the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100.
          - PYTHON\_MODULE : The Python module name to run after installing the packages.
          - PYTHON\_PACKAGE\_ARGS : (Optional.) Command-line arguments to be passed to the Python module.
      - SERVICE\_ACCOUNT : (Optional.) The service account that Agent Platform will use to run your code. Learn more about [attaching a custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) .
      - TIMEOUT : (Optional.) The maximum running time for each trial.
  - Specify the LABEL\_NAME and LABEL\_VALUE for any labels that you want to apply to this hyperparameter tuning job.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/hyperparameterTuningJobs

Request JSON body:

    {
      "displayName": DISPLAY_NAME,
      "studySpec": {
        "metrics": [
          {
            "metricId": METRIC_ID,
            "goal": METRIC_GOAL
          }
        ],
        "parameters": [
          {
            "parameterId": PARAMETER_ID,
            "scaleType": PARAMETER_SCALE,
    
            // Union field parameter_value_spec can be only one of the following:
            "doubleValueSpec": {
                "minValue": DOUBLE_MIN_VALUE,
                "maxValue": DOUBLE_MAX_VALUE
            },
            "integerValueSpec": {
                "minValue": INTEGER_MIN_VALUE,
                "maxValue": INTEGER_MAX_VALUE
            },
            "categoricalValueSpec": {
                "values": [
                  CATEGORICAL_VALUES
                ]
            },
            "discreteValueSpec": {
                "values": [
                  DISCRETE_VALUES
                ]
            }
            // End of list of possible types for union field parameter_value_spec.
    
            "conditionalParameterSpecs": [
                "parameterSpec": {
                  CONDITIONAL_PARAMETER
                }
    
                // Union field parent_value_condition can be only one of the following:
                "parentIntValues": {
                    "values": [INTEGERS_TO_MATCH]
                }
                "parentCategoricalValues": {
                    "values": [CATEGORIES_TO_MATCH]
                }
                "parentDiscreteValues": {
                    "values": [DISCRETE_VALUES_TO_MATCH]
                }
                // End of list of possible types for union field parent_value_condition.
            ]
          }
        ],
        "ALGORITHM": ALGORITHM
      },
      "maxTrialCount": MAX_TRIAL_COUNT,
      "parallelTrialCount": PARALLEL_TRIAL_COUNT,
      "maxFailedTrialCount": MAX_FAILED_TRIAL_COUNT,
      "trialJobSpec": {
          "workerPoolSpecs": [
            {
              "machineSpec": {
                "machineType": MACHINE_TYPE,
                "acceleratorType": ACCELERATOR_TYPE,
                "acceleratorCount": ACCELERATOR_COUNT
              },
              "replicaCount": REPLICA_COUNT,
    
              // Union field task can be only one of the following:
              "containerSpec": {
                "imageUri": CUSTOM_CONTAINER_IMAGE_URI,
                "command": [
                  CUSTOM_CONTAINER_COMMAND
                ],
                "args": [
                  CUSTOM_CONTAINER_ARGS
                ]
              },
              "pythonPackageSpec": {
                "executorImageUri": PYTHON_PACKAGE_EXECUTOR_IMAGE_URI,
                "packageUris": [
                  PYTHON_PACKAGE_URIS
                ],
                "pythonModule": PYTHON_MODULE,
                "args": [
                  PYTHON_PACKAGE_ARGS
                ]
              }
              // End of list of possible types for union field task.
            }
          ],
          "scheduling": {
            "TIMEOUT": TIMEOUT
          },
          "serviceAccount": SERVICE_ACCOUNT
      },
      "labels": {
        LABEL_NAME_1": LABEL_VALUE_1,
        LABEL_NAME_2": LABEL_VALUE_2
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/hyperparameterTuningJobs"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/hyperparameterTuningJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/12345/locations/us-central1/hyperparameterTuningJobs/6789",
      "displayName": "myHyperparameterTuningJob",
      "studySpec": {
        "metrics": [
          {
            "metricId": "myMetric",
            "goal": "MINIMIZE"
          }
        ],
        "parameters": [
          {
            "parameterId": "myParameter1",
            "integerValueSpec": {
              "minValue": "1",
              "maxValue": "128"
            },
            "scaleType": "UNIT_LINEAR_SCALE"
          },
          {
            "parameterId": "myParameter2",
            "doubleValueSpec": {
              "minValue": 1e-07,
              "maxValue": 1
            },
            "scaleType": "UNIT_LINEAR_SCALE"
          }
        ],
        "ALGORITHM": "RANDOM_SEARCH"
      },
      "maxTrialCount": 20,
      "parallelTrialCount": 1,
      "trialJobSpec": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": "n1-standard-4"
            },
            "replicaCount": "1",
            "pythonPackageSpec": {
              "executorImageUri": "us-docker.pkg.dev/vertex-ai/training/training-tf-cpu.2-1:latest",
              "packageUris": [
                "gs://my-bucket/my-training-application/trainer.tar.bz2"
              ],
              "pythonModule": "my-trainer.trainer"
            }
          }
        ]
      }
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.AcceleratorType;
    import com.google.cloud.aiplatform.v1.CustomJobSpec;
    import com.google.cloud.aiplatform.v1.HyperparameterTuningJob;
    import com.google.cloud.aiplatform.v1.JobServiceClient;
    import com.google.cloud.aiplatform.v1.JobServiceSettings;
    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.cloud.aiplatform.v1.MachineSpec;
    import com.google.cloud.aiplatform.v1.PythonPackageSpec;
    import com.google.cloud.aiplatform.v1.StudySpec;
    import com.google.cloud.aiplatform.v1.StudySpec.MetricSpec;
    import com.google.cloud.aiplatform.v1.StudySpec.MetricSpec.GoalType;
    import com.google.cloud.aiplatform.v1.StudySpec.ParameterSpec;
    import com.google.cloud.aiplatform.v1.StudySpec.ParameterSpec.ConditionalParameterSpec;
    import com.google.cloud.aiplatform.v1.StudySpec.ParameterSpec.ConditionalParameterSpec.DiscreteValueCondition;
    import com.google.cloud.aiplatform.v1.StudySpec.ParameterSpec.DiscreteValueSpec;
    import com.google.cloud.aiplatform.v1.StudySpec.ParameterSpec.DoubleValueSpec;
    import com.google.cloud.aiplatform.v1.StudySpec.ParameterSpec.ScaleType;
    import com.google.cloud.aiplatform.v1.WorkerPoolSpec;
    import java.io.IOException;
    import java.util.Arrays;
    
    public class CreateHyperparameterTuningJobPythonPackageSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "PROJECT";
        String displayName = "DISPLAY_NAME";
        String executorImageUri = "EXECUTOR_IMAGE_URI";
        String packageUri = "PACKAGE_URI";
        String pythonModule = "PYTHON_MODULE";
        createHyperparameterTuningJobPythonPackageSample(
            project, displayName, executorImageUri, packageUri, pythonModule);
      }
    
      static void createHyperparameterTuningJobPythonPackageSample(
          String project,
          String displayName,
          String executorImageUri,
          String packageUri,
          String pythonModule)
          throws IOException {
        JobServiceSettings settings =
            JobServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
        String location = "us-central1";
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (JobServiceClient client = JobServiceClient.create(settings)) {
          // study spec
          MetricSpec metric =
              MetricSpec.newBuilder().setMetricId("val_rmse").setGoal(GoalType.MINIMIZE).build();
    
          // decay
          DoubleValueSpec doubleValueSpec =
              DoubleValueSpec.newBuilder().setMinValue(1e-07).setMaxValue(1).build();
          ParameterSpec parameterDecaySpec =
              ParameterSpec.newBuilder()
                  .setParameterId("decay")
                  .setDoubleValueSpec(doubleValueSpec)
                  .setScaleType(ScaleType.UNIT_LINEAR_SCALE)
                  .build();
          Double[] decayValues = {32.0, 64.0};
          DiscreteValueCondition discreteValueDecay =
              DiscreteValueCondition.newBuilder().addAllValues(Arrays.asList(decayValues)).build();
          ConditionalParameterSpec conditionalParameterDecay =
              ConditionalParameterSpec.newBuilder()
                  .setParameterSpec(parameterDecaySpec)
                  .setParentDiscreteValues(discreteValueDecay)
                  .build();
    
          // learning rate
          ParameterSpec parameterLearningSpec =
              ParameterSpec.newBuilder()
                  .setParameterId("learning_rate")
                  .setDoubleValueSpec(doubleValueSpec) // Use the same min/max as for decay
                  .setScaleType(ScaleType.UNIT_LINEAR_SCALE)
                  .build();
    
          Double[] learningRateValues = {4.0, 8.0, 16.0};
          DiscreteValueCondition discreteValueLearning =
              DiscreteValueCondition.newBuilder()
                  .addAllValues(Arrays.asList(learningRateValues))
                  .build();
          ConditionalParameterSpec conditionalParameterLearning =
              ConditionalParameterSpec.newBuilder()
                  .setParameterSpec(parameterLearningSpec)
                  .setParentDiscreteValues(discreteValueLearning)
                  .build();
    
          // batch size
          Double[] batchSizeValues = {4.0, 8.0, 16.0, 32.0, 64.0, 128.0};
    
          DiscreteValueSpec discreteValueSpec =
              DiscreteValueSpec.newBuilder().addAllValues(Arrays.asList(batchSizeValues)).build();
          ParameterSpec parameter =
              ParameterSpec.newBuilder()
                  .setParameterId("batch_size")
                  .setDiscreteValueSpec(discreteValueSpec)
                  .setScaleType(ScaleType.UNIT_LINEAR_SCALE)
                  .addConditionalParameterSpecs(conditionalParameterDecay)
                  .addConditionalParameterSpecs(conditionalParameterLearning)
                  .build();
    
          // trial_job_spec
          MachineSpec machineSpec =
              MachineSpec.newBuilder()
                  .setMachineType("n1-standard-4")
                  .setAcceleratorType(AcceleratorType.NVIDIA_TESLA_T4)
                  .setAcceleratorCount(1)
                  .build();
    
          PythonPackageSpec pythonPackageSpec =
              PythonPackageSpec.newBuilder()
                  .setExecutorImageUri(executorImageUri)
                  .addPackageUris(packageUri)
                  .setPythonModule(pythonModule)
                  .build();
    
          WorkerPoolSpec workerPoolSpec =
              WorkerPoolSpec.newBuilder()
                  .setMachineSpec(machineSpec)
                  .setReplicaCount(1)
                  .setPythonPackageSpec(pythonPackageSpec)
                  .build();
    
          StudySpec studySpec =
              StudySpec.newBuilder()
                  .addMetrics(metric)
                  .addParameters(parameter)
                  .setAlgorithm(StudySpec.Algorithm.RANDOM_SEARCH)
                  .build();
          CustomJobSpec trialJobSpec =
              CustomJobSpec.newBuilder().addWorkerPoolSpecs(workerPoolSpec).build();
          // hyperparameter_tuning_job
          HyperparameterTuningJob hyperparameterTuningJob =
              HyperparameterTuningJob.newBuilder()
                  .setDisplayName(displayName)
                  .setMaxTrialCount(4)
                  .setParallelTrialCount(2)
                  .setStudySpec(studySpec)
                  .setTrialJobSpec(trialJobSpec)
                  .build();
          LocationName parent = LocationName.of(project, location);
          HyperparameterTuningJob response =
              client.createHyperparameterTuningJob(parent, hyperparameterTuningJob);
          System.out.format("response: %s\n", response);
          System.out.format("Name: %s\n", response.getName());
        }
      }
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    from google.cloud.aiplatform import hyperparameter_tuning as hpt
    
    
    def create_hyperparameter_tuning_job_sample(
        project: str,
        location: str,
        staging_bucket: str,
        display_name: str,
        container_uri: str,
    ):
        aiplatform.init(project=project, location=location, staging_bucket=staging_bucket)
    
        worker_pool_specs = [
            {
                "machine_spec": {
                    "machine_type": "n1-standard-4",
                    "accelerator_type": "NVIDIA_TESLA_K80",
                    "accelerator_count": 1,
                },
                "replica_count": 1,
                "container_spec": {
                    "image_uri": container_uri,
                    "command": [],
                    "args": [],
                },
            }
        ]
    
        custom_job = aiplatform.CustomJob(
            display_name='custom_job',
            worker_pool_specs=worker_pool_specs,
        )
    
        hpt_job = aiplatform.HyperparameterTuningJob(
            display_name=display_name,
            custom_job=custom_job,
            metric_spec={
                'loss': 'minimize',
            },
            parameter_spec={
                'lr': hpt.DoubleParameterSpec(min=0.001, max=0.1, scale='log'),
                'units': hpt.IntegerParameterSpec(min=4, max=128, scale='linear'),
                'activation': hpt.CategoricalParameterSpec(values=['relu', 'selu']),
                'batch_size': hpt.DiscreteParameterSpec(values=[128, 256], scale='linear')
            },
            max_trial_count=128,
            parallel_trial_count=8,
            labels={'my_key': 'my_value'},
        )
    
        hpt_job.run()
    
        print(hpt_job.resource_name)
        return hpt_job

## Hyperparameter training job configuration

Hyperparameter tuning jobs search for the best combination of hyperparameters to optimize your metrics. Hyperparameter tuning jobs do this by running multiple trials of your training application with different sets of hyperparameters.

When you configure a hyperparameter tuning job, you must specify the following details:

  - The hyperparameters you want to tune and the metrics that you want to use to evaluate trials.
    
    [Learn more about selecting hyperparameters and metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) .

  - Details about the number of trials to run as a part of this tuning job, such as the following:
    
      - [The maximum number of trials to run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#understanding-trials) .
      - [The number of trials that can run in parallel](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#parallel-trials) .
      - [The maximum number of trials that are allowed to fail before the job stops early](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#failed-trials) .

  - Details about the serverless training job that is run for each trial, such as the following:
    
      - The [machine type](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) that the trials jobs run in and the accelerators that the job uses.
        
        > **Note:** Gemini Enterprise Agent Platform doesn't support hyperparameter tuning jobs that require TPUs.
    
      - The details of the custom container or Python package job.
        
        [Learn more about training code requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) .

### Limit the number of trials

Decide how many trials you want to allow the service to run and set the `maxTrialCount` value in the [HyperparameterTuningJob](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs#resource:-hyperparametertuningjob) object.

There are two competing interests to consider when deciding how many trials to allow:

  - time (and therefore cost)
  - accuracy

Increasing the number of trials generally yields better results, but it is not always so. Usually, there is a point of diminishing returns after which additional trials have little or no effect on the accuracy. Before starting a job with a large number of trials, you may want to start with a small number of trials to gauge the effect your chosen hyperparameters have on your model's accuracy.

To get the most out of hyperparameter tuning, you shouldn't set your maximum value lower than ten times the number of hyperparameters you use.

### Parallel trials

You can specify how many trials can run in parallel by setting `parallelTrialCount` in the [HyperparameterTuningJob](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs#resource:-hyperparametertuningjob) .

Running parallel trials has the benefit of reducing the time the training job takes (real time—the total processing time required is not typically changed). However, running in parallel can reduce the effectiveness of the tuning job overall. That is because hyperparameter tuning uses the results of previous trials to inform the values to assign to the hyperparameters of subsequent trials. When running in parallel, some trials start without having the benefit of the results of any trials still running.

If you use parallel trials, the hyperparameter tuning service provisions multiple training processing clusters (or multiple individual machines in the case of a single-process trainer). The work pool spec that you set for your job is used for each individual training cluster.

### Handle failed trials

If your hyperparameter tuning trials exit with errors, you might want to end the training job early. Set the `maxFailedTrialCount` field in the [HyperparameterTuningJob](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs#resource:-hyperparametertuningjob) to the number of failed trials that you want to allow. After this number of trials fails, Agent Platform ends the training job. The `maxFailedTrialCount` value must be less than or equal to `maxTrialCount` .

If you don't set `maxFailedTrialCount` , or if you set it to `0` , Agent Platform uses the following rules to handle failing trials:

  - If the first trial of your job fails, Agent Platform ends the job immediately. Failure during the first trial suggests a problem in your training code, so further trials are also likely to fail. Ending the job lets you diagnose the problem without waiting for more trials and incurring greater costs.
  - If the first trial succeeds, Agent Platform might end the job after failures during subsequent trials based on one of the following criteria:
      - The number of failed trials has grown too high.
      - The ratio of failed trials to successful trials has grown too high.

These rules are subject to change. To ensure a specific behavior, set the `maxFailedTrialCount` field.

## Manage hyperparameter tuning jobs

The following sections describe how to manage your hyperparameter tuning jobs.

### Retrieve information about a hyperparameter tuning job

The following code samples demonstrate how to retrieve a hyperparameter tuning job.

### gcloud

Use the [`gcloud ai hp-tuning-jobs describe` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/hp-tuning-jobs/describe) :

    gcloud ai hp-tuning-jobs describe ID_OR_NAME \
        --region=LOCATION

Replace the following:

  - `  ID_OR_NAME  ` : either the [name](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/get) or the numerical ID of the `HyperparameterTuningJob` . (The ID is the last part of the name.)
    
    You might have seen the ID or name when you created the `HyperparameterTuningJob` . If you don't know the ID or name, you can run the [`gcloud ai hp-tuning-jobs list` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/hp-tuning-jobs/list) and look for the appropriate resource.

  - `  LOCATION  ` : the region where the `HyperparameterTuningJob` was created.

### REST

Use the following code sample to retrieve a hyperparameter tuning job using the [`get` method of the `hyperparameterTuningJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/get) .

Before using any of the request data, make the following replacements:

  - `  LOCATION  ` : the region where the `HyperparameterTuningJob` was created.
  - NAME : The name of the hyperparameter tuning job. The job name uses the following format `projects/{project}/LOCATIONS/{LOCATION}/hyperparameterTuningJobs/{hyperparameterTuningJob}` .

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/NAME

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/NAME"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/12345/LOCATIONs/us-central1/hyperparameterTuningJobs/6789",
      "displayName": "my-hyperparameter-tuning-job",
      "studySpec": {
        "metrics": [
          {
            "metricId": "my_metric",
            "goal": "MINIMIZE"
          }
        ],
        "parameters": [
          {
            "parameterId": "my_parameter",
            "doubleValueSpec": {
              "minValue": 1e-05,
              "maxValue": 1
            }
          }
        ]
      },
      "maxTrialCount": 3,
      "parallelTrialCount": 1,
      "trialJobSpec": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": "n1-standard-4"
            },
            "replicaCount": "1",
            "pythonPackageSpec": {
              "executorImageUri": "us-docker.pkg.dev/vertex-ai/training/training-tf-cpu.2-1:latest",
              "packageUris": [
                "gs://my-bucket/my-training-application/trainer.tar.bz2"
              ],
              "pythonModule": "my-trainer.trainer"
            }
          }
        ]
      },
      "trials": [
        {
          "id": "2",
          "state": "SUCCEEDED",
          "parameters": [
            {
              "parameterId": "my_parameter",
              "value": 0.71426874725564571
            }
          ],
          "finalMeasurement": {
            "stepCount": "2",
            "metrics": [
              {
                "metricId": "my_metric",
                "value": 0.30007445812225342
              }
            ]
          },
          "startTime": "2020-09-09T23:39:15.549112551Z",
          "endTime": "2020-09-09T23:47:08Z"
        },
        {
          "id": "3",
          "state": "SUCCEEDED",
          "parameters": [
            {
              "parameterId": "my_parameter",
              "value": 0.3078893356622992
            }
          ],
          "finalMeasurement": {
            "stepCount": "2",
            "metrics": [
              {
                "metricId": "my_metric",
                "value": 0.30000102519989014
              }
            ]
          },
          "startTime": "2020-09-09T23:49:22.451699360Z",
          "endTime": "2020-09-09T23:57:15Z"
        },
        {
          "id": "1",
          "state": "SUCCEEDED",
          "parameters": [
            {
              "parameterId": "my_parameter",
              "value": 0.500005
            }
          ],
          "finalMeasurement": {
            "stepCount": "2",
            "metrics": [
              {
                "metricId": "my_metric",
                "value": 0.30005377531051636
              }
            ]
          },
          "startTime": "2020-09-09T23:23:12.283374629Z",
          "endTime": "2020-09-09T23:36:56Z"
        }
      ],
      "state": "JOB_STATE_SUCCEEDED",
      "createTime": "2020-09-09T23:22:31.777386Z",
      "startTime": "2020-09-09T23:22:34Z",
      "endTime": "2020-09-10T01:31:24.271307Z",
      "updateTime": "2020-09-10T01:31:24.271307Z"
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.HyperparameterTuningJob;
    import com.google.cloud.aiplatform.v1.HyperparameterTuningJobName;
    import com.google.cloud.aiplatform.v1.JobServiceClient;
    import com.google.cloud.aiplatform.v1.JobServiceSettings;
    import java.io.IOException;
    
    public class GetHyperparameterTuningJobSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "PROJECT";
        String hyperparameterTuningJobId = "HYPERPARAMETER_TUNING_JOB_ID";
        getHyperparameterTuningJobSample(project, hyperparameterTuningJobId);
      }
    
      static void getHyperparameterTuningJobSample(String project, String hyperparameterTuningJobId)
          throws IOException {
        JobServiceSettings settings =
            JobServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
        String location = "us-central1";
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (JobServiceClient client = JobServiceClient.create(settings)) {
          HyperparameterTuningJobName name =
              HyperparameterTuningJobName.of(project, location, hyperparameterTuningJobId);
          HyperparameterTuningJob response = client.getHyperparameterTuningJob(name);
          System.out.format("response: %s\n", response);
        }
      }
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

``` 
# Copyright 2022 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from google.cloud import aiplatform


def get_hyperparameter_tuning_job_sample(
    project: str,
    hyperparameter_tuning_job_id: str,
    location: str = "us-central1",
):

    aiplatform.init(project=project, location=location)

    hpt_job = aiplatform.HyperparameterTuningJob.get(
        resource_name=hyperparameter_tuning_job_id,
    )

    return hpt_job

```

### Cancel a hyperparameter tuning job

The following code samples demonstrate how to cancel a hyperparameter tuning job.

### gcloud

Use the [`gcloud ai hp-tuning-jobs cancel` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/hp-tuning-jobs/cancel) :

    gcloud ai hp-tuning-jobs cancel ID_OR_NAME \
        --region=LOCATION

Replace the following:

  - `  ID_OR_NAME  ` : either the [name](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/cancel) or the numerical ID of the `HyperparameterTuningJob` . (The ID is the last part of the name.)
    
    You might have seen the ID or name when you created the `HyperparameterTuningJob` . If you don't know the ID or name, you can run the [`gcloud ai hp-tuning-jobs list` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/hp-tuning-jobs/list) and look for the appropriate resource.

  - `  LOCATION  ` : the region where the `HyperparameterTuningJob` was created.

### REST

Use the following code sample to cancel a hyperparameter tuning job using the [`cancel` method of the `hyperparameterTuningJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/cancel) .

Before using any of the request data, make the following replacements:

  - `  LOCATION  ` : the region where the `HyperparameterTuningJob` was created.
  - NAME : The name of the hyperparameter tuning job. The job name uses the following format `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameterTuningJob}` .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/NAME:cancel

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION-aiplatform.googleapis.com/v1/NAME:cancel"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/NAME:cancel" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def cancel_hyperparameter_tuning_job_sample(
        project: str,
        hyperparameter_tuning_job_id: str,
        location: str = "us-central1",
    ):
    
        aiplatform.init(project=project, location=location)
    
        hpt_job = aiplatform.HyperparameterTuningJob.get(
            resource_name=hyperparameter_tuning_job_id,
        )
    
        hpt_job.cancel()

### Delete a hyperparameter tuning job

The following code samples demonstrate how to delete a hyperparameter tuning job using the Agent Platform SDK for Python and the REST API.

### REST

Use the following code sample to delete a hyperparameter tuning job using the [`delete` method of the `hyperparameterTuningJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/delete) .

Before using any of the request data, make the following replacements:

  - LOCATION : Your region.
  - NAME : The name of the hyperparameter tuning job. The job name uses the following format `projects/{project}/LOCATIONs/{LOCATION}/hyperparameterTuningJobs/{hyperparameterTuningJob}` .

HTTP method and URL:

    DELETE https://LOCATION-aiplatform.googleapis.com/v1/NAME

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/NAME"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/NAME" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def delete_hyperparameter_tuning_job_sample(
        project: str,
        hyperparameter_tuning_job_id: str,
        location: str = "us-central1",
    ):
    
        aiplatform.init(project=project, location=location)
    
        hpt_job = aiplatform.HyperparameterTuningJob.get(
            resource_name=hyperparameter_tuning_job_id,
        )
    
        hpt_job.delete()

## What's next

  - Learn more about [the concepts involved in hyperparameter tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) .
  - Learn how to [schedule serverless training jobs based on resource availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/schedule-jobs-dws) .
