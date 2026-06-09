---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings
title: Configure container settings for Gemini Enterprise Agent Platform serverless training
description: Configure training container settings for either a custom container or a Python training application that runs on a prebuilt container.
data_source: docs.cloud.google.com
---

When you perform Gemini Enterprise Agent Platform serverless training, you must specify what machine learning (ML) code you want Gemini Enterprise Agent Platform to run. To do this, configure training container settings for either a [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) or a [Python training application that runs on a prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) .

To determine whether you want to use a custom container or a prebuilt container, read [Training code requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) .

This document describes the fields of the Agent Platform API that you must specify in either of the preceding cases.

## Where to specify container settings

Specify configuration details within a [`WorkerPoolSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#workerpoolspec) . Depending on how you perform serverless training, put this `WorkerPoolSpec` in one of the following API fields:

  - **If you are creating a [`CustomJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.customJobs) ,** specify the `WorkerPoolSpec` in `CustomJob.jobSpec.workerPoolSpecs` .
    
    If you are using the Google Cloud CLI, then you can use the `--worker-pool-spec` flag or the `--config` flag on the [`gcloud ai custom-jobs create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/create) to specify worker pool options.
    
    Learn more about [creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

  - **If you are creating a [`HyperparameterTuningJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs) ,** specify the `WorkerPoolSpec` in `HyperparameterTuningJob.trialJobSpec.workerPoolSpecs` .
    
    If you are using the gcloud CLI, then you can use the `--config` flag on the [`gcloud ai hpt-tuning-jobs create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/hp-tuning-jobs/create) to specify worker pool options.
    
    Learn more about [creating a `HyperparameterTuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) .

  - **If you are creating a [`TrainingPipeline` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines) without hyperparameter tuning,** specify the `WorkerPoolSpec` in `TrainingPipeline.trainingTaskInputs.workerPoolSpecs` .
    
    Learn more about [creating a custom `TrainingPipeline`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) .

  - **If you are creating a `TrainingPipeline` with hyperparameter tuning** , specify the `WorkerPoolSpec` in `TrainingPipeline.trainingTaskInputs.trialJobSpec.workerPoolSpecs` .

If you are performing [distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#distributed) , you can use different settings for each worker pool.

## Configure container settings

Depending on whether you are using a prebuilt container or a custom container, you must specify different fields within the `WorkerPoolSpec` . Select the tab for your scenario:

### Prebuilt container

1.  Select a [prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) that supports the ML framework you plan to use for training. Specify one of the container image's URIs in the [`pythonPackageSpec.executorImageUri` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#PythonPackageSpec.FIELDS.executor_image_uri) .

2.  Specify the Cloud Storage URIs of your [Python training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) in the [`pythonPackageSpec.packageUris` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#PythonPackageSpec.FIELDS.package_uris) .

3.  Specify your training application's entry point module in the [`pythonPackageSpec.pythonModule` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#PythonPackageSpec.FIELDS.python_module) .

4.  Optionally, specify a list of command-line arguments to pass to your training application's entry point module in the [`pythonPackageSpec.args` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#PythonPackageSpec.FIELDS.args) .

The following examples highlight where you specify these container settings when you create a `CustomJob` :

### Console

In the Google Cloud console, you can't create a `CustomJob` directly. However, you can [create a `TrainingPipeline` that creates a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#create) . When you create a `TrainingPipeline` in the Google Cloud console, you can specify prebuilt container settings in certain fields on the **Training container** step:

  - `pythonPackageSpec.executorImageUri` : Use the **Model framework** and **Model framework version** drop-down lists.

  - `pythonPackageSpec.packageUris` : Use the **Package location** field.

  - `pythonPackageSpec.pythonModule` : Use the **Python module** field.

  - `pythonPackageSpec.args` : Use the **Arguments** field.

### gcloud

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --python-package-uris=PYTHON_PACKAGE_URIS \
      --worker-pool-spec=machine-type=MACHINE_TYPE,replica-count=REPLICA_COUNT,executor-image-uri=PYTHON_PACKAGE_EXECUTOR_IMAGE_URI,python-module=PYTHON_MODULE

For more context, read the [guide to creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

### Custom container

1.  Specify the Artifact Registry or Docker Hub URI of your [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) in the [`containerSpec.imageUri` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#ContainerSpec.FIELDS.image_uri) .

2.  Optionally, if you want to override the [`ENTRYPOINT`](https://docs.docker.com/engine/reference/builder/#entrypoint) or [`CMD`](https://docs.docker.com/engine/reference/builder/#cmd) instructions in your container, specify the [`containerSpec.command` or `containerSpec.args` fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#containerspec) . These fields affect how your container runs according to the following rules:
    
      - **If you specify neither field:** Your container runs according to its `ENTRYPOINT` instruction and `CMD` instruction (if it exists). Refer to the [Docker documentation about how `CMD` and `ENTRYPOINT` interact](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact) .
    
      - **If you specify only `containerSpec.command` :** Your container runs with the value of `containerSpec.command` replacing its `ENTRYPOINT` instruction. If the container has a `CMD` instruction, it is ignored.
    
      - **If you specify only `containerSpec.args` :** Your container runs according to its `ENTRYPOINT` instruction, with the value of `containerSpec.args` replacing its `CMD` instruction.
    
      - **If you specify both fields:** Your container runs with `containerSpec.command` replacing its `ENTRYPOINT` instruction and `containerSpec.args` replacing its `CMD` instruction.

The following example highlights where you can specify some of these container settings when you create a `CustomJob` :

### Console

In the Google Cloud console, you can't create a `CustomJob` directly. However, you can [create a `TrainingPipeline` that creates a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#create) . When you create a `TrainingPipeline` in the Google Cloud console, you can specify custom container settings in certain fields on the **Training container** step:

  - `containerSpec.imageUri` : Use the **Container image** field.

  - `containerSpec.command` : This API field is not configurable in the Google Cloud console.

  - `containerSpec.args` : Use the **Arguments** field.

### gcloud

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --worker-pool-spec=machine-type=MACHINE_TYPE,replica-count=REPLICA_COUNT,container-image-uri=CUSTOM_CONTAINER_IMAGE_URI

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

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

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

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

    from google.cloud import aiplatform
    
    
    def create_custom_job_sample(
        project: str,
        display_name: str,
        container_image_uri: str,
        location: str = "us-central1",
        api_endpoint: str = "us-central1-aiplatform.googleapis.com",
    ):
        # The AI Platform services require regional API endpoints.
        client_options = {"api_endpoint": api_endpoint}
        # Initialize client that will be used to create and send requests.
        # This client only needs to be created once, and can be reused for multiple requests.
        client = aiplatform.gapic.JobServiceClient(client_options=client_options)
        custom_job = {
            "display_name": display_name,
            "job_spec": {
                "worker_pool_specs": [
                    {
                        "machine_spec": {
                            "machine_type": "n1-standard-4",
                            "accelerator_type": aiplatform.gapic.AcceleratorType.NVIDIA_TESLA_K80,
                            "accelerator_count": 1,
                        },
                        "replica_count": 1,
                        "container_spec": {
                            "image_uri": container_image_uri,
                            "command": [],
                            "args": [],
                        },
                    }
                ]
            },
        }
        parent = f"projects/{project}/locations/{location}"
        response = client.create_custom_job(parent=parent, custom_job=custom_job)
        print("response:", response)

For more context, read the [guide to creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

## What's next

  - Learn how to perform serverless training by [creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .
