---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/environment-setup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/environment-setup
title: Set up your environment
description: Set up an environment before launching a Agent Platform Neural Architecture Search experiment.
data_source: docs.cloud.google.com
---

Set up an environment before you launch a Agent Platform Neural Architecture Search experiment.

## Before you begin

1.  To grant all Agent Platform Neural Architecture Search Neural Architecture Search users the [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform) role ( `roles/aiplatform.user` ), contact your project administrator.

2.  [Install Docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/) .
    
    If you're using a Linux-based operating system, such as Ubuntu or Debian, add your username to the `docker` group so that you can run Docker without using `sudo` :
    
        sudo usermod -a -G docker ${USER}
    
    > **Caution** : The `docker` group is equivalent to the `root` user. For information about how this affects the security of your system, see [Docker's documentation](https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface) .
    
    You might need to restart your system after adding yourself to the `docker` group.

3.  Open Docker. To ensure that Docker is running, run the following Docker command, which returns the current time and date:
    
        docker run busybox date

4.  Use `gcloud` as the credential helper for Docker:
    
        gcloud auth configure-docker

5.  (Optional) If you want to run the container using GPU locally, install [`nvidia-docker`](https://github.com/NVIDIA/nvidia-docker#quickstart) .

### Set up your Cloud Storage bucket

This section demonstrates how to create a new bucket. You can use an existing bucket, but it must be in the same region where you are running AI Platform jobs. Additionally, if it isn't part of the project you are using to run Agent Platform Neural Architecture Search, you must explicitly grant access to the Agent Platform Neural Architecture Search service accounts.

1.  Specify a name for your new bucket. The name must be unique across all buckets in Cloud Storage.
    
        BUCKET_NAME="YOUR_BUCKET_NAME"
    
    For example, use your project name with `-vertexai-nas` appended:
    
        PROJECT_ID="YOUR_PROJECT_ID"
        BUCKET_NAME=${PROJECT_ID}-vertexai-nas

2.  Check the bucket name that you created.
    
        echo $BUCKET_NAME

3.  Select a region for your bucket and set a `REGION` environment variable.
    
    Use the same region where you plan on running Agent Platform Neural Architecture Search jobs.
    
    For example, the following code creates `REGION` and sets it to `us-central1` :
    
        REGION=us-central1

4.  Create the new bucket:
    
        gcloud storage buckets create gs://$BUCKET_NAME --location=$REGION

## Request additional device quota for the project

The [tutorials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/nas-tutorials) use approximately five CPU machines and don't require any additional quota. After running the tutorials, run your Agent Platform Neural Architecture Search job.

The Agent Platform Neural Architecture Search job trains a batch of models in parallel. Each trained model corresponds to a *trial* . Read the section on [setting the `number-of-parallel-trials`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/suggested-workflow#parallel_trials) to estimate the amount of CPUs and GPUs needed for a search job. For example, if each trial uses 2 T4 GPUs and you set `number-of-parallel-trials` to 20, then you need a total quota of 40 T4 GPUs for a search job. In addition, if each trial is using a `highmem-16` CPU, then you need 16 CPU units per trial, which is 320 CPU units for 20 parallel trials. *However we ask for a minimum of 10 parallel trial quota (or 20 GPU quota).* The default initial quota for GPUs *varies by region and GPU type* and is usually found to be 0, 6, or 12 for Tesla\_T4 and 0 or 6 for Tesla\_V100. The default initial quota for CPUs varies by region and is usually found to be 20, 450, or 2,200.

> **Note:** Agent Platform Neural Architecture Search currently doesn't support TPUs.

Optional: if you plan to run multiple search jobs in parallel, then scale the quota requirement. Requesting a quota doesn't charge you immediately. You are charged once you run a job.

> **Note:** The quota is requested per region. For example, you can't use `us-central1` quota for running jobs in `europe-west4` region.

If you don't have enough quota and try to launch a job which needs more resources than your quota, then the job won't launch giving an error which looks like:

    Exception: Starting job failed: {'code': 429, 'message': 'The following quota metrics exceed quota limits: aiplatform.googleapis.com/custom_model_training_cpus,aiplatform.googleapis.com/custom_model_training_nvidia_v100_gpus,aiplatform.googleapis.com/custom_model_training_pd_ssd', 'status': 'RESOURCE_EXHAUSTED', 'details': [{'@type': 'type.googleapis.com/google.rpc.DebugInfo', 'detail': '[ORIGINAL ERROR] generic::resource_exhausted: com.google.cloud.ai.platform.common.errors.AiPlatformException: code=RESOURCE_EXHAUSTED, message=The following quota metrics exceed quota limits: aiplatform.googleapis.com/custom_model_training_cpus,aiplatform.googleapis.com/custom_model_training_nvidia_v100_gpus,aiplatform.googleapis.com/custom_model_training_pd_ssd, cause=null [google.rpc.error_details_ext] { code: 8 message: "The following quota metrics exceed quota limits: aiplatform.googleapis.com/custom_model_training_cpus,aiplatform.googleapis.com/custom_model_training_nvidia_v100_gpus,aiplatform.googleapis.com/custom_model_training_pd_ssd" }'}]}

In some cases, if multiple jobs for the same project were started at the same time and the quota isn't sufficient for all of them, then one of the jobs remain in queued state and won't start training. In this case, cancel the queued job and either request more quota or wait until the previous job finishes.

You can request the additional device quota from the **Quotas** page. You can apply filters to find the desired quota to edit: ![Filter Quota](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/images/filter_quota.png)

1.  For **Service** , select **Agent Platform API** .
2.  For **region** , select the region you want to filter on.
3.  For **Quota** , select an accelerator name whose prefix is **Custom model training** .
      - For V100 GPUs, the value is **Custom model training Nvidia V100 GPUs per region** .
      - For CPUs, the value can be **Custom model training CPUs for N1/E2 machine types per region** . The number for the CPU represents the unit of CPUs. If you want 8 `highmem-16` CPUs, then make your quota request for 8 \* 16 = 128 CPU units. Also enter the desired value for **region** .

Once you create a quota request, you receive a `Case number` and follow up emails about the status of your request. A GPU quota approval might take approximately two to five business days to get approved. In general, getting a quota of approximately 20-30 GPUs should be faster to get approved in approximately two to three days and getting approval for approximately 100 GPUs might take five business days. A CPU quota approval might take up to two business days to get approved. However, if a region is experiencing a big shortage of a GPU type, then there is no guarantee even with a small quota ask. In this case, you might be asked to go for a different region or a different GPU type. In general, T4 GPUs are easier to get than V100s. T4 GPUs take more wall-clock time but are more cost effective.

For more information, see [Request a quota adjustment](https://docs.cloud.google.com/docs/quotas/help/request_increase) .

## Set up artifact registry for your project

You must set up an [artifact registry](https://cloud.google.com/artifact-registry/docs/overview#introduction) for your project and region where you push your docker images.

Go to the **Artifact Registry** page for your project. If not already enabled, enable the artifact registry API for your project first:

![Enable artifact registry](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/images/enable_artifact_registry.png)

Once enabled, start creating a new repository by clicking **CREATE REPOSITORY** :

![Create artifact registry](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/images/create_artifact_registry.png)

Choose **Name** as **nas** , **Format** as **Docker** , and **Location type** as **Region** . For **Region** , select the location where you run your jobs and then click **CREATE** .

![Artifact registry setting](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/images/artifact_registry_setting.png)

This should create your desired docker repository as shown below:

![Artifact registry created](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/images/artifact_registry_created.png)

You also need to set up authentication to push dockers to this repository. The [local environment set up section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/environment-setup#local-environment-setup) below contains this step.

## Set up your local environment

You can run these steps using the Bash shell in your local environment, or run them from a notebook in a Vertex AI Workbench instance.

1.  Set up basic environment variables:
    
        gcloud config set project PROJECT_ID
        gcloud auth login
        gcloud auth application-default login

2.  Set up [docker authentication](https://docs.cloud.google.com/artifact-registry/docs/docker/authentication#gcloud-helper) for your artifact registry:
    
        # example: REGION=europe-west4
        gcloud auth configure-docker REGION-docker.pkg.dev

3.  (Optional) Configure a Python 3 virtual environment. Python 3 usage is recommended but not required:
    
        sudo apt install python3-pip && \
        pip3 install virtualenv && \
        python3 -m venv --system-site-packages ~/./nas_venv && \
        source ~/./nas_venv/bin/activate

4.  Install additional libraries:
    
        pip install google-cloud-storage==2.6.0
        pip install pyglove==0.1.0

## Set up a service account

You must set up a [service account](https://docs.cloud.google.com/iam/docs/service-accounts) before running NAS jobs. You can run these steps using the Bash shell in your local environment, or run them from a notebook in a Vertex AI Workbench instance.

1.  Create a service account:
    
        gcloud iam service-accounts create NAME \
            --description=DESCRIPTION \
            --display-name=DISPLAY_NAME

2.  Grant the `aiplatform.user` and `storage.objectAdmin` role to the service account:
    
        gcloud projects add-iam-policy-binding PROJECT_ID \
            --member=serviceAccount:NAME@PROJECT_ID.iam.gserviceaccount.com \
            --role=roles/aiplatform.user
        gcloud projects add-iam-policy-binding PROJECT_ID \
            --member=serviceAccount:NAME@PROJECT_ID.iam.gserviceaccount.com \
            --role=roles/storage.objectAdmin

For example, the following commands create a service account named `my-nas-sa` under the project `my-nas-project` with the `aiplatform.user` and `storage.objectAdmin` role:

``` 
  gcloud iam service-accounts create my-nas-sa \
      --description="Service account for NAS" \
      --display-name="NAS service account"
  gcloud projects add-iam-policy-binding my-nas-project \
      --member=serviceAccount:my-nas-sa@my-nas-project.iam.gserviceaccount.com \
      --role=roles/aiplatform.user
  gcloud projects add-iam-policy-binding my-nas-project \
      --member=serviceAccount:my-nas-sa@my-nas-project.iam.gserviceaccount.com \
      --role=roles/storage.objectAdmin
```

## Download code

To start an Agent Platform Neural Architecture Search experiment, you need to download the sample Python code, which includes prebuilt trainers, search space definitions, and associated client libraries.

Run the following steps to download the source code.

1.  Open a new Shell Terminal.

2.  Run the Git clone command:
    
        git clone https://github.com/google/vertex-ai-nas.git
