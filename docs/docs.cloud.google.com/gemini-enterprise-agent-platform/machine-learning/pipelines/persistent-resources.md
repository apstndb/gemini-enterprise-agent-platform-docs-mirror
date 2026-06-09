---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/persistent-resources
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/persistent-resources
title: Configure a pipeline run on a persistent resource
description: Learn how to execute pipeline runs on managed compute resources that persist across runs.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

A Gemini Enterprise Agent Platform persistent resource is a long-running cluster that you can use to run custom training jobs and pipeline runs. By using a persistent resource for a pipeline run, you can help ensure compute resource availability and reduce pipeline task startup time. Persistent resources support all VMs and GPUs that are supported by custom training jobs. To learn more about persistent resources, see [Overview of persistent resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-overview) .

This page shows you how to do the following:

  - [Create a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/persistent-resources#create-persistent-resource)

  - [Create a pipeline run using the persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/persistent-resources#create-pipeline-run)

## Before you begin

Before you can create a pipeline run with a persistent resource, you must first complete the following prerequisites.

### Define and compile a pipeline

[Define your pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline#define_your_workflow_using_kubeflow_pipelines_dsl_package) and then [compile the pipeline definition into a YAML file](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline#compile_your_pipeline_into_a_yaml_file) . For more information about defining and compiling a pipeline, see [Build a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline) .

### Required IAM roles

To get the permission that you need to create a persistent resource, ask your administrator to grant you the [Agent Platform Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.admin) ( `roles/aiplatform.admin` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `aiplatform.persistentResources.create` permission, which is required to create a persistent resource.

You might also be able to get this permission with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create a persistent resource

Use the following samples to create a persistent resource that you can associate with a pipeline run. For more information about creating persistent resources, see [Create a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-create) .

### gcloud

To create a persistent resource that you can associate with a pipeline run, use the [`gcloud ai persistent-resources create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/persistent-resources/create) along with the `--enable-custom-service-account` flag.

A persistent resource can have one or more resource pools. To create multiple resource pools in a persistent resource, specify multiple `--resource-pool-spec` flags.

You can specify all resource pool configurations as part of the command-line or use the `--config` flag to specify the path to a YAML file that contains the configurations.

Before using any of the command data below, make the following replacements:

  - PROJECT\_ID : The project ID of the Google Cloud project where you want to create the persistent resource.

  - LOCATION : The region where you want to create the persistent resource. For a list of supported regions, see [Feature availability](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .

  - PERSISTENT\_RESOURCE\_ID : A unique, user-defined ID for the persistent resource. It must start with a letter, end with a letter or number, and contain only lowercase letters, numbers, and hyphens (-).

  - DISPLAY\_NAME : Optional. The display name of the persistent resource.

  - MACHINE\_TYPE : The type of virtual machine (VM) to use. For a list of supported VMs, see [Machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . This field corresponds to the `machineSpec.machineType` field in the `ResourcePool` API message.

  - REPLICA\_COUNT : Optional. The number of replicas to create for the resource pool, if you don't want to use autoscaling. This field corresponds to the `replicaCount` field in the `ResourcePool` API message. You must specify the replica count if you don't specify the MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT fields.

  - MIN\_REPLICA\_COUNT : Optional. The minimum number of replicas if you're using autoscaling for the resource pool. You must specify both MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT to use autoscaling.

  - MAX\_REPLICA\_COUNT : Optional. The maximum number of replicas if you're using autoscaling for the resource pool. You must specify both MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT to use autoscaling.

  - CONFIG : Path to the persistent resource YAML configuration file, containing a list of `ResourcePool` specs. If an option is specified in both the configuration file and the command-line arguments, the command-line arguments override the configuration file. Note that keys with underscores are considered invalid.
    
    Example YAML configuration file:
    
    ``` 
    resourcePoolSpecs:
      machineSpec:
        machineType: n1-standard-4
      replicaCount: 1
        
    ```

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources create \
        --persistent-resource-id=PERSISTENT_RESOURCE_ID \
        --display-name=DISPLAY_NAME \
        --project=PROJECT_ID \
        --region=LOCATION \
        --resource-pool-spec="replica-count=REPLICA_COUNT,machine-type=MACHINE_TYPE,min-replica-count=MIN_REPLICA_COUNT,max-replica-count=MAX_REPLICA_COUNT" \
        --enable-custom-service-account

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources create `
        --persistent-resource-id=PERSISTENT_RESOURCE_ID `
        --display-name=DISPLAY_NAME `
        --project=PROJECT_ID `
        --region=LOCATION `
        --resource-pool-spec="replica-count=REPLICA_COUNT,machine-type=MACHINE_TYPE,min-replica-count=MIN_REPLICA_COUNT,max-replica-count=MAX_REPLICA_COUNT" `
        --enable-custom-service-account

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources create ^
        --persistent-resource-id=PERSISTENT_RESOURCE_ID ^
        --display-name=DISPLAY_NAME ^
        --project=PROJECT_ID ^
        --region=LOCATION ^
        --resource-pool-spec="replica-count=REPLICA_COUNT,machine-type=MACHINE_TYPE,min-replica-count=MIN_REPLICA_COUNT,max-replica-count=MAX_REPLICA_COUNT" ^
        --enable-custom-service-account

You should receive a response similar to the following:

    Using endpoint [https://us-central1-aiplatform.googleapis.com/]
    Operation to create PersistentResource [projects/PROJECT_NUMBER/locations/us-central1/persistentResources/mypersistentresource/operations/OPERATION_ID] is submitted successfully.
    
    You can view the status of your PersistentResource create operation with the command
    
      $ gcloud ai operations describe projects/sample-project/locations/us-central1/operations/OPERATION_ID

Example `gcloud` command:

    gcloud ai persistent-resources create \
        --persistent-resource-id=my-persistent-resource \
        --region=us-central1 \
        --resource-pool-spec="replica-count=4,machine-type=n1-standard-4"
        --enable-custom-service-account

#### Advanced `gcloud` configurations

If you want to specify configuration options that are not available in the preceding examples, you can use the `--config` flag to specify the path to a `config.yaml` file in your local environment that contains the fields of [`persistentResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.persistentResources) . For example:

    gcloud ai persistent-resources create \
        --persistent-resource-id=PERSISTENT_RESOURCE_ID \
        --project=PROJECT_ID \
        --region=LOCATION \
        --config=CONFIG
        --enable-custom-service-account

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

To create a [persistent resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PersistentResource) that you can use with a pipeline run, set the `enable_custom_service_account` parameter to `True` in the `ResourceRuntimeSpec` object while creating the persistent resource.

    from google.cloud.aiplatform.preview import persistent_resource
    from google.cloud.aiplatform_v1beta1.types.persistent_resource import ResourcePool
    from google.cloud.aiplatform_v1beta1.types.machine_resources import MachineSpec
    
    my_example_resource = persistent_resource.PersistentResource.create(
        persistent_resource_id='PERSISTENT_RESOURCE_ID',
        display_name='DISPLAY_NAME',
        resource_pools=[
            ResourcePool(
                machine_spec=MachineSpec(
                    machine_type='MACHINE_TYPE'
                ),
                replica_count=REPLICA_COUNT
            )
        ],
        enable_custom_service_account=True,
    )

Replace the following:

  - PERSISTENT\_RESOURCE\_ID : A unique, user-defined ID for the persistent resource. The ID must contain only lowercase letters, numbers, and hyphens ( `-` ). The first character must be a lowercase letter and the last character must be either be a lowercase letter or a number.
  - DISPLAY\_NAME : Optional. The display name of the persistent resource.
  - MACHINE\_TYPE : The type of virtual machine (VM) to use. For a list of supported VMs, see [Machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . This field corresponds to the `machineSpec.machineType` field in the `ResourcePool` API message.
  - REPLICA\_COUNT : The number of replicas to create when creating this resource pool.

### REST

To create a [`PersistentResource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.persistentResources#PersistentResource) resource that you can associate with a pipeline run, send a POST request by using the [`persistentResources/create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.persistentResources/create) method with the `enable_custom_service_account` parameter set to `true` in the request body.

A persistent resource can have one or more resource pools. You can configure each resource pool to use either a fixed number of replicas or autoscaling.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : The project ID of the Google Cloud project where you want to create the persistent resource.
  - LOCATION : The region where you want to create the persistent resource. For a list of supported regions, see [Feature availability](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .
  - PERSISTENT\_RESOURCE\_ID : A unique, user-defined ID for the persistent resource. It must start with a letter, end with a letter or number, and contain only lowercase letters, numbers, and hyphens (-).
  - DISPLAY\_NAME : Optional. The display name of the persistent resource.
  - MACHINE\_TYPE : The type of virtual machine (VM) to use. For a list of supported VMs, see [Machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . This field corresponds to the `machineSpec.machineType` field in the `ResourcePool` API message.
  - REPLICA\_COUNT : Optional. The number of replicas to create for the resource pool, if you don't want to use autoscaling. This field corresponds to the `replicaCount` field in the `ResourcePool` API message. You must specify the replica count if you don't specify the MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT fields.
  - MIN\_REPLICA\_COUNT : Optional. The minimum number of replicas if you're using autoscaling for the resource pool. You must specify both MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT to use autoscaling.
  - MAX\_REPLICA\_COUNT : Optional. The maximum number of replicas if you're using autoscaling for the resource pool. You must specify both MIN\_REPLICA\_COUNT and MAX\_REPLICA\_COUNT to use autoscaling.

HTTP method and URL:

    POST https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources?persistent_resource_id=PERSISTENT_RESOURCE_ID

Request JSON body:

    {
      "display_name": "DISPLAY_NAME",
      "resource_pools": [
        {
          "machine_spec": {
            "machine_type": "MACHINE_TYPE"
          },
          "replica_count": REPLICA_COUNT,
          "autoscaling_spec": {
            "min_replica_count": MIN_REPLICA_COUNT,
            "max_replica_count": MAX_REPLICA_COUNT
          }
        }
      ],
      "resource_runtime_spec": {
        "service_account_spec": {
          "enable_custom_service_account": true
        }
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    cat > request.json << 'EOF'
    {
      "display_name": "DISPLAY_NAME",
      "resource_pools": [
        {
          "machine_spec": {
            "machine_type": "MACHINE_TYPE"
          },
          "replica_count": REPLICA_COUNT,
          "autoscaling_spec": {
            "min_replica_count": MIN_REPLICA_COUNT,
            "max_replica_count": MAX_REPLICA_COUNT
          }
        }
      ],
      "resource_runtime_spec": {
        "service_account_spec": {
          "enable_custom_service_account": true
        }
      }
    }
    EOF

Then execute the following command to send your REST request:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources?persistent_resource_id=PERSISTENT_RESOURCE_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

    @'
    {
      "display_name": "DISPLAY_NAME",
      "resource_pools": [
        {
          "machine_spec": {
            "machine_type": "MACHINE_TYPE"
          },
          "replica_count": REPLICA_COUNT,
          "autoscaling_spec": {
            "min_replica_count": MIN_REPLICA_COUNT,
            "max_replica_count": MAX_REPLICA_COUNT
          }
        }
      ],
      "resource_runtime_spec": {
        "service_account_spec": {
          "enable_custom_service_account": true
        }
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
        -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources?persistent_resource_id=PERSISTENT_RESOURCE_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/persistentResources/mypersistentresource/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreatePersistentResourceOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-02-08T21:17:15.009668Z",
          "updateTime": "2023-02-08T21:17:15.009668Z"
        }
      }
    }

## Create a pipeline run using the persistent resource

To create a pipeline job, you must first create a pipeline spec. A pipeline spec is an in-memory object that you create by converting a compiled pipeline definition.

### Create a pipeline spec

Follow these instructions to create an in-memory pipeline spec that you can use to create the pipeline run:

1.  Define a pipeline and compile it into a YAML file. For more information about defining and compiling a pipeline, see [Build a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline) .

2.  Use the following code sample to convert the compiled pipeline YAML file to an in-memory pipeline spec.
    
        import yaml
        with open("COMPILED_PIPELINE_PATH", "r") as stream:
          try:
            pipeline_spec = yaml.safe_load(stream)
            print(pipeline_spec)
          except yaml.YAMLError as exc:
            print(exc)
    
    Replace COMPILED\_PIPELINE\_PATH with the local path to your compiled pipeline YAML file.

### Create a pipeline run

Use the following Python code sample to create a pipeline run that uses the persistent resource:

    # Import aiplatform and the appropriate API version v1beta1
    from google.cloud import aiplatform, aiplatform_v1beta1
    from google.cloud.aiplatform_v1beta1.types import pipeline_job as pipeline_job_types
    
    # Initialize the Vertex SDK using PROJECT_ID and LOCATION
    aiplatform.init(project='PROJECT_ID', location='LOCATION')
    
    # Create the API Endpoint
    client_options = {
        "api_endpoint": f"LOCATION-aiplatform.googleapis.com"
    }
    
    # Initialize the PipeLineServiceClient
    client = aiplatform_v1beta1.PipelineServiceClient(client_options=client_options)
    
    # Construct the runtime detail
    pr_runtime_detail = pipeline_job_types.PipelineJob.RuntimeConfig.PersistentResourceRuntimeDetail(
        persistent_resource_name=(
            f"projects/PROJECT_NUMBER/"
            f"locations/LOCATION/"
            f"persistentResources/PERSISTENT_RESOURCE_ID"
        ),
        task_resource_unavailable_wait_time_ms=WAIT_TIME,
        task_resource_unavailable_timeout_behavior='TIMEOUT_BEHAVIOR',
    )
    
    # Construct the default runtime configuration block
    default_runtime = pipeline_job_types.PipelineJob.RuntimeConfig.DefaultRuntime(
        persistent_resource_runtime_detail=pr_runtime_detail
    )
    
    # Construct the main runtime configuration
    runtime_config = pipeline_job_types.PipelineJob.RuntimeConfig(
        gcs_output_directory='PIPELINE_ROOT',
        parameter_values={
            'project_id': 'PROJECT_ID'
        },
        default_runtime=default_runtime
    )
    
    # Construct the pipeline job object
    pipeline_job = pipeline_job_types.PipelineJob(
        display_name='PIPELINE_DISPLAY_NAME',
        pipeline_spec=PIPELINE_SPEC,
        runtime_config=runtime_config,
    )
    
    # Construct the request
    parent_path = f"projects/PROJECT_ID/locations/LOCATION"
    request = aiplatform_v1beta1.CreatePipelineJobRequest(
        parent=parent_path,
        pipeline_job=pipeline_job,
    )
    
    # Make the API Call to create the pipeline job
    response = client.create_pipeline_job(request=request)
    
    # Construct the Google Cloud console link
    job_id = response.name.split('/')[-1]
    console_link = (
        f"https://console.cloud.google.com/vertex-ai/locations/LOCATION"
        f"/pipelines/runs/{job_id}"
        f"?project=PROJECT_ID"
    )
    
    # Print the Google Cloud console link to the pipeline run
    print(f"View Pipeline Run in Google Cloud console: {console_link}")

Replace the following:

  - PROJECT\_ID : The Google Cloud project that the pipeline runs in.

  - LOCATION : The region where the pipeline run is executed. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) . If you don't set this parameter, Agent Platform Pipelines uses the default location set in `aiplatform.init` .

  - PERSISTENT\_RESOURCE\_ID : The ID of the persistent resource that you created.

  - PROJECT\_NUMBER : The project number for your Google Cloud project. This is different from the project ID. You can find the project number on the [Project Settings](https://console.cloud.google.com/iam-admin/settings) page in the Google Cloud console.

  - COMPILED\_PIPELINE\_PATH : The path to your compiled pipeline YAML file. It can be a local path or a Cloud Storage URI.

  - WAIT\_TIME : The time in milliseconds to wait if the persistent resource is unavailable.

  - TIMEOUT\_BEHAVIOR : The fall back behavior of the pipeline task in case the WAIT\_TIME is exceeded. Possible values include the following:
    
      - `FAIL` The pipeline task fails after exceeding the wait time.
    
      - `FALL_BACK_TO_ON_DEMAND` The pipeline task continues to run using the default Gemini Enterprise Agent Platform training resources, without using the persistent resource.

  - PIPELINE\_ROOT : The path to a Cloud Storage URI to store the artifacts of your pipeline run.

  - PIPELINE\_DISPLAY\_NAME : The name of the pipeline run. The maximum length for a display name is 128 UTF-8 characters.

  - PIPELINE\_SPEC : The pipeline spec you created in [Create a pipeline spec](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/persistent-resources#create-spec) .

## What's next

  - Learn how to [run a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline) .
