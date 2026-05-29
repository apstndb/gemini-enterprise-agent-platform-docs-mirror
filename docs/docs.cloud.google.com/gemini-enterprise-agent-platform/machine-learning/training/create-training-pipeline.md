---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline
title: Create training pipelines
description: Launch a CustomJob or a hyperparameter tuning job, and upload the resulting model to Agent Platform.
data_source: docs.cloud.google.com
---

Training pipelines let you perform custom machine learning (ML) training and automatically create a `Model` resource based on your training output.

If your task only involves running a training job and automatically creating a model resource without orchestrating a full workflow, using a standalone training pipeline as described in this document might be sufficient. However, if your goal is to build a robust, automated, and repeatable end-to-end ML lifecycle that involves multiple steps (like data processing, training, evaluation, deployment, or monitoring), [Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction) is the recommended approach since it's designed for workflow orchestration.

## Before you create a pipeline

Before you create a training pipeline on Agent Platform, you need to create a [Python training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) or a [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) to define the training code and dependencies you want to run on Agent Platform. If you create a Python training application using PyTorch, TensorFlow, scikit-learn, or XGBoost, you can use our prebuilt containers to run your code. If you're not sure which of these options to choose, refer to the [training code requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) to learn more.

## Training pipeline options

A *training pipeline* encapsulates training jobs with additional steps. This guide explains two different training pipelines:

  - Launch a `CustomJob` and upload the resulting model to Agent Platform
  - Launch a hyperparameter tuning job and upload the resulting model to Agent Platform

Additionally, you can use managed datasets in your training pipeline. [Learn more about configuring your training pipeline to use a managed dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline#managed-dataset) .

### What a `CustomJob` includes

When you create a *custom job* , you specify settings that Agent Platform needs to run your training code, including:

  - One worker pool for single-node training ( [`WorkerPoolSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#workerpoolspec) ), or multiple worker pools for distributed training
  - Optional settings for configuring job scheduling ( [`Scheduling`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#scheduling) ), [setting certain environment variables for your training code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#environment-variables) , [using a custom service account](https://docs.cloud.google.com/vertex-ai/docs/general/custom-service-account) , and [using VPC Network Peering](https://docs.cloud.google.com/vertex-ai/docs/general/vpc-peering)

Within the worker pool(s), you can specify the following settings:

  - [Machine types and accelerators](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute)
  - [Configuration of what type of training code the worker pool runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings) : either a Python training application ( [`PythonPackageSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#pythonpackagespec) ) or a custom container ( [`ContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#containerspec) )

If you want to create a standalone custom job outside of a Vertex AI Training pipeline, refer to the [guide on custom jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

### Configure your pipeline to use a managed dataset

Within your training pipeline, you can configure your serverless training job or hyperparameter tuning job to use a managed dataset. Managed datasets let you manage your datasets with your training applications and models.

To use a managed dataset in your training pipeline:

1.  [Create your dataset](https://docs.cloud.google.com/vertex-ai/docs/datasets/overview) .

2.  Update your training application to use a managed dataset. For more information, see [how Agent Platform passes your dataset to your training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-managed-datasets) .

3.  Specify a managed dataset when you create your training pipeline. For example, if you create your training pipeline using the REST API, specify the dataset settings in the `inputDataConfig` section.
    
    You must create the training pipeline in the same region where you created the dataset.

To learn more, refer to the API reference on [`TrainingPipeline`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines) .

### Configure distributed training

Within your training pipeline, you can configure your serverless training job or hyperparameter tuning job for distributed training by specifying multiple worker pools.

All the examples on this page show single-replica training jobs with one worker pool. To modify them for distributed training:

  - Use your first worker pool to configure your primary replica, and set the replica count to 1.
  - Add more worker pools to configure worker replicas, parameter server replicas, or evaluator replicas, if your machine learning framework supports these additional cluster tasks for distributed training.

Learn more about [using distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) .

## CustomJob and model upload

This training pipeline encapsulates a custom job with an added convenience step that makes it easier to deploy your model to Agent Platform after training. This training pipeline does two main things:

1.  The training pipeline creates a `CustomJob` resource. The custom job runs the training application using the computing resources that you specify.

2.  After the custom job completes, the training pipeline finds the model artifacts that your training application creates in the output directory you specified for your Cloud Storage bucket. It uses these artifacts to create a *model* resource, which sets you up for [model deployment](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api) .

There are two different ways to set the location for your model artifacts:

  - If you set a [`baseOutputDirectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#FIELDS.base_output_directory) for your training job, make sure your training code saves your model artifacts to that location, using the [`$AIP_MODEL_DIR` environment variable](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#environment-variables) set by Agent Platform. After the training job is completed, Agent Platform searches for the resulting model artifacts in `gs:// BASE_OUTPUT_DIRECTORY /model` .
    
    > **Note** : If you're using the Agent Platform SDK for Python, you can omit the `base_output_dir` attribute. In this case, Gemini Enterprise Agent Platform outputs your model artifacts to a timestamped directory in the staging directory. For details, see:
    > 
    >   - [`CustomJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob)
    > 
    >   - [`CustomContainerTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob#google_cloud_aiplatform_CustomContainerTrainingJob_run)
    > 
    >   - [`CustomPythonPackageTrainingJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob#google_cloud_aiplatform_CustomPythonPackageTrainingJob_run)

  - If you set the [`modelToUpload.artifactUri` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.artifact_uri) , the training pipeline uploads the model artifacts from that URI. You must set this field if you didn't set [`baseOutputDirectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#FIELDS.base_output_directory) .

If you specify both `baseOutputDirectory` and `modelToUpload.artifactUri` , Agent Platform uses `modelToUpload.artifactUri` .

To create this type of training pipeline:

### Console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Training pipelines** page.

2.  Click **add\_box Create** to open the **Train new model** pane.

3.  On the **Training method** step, specify the following settings:
    
    1.  If you want to [use a managed dataset for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline#managed-dataset) , then specify a **Dataset** and an **Annotation set** .
        
        Otherwise, in the **Dataset** drop-down list, select **No managed dataset** .
    
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
    
    3.  In the **Model output directory** field, specify the Cloud Storage URI of a directory in a bucket that you have access to. The directory does not need to exist yet.
        
        This value gets passed to Agent Platform in the [`baseOutputDirectory` API field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#FIELDS.base_output_directory) , which sets [several environment variables that your training application can access when it runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#environment-variables) .
        
        At the end of training, Agent Platform looks for [model artifacts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts) in a subdirectory of this URI in order to create a `Model` . (This subdirectory is available to your training code as the `AIP_MODEL_DIR` environment variable.)
        
        When you don't use hyperparameter tuning, Agent Platform expects to find model artifacts in `  BASE_OUTPUT_DIRECTORY /model/ ` .
    
    4.  **Optional** : In the **Arguments** field, you can specify arguments for Agent Platform to use when it starts running your training code. The maximum length for all arguments combined is 100,000 characters. The behavior of these arguments differs depending on what type of container you are using:
        
          - If you are using a prebuilt container, then Agent Platform passes the arguments as command-line flags to your **Python module** .
        
          - If you are using a custom container, then Agent Platform [overrides your container's `CMD` instruction with the arguments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings#configure) .
    
    Click **Continue** .

6.  On the **Hyperparameter tuning** step, make sure that the **Enable hyperparameter tuning** checkbox is not selected. Click **Continue** .

7.  On the **Compute and pricing** step, specify the following settings:
    
    1.  In the **Region** drop-down list, select a " [region that supports custom training](https://docs.cloud.google.com/vertex-ai/docs/general/locations) "
    
    2.  In the **Worker pool 0** section, specify [compute resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) to use for training.
        
        If you specify accelerators, [make sure the type of accelerator that you choose is available in your selected region](https://docs.cloud.google.com/vertex-ai/docs/general/locations#region_considerations) .
        
        If you want to perform [distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) , then click **Add more worker pools** and specify an additional set of compute resources for each additional worker pool that you want.
    
    Click **Continue** .

8.  On the **Prediction container** step, specify the following settings:
    
    1.  Select [whether to use a **Prebuilt container** or a **Custom container**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model#container-type) to serve predictions from your trained model.
    
    2.  Depending on your choice, do one of the following:
        
          - If you want to use a prebuilt container to serve predictions, then use the **Model framework** , **Model framework version** , and **Accelerator type** fields to choose [which prebuilt prediction container](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) to use for prediction.
            
            Match **Model framework** and **Model framework version** to the machine learning framework you used for training. Only specify an **Accelerator type** if you want to later [use GPUs for online or batch predictions](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute) .
        
          - If you want to use a custom container to serve predictions, then do the following:
            
            1.  In the **Container image** field, specify the [Artifact Registry URI of your container image](https://docs.cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#publishing) .
            
            2.  Optionally, you may specify a **Command** to [override the container's `ENTRYPOINT` instruction](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container#create-model) .
    
    3.  The **Model directory** field contains the value that you previously set in the **Model output directory** field of the **Training container** step. Changing either of these fields has the same effect. See the [previous instruction](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline#model-output-directory-False) for more information about this field.
    
    4.  Leave the fields in the **Predict schemata** section blank.

9.  Click **Start training** to start the serverless training pipeline.

### REST

Use the following code sample to create a training pipeline using the [`create` method of the `trainingPipeline` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/create) .

**Note:** If you want to set this pipeline to create a new model *version* , you can optionally add the `PARENT_MODEL` in the `trainingPipeline` field.

To learn more, see [Model versioning with Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/versioning) .

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where the training code is run and the `Model` is stored.
  - PROJECT\_ID : Your project ID.
  - TRAINING\_PIPELINE\_NAME : Required. A display name for the trainingPipeline.
  - If your training application uses an Agent Platform dataset, specify the following:
      - DATASET\_ID : The ID of the dataset.
      - ANNOTATIONS\_FILTER : Filters the dataset by the annotations that you specify.
      - ANNOTATION\_SCHEMA\_URI : Filters the dataset by the specified annotation schema URI.
      - Use one of the following options to specify how data items are split into training, validation, and test sets.
          - To split the dataset based on fractions defining the size of each set, specify the following:
              - TRAINING\_FRACTION : The fraction of the dataset to use to train your model.
              - VALIDATION\_FRACTION : The fraction of the dataset to use to validate your model.
              - TEST\_FRACTION : The fraction of the dataset to use to evaluate your model.
          - To split the dataset based on filters, specify the following:
              - TRAINING\_FILTER : Filters the dataset to data items to use for training your model.
              - VALIDATION\_FILTER : Filters the dataset to data items to use for validating your model.
              - TEST\_FILTER : Filters the dataset to data items to use for evaluating your model.
          - To use a predefined split, specify the following:
              - PREDEFINED\_SPLIT\_KEY : The name of the column to use to split the dataset. Acceptable values in this column include \`training\`, \`validation\`, and \`test\`.
          - To split the dataset based on the timestamp on the dataitems, specify the following:
              - TIMESTAMP\_TRAINING\_FRACTION : The fraction of the dataset to use to train your model.
              - TIMESTAMP\_VALIDATION\_FRACTION : The fraction of the dataset to use to validate your model.
              - TIMESTAMP\_TEST\_FRACTION : The fraction of the dataset to use to evaluate your model.
              - TIMESTAMP\_SPLIT\_KEY : The name of the timestamp column to use to split the dataset.
      - OUTPUT\_URI\_PREFIX : The Cloud Storage location where Agent Platform exports your training dataset, once it has been split into training, validation, and test sets.
  - Define the custom training job:
      - MACHINE\_TYPE : The type of the machine. Refer to [available machine types for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) .
      - ACCELERATOR\_TYPE : (Optional.) The type of accelerator to attach to each trial.
      - ACCELERATOR\_COUNT : (Optional.) The number of accelerators to attach to each trial.
      - REPLICA\_COUNT : The number of worker replicas to use for each trial.
      - If your training application runs in a custom container, specify the following:
          - CUSTOM\_CONTAINER\_IMAGE\_URI : The URI of a container image in Artifact Registry or Docker Hub that is to be run on each worker replica.
          - CUSTOM\_CONTAINER\_COMMAND : (Optional.) The command to be invoked when the container is started. This command overrides the container's default entrypoint.
          - CUSTOM\_CONTAINER\_ARGS : (Optional.) The arguments to be passed when starting the container. The maximum length for all arguments combined is 100,000 characters.
      - If your training application is a Python package that runs in a prebuilt container, specify the following:
          - PYTHON\_PACKAGE\_EXECUTOR\_IMAGE\_URI : The URI of the container image that runs the provided Python package. Refer to the [available prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) .
          - PYTHON\_PACKAGE\_URIS : The Cloud Storage location of the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100.
          - PYTHON\_MODULE : The Python module name to run after installing the packages.
          - PYTHON\_PACKAGE\_ARGS : (Optional.) Command-line arguments to be passed to the Python module. The maximum length for all arguments combined is 100,000 characters.
      - TIMEOUT : (Optional.) The maximum running time for the job.
  - MODEL\_NAME : A display name for the model uploaded (created) by the TrainingPipeline.
  - MODEL\_DESCRIPTION : A description for the model.
  - IMAGE\_URI : The URI of the container image to use for running predictions. For example, `us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-1:latest` . Use [prebuilt containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) or [custom containers](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container) .
  - modelToUpload.labels : Any set of key-value pairs to organize your models. For example:
      - "env": "prod"
      - "tier": "backend"
  - Specify the LABEL\_NAME and LABEL\_VALUE for any labels that you want to apply to this training pipeline.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/trainingPipelines

Request JSON body:

    {
      "displayName": "TRAINING_PIPELINE_NAME",
      "inputDataConfig": {
        "datasetId": DATASET_ID,
        "annotationsFilter": ANNOTATIONS_FILTER,
        "annotationSchemaUri": ANNOTATION_SCHEMA_URI,
    
        // Union field split can be only one of the following:
        "fractionSplit": {
          "trainingFraction": TRAINING_FRACTION,
          "validationFraction": VALIDATION_FRACTION,
          "testFraction": TEST_FRACTION
        },
        "filterSplit": {
          "trainingFilter": TRAINING_FILTER,
          "validationFilter": VALIDATION_FILTER,
          "testFilter": TEST_FILTER
        },
        "predefinedSplit": {
          "key": PREDEFINED_SPLIT_KEY
        },
        "timestampSplit": {
          "trainingFraction": TIMESTAMP_TRAINING_FRACTION,
          "validationFraction": TIMESTAMP_VALIDATION_FRACTION,
          "testFraction": TIMESTAMP_TEST_FRACTION,
          "key": TIMESTAMP_SPLIT_KEY
        }
        // End of list of possible types for union field split.
        "gcsDestination": {
          "outputUriPrefix": OUTPUT_URI_PREFIX
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/custom_task_1.0.0.yaml",
      "trainingTaskInputs": {
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
          }
        }
      },
      "modelToUpload": {
        "displayName": "MODEL_NAME",
        "predictSchemata": {},
        "containerSpec": {
          "imageUri": "IMAGE_URI"
        }
      },
      "labels": {
        LABEL_NAME_1": LABEL_VALUE_1,
        LABEL_NAME_2": LABEL_VALUE_2
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/trainingPipelines"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/trainingPipelines" | Select-Object -Expand Content

The response contains information about specifications as well as the TRAININGPIPELINE\_ID .

#### Response

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/trainingPipelines/TRAININGPIPELINE_ID",
      "displayName": "TRAINING_PIPELINE_NAME",
      "input_data_config" {
        "dataset_id": "1234567891011121314"
        "gcs_destination" {
          "output_uri_prefix": "gs://BUCKET_NAME/data/20200915191342"
        }
        "annotation_schema_uri": "gs://google-cloud-aiplatform/schema/dataset/annotation/image_classification_1.0.0.yaml"
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/custom_task_1.0.0.yaml",
      "trainingTaskInputs": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": "n1-standard-4"
            },
            "replicaCount": "1",
            "pythonPackageSpec": {
              "executorImageUri": "us-docker.pkg.dev/vertex-ai/training/training-tf-cpu.2-1:latest",
              "packageUris": [
                "gs://BUCKET_NAME/training/hello-custom-training-1.0.tar.gz"
              ],
              "pythonModule": "trainer.task",
              "args": [
                "--model-dir=gs://BUCKET_NAME/output/"
              ]
            }
          }
        ]
      },
      "trainingTaskMetadata": {
        "backingCustomJob": "projects/PROJECT_ID/locations/LOCATION_ID/customJobs/CUSTOM_JOB_ID"
      },
      "modelToUpload": {
        "displayName": "MODEL_NAME",
        "predictSchemata": {},
        "containerSpec": {
          "imageUri": "us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-1:latest"
        }
      },
      "state": "PIPELINE_STATE_PENDING",
      "createTime": "2020-09-15T19:09:54.342080Z",
      "startTime": "2020-09-15T19:13:42.991045Z",
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.cloud.aiplatform.v1.Model;
    import com.google.cloud.aiplatform.v1.ModelContainerSpec;
    import com.google.cloud.aiplatform.v1.PipelineServiceClient;
    import com.google.cloud.aiplatform.v1.PipelineServiceSettings;
    import com.google.cloud.aiplatform.v1.TrainingPipeline;
    import com.google.gson.JsonArray;
    import com.google.gson.JsonObject;
    import com.google.protobuf.Value;
    import com.google.protobuf.util.JsonFormat;
    import java.io.IOException;
    
    public class CreateTrainingPipelineCustomJobSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "PROJECT";
        String displayName = "DISPLAY_NAME";
        String modelDisplayName = "MODEL_DISPLAY_NAME";
        String containerImageUri = "CONTAINER_IMAGE_URI";
        String baseOutputDirectoryPrefix = "BASE_OUTPUT_DIRECTORY_PREFIX";
        createTrainingPipelineCustomJobSample(
            project, displayName, modelDisplayName, containerImageUri, baseOutputDirectoryPrefix);
      }
    
      static void createTrainingPipelineCustomJobSample(
          String project,
          String displayName,
          String modelDisplayName,
          String containerImageUri,
          String baseOutputDirectoryPrefix)
          throws IOException {
        PipelineServiceSettings settings =
            PipelineServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
        String location = "us-central1";
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (PipelineServiceClient client = PipelineServiceClient.create(settings)) {
          JsonObject jsonMachineSpec = new JsonObject();
          jsonMachineSpec.addProperty("machineType", "n1-standard-4");
    
          // A working docker image can be found at
          // gs://cloud-samples-data/ai-platform/mnist_tfrecord/custom_job
          // This sample image accepts a set of arguments including model_dir.
          JsonObject jsonContainerSpec = new JsonObject();
          jsonContainerSpec.addProperty("imageUri", containerImageUri);
          JsonArray jsonArgs = new JsonArray();
          jsonArgs.add("--model_dir=$(AIP_MODEL_DIR)");
          jsonContainerSpec.add("args", jsonArgs);
    
          JsonObject jsonJsonWorkerPoolSpec0 = new JsonObject();
          jsonJsonWorkerPoolSpec0.addProperty("replicaCount", 1);
          jsonJsonWorkerPoolSpec0.add("machineSpec", jsonMachineSpec);
          jsonJsonWorkerPoolSpec0.add("containerSpec", jsonContainerSpec);
    
          JsonArray jsonWorkerPoolSpecs = new JsonArray();
          jsonWorkerPoolSpecs.add(jsonJsonWorkerPoolSpec0);
    
          JsonObject jsonBaseOutputDirectory = new JsonObject();
          // The GCS location for outputs must be accessible by the project's AI Platform
          // service account.
          jsonBaseOutputDirectory.addProperty("output_uri_prefix", baseOutputDirectoryPrefix);
    
          JsonObject jsonTrainingTaskInputs = new JsonObject();
          jsonTrainingTaskInputs.add("workerPoolSpecs", jsonWorkerPoolSpecs);
          jsonTrainingTaskInputs.add("baseOutputDirectory", jsonBaseOutputDirectory);
    
          Value.Builder trainingTaskInputsBuilder = Value.newBuilder();
          JsonFormat.parser().merge(jsonTrainingTaskInputs.toString(), trainingTaskInputsBuilder);
          Value trainingTaskInputs = trainingTaskInputsBuilder.build();
          String trainingTaskDefinition =
              "gs://google-cloud-aiplatform/schema/trainingjob/definition/custom_task_1.0.0.yaml";
          String imageUri = "gcr.io/cloud-aiplatform/prediction/tf-cpu.1-15:latest";
          ModelContainerSpec containerSpec =
              ModelContainerSpec.newBuilder().setImageUri(imageUri).build();
          Model modelToUpload =
              Model.newBuilder()
                  .setDisplayName(modelDisplayName)
                  .setContainerSpec(containerSpec)
                  .build();
          TrainingPipeline trainingPipeline =
              TrainingPipeline.newBuilder()
                  .setDisplayName(displayName)
                  .setTrainingTaskDefinition(trainingTaskDefinition)
                  .setTrainingTaskInputs(trainingTaskInputs)
                  .setModelToUpload(modelToUpload)
                  .build();
          LocationName parent = LocationName.of(project, location);
          TrainingPipeline response = client.createTrainingPipeline(parent, trainingPipeline);
          System.out.format("response: %s\n", response);
          System.out.format("Name: %s\n", response.getName());
        }
      }
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

The following examples show how to use the [Agent Platform SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) to create a serverless training pipeline. Choose whether you plan to use a [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) or a [prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) for training:

### Prebuilt container

When you use the Agent Platform SDK for Python to create a training pipeline that runs your Python code in a prebuilt container, you can provide your training code in one of the following ways:

  - Specify the [URI of a Python source distribution package in Cloud Storage.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container)
    
    (This option is also available when you create a training pipeline without using the Agent Platform SDK for Python.)

  - Specify the path to a Python script on your local machine. Before it creates a training pipeline, the Agent Platform SDK for Python packages your script as a source distribution and uploads it to the Cloud Storage bucket of your choice.
    
    (This option is only available when you use the Agent Platform SDK for Python.)

To see a code sample for each of these options, select the corresponding tab:

### Package

The following sample uses the [`CustomPythonPackageTrainingJob` class](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob) .

    def create_training_pipeline_custom_package_job_sample(
        project: str,
        location: str,
        staging_bucket: str,
        display_name: str,
        python_package_gcs_uri: str,
        python_module_name: str,
        container_uri: str,
        model_serving_container_image_uri: str,
        dataset_id: Optional[str] = None,
        model_display_name: Optional[str] = None,
        args: Optional[List[Union[str, float, int]]] = None,
        replica_count: int = 1,
        machine_type: str = "n1-standard-4",
        accelerator_type: str = "ACCELERATOR_TYPE_UNSPECIFIED",
        accelerator_count: int = 0,
        training_fraction_split: float = 0.8,
        validation_fraction_split: float = 0.1,
        test_fraction_split: float = 0.1,
        sync: bool = True,
        tensorboard_resource_name: Optional[str] = None,
        service_account: Optional[str] = None,
    ):
        aiplatform.init(project=project, location=location, staging_bucket=staging_bucket)
    
        job = aiplatform.CustomPythonPackageTrainingJob(
            display_name=display_name,
            python_package_gcs_uri=python_package_gcs_uri,
            python_module_name=python_module_name,
            container_uri=container_uri,
            model_serving_container_image_uri=model_serving_container_image_uri,
        )
    
        # This example uses an ImageDataset, but you can use another type
        dataset = aiplatform.ImageDataset(dataset_id) if dataset_id else None
    
        model = job.run(
            dataset=dataset,
            model_display_name=model_display_name,
            args=args,
            replica_count=replica_count,
            machine_type=machine_type,
            accelerator_type=accelerator_type,
            accelerator_count=accelerator_count,
            training_fraction_split=training_fraction_split,
            validation_fraction_split=validation_fraction_split,
            test_fraction_split=test_fraction_split,
            sync=sync,
            tensorboard=tensorboard_resource_name,
            service_account=service_account,
        )
    
        model.wait()
    
        print(model.display_name)
        print(model.resource_name)
        print(model.uri)
        return model

### Script

The following sample uses the [`CustomTrainingJob` class](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob) .

    def create_training_pipeline_custom_job_sample(
        project: str,
        location: str,
        staging_bucket: str,
        display_name: str,
        script_path: str,
        container_uri: str,
        model_serving_container_image_uri: str,
        dataset_id: Optional[str] = None,
        model_display_name: Optional[str] = None,
        args: Optional[List[Union[str, float, int]]] = None,
        replica_count: int = 0,
        machine_type: str = "n1-standard-4",
        accelerator_type: str = "ACCELERATOR_TYPE_UNSPECIFIED",
        accelerator_count: int = 0,
        training_fraction_split: float = 0.8,
        validation_fraction_split: float = 0.1,
        test_fraction_split: float = 0.1,
        sync: bool = True,
        tensorboard_resource_name: Optional[str] = None,
        service_account: Optional[str] = None,
    ):
        aiplatform.init(project=project, location=location, staging_bucket=staging_bucket)
    
        job = aiplatform.CustomTrainingJob(
            display_name=display_name,
            script_path=script_path,
            container_uri=container_uri,
            model_serving_container_image_uri=model_serving_container_image_uri,
        )
    
        # This example uses an ImageDataset, but you can use another type
        dataset = aiplatform.ImageDataset(dataset_id) if dataset_id else None
    
        model = job.run(
            dataset=dataset,
            model_display_name=model_display_name,
            args=args,
            replica_count=replica_count,
            machine_type=machine_type,
            accelerator_type=accelerator_type,
            accelerator_count=accelerator_count,
            training_fraction_split=training_fraction_split,
            validation_fraction_split=validation_fraction_split,
            test_fraction_split=test_fraction_split,
            sync=sync,
            tensorboard=tensorboard_resource_name,
            service_account=service_account,
        )
    
        model.wait()
    
        print(model.display_name)
        print(model.resource_name)
        print(model.uri)
        return model

### Custom container

The following sample uses the [`CustomContainerTrainingJob` class](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob) .

    def create_training_pipeline_custom_container_job_sample(
        project: str,
        location: str,
        staging_bucket: str,
        display_name: str,
        container_uri: str,
        model_serving_container_image_uri: str,
        dataset_id: Optional[str] = None,
        model_display_name: Optional[str] = None,
        args: Optional[List[Union[str, float, int]]] = None,
        replica_count: int = 1,
        machine_type: str = "n1-standard-4",
        accelerator_type: str = "ACCELERATOR_TYPE_UNSPECIFIED",
        accelerator_count: int = 0,
        training_fraction_split: float = 0.8,
        validation_fraction_split: float = 0.1,
        test_fraction_split: float = 0.1,
        sync: bool = True,
        tensorboard_resource_name: Optional[str] = None,
        service_account: Optional[str] = None,
    ):
        aiplatform.init(project=project, location=location, staging_bucket=staging_bucket)
    
        job = aiplatform.CustomContainerTrainingJob(
            display_name=display_name,
            container_uri=container_uri,
            model_serving_container_image_uri=model_serving_container_image_uri,
        )
    
        # This example uses an ImageDataset, but you can use another type
        dataset = aiplatform.ImageDataset(dataset_id) if dataset_id else None
    
        model = job.run(
            dataset=dataset,
            model_display_name=model_display_name,
            args=args,
            replica_count=replica_count,
            machine_type=machine_type,
            accelerator_type=accelerator_type,
            accelerator_count=accelerator_count,
            training_fraction_split=training_fraction_split,
            validation_fraction_split=validation_fraction_split,
            test_fraction_split=test_fraction_split,
            sync=sync,
            tensorboard=tensorboard_resource_name,
            service_account=service_account,
        )
    
        model.wait()
    
        print(model.display_name)
        print(model.resource_name)
        print(model.uri)
        return model

## Hyperparameter tuning job and model upload

This training pipeline encapsulates a hyperparameter tuning job with an added convenience step that makes it easier to deploy your model to Agent Platform after training. This training pipeline does two main things:

1.  The training pipeline creates a *hyperparameter tuning job* resource. The hyperparameter tuning job creates multiple trials. For each trial, a custom job runs your training application using the computing resources and hyperparameters that you specify.

2.  After the hyperparameter tuning job completes, the training pipeline finds the model artifacts from the best trial, within the output directory ( [`baseOutputDirectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#FIELDS.base_output_directory) ) you specified for your Cloud Storage bucket. The training pipeline uses these artifacts to create a *model* resource, which sets you up for [model deployment](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api) .

For this training pipeline, you must specify a [`baseOutputDirectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#FIELDS.base_output_directory) where Agent Platform searches for the model artifacts from the best trial.

[Hyperparameter tuning jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) have additional settings to configure. Learn more about the settings for a [`HyperparameterTuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs) .

### REST

Use the following code sample to create a training pipeline using the [`create` method of the `trainingPipeline` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/create) .

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your project's region.
  - PROJECT\_ID : Your project ID.
  - TRAINING\_PIPELINE\_NAME : Required. A display name for the trainingPipeline.
  - If your training application uses an Agent Platform dataset, specify the following:
      - DATASET\_ID : The ID of the dataset.
      - ANNOTATIONS\_FILTER : Filters the dataset by the annotations that you specify.
      - ANNOTATION\_SCHEMA\_URI : Filters the dataset by the specified annotation schema URI.
      - Use one of the following options to specify how data items are split into training, validation, and test sets.
          - To split the dataset based on fractions defining the size of each set, specify the following:
              - TRAINING\_FRACTION : The fraction of the dataset to use to train your model.
              - VALIDATION\_FRACTION : The fraction of the dataset to use to validate your model.
              - TEST\_FRACTION : The fraction of the dataset to use to evaluate your model.
          - To split the dataset based on filters, specify the following:
              - TRAINING\_FILTER : Filters the dataset to data items to use for training your model.
              - VALIDATION\_FILTER : Filters the dataset to data items to use for validating your model.
              - TEST\_FILTER : Filters the dataset to data items to use for evaluating your model.
          - To use a predefined split, specify the following:
              - PREDEFINED\_SPLIT\_KEY : The name of the column to use to split the dataset. Acceptable values in this column include \`training\`, \`validation\`, and \`test\`.
          - To split the dataset based on the timestamp on the dataitems, specify the following:
              - TIMESTAMP\_TRAINING\_FRACTION : The fraction of the dataset to use to train your model.
              - TIMESTAMP\_VALIDATION\_FRACTION : The fraction of the dataset to use to validate your model.
              - TIMESTAMP\_TEST\_FRACTION : The fraction of the dataset to use to evaluate your model.
              - TIMESTAMP\_SPLIT\_KEY : The name of the timestamp column to use to split the dataset.
      - OUTPUT\_URI\_PREFIX : The Cloud Storage location where Agent Platform exports your training dataset, after it has been split into training, validation, and test sets.
  - Specify your hyperparameter tuning job:
      - Specify your metrics:
          - METRIC\_ID : The name of this metric.
          - METRIC\_GOAL : The goal of this metric. Can be `MAXIMIZE` or `MINIMIZE` .
      - Specify your hyperparameters:
          - PARAMETER\_ID : The name of this hyperparameter.
          - PARAMETER\_SCALE : (Optional.) How the parameter should be scaled. Leave unset for CATEGORICAL parameters. Can be `UNIT_LINEAR_SCALE` , `UNIT_LOG_SCALE` , `UNIT_REVERSE_LOG_SCALE` , or `SCALE_TYPE_UNSPECIFIED`
          - If this hyperparameter's type is DOUBLE, specify the minimum ( DOUBLE\_MIN\_VALUE ) and maximum ( DOUBLE\_MAX\_VALUE ) values for this hyperparameter.
          - If this hyperparameter's type is INTEGER, specify the minimum ( INTEGER\_MIN\_VALUE ) and maximum ( INTEGER\_MAX\_VALUE ) values for this hyperparameter.
          - If this hyperparameter's type is CATEGORICAL, specify the acceptable values ( CATEGORICAL\_VALUES ) as an array of strings.
          - If this hyperparameter's type is DISCRETE, specify the acceptable values ( DISCRETE\_VALUES ) as an array of numbers.
      - ALGORITHM : (Optional.) The search algorithm to use in this hyperparameter tuning job. Can be `ALGORITHM_UNSPECIFIED` , `GRID_SEARCH` , or `RANDOM_SEARCH` .
      - MAX\_TRIAL\_COUNT : The maximum number of trials to run in this job.
      - PARALLEL\_TRIAL\_COUNT : The maximum number of trials that can run in parallel.
      - MAX\_FAILED\_TRIAL\_COUNT : The number of jobs that can fail before the hyperparameter tuning job fails.
      - Define the trial custom training job:
          - MACHINE\_TYPE : The type of the machine. Refer to the [available machine types for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) .
          - ACCELERATOR\_TYPE : (Optional.) The type of accelerator to attach to each trial.
          - ACCELERATOR\_COUNT : (Optional.) The number of accelerators to attach to each trial.
          - REPLICA\_COUNT : The number of worker replicas to use for each trial.
          - If your training application runs in a custom container, specify the following:
              - CUSTOM\_CONTAINER\_IMAGE\_URI : The URI of a container image in Artifact Registry or Docker Hub that is to be run on each worker replica.
              - CUSTOM\_CONTAINER\_COMMAND : (Optional.) The command to be invoked when the container is started. This command overrides the container's default entrypoint.
              - CUSTOM\_CONTAINER\_ARGS : (Optional.) The arguments to be passed when starting the container.
          - If your training application is a Python package that runs in a prebuilt container, specify the following:
              - PYTHON\_PACKAGE\_EXECUTOR\_IMAGE\_URI : The URI of the container image that runs the provided Python package. Refer to the [available prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) .
              - PYTHON\_PACKAGE\_URIS : The Cloud Storage location of the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100.
              - PYTHON\_MODULE : The Python module name to run after installing the packages.
              - PYTHON\_PACKAGE\_ARGS : (Optional.) Command-line arguments to be passed to the Python module.
      - Learn about [job scheduling options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#Scheduling) .
      - TIMEOUT : (Optional.) The maximum running time for each trial.
      - Specify the LABEL\_NAME and LABEL\_VALUE for any labels that you want to apply to this hyperparameter tuning job.
  - MODEL\_NAME : A display name for the model uploaded (created) by the TrainingPipeline.
  - MODEL\_DESCRIPTION : Optional. A description for the model.
  - PREDICTION\_IMAGE\_URI : Required. Specify one of the two following options:
      - The image URI of the [prebuilt container to use for prediction](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) , such as "tf2-cpu.2-1:latest".
      - The image URI of your own [custom container to use for prediction](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-custom-container) .
  - modelToUpload.labels : Optional. Any set of key-value pairs to organize your models. For example:
      - "env": "prod"
      - "tier": "backend"
  - Specify the LABEL\_NAME and LABEL\_VALUE for any labels that you want to apply to this training pipeline.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/trainingPipelines

Request JSON body:

    {
      "displayName": "TRAINING_PIPELINE_NAME",
      "inputDataConfig": {
        "datasetId": DATASET_ID,
        "annotationsFilter": ANNOTATIONS_FILTER,
        "annotationSchemaUri": ANNOTATION_SCHEMA_URI,
    
        // Union field split can be only one of the following:
        "fractionSplit": {
          "trainingFraction": TRAINING_FRACTION,
          "validationFraction": VALIDATION_FRACTION,
          "testFraction": TEST_FRACTION
        },
        "filterSplit": {
          "trainingFilter": TRAINING_FILTER,
          "validationFilter": VALIDATION_FILTER,
          "testFilter": TEST_FILTER
        },
        "predefinedSplit": {
          "key": PREDEFINED_SPLIT_KEY
        },
        "timestampSplit": {
          "trainingFraction": TIMESTAMP_TRAINING_FRACTION,
          "validationFraction": TIMESTAMP_VALIDATION_FRACTION,
          "testFraction": TIMESTAMP_TEST_FRACTION,
          "key": TIMESTAMP_SPLIT_KEY
        }
        // End of list of possible types for union field split.
        "gcsDestination": {
          "outputUriPrefix": OUTPUT_URI_PREFIX
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/hyperparameter_tuning_task_1.0.0.yaml",
      "trainingTaskInputs": {
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
          }
        },
        "labels": {
          LABEL_NAME_1": LABEL_VALUE_1,
          LABEL_NAME_2": LABEL_VALUE_2
        }
      },
      "modelToUpload": {
        "displayName": "MODEL_NAME",
        "description": "MODEL_DESCRIPTION",
        "predictSchemata": {},
        "containerSpec": {
          "imageUri": "PREDICTION_IMAGE_URI"
        }
      },
      "labels": {
        LABEL_NAME_1": LABEL_VALUE_1,
        LABEL_NAME_2": LABEL_VALUE_2
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/trainingPipelines"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/trainingPipelines" | Select-Object -Expand Content

The response contains information about specifications as well as the TRAININGPIPELINE\_ID .

#### Response

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/trainingPipelines/TRAININGPIPELINE_ID",
      "displayName": "TRAINING_PIPELINE_NAME",
      "input_data_config" {
        "dataset_id": "1234567891011121314"
        "gcs_destination" {
          "output_uri_prefix": "gs://BUCKET_NAME/data/20200915191342"
        }
        "annotation_schema_uri": "gs://google-cloud-aiplatform/schema/dataset/annotation/image_classification_1.0.0.yaml"
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/custom_task_1.0.0.yaml",
      "trainingTaskInputs": {
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
      },
      "state": "PIPELINE_STATE_PENDING",
      "createTime": "2020-09-15T19:09:54.342080Z",
      "startTime": "2020-09-15T19:13:42.991045Z",
    }

## Monitor training

To view training logs, do the following:

1.  In the Google Cloud console, in the Agent Platform section, go to the **Training** page.

2.  Click the name of your job to go to the custom job page.

3.  Click **View logs** .

You can also [use an interactive shell](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/monitor-debug-interactive-shell) to inspect your training containers while the training pipeline is running.

## View your trained model

When the serverless training pipeline completes, you can find the trained model in the Google Cloud console, in the Agent Platform section, on the **Models** page.

## What's next

  - Learn how to pinpoint training performance bottlenecks to train models faster and cheaper using [Cloud Profiler](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler) .
  - [Deploy your model to an endpoint](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api) .
  - Create a [hyperparameter tuning job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) .
  - Learn how to [schedule serverless training jobs based on resource availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/schedule-jobs-dws) .
