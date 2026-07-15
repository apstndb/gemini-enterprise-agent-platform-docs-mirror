---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute
title: Configure compute resources for Gemini Enterprise Agent Platform serverless training
description: Learn about the different compute resources that you can use for Gemini Enterprise Agent Platform serverless training and how to configure them.
data_source: docs.cloud.google.com
---

When you perform serverless training, your training code runs on one or more virtual machine (VM) instances. You can configure what types of VM to use for training: using VMs with more compute resources can speed up training and let you work with larger datasets, but they can also incur greater [training costs](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing) .

In some cases, you can additionally use GPUs to accelerate training. GPUs incur additional costs.

You can also optionally customize the type and size of your training VMs' boot disks.

This document describes the different compute resources that you can use for serverless training and how to configure them.

## Manage cost and availability

To help manage costs or ensure availability of VM resources, Agent Platform provides the following:

  - To ensure that VM resources are available when your training jobs need them, you can use Compute Engine reservations. Reservations provide a high level of assurance in obtaining capacity for Compute Engine resources. For more information, see [Use reservations with training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-reservations) .

  - To reduce the cost of running your training jobs, you can use Spot VMs. Spot VMs are virtual machine (VM) instances that are excess Compute Engine capacity. Spot VMs have significant discounts, but Compute Engine might preemptively stop or delete Spot VMs to reclaim the capacity at any time. For more information, see [Use Spot VMs with training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-spot-vms) .

  - For serverless training jobs that request GPU resources, Dynamic Workload Scheduler lets you schedule the jobs based on when the requested GPU resources become available. For more information, see [Schedule training jobs based on resource availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/schedule-jobs-dws) .

## Where to specify compute resources

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

## Machine types

In your `WorkerPoolSpec` , you must specify one of the following machine types in the [`machineSpec.machineType` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MachineSpec) . Each replica in the worker pool runs on a separate VM that has the specified machine type.

  - `a4x-highgpu-4g` <sup>\*</sup>
  - `a4-highgpu-8g` <sup>\*</sup>
  - `a3-ultragpu-8g` <sup>\*</sup>
  - `a3-megagpu-8g` <sup>\*</sup>
  - `a3-highgpu-1g` <sup>\*</sup>
  - `a3-highgpu-2g` <sup>\*</sup>
  - `a3-highgpu-4g` <sup>\*</sup>
  - `a3-highgpu-8g` <sup>\*</sup>
  - `a2-ultragpu-1g` <sup>\*</sup>
  - `a2-ultragpu-2g` <sup>\*</sup>
  - `a2-ultragpu-4g` <sup>\*</sup>
  - `a2-ultragpu-8g` <sup>\*</sup>
  - `a2-highgpu-1g` <sup>\*</sup>
  - `a2-highgpu-2g` <sup>\*</sup>
  - `a2-highgpu-4g` <sup>\*</sup>
  - `a2-highgpu-8g` <sup>\*</sup>
  - `a2-megagpu-16g` <sup>\*</sup>
  - `e2-standard-4`
  - `e2-standard-8`
  - `e2-standard-16`
  - `e2-standard-32`
  - `e2-highmem-2`
  - `e2-highmem-4`
  - `e2-highmem-8`
  - `e2-highmem-16`
  - `e2-highcpu-16`
  - `e2-highcpu-32`
  - `n4-standard-2`
  - `n4-standard-4`
  - `n4-standard-8`
  - `n4-standard-16`
  - `n4-standard-32`
  - `n4-standard-48`
  - `n4-standard-64`
  - `n4-standard-80`
  - `n4-highmem-2`
  - `n4-highmem-4`
  - `n4-highmem-8`
  - `n4-highmem-16`
  - `n4-highmem-32`
  - `n4-highmem-48`
  - `n4-highmem-64`
  - `n4-highmem-80`
  - `n4-highcpu-2`
  - `n4-highcpu-4`
  - `n4-highcpu-8`
  - `n4-highcpu-16`
  - `n4-highcpu-32`
  - `n4-highcpu-48`
  - `n4-highcpu-64`
  - `n4-highcpu-80`
  - `n2-standard-4`
  - `n2-standard-8`
  - `n2-standard-16`
  - `n2-standard-32`
  - `n2-standard-48`
  - `n2-standard-64`
  - `n2-standard-80`
  - `n2-highmem-2`
  - `n2-highmem-4`
  - `n2-highmem-8`
  - `n2-highmem-16`
  - `n2-highmem-32`
  - `n2-highmem-48`
  - `n2-highmem-64`
  - `n2-highmem-80`
  - `n2-highcpu-16`
  - `n2-highcpu-32`
  - `n2-highcpu-48`
  - `n2-highcpu-64`
  - `n2-highcpu-80`
  - `n1-standard-4`
  - `n1-standard-8`
  - `n1-standard-16`
  - `n1-standard-32`
  - `n1-standard-64`
  - `n1-standard-96`
  - `n1-highmem-2`
  - `n1-highmem-4`
  - `n1-highmem-8`
  - `n1-highmem-16`
  - `n1-highmem-32`
  - `n1-highmem-64`
  - `n1-highmem-96`
  - `n1-highcpu-16`
  - `n1-highcpu-32`
  - `n1-highcpu-64`
  - `n1-highcpu-96`
  - `c2-standard-4`
  - `c2-standard-8`
  - `c2-standard-16`
  - `c2-standard-30`
  - `c2-standard-60`
  - `ct5lp-hightpu-1t` <sup>\*</sup>
  - `ct5lp-hightpu-4t` <sup>\*</sup>
  - `ct5lp-hightpu-8t` <sup>\*</sup>
  - `m1-ultramem-40`
  - `m1-ultramem-80`
  - `m1-ultramem-160`
  - `m1-megamem-96`
  - `g2-standard-4` <sup>\*</sup>
  - `g2-standard-8` <sup>\*</sup>
  - `g2-standard-12` <sup>\*</sup>
  - `g2-standard-16` <sup>\*</sup>
  - `g2-standard-24` <sup>\*</sup>
  - `g2-standard-32` <sup>\*</sup>
  - `g2-standard-48` <sup>\*</sup>
  - `g2-standard-96` <sup>\*</sup>
  - `g4-standard-48` <sup>\*</sup>
  - `g4-standard-96` <sup>\*</sup>
  - `g4-standard-192` <sup>\*</sup>
  - `g4-standard-384` <sup>\*</sup>
  - `cloud-tpu` <sup>\*</sup>

