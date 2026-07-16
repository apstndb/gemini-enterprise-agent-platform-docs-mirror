---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job
title: Create a serverless training job
description: Create a Gemini Enterprise Agent Platform serverless training job.
data_source: docs.cloud.google.com
---

Serverless training jobs ( `CustomJob` resources in the Agent Platform API) are the basic way to run your custom machine learning (ML) training code in Gemini Enterprise Agent Platform.

## Before you submit a job

Before you create a `CustomJob` in Agent Platform, you must create a Python training application or a custom container image to define the training code and dependencies you want to run on Agent Platform.

We recommend that you use the Google Cloud CLI's *autopackaging* feature, described in a [later section of this guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#create) , to create a Docker container image from code on your local machine, push this container image to Artifact Registry, and create a `CustomJob` , all with a single command.

Otherwise, you must manually create a [Python training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) or a [custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .

If you're not sure which of these options to choose, refer to the [training code requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) to learn more.

## What a custom job includes

When you create a *custom job* , you specify settings that Agent Platform needs to run your training code, including:

  - One worker pool for single-node training ( [`WorkerPoolSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#workerpoolspec) ), or multiple worker pools for distributed training
  - Optional settings for configuring job scheduling ( [`Scheduling`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#scheduling) ), [setting certain environment variables for your training code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#environment-variables) , [using a custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) , and [using VPC Network Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering)

Within the worker pool(s), you can specify the following settings:

  - [Machine types and accelerators](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute)
  - [Configuration of what type of training code the worker pool runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings) : either a Python training application ( [`PythonPackageSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#pythonpackagespec) ) or a custom container ( [`ContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#containerspec) )

You can also configure custom jobs to run on a persistent resource instead of creating new compute resources during job startup. To learn more about a persistent resource, see [Overview of persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-overview) .

## Configure distributed training

You can configure a `CustomJob` for distributed training by specifying multiple worker pools.

Most examples on this page show single-replica training jobs with one worker pool. To modify them for distributed training:

  - Use your first worker pool to configure your primary replica, and set the replica count to 1.
  - [Add more worker pools](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training#additional-worker-pools) to configure worker replicas, parameter server replicas, or evaluator replicas, if your machine learning framework supports these additional cluster tasks for distributed training.

Learn more about [using distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) .

## Create a `CustomJob`

To create a `CustomJob` , follow the instructions in one of the following tabs, depending on what tool you want to use. If you use the gcloud CLI, you can use a single command to autopackage training code on your local machine into a Docker container image, push the container image to Artifact Registry, and create a `CustomJob` . Other options assume you have [already created a Python training application or custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#before) .

### gcloud

The following examples use the [`gcloud ai custom-jobs create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/create) .

If your training code is on your local computer, we recommend that you follow the [With autopackaging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#autopackaging) section. Alternatively, if you have [already created a Python training application or custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#before) , then skip ahead to the [Without autopackaging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#without-autopackaging) section.

### With autopackaging

If you have training code on your local computer, you can use a single command to do the following:

  - Build a custom Docker image based on your code.
  - Push the image to Artifact Registry.
  - Start a `CustomJob` based on the image.

The result is similar to creating a `CustomJob` using any other custom container; you can use this version of the command if it is convenient for your workflow.

#### Before you begin

Since this version of the command builds and pushes a Docker image, you must perform the following configuration on your local computer:

1.  [Install Docker Engine.](https://docs.docker.com/engine/install/)

2.  If you are using Linux, [configure Docker so you can run it without `sudo`](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user) .

3.  Enable the Artifact Registry API.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

4.  [Configure authentication for Docker](https://docs.cloud.google.com/artifact-registry/docs/docker/store-docker-container-images#auth) , so that you can push Docker images to Artifact Registry:
    
        gcloud auth configure-docker

#### Build and push the Docker image, and create a `CustomJob`

The following command builds a Docker image based on a prebuilt training container image and your local Python code, pushes the image to Artifact Registry, and creates a `CustomJob` .

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --worker-pool-spec=machine-type=MACHINE_TYPE,replica-count=REPLICA_COUNT,executor-image-uri=EXECUTOR_IMAGE_URI,local-package-path=WORKING_DIRECTORY,script=SCRIPT_PATH

Replace the following:

  - LOCATION : The region where the container or Python package will be run.

  - JOB\_NAME : Required. A display name for the `CustomJob` .

  - MACHINE\_TYPE : The type of the machine. Refer to [available machine types for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) .

  - REPLICA\_COUNT : The number of worker replicas to use. In most cases, set this to `1` for your [first worker pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#configure_distributed_training) .

  - EXECUTOR\_IMAGE\_URI : The URI of the container image that runs the provided code. Refer to the [available prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) .
    
    This image acts as the base image for the new Docker image that you are building with this command.

  - WORKING\_DIRECTORY : A directory in your local file system containing the entry point script that runs your training code (see the following list item).
    
    You can use the parent directory of the script, or a higher-level directory. You might want to use a higher-level directory in order to specify a fully-qualified Python module name (see the following list item). You might also want to use a higher-level directory if it contains a `requirements.txt` or `setup.py` file. To learn more, see [Install dependencies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#install-dependencies) .
    
    Note that even if you specify a higher-level directory, this command only copies the parent directory of your entry point script to the Docker image.

  - SCRIPT\_PATH : The path, relative to WORKING\_DIRECTORY on your local file system, to the script that is the entry point for your training code. This can be a Python script (ending in `.py` ) or a Bash script.
    
    For example, if you want to run `/hello-world/trainer/task.py` and WORKING\_DIRECTORY is `/hello-world` , then use `trainer/task.py` for this value.
    
    ##### Use `python-module` instead of `script`
    
    You can optionally replace ` script= SCRIPT_PATH  ` with ` python-module= PYTHON_MODULE  ` to specify the name of a Python module in WORKING\_DIRECTORY to run as the entry point for training. For example, instead of `script=trainer/task.py` , you might specify `python-module=trainer.task` .
    
    In this case, the resulting Docker container [loads your code as a module](https://docs.python.org/3/using/cmdline.html#cmdoption-m) rather than as a script. You likely want to use this option if your entry point script imports other Python modules in WORKING\_DIRECTORY .

#### Install dependencies

When using autopackaging, you can install Python dependencies in your container in the same ways that are available when you use the gcloud CLI's `local-run` command. To learn about the various ways to install Python dependencies, read the [Install dependencies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containerize-run-code-local#dependencies) section of the guide to the `local-run` command.

The syntax for specifying dependencies differs slightly when you use autopackaging compared to when you use the `local-run` command. Instead of using command-line flags to specify dependencies, you must use options in the value of the `--worker-pool-spec` flag. Additionally, values *within* these options must be separated by semicolons rather than commas. Specifically, the syntax:

  - Instead of the `local-run` command's `--local-package-path` flag, use the `local-package-path` option in the value of the `--worker-pool-spec` flag. If the working directory that you specify with this option contains a `requirements.txt` or `setup.py` file, autopackaging installs dependencies based on this file.
    
    The preceding example demonstrates this syntax.

  - (Optional) Instead of the `--requirements` flag, use the `requirements` option in the value of the `--worker-pool-spec` flag. Instead of separating PyPI dependencies with commas, use semicolons.

  - (Optional) Instead of the `--extra-packages` flag, use the `extra-packages` option in the value of the `--worker-pool-spec` flag. Instead of separating local dependencies with commas, use semicolons.

  - (Optional) Instead of the `--extra-dirs` flag, use the `extra-dirs` option in the value of the `--worker-pool-spec` flag. Instead of separating directory paths with commas, use semicolons.

The following example shows how you might install dependencies using all the optional techniques. (You can specify any subset of them.) To demonstrate the semicolon syntax, the example specifies two values for each option. To reduce the length of the example, other `--worker-pool-spec` options are replaced with `[...]` .

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --worker-pool-spec=[...],requirements=PYPI_DEP_1;PYPI_DEP_2,extra-packages=LOCAL_DEP_1;LOCAL_DEP_2,extra-dirs=EXTRA_DIR_1;EXTRA_DIR_2

To learn about appropriate values for these placeholders, see "Install dependencies" in the guide to the `local-run` command.

### Without autopackaging

If you don't use autopackaging, you can create a `CustomJob` with a command similar to one of the following. Depending on whether you have [created a Python training application or a custom container image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#before) , choose one of the following tabs:

### Python training app

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --python-package-uris=PYTHON_PACKAGE_URIS \
      --worker-pool-spec=machine-type=MACHINE_TYPE,replica-count=REPLICA_COUNT,executor-image-uri=EXECUTOR_IMAGE_URI,python-module=PYTHON_MODULE

Replace the following:

  - LOCATION : The region where the container or Python package will be run.
  - JOB\_NAME : Required. A display name for the `CustomJob` .
  - PYTHON\_PACKAGE\_URIS : Comma-separated list of Cloud Storage URIs specifying the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100.
  - MACHINE\_TYPE : The type of the machine. Refer to [available machine types for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) .
  - REPLICA\_COUNT : The number of worker replicas to use. In most cases, set this to `1` for your [first worker pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#configure_distributed_training) .
  - EXECUTOR\_IMAGE\_URI : The URI of the container image that runs the provided code. Refer to the [available prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) .
  - PYTHON\_MODULE : The Python module name to run after installing the packages.

### Custom container image

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --worker-pool-spec=machine-type=MACHINE_TYPE,replica-count=REPLICA_COUNT,container-image-uri=CUSTOM_CONTAINER_IMAGE_URI

Replace the following:

  - LOCATION : The region where the container or Python package will be run.
  - JOB\_NAME : Required. A display name for the `CustomJob` .
  - MACHINE\_TYPE : The type of the machine. Refer to [available machine types for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) .
  - REPLICA\_COUNT : The number of worker replicas to use. In most cases, set this to `1` for your [first worker pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#configure_distributed_training) .
  - CUSTOM\_CONTAINER\_IMAGE\_URI : The URI of a container image in Artifact Registry or Docker Hub that is to be run on each worker replica.

### Distributed training

To perform [distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings) , you configure your job with multiple replicas. For example, when using the Google Cloud CLI, you can specify the `--worker-pool-spec` flag multiple times.

If you are using autopackaging, then you must only specify `local-package-path` , `script` , and other options related to autopackaging in the first worker pool. Omit fields related to your training code in subsequent worker pools, which will all use the same training container built by autopackaging.

For example, the following command adapts an earlier autopackaging example to use a second worker pool:

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --worker-pool-spec=machine-type=MACHINE_TYPE,replica-count=REPLICA_COUNT,executor-image-uri=EXECUTOR_IMAGE_URI,local-package-path=WORKING_DIRECTORY,script=SCRIPT_PATH \
      --worker-pool-spec=machine-type=SECOND_POOL_MACHINE_TYPE,replica-count=SECOND_POOL_REPLICA_COUNT

If you aren't using autopackaging, then specify each worker pool completely and independently; do not omit any fields.

The following commands adapt earlier examples to use a second worker pool:

### Python training app

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --python-package-uris=PYTHON_PACKAGE_URIS \
      --worker-pool-spec=machine-type=MACHINE_TYPE,replica-count=REPLICA_COUNT,executor-image-uri=EXECUTOR_IMAGE_URI,python-module=PYTHON_MODULE \
      --worker-pool-spec=machine-type=SECOND_POOL_MACHINE_TYPE,replica-count=SECOND_POOL_REPLICA_COUNT,executor-image-uri=SECOND_POOL_EXECUTOR_IMAGE_URI,python-module=SECOND_POOL_PYTHON_MODULE

> **Note:** In this case, each worker pool uses the same Python package URIs.

### Custom container image

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --worker-pool-spec=machine-type=MACHINE_TYPE,replica-count=REPLICA_COUNT,container-image-uri=CUSTOM_CONTAINER_IMAGE_URI \
      --worker-pool-spec=machine-type=SECOND_POOL_MACHINE_TYPE,replica-count=SECOND_POOL_REPLICA_COUNT,container-image-uri=SECOND_POOL_CUSTOM_CONTAINER_IMAGE_URI

### Advanced configuration

If you want to specify configuration options that are not available in the preceding examples, you can use the `--config` flag to specify the path to a `config.yaml` file in your local environment that contains the fields of [`CustomJobSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec) . For example:

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --config=config.yaml

See an [example of a `config.yaml` file](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/create#--config) .

### Console

In the Google Cloud console, you can't create a `CustomJob` resource directly. However, you can create a `TrainingPipeline` resource that creates a `CustomJob` .

The following instructions describe how to create a `TrainingPipeline` that creates a `CustomJob` and doesn't do anything else. If you want to use additional `TrainingPipeline` features, like training with a managed dataset or creating a `Model` resource at the end of training, read [Creating training pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) .

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

6.  On the **Hyperparameter tuning** step, make sure that the **Enable hyperparameter tuning** checkbox is not selected. Click **Continue** .

7.  On the **Compute and pricing** step, specify the following settings:
    
    1.  In the **Region** drop-down list, select a " [region that supports custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations) "
    
    2.  In the **Worker pool 0** section, specify [compute resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) to use for training.
        
        If you specify accelerators, [make sure the type of accelerator that you choose is available in your selected region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#region_considerations) .
        
        If you want to perform [distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) , then click **Add more worker pools** and specify an additional set of compute resources for each additional worker pool that you want.
    
    Click **Continue** .

8.  On the **Prediction container** step, select **No prediction container** .

9.  Click **Start training** to start the serverless training pipeline.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the container or Python package will be run.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - JOB\_NAME : Required. A display name for the `CustomJob` .
  - Define the custom training job:
      - MACHINE\_TYPE : The type of the machine. Refer to [available machine types for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) .
      - ACCELERATOR\_TYPE : (Optional.) The type of accelerator to attach to the job.
      - ACCELERATOR\_COUNT : (Optional.) The number of accelerators to attach to the job.
      - DISK\_TYPE : (Optional.) The type of the boot disk to use for the job, either `pd-standard` (default) or `pd-ssd` . [Learn more about disk types.](https://docs.cloud.google.com/compute/docs/disks#disk-types)
      - DISK\_SIZE : (Optional.) The size in GB of the boot disk to use for the job. The default value is 100.
      - REPLICA\_COUNT : The number of worker replicas to use. In most cases, set this to `1` for your [first worker pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#configure_distributed_training) .
      - If your training application runs in a custom container, specify the following:
          - CUSTOM\_CONTAINER\_IMAGE\_URI : The URI of a container image in Artifact Registry or Docker Hub that is to be run on each worker replica. /li\>
          - CUSTOM\_CONTAINER\_COMMAND : (Optional.) The command to be invoked when the container is started. This command overrides the container's default entrypoint.
          - CUSTOM\_CONTAINER\_ARGS : (Optional.) The arguments to be passed when starting the container.
      - If your training application is a Python package that runs in a prebuilt container, specify the following:
          - EXECUTOR\_IMAGE\_URI : The URI of the container image that runs the provided code. Refer to the [available prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) .
          - PYTHON\_PACKAGE\_URIS : Comma-separated list of Cloud Storage URIs specifying the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100.
          - PYTHON\_MODULE : The Python module name to run after installing the packages.
          - PYTHON\_PACKAGE\_ARGS : (Optional.) Command-line arguments to be passed to the Python module.
      - Learn about [job scheduling options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#Scheduling) .
      - TIMEOUT : (Optional.) The maximum running time for the job.
  - Specify the LABEL\_NAME and LABEL\_VALUE for any labels that you want to apply to this custom job.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs

Request JSON body:

    {
      "displayName": "JOB_NAME",
      "jobSpec": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": MACHINE_TYPE,
              "acceleratorType": ACCELERATOR_TYPE,
              "acceleratorCount": ACCELERATOR_COUNT
            },
            "replicaCount": REPLICA_COUNT,
            "diskSpec": {
              "bootDiskType": DISK_TYPE,
              "bootDiskSizeGb": DISK_SIZE
            },
    
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
              "executorImageUri": EXECUTOR_IMAGE_URI,
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
          // Specify one workerPoolSpec for single replica training, or multiple workerPoolSpecs
          // for distributed training.
        ],
        "scheduling": {
          "timeout": TIMEOUT
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs" | Select-Object -Expand Content

The response contains information about specifications as well as the JOB\_ID .

#### Response

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/customJobs/JOB_ID",
      "displayName": "JOB_NAME",
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
      "state": "JOB_STATE_PENDING",
      "createTime": "2020-09-15T19:09:54.342080Z",
      "startTime": "2020-09-15T19:13:42.991045Z",
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.AcceleratorType;
    import com.google.cloud.aiplatform.v1.ContainerSpec;
    import com.google.cloud.aiplatform.v1.CustomJob;
    import com.google.cloud.aiplatform.v1.CustomJobSpec;
    import com.google.cloud.aiplatform.v1.JobServiceClient;
    import com.google.cloud.aiplatform.v1.JobServiceSettings;
    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.cloud.aiplatform.v1.MachineSpec;
    import com.google.cloud.aiplatform.v1.WorkerPoolSpec;
    import java.io.IOException;
    
    // Create a custom job to run machine learning training code in Vertex AI
    public class CreateCustomJobSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "PROJECT";
        String displayName = "DISPLAY_NAME";
    
        // Vertex AI runs your training application in a Docker container image. A Docker container
        // image is a self-contained software package that includes code and all dependencies. Learn
        // more about preparing your training application at
        // https://cloud.google.com/vertex-ai/docs/training/overview#prepare_your_training_application
        String containerImageUri = "CONTAINER_IMAGE_URI";
        createCustomJobSample(project, displayName, containerImageUri);
      }
    
      static void createCustomJobSample(String project, String displayName, String containerImageUri)
          throws IOException {
        JobServiceSettings settings =
            JobServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
        String location = "us-central1";
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests.
        try (JobServiceClient client = JobServiceClient.create(settings)) {
          MachineSpec machineSpec =
              MachineSpec.newBuilder()
                  .setMachineType("n1-standard-4")
                  .setAcceleratorType(AcceleratorType.NVIDIA_TESLA_T4)
                  .setAcceleratorCount(1)
                  .build();
    
          ContainerSpec containerSpec =
              ContainerSpec.newBuilder().setImageUri(containerImageUri).build();
    
          WorkerPoolSpec workerPoolSpec =
              WorkerPoolSpec.newBuilder()
                  .setMachineSpec(machineSpec)
                  .setReplicaCount(1)
                  .setContainerSpec(containerSpec)
                  .build();
    
          CustomJobSpec customJobSpecJobSpec =
              CustomJobSpec.newBuilder().addWorkerPoolSpecs(workerPoolSpec).build();
    
          CustomJob customJob =
              CustomJob.newBuilder()
                  .setDisplayName(displayName)
                  .setJobSpec(customJobSpecJobSpec)
                  .build();
          LocationName parent = LocationName.of(project, location);
          CustomJob response = client.createCustomJob(parent, customJob);
          System.out.format("response: %s\n", response);
          System.out.format("Name: %s\n", response.getName());
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
     * (Not necessary if passing values as arguments)
     */
    
    // const customJobDisplayName = 'YOUR_CUSTOM_JOB_DISPLAY_NAME';
    // const containerImageUri = 'YOUR_CONTAINER_IMAGE_URI';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    
    // Imports the Google Cloud Job Service Client library
    const {JobServiceClient} = require('@google-cloud/aiplatform');
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const jobServiceClient = new JobServiceClient(clientOptions);
    
    async function createCustomJob() {
      // Configure the parent resource
      const parent = `projects/${project}/locations/${location}`;
      const customJob = {
        displayName: customJobDisplayName,
        jobSpec: {
          workerPoolSpecs: [
            {
              machineSpec: {
                machineType: 'n1-standard-4',
                acceleratorType: 'NVIDIA_TESLA_T4',
                acceleratorCount: 1,
              },
              replicaCount: 1,
              containerSpec: {
                imageUri: containerImageUri,
                command: [],
                args: [],
              },
            },
          ],
        },
      };
      const request = {parent, customJob};
    
      // Create custom job request
      const [response] = await jobServiceClient.createCustomJob(request);
    
      console.log('Create custom job response:\n', JSON.stringify(response));
    }
    createCustomJob();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def create_custom_job_with_experiment_autologging_sample(
        project: str,
        location: str,
        staging_bucket: str,
        display_name: str,
        script_path: str,
        container_uri: str,
        service_account: str,
        experiment: str,
        experiment_run: Optional[str] = None,
    ) -> None:
        aiplatform.init(project=project, location=location, staging_bucket=staging_bucket, experiment=experiment)
    
        job = aiplatform.CustomJob.from_local_script(
            display_name=display_name,
            script_path=script_path,
            container_uri=container_uri,
            enable_autolog=True,
        )
    
        job.run(
            service_account=service_account,
            experiment=experiment,
            experiment_run=experiment_run,
        )

## What's next

  - Learn how to pinpoint training performance bottlenecks to train models faster and cheaper using [Cloud Profiler](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler) .
  - See [Create training pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) to learn how to create training pipelines to run serverless training applications on Gemini Enterprise Agent Platform.
  - Learn how to [schedule serverless training jobs based on resource availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/schedule-jobs-dws) .
