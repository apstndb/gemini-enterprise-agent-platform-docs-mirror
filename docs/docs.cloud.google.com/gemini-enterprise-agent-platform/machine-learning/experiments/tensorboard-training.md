---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-training
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-training
title: Use Vertex AI TensorBoard with custom training
description: Set up your custom training job to train models, and set up your training job to automatically upload your Vertex AI TensorBoard logs to Vertex AI TensorBoard.
data_source: docs.cloud.google.com
---

> To see examples of enabling TensorBoard for a custom training job that uses custom containers, run the following notebooks in the environment of your choice:
> 
>   - "Vertex AI TensorBoard custom training with prebuilt containers":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_prebuilt_container.ipynb)
> 
>   - "Vertex AI TensorBoard custom training with custom containers":
>     
>     [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_custom_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_custom_training_with_custom_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_custom_training_with_custom_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_custom_container.ipynb)

When using custom training to train models, you can set up your training job to automatically upload your Vertex AI TensorBoard logs to Vertex AI TensorBoard.

You can use this integration to monitor your training in near real time as Vertex AI TensorBoard streams in Vertex AI TensorBoard logs as they're written to Cloud Storage.

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

### Create a custom training job

The following example shows how to create your own custom training job.

For a detailed example of how to create a custom training job, see [Hello custom training](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/overview) . For steps to build custom training containers, see [Create a custom container image for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .

To create a custom training job use either Vertex AI SDK for Python or REST.

### Python

### Python

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

  - `project` : . You can find these IDs in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.  
  - `location` : The location to run the CustomJob in. This should be the same location as the provided TensorBoard instance.
  - `staging_bucket` : The Cloud Storage bucket to stage artifacts during API calls, including TensorBoard logs.
  - `display_name` : Display name of the custom training job.
  - `script_path` : The path, relative to the working directory on your local file system, to the script that is the entry point for your training code.
  - `container_uri` : The URI of the training container image can be Gemini Enterprise Agent Platform. [prebuilt training container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) or a [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containers-overview) .
  - `model_serving_container_image_uri` : The URI of the model serving container suitable for serving the model produced by the training script.
  - `dataset_id` : The ID number for the dataset to use for training.
  - `model_display_name` : Display name of the trained model.
  - `args` : Command line arguments to be passed to the Python script.
  - `replica_count` : The number of worker replicas to use. In most cases, set this to 1 for your [first worker pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#configure_distributed_training) .
  - `machine_type` : The type of VM to use. For a list of supported VMs, see [Machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types)
  - `accelerator_type` : The type of GPU to attach to each VM in the resource pool. For a list of supported GPUs, see [GPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#specifying_gpus) .
  - `accelerator_count` The number of GPUs to attach to each VM in the resource pool. The default the value is `1` .
  - `training_fraction_split` : The fraction of the dataset to use to train your model.
  - `validation_fraction_split` : The fraction of the dataset to use to validate your model.
  - `test_fraction_split` : The fraction of the dataset to use to evaluate your model.
  - `sync` : Whether to execute this method synchronously.
  - `tensorboard_resource_name` : The resource name of the Vertex TensorBoard instance to which CustomJob will upload TensorBoard logs.
  - `service_account` : Required when running with TensorBoard. See [Create a service account with required permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-setup#create-service-account) .

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The location to run the `CustomJob` in, for example, us-central1. This should be the same location as the provided TensorBoard instance.
  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TENSORBOARD\_INSTANCE\_NAME : (Obligatory) The full name of the existing Vertex AI TensorBoard instance storing your Vertex AI TensorBoard logs:  
    `projects/ PROJECT_ID` /locations/ `LOCATION_ID` /tensorboards/TENSORBOARD\_INSTANCE\_ID  
    Note: If the tensorboard instance is not an existing one, the customJobs creation throws a 404.
  - GCS\_BUCKET\_NAME : The name of the Cloud Storage bucket created during [setup](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-setup#create_storage_bucket) . Use a unique, non-predictable name (for example, include a random suffix).  
  - USER\_SA\_EMAIL : (Obligatory) The service account created in previous steps, or your own service account. "USER\_SA\_NAME@${PROJECT\_ID}.iam.gserviceaccount.com"
  - TRAINING\_CONTAINER : TRAINING\_CONTAINER.
  - INVOCATION\_TIMESTAMP : "$(date +'%Y%m%d-%H%M%S')"
  - JOB\_NAME : "tensorboard-example-job-${INVOCATION\_TIMESTAMP}"
  - BASE\_OUTPUT\_DIR : (Obligatory) the Google Cloud path where all the output of the training is written to. "gs://$GCS\_BUCKET\_NAME/$JOB\_NAME"

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/customJobs

Request JSON body:

    {
    "displayName": JOB_NAME,
    "jobSpec":{
    "workerPoolSpecs":[
      {
        "replicaCount": "1",
         "machineSpec": {
            "machineType": "n1-standard-8",
          },
          "containerSpec": {
            "imageUri": TRAINING_CONTAINER,
          }
        }
      ],
      
      "base_output_directory": {
      "output_uri_prefix": BASE_OUTPUT_DIR,
       },
      "serviceAccount": USER_SA_EMAIL,
      "tensorboard": TENSORBOARD_INSTANCE_NAME,
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
    "displayName": JOB_NAME,
    "jobSpec":{
    "workerPoolSpecs":[
      {
        "replicaCount": "1",
         "machineSpec": {
            "machineType": "n1-standard-8",
          },
          "containerSpec": {
            "imageUri": TRAINING_CONTAINER,
          }
        }
      ],
      
      "base_output_directory": {
      "output_uri_prefix": BASE_OUTPUT_DIR,
       },
      "serviceAccount": USER_SA_EMAIL,
      "tensorboard": TENSORBOARD_INSTANCE_NAME,
      }
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/customJobs"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
    "displayName": JOB_NAME,
    "jobSpec":{
    "workerPoolSpecs":[
      {
        "replicaCount": "1",
         "machineSpec": {
            "machineType": "n1-standard-8",
          },
          "containerSpec": {
            "imageUri": TRAINING_CONTAINER,
          }
        }
      ],
      
      "base_output_directory": {
      "output_uri_prefix": BASE_OUTPUT_DIR,
       },
      "serviceAccount": USER_SA_EMAIL,
      "tensorboard": TENSORBOARD_INSTANCE_NAME,
      }
    }
    '@  | Out-File -FilePath request.json -Encoding utf8

Then execute the following command to send your REST request:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/customJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/customJobs/CUSTOM_JOB_ID",
      "displayName": "DISPLAY_NAME",
      "jobSpec": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": "n1-standard-8"
            },
            "replicaCount": "1",
            "diskSpec": {
              "bootDiskType": "pd-ssd",
              "bootDiskSizeGb": 100
            },
            "containerSpec": {
              "imageUri": "IMAGE_URI"
            }
          }
        ],
        "serviceAccount": "SERVICE_ACCOUNT",
        "baseOutputDirectory": {
          "outputUriPrefix": "OUTPUT_URI_PREFIX"
        },
        "tensorboard": "projects//locations/LOCATION_ID/tensorboards/tensorboard-id"
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "CREATE-TIME",
      "updateTime": "UPDATE-TIME"
    }

## What's next

  - Check out [View Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-view#custom-training) .
  - Learn how to optimize the performance of your custom training jobs using [Cloud Profiler](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler) .