\* Machine types marked with asterisks in the preceding list must be used with certain GPUs or TPUs. See the following sections of this guide.

To learn about the technical specifications of each machine type, read the [Compute Engine documentation about machine types](https://docs.cloud.google.com/compute/docs/machine-resource) . To learn about the cost of using each machine type for serverless training, read [Pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing) .

The following examples highlight where you specify a machine type when you create a `CustomJob` :

### Console

In the Google Cloud console, you can't create a `CustomJob` directly. However, you can [create a `TrainingPipeline` that creates a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#create) . When you create a `TrainingPipeline` in the Google Cloud console, specify a machine type for each worker pool on the **Compute and pricing** step, in the **Machine type** field.

### gcloud

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --worker-pool-spec=machine-type=MACHINE_TYPE,replica-count=REPLICA_COUNT,container-image-uri=CUSTOM_CONTAINER_IMAGE_URI

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

## GPUs

If you have [written your training code to use GPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#gpus) , then you may configure your worker pool to use one or more GPUs on each VM. To use GPUs, you must use an A2, N1, or G2 machine type. Additionally, using smaller machines types like `n1-highmem-2` with GPUs might cause logging to fail for some workloads because of CPU constraints. If your training job stops returning logs, consider selecting a larger machine type.

Agent Platform supports the following types of GPU for serverless training:

> **Caution:** NVIDIA P100 GPUs reach end of support on September 15, 2026. For more information, see [NVIDIA P100 end of support](https://docs.cloud.google.com/compute/docs/eol/p100-eos) .

  - `NVIDIA_GB200` <sup>+</sup> (includes [GPUDirect-RDMA](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#gpudirect-rdma) )
  - `NVIDIA_B200` <sup>\*</sup> (includes [GPUDirect-RDMA](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#gpudirect-rdma) )
  - `NVIDIA_H100_MEGA_80GB` <sup>\*</sup> (includes [GPUDirect-TCPXO](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#gpudirect-tcpxo) )
  - `NVIDIA_H100_80GB`
  - `NVIDIA_H200_141GB` <sup>\*</sup> (includes [GPUDirect-RDMA](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#gpudirect-rdma) )
  - `NVIDIA_A100_80GB`
  - `NVIDIA_TESLA_A100` (NVIDIA A100 40GB)
  - `NVIDIA_TESLA_P4`
  - `NVIDIA_TESLA_P100`
  - `NVIDIA_TESLA_T4`
  - `NVIDIA_TESLA_V100`
  - `NVIDIA_L4`
  - `NVIDIA_RTX_PRO_6000`

<sup>\*</sup> It's recommended that you obtain capacity using [shared reservations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-reservations) or [spot vms](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-spot-vms) .

<sup>+</sup> Requires obtaining capacity using [shared reservations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-reservations) .

To learn more about the technical specification for each type of GPU, read the [Compute Engine short documentation about GPUs for compute workloads](https://docs.cloud.google.com/compute/docs/gpus#gpus-list) . To learn about the cost of using each machine type for serverless training, read [Pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing) .

In your `WorkerPoolSpec` , specify the type of GPU that you want to use in the [`machineSpec.acceleratorType` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MachineSpec) and number of GPUs that you want each VM in the worker pool to use in the [`machineSpec.acceleratorCount` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MachineSpec) . However, your choices for these fields must meet the following restrictions:

  - The type of GPU that you choose must be available in the location where you are performing serverless training. Not all types of GPU are available in all regions. [Learn about regional availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators) .

  - You can only use certain numbers of GPUs in your configuration. For example, you can use 2 or 4 `NVIDIA_TESLA_T4` GPUs on a VM, but not 3. To see what `acceleratorCount` values are valid for each type of GPU, see the [following compatibility table](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#gpu-compatibility-table) .

  - You must make sure that your GPU configuration provides sufficient virtual CPUs and memory to the machine type that you use it with. For example, if you use the `n1-standard-32` machine type in your worker pool, then each VM has 32 virtual CPUs and 120 GB of memory. Since each `NVIDIA_TESLA_V100` GPU can provide up to 12 virtual CPUs and 76 GB of memory, you must use at least 4 GPUs for each `n1-standard-32` VM to support its requirements. (2 GPUs provide insufficient resources, and you can't specify 3 GPUs.)
    
    The [following compatibility table](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#gpu-compatibility-table) accounts for this requirement.
    
    Note the following additional limitation on using GPUs for custom training that differ from using GPUs with Compute Engine:
    
      - A configuration with 4 `NVIDIA_TESLA_P100` GPUs only provides up to 64 virtual CPUS and up to 208 GB of memory in *all* regions and zones.

  - For jobs that use [Dynamic Workload Scheduler](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/schedule-jobs-dws) or [Spot VMs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-spot-vms) , update the `scheduling.strategy` field of the `CustomJob` to the chosen strategy.

The following compatibility table lists the valid values for `machineSpec.acceleratorCount` depending on your choices for `machineSpec.machineType` and `machineSpec.acceleratorType` :

Valid numbers of GPUs for each machine type

Machine type

`NVIDIA_H100_MEGA_80GB`

`NVIDIA_H100_80GB`

`NVIDIA_A100_80GB`

`NVIDIA_TESLA_A100`

`NVIDIA_TESLA_P4`

`NVIDIA_TESLA_P100`

`NVIDIA_TESLA_T4`

`NVIDIA_TESLA_V100`

`NVIDIA_L4`

`NVIDIA_H200_141GB`

`NVIDIA_B200`

`NVIDIA_GB200`

`NVIDIA_RTX_PRO_6000`

`a3-megagpu-8g`

8

`a3-highgpu-1g`

1

`a3-highgpu-2g`

2

`a3-highgpu-4g`

4

`a3-highgpu-8g`

8

`a3-ultragpu-8g`

8

`a4-highgpu-8g`

8

`a4x-highgpu-4g`

4

`a2-ultragpu-1g`

1

`a2-ultragpu-2g`

2

`a2-ultragpu-4g`

4

`a2-ultragpu-8g`

8

`a2-highgpu-1g`

1

`a2-highgpu-2g`

2

`a2-highgpu-4g`

4

`a2-highgpu-8g`

8

`a2-megagpu-16g`

16

`n1-standard-4`

1, 2, 4

1, 2, 4

1, 2, 4

1, 2, 4, 8

`n1-standard-8`

1, 2, 4

1, 2, 4

1, 2, 4

1, 2, 4, 8

`n1-standard-16`

1, 2, 4

1, 2, 4

1, 2, 4

2, 4, 8

`n1-standard-32`

2, 4

2, 4

2, 4

4, 8

`n1-standard-64`

4

4

8

`n1-standard-96`

4

4

8

`n1-highmem-2`

1, 2, 4

1, 2, 4

1, 2, 4

1, 2, 4, 8

`n1-highmem-4`

1, 2, 4

1, 2, 4

1, 2, 4

1, 2, 4, 8

`n1-highmem-8`

1, 2, 4

1, 2, 4

1, 2, 4

1, 2, 4, 8

`n1-highmem-16`

1, 2, 4

1, 2, 4

1, 2, 4

2, 4, 8

`n1-highmem-32`

2, 4

2, 4

2, 4

4, 8

`n1-highmem-64`

4

4

8

`n1-highmem-96`

4

4

8

`n1-highcpu-16`

1, 2, 4

1, 2, 4

1, 2, 4

2, 4, 8

`n1-highcpu-32`

2, 4

2, 4

2, 4

4, 8

`n1-highcpu-64`

4

4

4

8

`n1-highcpu-96`

4

4

8

`g2-standard-4`

1

`g2-standard-8`

1

`g2-standard-12`

1

`g2-standard-16`

1

`g2-standard-24`

2

`g2-standard-32`

1

`g2-standard-48`

4

`g2-standard-96`

8

`g4-standard-48`

1

`g4-standard-96`

2

`g4-standard-192`

4

`g4-standard-384`

8

The following examples highlight where you can specify GPUs when you create a `CustomJob` :

### Console

In the Google Cloud console, you can't create a `CustomJob` directly. However, you can [create a `TrainingPipeline` that creates a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#create) . When you create a `TrainingPipeline` in the Google Cloud console, you can specify GPUs for each worker pool on the **Compute and pricing** step. First specify a **Machine type** . Then, you can specify GPU details in the **Accelerator type** and **Accelerator count** fields.

### gcloud

To specify GPUs using the Google Cloud CLI tool, you must use a [`config.yaml` file](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/create#--config) . For example:

#### `config.yaml`

    workerPoolSpecs:
      machineSpec:
        machineType: MACHINE_TYPE
        acceleratorType: ACCELERATOR_TYPE
        acceleratorCount: ACCELERATOR_COUNT
      replicaCount: REPLICA_COUNT
      containerSpec:
        imageUri: CUSTOM_CONTAINER_IMAGE_URI

Then run a command like the following:

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --config=config.yaml

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

## GPUDirect Networking

On Vertex Training, some H100, H200, B200, and GB200 series machines come pre-configured with the GPUDirect networking stack. GPUDirect can increase the intergpu networking speed by up to 2x compared to GPUs without GPUDirect.

GPUDirect does this by reducing the overhead required to transfer packet payloads between GPUs, significantly improving throughput at scale.

### GPUDirect-TCPXO

The `a3-megagpu-8g` machine type has:

  - 8 NVIDIA H100 GPUs per machine
  - Up to 200 Gbps bandwidth on the primary NIC
  - 8 secondary NICs each supporting up to 200 Gbps for GPU data transfer
  - GPUDirect-TCPXO, which further improves GPU to VM communication

GPUs with GPUDirect are especially equipped for distributed training of large models.

> **Note:** For troubleshooting, set `NCCL_DEBUG=INFO` within the `containerSpec.env` list of all GPU nodes to get additional logs.

### GPUDirect-RDMA

The `a4x-highgpu-4g` machine types have:

  - 4 GB200 GPUs per machine
  - 2 host NICs providing a bandwidth of 400 Gbps
  - 6 NICs offering up to 2400 Gbps for GPU data transfer
  - GPUDirect-RDMA, which enables higher network performance for GPU communication for large scale ML training workloads through RoCE (RDMA over Converged Ethernet)

The `a3-ultragpu-8g` and `a4-highgpu-8g` machine types have:

  - 8 NVIDIA H200/B200 GPUs per machine
  - 2 host NICs providing a bandwidth of 400 Gbps
  - 8 NICs offering up to 3200 Gbps for GPU data transfer
  - GPUDirect-RDMA, which enables higher network performance for GPU communication for large scale ML training workloads through RoCE (RDMA over Converged Ethernet)

> **Note:** When using RDMA, add `source /usr/local/gib/scripts/set_nccl_env.sh` to the beginning of the training command to set all the required environment variables to configure NCCL.

## TPUs

To use [Tensor Processing Units (TPUs)](https://docs.cloud.google.com/tpu/docs/tpus) for custom training on Agent Platform, you can configure a worker pool to use a [TPU VM](https://docs.cloud.google.com/tpu/docs/system-architecture-tpu-vm#tpu-vm) .

When you use a TPU VM in Agent Platform, you must only use a single worker pool for custom training, and you must configure this worker pool to use only one replica.

### TPU v2 and v3

To use TPU v2 or v3 VMs in your worker pool, you must use one of the following configurations:

  - To configure a TPU VM with [TPU v2](https://docs.cloud.google.com/tpu/docs/v2) , specify the following fields in the `WorkerPoolSpec` :
    
      - Set `machineSpec.machineType` to `cloud-tpu` .
      - Set `machineSpec.acceleratorType` to `TPU_V2` .
      - Set `machineSpec.acceleratorCount` to `8` for single TPU or `32 or multiple of 32` for TPU Pods.
      - Set `replicaCount` to `1` .

  - To configure a TPU VM with [TPU v3](https://docs.cloud.google.com/tpu/docs/v3) , specify the following fields in the `WorkerPoolSpec` :
    
      - Set `machineSpec.machineType` to `cloud-tpu` .
      - Set `machineSpec.acceleratorType` to `TPU_V3` .
      - Set `machineSpec.acceleratorCount` to `8` for single TPU or `32+` for TPU Pods.
      - Set `replicaCount` to `1` .

For information about the regional availability of TPUs, see [Using accelerators](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators) .

### TPU v5e

[TPU v5e](https://docs.cloud.google.com/tpu/docs/v5e) requires JAX 0.4.6+, TensorFlow 2.15+, or PyTorch 2.1+. To configure a TPU VM with TPU v5e, specify the following fields in the `WorkerPoolSpec` :

  - Set `machineSpec.machineType` to `ct5lp-hightpu-1t` , `ct5lp-hightpu-4t` , or `ct5lp-hightpu-8t` .
  - Set `machineSpec.tpuTopology` to a supported topology for the machine type. For details, see the following table.
  - Set `replicaCount` to `1` .

The following table shows the TPU v5e machine types and topologies that are supported for custom training:

| *Machine Type*     | *Topology* | *Number of TPU chips* | *Number of VMs* | *Recommended use case*         |
| ------------------ | ---------- | --------------------- | --------------- | ------------------------------ |
| `ct5lp-hightpu-1t` | 1x1        | 1                     | 1               | Small to medium scale training |
| `ct5lp-hightpu-4t` | 2x2        | 4                     | 1               | Small to medium scale training |
| `ct5lp-hightpu-8t` | 2x4        | 8                     | 1               | Small to medium scale training |
| `ct5lp-hightpu-4t` | 2x4        | 8                     | 2               | Small to medium scale training |
| `ct5lp-hightpu-4t` | 4x4        | 16                    | 4               | Large-scale training           |
| `ct5lp-hightpu-4t` | 4x8        | 32                    | 8               | Large-scale training           |
| `ct5lp-hightpu-4t` | 8x8        | 64                    | 16              | Large-scale training           |
| `ct5lp-hightpu-4t` | 8x16       | 128                   | 32              | Large-scale training           |
| `ct5lp-hightpu-4t` | 16x16      | 256                   | 64              | Large-scale training           |

Custom training jobs running on TPU v5e VMs are optimized for throughput and availability. For more information see [v5e Training accelerator types](https://docs.cloud.google.com/tpu/docs/v5e-training#accelerator-types) .

For information about the regional availability of TPUs, see [Using accelerators](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators) . For more information about TPU v5e, see [Cloud TPU v5e training](https://docs.cloud.google.com/tpu/docs/v5e-training) .

Machine type comparison:

| *Machine Type*           | *ct5lp-hightpu-1t* | *ct5lp-hightpu-4t* | *ct5lp-hightpu-8t* |
| ------------------------ | ------------------ | ------------------ | ------------------ |
| Number of v5e chips      | 1                  | 4                  | 8                  |
| Number of vCPUs          | 24                 | 112                | 224                |
| RAM (GB)                 | 48                 | 192                | 384                |
| Number of NUMA nodes     | 1                  | 1                  | 2                  |
| Likelihood of preemption | High               | Medium             | Low                |

### TPU v6e

[TPU v6e](https://docs.cloud.google.com/tpu/docs/v6e) requires Python 3.10+, JAX 0.4.37+, PyTorch 2.1+ using PJRT as the default runtime, or TensorFlow using only the tf-nightly runtime version 2.18+. To configure a TPU VM with TPU v6e, specify the following fields in the `WorkerPoolSpec` :

  - Set `machineSpec.machineType` to `ct6e` .
  - Set `machineSpec.tpuTopology` to a supported topology for the machine type. For details, see the following table.
  - Set `replicaCount` to `1` .

The following table shows the TPU v6e machine types and topologies that are supported for custom training:

| *Machine Type*     | *Topology* | *Number of TPU chips* | *Number of VMs* | *Recommended use case*         |
| ------------------ | ---------- | --------------------- | --------------- | ------------------------------ |
| `ct6e-standard-1t` | 1x1        | 1                     | 1               | Small to medium scale training |
| `ct6e-standard-8t` | 2x4        | 8                     | 1               | Small to medium scale training |
| `ct6e-standard-4t` | 2x2        | 4                     | 1               | Small to medium scale training |
| `ct6e-standard-4t` | 2x4        | 8                     | 2               | Small to medium scale training |
| `ct6e-standard-4t` | 4x4        | 16                    | 4               | Large-scale training           |
| `ct6e-standard-4t` | 4x8        | 32                    | 8               | Large-scale training           |
| `ct6e-standard-4t` | 8x8        | 64                    | 16              | Large-scale training           |
| `ct6e-standard-4t` | 8x16       | 128                   | 32              | Large-scale training           |
| `ct6e-standard-4t` | 16x16      | 256                   | 64              | Large-scale training           |

For information about the regional availability of TPUs, see [Using accelerators](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators) . For more information about TPU v6e, see [Cloud TPU v6e training](https://docs.cloud.google.com/tpu/docs/v6e-intro) .

Machine type comparison:

| *Machine Type*           | *ct6e-standard-1t* | *ct6e-standard-4t* | *ct6e-standard-8t* |
| ------------------------ | ------------------ | ------------------ | ------------------ |
| Number of v6e chips      | 1                  | 4                  | 8                  |
| Number of vCPUs          | 44                 | 180                | 180                |
| RAM (GB)                 | 48                 | 720                | 1440               |
| Number of NUMA nodes     | 2                  | 1                  | 2                  |
| Likelihood of preemption | High               | Medium             | Low                |

### TPU 7x

[TPU7x](https://docs.cloud.google.com/tpu/docs/tpu7x) requires Python 3.12+.

We recommend the following stable combination for functionality tests and workload migration:

  - JAX + JAX Lib: `jax-0.8.1.dev20251104` , `jaxlib-0.8.1.dev2025104`
  - Stable libtpu: `libtpu-0.0.27`

To configure a TPU VM with TPU 7x, specify the following fields in the `WorkerPoolSpec` :

  - Set `machineSpec.machineType` to `tpu7x-standard-4t` .
  - Set `machineSpec.tpuTopology` to a supported topology for the machine type. For details, see the following table.
  - Set `replicaCount` to `1` .

The following table shows the TPU 7x topologies that are supported for custom training. All topologies use the `tpu7x-standard-4t` machine type.

| *Topology* | *Number of TPU chips* | *Number of VMs* | *Scope*     |
| ---------- | --------------------- | --------------- | ----------- |
| 2x2x1      | 4                     | 1               | Single-host |
| 2x2x2      | 8                     | 2               | Multi-host  |
| 2x2x4      | 16                    | 4               | Multi-host  |
| 2x4x4      | 32                    | 8               | Multi-host  |
| 4x4x4      | 64                    | 16              | Multi-host  |
| 4x4x8      | 128                   | 32              | Multi-host  |
| 4x8x8      | 256                   | 64              | Multi-host  |
| 8x8x8      | 512                   | 128             | Multi-host  |
| 8x8x16     | 1024                  | 256             | Multi-host  |

For information about the regional availability of TPUs, see [Using accelerators](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#accelerators) . For more information about TPU7x, see [Cloud TPU7x training](https://docs.cloud.google.com/tpu/docs/tpu7x-training) .

### Example `CustomJob` specifying a TPU VM

The following example highlights how to specify a TPU VM when you create a `CustomJob` :

### gcloud

To specify a TPU VM using the gcloud CLI tool, you must use a [`config.yaml` file](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/create#--config) . Select one of the following tabs to see an example:

### TPU v2/v3

    workerPoolSpecs:
      machineSpec:
        machineType: cloud-tpu
        acceleratorType: TPU_V2
        acceleratorCount: 8
      replicaCount: 1
      containerSpec:
        imageUri: CUSTOM_CONTAINER_IMAGE_URI

### TPU v5e

    workerPoolSpecs:
      machineSpec:
        machineType: ct5lp-hightpu-4t
        tpuTopology: 4x4
      replicaCount: 1
      containerSpec:
        imageUri: CUSTOM_CONTAINER_IMAGE_URI

Then run a command like the following:

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --config=config.yaml

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

To specify a TPU VM using the Agent Platform SDK for Python, see the following example:

    from google.cloud.aiplatform import aiplatform
    
    job = aiplatform.CustomContainerTrainingJob(
        display_name='DISPLAY_NAME',
        location='us-west1',
        project='PROJECT_ID',
        staging_bucket="gs://CLOUD_STORAGE_URI",
        container_uri='CONTAINER_URI')
    
    job.run(machine_type='ct5lp-hightpu-4t', tpu_topology='2x2')

For more information about creating a custom training job, see [Create custom training jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

## Boot disk options

You can optionally customize the boot disks for your training VMs. All VMs in a worker pool use the same type and size of boot disk.

  - **To customize the type of boot disk that each training VM uses,** specify the [`diskSpec.bootDiskType` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#diskspec) in your `WorkerPoolSpec` .
    
    You can set this field to one of the following:
    
      - `pd-standard` to use a standard persistent disk backed by a standard hard drive
      - `pd-ssd` to use an SSD persistent disk backed by a solid-state drive
      - [`hyperdisk-balanced`](https://docs.cloud.google.com/compute/docs/disks/hyperdisks) for higher IOPS and throughput rates.
    
    The default value is `pd-ssd` ( `hyperdisk-balanced` is the default for `a3-ultragpu-8g` and `a4-highgpu-8g` ).
    
    Using `pd-ssd` or [`hyperdisk-balanced`](https://docs.cloud.google.com/compute/docs/disks/hyperdisks#machine-type-support) might improve performance if your training code reads and writes to disk. Learn about [disk types](https://docs.cloud.google.com/compute/docs/disks#disk-types) . Also see [hyperdisk supported machines](https://docs.cloud.google.com/compute/docs/disks/hyperdisks#machine-type-support) .

  - **To customize the size (in GB) of the boot disk that each training VM uses,** specify the [`diskSpec.bootDiskSizeGb` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#diskspec) in your `WorkerPoolSpec` .
    
    You can set this field to an integer between 100 and 64,000, inclusive. The default value is `100` .
    
    You might want to increase the boot disk size if your training code writes a lot of temporary data to disk. Note that any data you write to the boot disk is temporary, and you can't retrieve it after training completes.

Changing the type and size of your boot disks affects [custom training pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#training) .

The following examples highlight where you can specify boot disk options when you create a `CustomJob` :

### Console

In the Google Cloud console, you can't create a `CustomJob` directly. However, you can [create a `TrainingPipeline` that creates a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#create) . When you create a `TrainingPipeline` in the Google Cloud console, you can specify boot disk options for each worker pool on the **Compute and pricing** step, in the **Disk type** drop-down list and the **Disk size (GB)** field.

### gcloud

To specify boot disk options using the Google Cloud CLI tool, you must use a [`config.yaml` file](https://docs.cloud.google.com/sdk/gcloud/reference/ai/custom-jobs/create#--config) . For example:

#### `config.yaml`

    workerPoolSpecs:
      machineSpec:
        machineType: MACHINE_TYPE
      diskSpec:
        bootDiskType: DISK_TYPE
        bootDiskSizeGb: DISK_SIZE
      replicaCount: REPLICA_COUNT
      containerSpec:
        imageUri: CUSTOM_CONTAINER_IMAGE_URI

Then run a command like the following:

    gcloud ai custom-jobs create \
      --region=LOCATION \
      --display-name=JOB_NAME \
      --config=config.yaml

For more context, read the [guide to creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

## What's next

  - Learn how to [create a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-overview) to run custom training jobs.
  - Learn how to perform custom training by [creating a `CustomJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .
