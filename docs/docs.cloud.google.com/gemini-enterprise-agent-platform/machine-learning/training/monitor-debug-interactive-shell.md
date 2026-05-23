---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/monitor-debug-interactive-shell
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/monitor-debug-interactive-shell
title: Monitor and debug training with an interactive shell
description: Monitor and debug training with an interactive shell.
data_source: docs.cloud.google.com
---

This page shows you how to use an interactive shell to inspect the container where your training code is running. You can browse the file system and run debugging utilities in each [prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) or [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containers-overview) running on Gemini Enterprise Agent Platform.

Using an interactive shell to inspect your training container can help you debug problems with your training code or your Agent Platform configuration. For example, you can use an interactive shell to do the following:

  - Run tracing and profiling tools.
  - Analyze GPU usage.
  - Check Google Cloud permissions available to the container.

You can also use Cloud Profiler to debug model training performance for your Gemini Enterprise Agent Platform serverless trainingjobs. For details, see [Profile model training performance using Profiler](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler) .

## Before you begin

You can use an interactive shell when you perform serverless training with a `CustomJob` resource, a `HyperparameterTuningJob` resource, or a custom `TrainingPipeline` resource. As you [prepare your training code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) and [configure the serverless training resource of your choice](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-training-methods) , make sure to meet the following requirements:

  - Ensure that your training container has [`bash`](https://www.gnu.org/software/bash/) installed.
    
    All [prebuilt training containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) have `bash` installed. If you [create a custom container for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) , use a base container that includes `bash` or install `bash` in your Dockerfile.

  - Perform serverless training in a [region that supports interactive shells](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .

  - Ensure that anyone who wants to access an interactive shell has the following permissions for the Google Cloud project where serverless training is running:
    
      - `aiplatform.customJobs.create`
      - `aiplatform.customJobs.get`
      - `aiplatform.customJobs.cancel`
    
    If you initiate serverless training yourself, then you most likely already have these permissions and can access an interactive shell. However, if you want to use an interactive shell to inspect a serverless training resource created by someone else in your organization, then you might need to obtain these permissions.
    
    One way to obtain these permissions is to ask an administrator of your organization to grant you the [Agent Platform User role](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#predefined-roles) ( `roles/aiplatform.user` ).

### Requirements for advanced cases

If you are using certain advanced features, meet the following additional requirements:

  - If you [attach a custom service account](https://docs.cloud.google.com/vertex-ai/docs/general/custom-service-account#attach) to your serverless training resource, then make sure that any user who wants to access an interactive shell has the `iam.serviceAccounts.actAs` permission for the attached service account.
    
    The guide to custom service accounts notes that you must have this permission to attach a service account. You also need this permission to view an interactive shell during serverless training.
    
    For example, to create a `CustomJob` with a service account attached, you must have the `iam.serviceAccounts.actAs` permission for the service account. If one of your colleagues then wants to view an interactive shell for this `CustomJob` , they must also have the same `iam.serviceAccounts.actAs` permission.

  - If you have configured your project to [use VPC Service Controls with Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/general/vpc-service-controls) , then account for the following additional limitations:
    
      - You can't use [private IP for serverless training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-private-ip) . If you require VPC-SC with VPC Peering, there is extra setup required to use the interactive shell. Follow the instructions covered in [Ray Dashboard and Interactive Shell with VPC-SC + VPC Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/monitor-debug-interactive-shell#workaround) to configure the interactive shell setup with VPC-SC and VPC Peering in your user project.
    
      - From within an interactive shell, you can't access the public internet or Google Cloud resources outside your service perimeter.
    
      - To secure access to interactive shells, you must add `notebooks.googleapis.com` as a restricted service in your service perimeter, in addition to `aiplatform.googleapis.com` . If you only restrict `aiplatform.googleapis.com` and not `notebooks.googleapis.com` , then users can access interactive shells from machines outside the service perimeter, which reduces the security benefit of using VPC Service Controls.
        
        > **Note:** More generally, we recommend that you restrict all services when you create a service perimeter. See the [VPC Service Controls guide to creating a service perimeter](https://docs.cloud.google.com/vpc-service-controls/docs/create-service-perimeters) .

## Enable interactive shells

To enable interactive shells for a serverless training resource, set the [`enableWebAccess` API field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#FIELDS.enable_web_access) to `true` when you create a `CustomJob` , `HyperparameterTuningJob` , or custom `TrainingPipeline` .

The following examples show how to do this using several different tools:

### Console

Follow the guide to [creating a custom `TrainingPipeline` in the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline#custom-job-model-upload) . In the **Train new model** pane, when you reach the **Model details** step, do the following:

1.  Click **Advanced options** .

2.  Select the **Enable training debugging** checkbox.

Then, complete the rest of the **Train new model** workflow.

### gcloud

  - If you want to create a `CustomJob` , run the [`gcloud ai custom-jobs create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/create) , and specify the `--enable-web-access` flag on this command.

  - If you want to create a `HyperparameterTuningJob` , run the [`gcloud ai hp-tuning-jobs create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/hp-tuning-jobs/create) , and specify the `--enable-web-access` flag on this command.

To learn how to use these commands, see the guide to [creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#create) and the guide to [creating a `HyperparameterTuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning#create) .

### API

The following partial REST request bodies show where to specify the `enableWebAccess` field for each type of serverless training resource:

### CustomJob

The following example is a partial request body for the [`projects.locations.customJobs.create` API method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs/create) :

    {
      ...
      "jobSpec": {
        ...
        "enableWebAccess": true
      }
      ...
    }

For an example of sending an API request to create a `CustomJob` , see [Creating serverless training jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

### HyperparameterTuningJob

The following example is a partial request body for the [`projects.locations.hyperparameterTuningJobs.create` API method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/create) :

    {
      ...
      "trialJobSpec": {
        ...
        "enableWebAccess": true
      }
      ...
    }

For an example of sending an API request to create a `HyperparameterTuningJob` , see [Using hyperparameter tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) .

### Custom TrainingPipeline

The following examples show partial request bodies for the [`projects.locations.trainingPipelines.create` API method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/create) . Select one of the following tabs, depending on whether you are using hyperparameter tuning:

### Without hyperparameter tuning

    {
      ...
      "trainingTaskInputs": {
        ...
        "enableWebAccess": true
      }
      ...
    }

### With hyperparameter tuning

    {
      ...
      "trainingTaskInputs": {
        ...
        "trialJobSpec": {
          ...
          "enableWebAccess": true
        }
      }
      ...
    }

For an example of sending an API request to create a custom `TrainingPipeline` , see [Creating training pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) .

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

Set the `enable_web_access` parameter to `true` when you run one of the following methods:

  - If you want to create a `CustomJob` , use the [`CustomJob.run` method](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob#google_cloud_aiplatform_CustomJob_run) .

  - If you want to create a `HyperparameterTuningJob` use the [`HyperparameterTuningJob.run` method](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob#google_cloud_aiplatform_HyperparameterTuningJob_run) .

  - If you want to create a custom `TrainingPipeline` , use one of the following methods:
    
      - [`CustomTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob#google_cloud_aiplatform_CustomTrainingJob_run)
      - [`CustomContainerTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob#google_cloud_aiplatform_CustomContainerTrainingJob_run)
      - [`CustomPythonPackageTrainingJob.run`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob#google_cloud_aiplatform_CustomPythonPackageTrainingJob_run)

## Navigate to an interactive shell

After you have initiated serverless training according to the guidance in the preceding section, Agent Platform generates one or more URIs that you can use to access interactive shells. Agent Platform generates a unique URI for each [training node](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) in your job.

You can navigate to an interactive shell in one of the following ways:

  - Click a link in the Google Cloud console
  - Use the Agent Platform API to get the shell's web access URI

### Navigate from the Google Cloud console

1.  In the Google Cloud console, in the **Agent Platform** section, go to one of the following pages:
    
      - If you aren't using hyperparameter tuning, go to the **Custom jobs** page:
    
      - If you are using hyperparameter tuning, go to the **Hyperparameter tuning jobs** page:

2.  Click the name of your serverless training resource.
    
    If you created a `TrainingPipeline` for serverless training, click the name of the `CustomJob` or `HyperparameterTuningJob` that was created by your `TrainingPipeline` . For example, if your pipeline has the name `  PIPELINE_NAME  ` , this might be called `  PIPELINE_NAME -custom-job ` or `  PIPELINE_NAME -hyperparameter-tuning-job ` .

3.  On the page for your job, click **Launch web terminal** . If your job uses multiple nodes, click **Launch web terminal** next to the node for which you want an interactive shell.
    
    Note that you can only access an interactive shell while the job is running. If you don't see **Launch web terminal** , this might be because Agent Platform hasn't started running your job yet, or because the job has already finished or failed. If the job's **Status** is `Queued` or `Pending` , wait a minute; then try refreshing the page.
    
    If you are using hyperparameter tuning, there are separate **Launch web terminal** links for each trial.

### Get the web access URI from the API

Use the [`projects.locations.customJobs.get` API method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs/get) or the [`projects.locations.hyperparameterTuningJobs.get` API method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/get) to see the URIs that you can use to access interactive shells.

> **Note:** If you created a `TrainingPipeline` for serverless training, run the appropriate `get` method on the `CustomJob` identified by the `TrainingPipeline` 's `trainingTaskMetadata.backingCustomJob` field or the `HyperparameterTuningJob` identified by the `TrainingPipeline` 's `trainingTaskMetadata.backingHyperparameterTuningJob` field.

Depending on which type of serverless training resource you are using, select one of the following tabs to see examples of how to find the `webAccessUris` API field, which contains an interactive shell URI for each node in your job:

### CustomJob

The following tabs show different ways to send a `projects.locations.customJobs.get` request:

### gcloud

Run the [`gcloud ai custom-jobs describe` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/describe) :

    gcloud ai custom-jobs describe JOB_ID \
      --region=LOCATION \
      --format=json

Replace the following:

  - JOB\_ID : The numerical ID of your job. This ID is the last last part of the job's `name` field. You might have seen the ID when you created the job. (If you don't know your job's ID, you can run the [`gcloud ai custom-jobs list` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/list) and look for the appropriate job.)

  - LOCATION : The region where you created the job.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : The region where you created the job.

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .

  - JOB\_ID : The numerical ID of your job. This ID is the last last part of the job's `name` field. You might have seen the ID when you created the job.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs/JOB_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs/JOB_ID"

#### PowerShell (Windows)

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    $cred = gcloud auth application-default print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs/JOB_ID" | Select-Object -Expand Content

In the output, look for the following:

    {
      ...
      "state": "JOB_STATE_RUNNING",
      ...
      "webAccessUris": {
        "workerpool0-0": "INTERACTIVE_SHELL_URI"
      }
    }

If you don't see the `webAccessUris` field, this might be because Agent Platform hasn't started running your job yet. Verify that you see `JOB_STATE_RUNNING` in the `state` field. If the state is `JOB_STATE_QUEUED` or `JOB_STATE_PENDING` , wait a minute; then try getting the project info again.

### HyperparameterTuningJob

The following tabs show different ways to send a `projects.locations.hyperparameterTuningJobs.get` request:

### gcloud

Run the [`gcloud ai hp-tuning-jobs describe` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/hp-tuning-jobs/describe) :

    gcloud ai hp-tuning-jobs describe JOB_ID \
      --region=LOCATION \
      --format=json

Replace the following:

  - JOB\_ID : The numerical ID of your job. This ID is the last last part of the job's `name` field. You might have seen the ID when you created the job. (If you don't know your job's ID, you can run the [`gcloud ai hp-tuning-jobs list` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/hp-tuning-jobs/list) and look for the appropriate job.)

  - LOCATION : The region where you created the job.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : The region where you created the job.

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .

  - JOB\_ID : The numerical ID of your job. This ID is the last last part of the job's `name` field. You might have seen the ID when you created the job.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/hyperparameterTuningJobs/JOB_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/hyperparameterTuningJobs/JOB_ID"

#### PowerShell (Windows)

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    $cred = gcloud auth application-default print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/hyperparameterTuningJobs/JOB_ID" | Select-Object -Expand Content

In the output, look for the following:

    {
      ...
      "state": "JOB_STATE_RUNNING",
      ...
      "trials": [
        ...
        {
          ...
          "state": "ACTIVE",
          ...
          "webAccessUris": {
            "workerpool0-0": "INTERACTIVE_SHELL_URI"
          }
        }
      ],
    }

If you don't see the `webAccessUris` field, this might be because Agent Platform hasn't started running your job yet. Verify that you see `JOB_STATE_RUNNING` in the `state` field. If the state is `JOB_STATE_QUEUED` or `JOB_STATE_PENDING` , wait a minute; then try getting the project info again.

Agent Platform provides a set of interactive shell URIs for each [hyperparameter tuning trial](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview#understanding-trials) as the trial enters the `ACTIVE` state. If you want to get interactive shell URIs for later trials, get the job info again after those trials start.

The preceding example shows the expected output for single-replica training: one URI for the primary training node. If you are performing distributed training, the output contains one URI for each training node, identified by worker pool.

For example, if your job has a primary worker pool with one replica and a secondary worker pool with two replicas, then the `webAccessUris` field looks similar to the following:

    {
      "workerpool0-0": "URI_FOR_PRIMARY",
      "workerpool1-0": "URI_FOR_FIRST_SECONDARY",
      "workerpool1-1": "URI_FOR_SECOND_SECONDARY"
    }

## Use an interactive shell

To use the interactive shell for a training node, navigate to one of the URIs that you found in the preceding section. A Bash shell appears in your browser, giving you access to the file system of the container where Agent Platform is running your training code.

The following sections describe some things to consider as you use the shell and provide some examples of monitoring tools you might use in the shell.

### Prevent the job from ending

When Agent Platform finishes running your job or trial, you will immediately lose access to your interactive shell. If this happens, you might see the message `command terminated with exit code 137` or the shell might stop responding. If you created any files in the container's file system, they will not persist after the job ends.

In some cases, you might want to purposefully make your job run longer in order to debug with an interactive shell. For example, you can add code like the following to your training code in order to make the job keep running for at least an hour after an exception occurs:

    import time
    import traceback
    
    try:
        # Replace with a function that runs your training code
        train_model()
    except Exception as e:
        traceback.print_exc()
        time.sleep(60 * 60)  # 1 hour

However, note that you incur [Vertex AI Training charges](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing) as long as the job keeps running.

### Check permissions issues

The interactive shell environment is authenticated using [application default credentials (ADC)](https://docs.cloud.google.com/docs/authentication#adc) for the service account that Agent Platform uses to run your training code. You can run `gcloud auth list` in the shell for more details.

In the shell, you can use [`bq`](https://docs.cloud.google.com/bigquery/docs/bq-command-line-tool) and other tools that support ADC. This can help you verify that the job is able to access a particular Cloud Storage bucket, BigQuery table, or other Google Cloud resource that your training code needs.

### Visualize Python execution with `py-spy`

[`py-spy`](https://github.com/benfred/py-spy) lets you profile an executing Python program, without modifying it. To use `py-spy` in an interactive shell, do the following:

1.  Install `py-spy` :
    
        pip3 install py-spy

2.  Run `ps aux` in the shell, and look for the PID of the Python training program.

3.  Run any of the subcommands described in the [`py-spy` documentation](https://github.com/benfred/py-spy) , using the PID that you found in the preceding step.

4.  If you use `py-spy record` to create an SVG file, copy this file to a Cloud Storage bucket so you can view it later on your local computer. For example:
    
        gcloud storage cp profile.svg gs://BUCKET
    
    Replace BUCKET with the name of a bucket you have access to.

### Analyze performance with `perf`

[`perf`](https://perf.wiki.kernel.org/) lets you analyze the performance of your training node. To install the version of `perf` appropriate for your node's Linux kernel, run the following commands:

    apt-get update
    apt-get install -y linux-tools-generic
    rm /usr/bin/perf
    LINUX_TOOLS_VERSION=$(ls /usr/lib/linux-tools | tail -n 1)
    ln -s "/usr/lib/linux-tools/${LINUX_TOOLS_VERSION}/perf" /usr/bin/perf

After this, you can run any of the subcommands described in the [`perf` documentation](https://perf.wiki.kernel.org/) .

### Retrieve information about GPU usage

GPU-enabled containers running on nodes with GPUs typically have several command-line tools preinstalled that can help you monitor GPU usage. For example:

  - Use [`nvidia-smi`](https://developer.nvidia.com/nvidia-system-management-interface) to monitor GPU utilization of various processes.

  - Use [`nvprof`](https://docs.nvidia.com/cuda/profiler-users-guide/index.html) to collect a variety of GPU profiling information. Since `nvprof` can't attach to an existing process, you might want to use the tool to start an additional process running your training code. (This means your training code will run twice on the node.) For example:
    
        nvprof -o prof.nvvp python3 -m MODULE_NAME
    
    Replace MODULE\_NAME with the fully-qualified name of your [training application's entry point module](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container#python-modules) ; for example, `trainer.task` .
    
    Then transfer the output file to a Cloud Storage bucket so you can analyze it later on your local computer. For example:
    
        gcloud storage cp prof.nvvp gs://BUCKET
    
    Replace BUCKET with the name of a bucket you have access to.

  - If you encounter a GPU error (not a problem with your configuration or with Agent Platform), use [`nvidia-bug-report.sh`](https://forums.developer.nvidia.com/t/if-you-have-a-problem-please-read-this-first/27131) to create a bug report.
    
    Then transfer the report to a Cloud Storage bucket so you can analyze it later on your local computer or send it to NVIDIA. For example:
    
        gcloud storage cp nvidia-bug-report.log.gz gs://BUCKET
    
    Replace BUCKET with the name of a bucket you have access to.

If `bash` can't find any of these NVIDIA commands, try adding `/usr/local/nvidia/bin` and `/usr/local/cuda/bin` to the shell's `PATH` :

    export PATH="/usr/local/nvidia/bin:/usr/local/cuda/bin:${PATH}"

## Ray Dashboard and Interactive Shell with VPC-SC + VPC Peering

1.  Configure `peered-dns-domains` .
    
    ``` 
    {
      VPC_NAME=NETWORK_NAME
      REGION=LOCATION
      gcloud services peered-dns-domains create training-cloud \
      --network=$VPC_NAME \
      --dns-suffix=$REGION.aiplatform-training.cloud.google.com.
    
      # Verify
      gcloud beta services peered-dns-domains list --network $VPC_NAME;
    }
        
    ```
    
      - NETWORK\_NAME : Change to peered network.
    
      - LOCATION : Desired location (for example, `us-central1` ).

2.  Configure `DNS managed zone` .
    
    ``` 
    {
      PROJECT_ID=PROJECT_ID
      ZONE_NAME=$PROJECT_ID-aiplatform-training-cloud-google-com
      DNS_NAME=aiplatform-training.cloud.google.com
      DESCRIPTION=aiplatform-training.cloud.google.com
    
      gcloud dns managed-zones create $ZONE_NAME  \
      --visibility=private  \
      --networks=https://www.googleapis.com/compute/v1/projects/$PROJECT_ID/global/networks/$VPC_NAME  \
      --dns-name=$DNS_NAME  \
      --description="Training $DESCRIPTION"
    }
        
    ```
    
      - PROJECT\_ID : Your project ID. You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.

3.  Record DNS transaction.
    
    ``` 
    {
      gcloud dns record-sets transaction start --zone=$ZONE_NAME
    
      gcloud dns record-sets transaction add \
      --name=$DNS_NAME. \
      --type=A 199.36.153.4 199.36.153.5 199.36.153.6 199.36.153.7 \
      --zone=$ZONE_NAME \
      --ttl=300
    
      gcloud dns record-sets transaction add \
      --name=*.$DNS_NAME. \
      --type=CNAME $DNS_NAME. \
      --zone=$ZONE_NAME \
      --ttl=300
    
      gcloud dns record-sets transaction execute --zone=$ZONE_NAME
    }
        
    ```

4.  Submit a training job with the interactive shell + VPC-SC + VPC Peering enabled.

## What's next

  - Learn how to optimize the performance of your serverless training jobs using [Profiler](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler) .
  - Learn more about [how Agent Platform orchestrates custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/understanding-training-service) .
  - Read about [Training code requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) .
