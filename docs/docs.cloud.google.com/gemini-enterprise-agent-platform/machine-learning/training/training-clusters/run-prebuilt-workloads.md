---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/run-prebuilt-workloads
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/run-prebuilt-workloads
title: Run prebuilt workloads
description: Leverage the NVIDIA NeMo ecosystem on a Managed Training cluster for end-to-end generative AI model development, including pre-training, fine-tuning, and reinforcement learning.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform Managed Training, contact your sales representative for access.

This guide shows you how to use the NVIDIA NeMo ecosystem on a Managed Training cluster for end-to-end generative AI model development. It provides step-by-step instructions for the following distinct but related workflows, each covered in its own dedicated section:

  - [NVIDIA NeMo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/run-prebuilt-workloads#nvidia-nemo) : For foundational model development, follow these instructions to perform large-scale pre-training, continuous pre-training (CPT), and supervised fine-tuning (SFT).
  - [NVIDIA NeMo-RL](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/run-prebuilt-workloads#nvidia-nemo-rl) : For model alignment and preference tuning, use this section to apply advanced techniques like Reinforcement Learning (RL) to align your model with human instructions and preferences.

Whether you're building a model from scratch or refining an existing one, this document guides you through setting up your environment, managing containerized jobs, and launching training scripts on the cluster.

## NVIDIA NeMo

The [NVIDIA NeMo framework](https://docs.nvidia.com/nemo-framework/user-guide/latest/overview.html) is an end-to-end platform for building, customizing, and deploying generative AI models. This section of the guide is specifically for developers and researchers focused on the foundational stages of model development. It provides step-by-step instructions for using NeMo to perform large-scale pre-training, continuous pre-training (CPT), and supervised fine-tuning (SFT) on a Managed Training cluster.

This training clusters guide provides the complete workflow for running a training job with the NeMo framework. The process is divided into two main parts: the initial one-time setup of your environment and the recurring steps for launching a job.

### Set up your environment

Before launching a job, you need to prepare your environment by ensuring you have a container image and the necessary training scripts.

#### Install NeMo-Run

    pip install git+https://github.com/NVIDIA/NeMo-Run.git

#### Prepare a container image

You have two options for the container image: use a prebuilt image (recommended) or build a custom one.

##### Use a prebuilt image (recommended)

Prebuilt container images are provided in the `.squashfs` format. Copy the appropriate image for your region into your working directory.

    # Example for the US region
    gcloud storage cp gs://vmds-containers-us/vmds_nemo_squashfs/nemo-20250721.sqsh .

##### Build a customized container (advanced)

Follow these steps only if the prebuilt containers don't meet your needs. This procedure guides you through converting a custom container image into the `.squashfs` format using `enroot` .

Step 1: Authenticate with Google Cloud.

Use the following commands to ensure that both your Google Cloud user account and the Docker registry where your image is hosted are authenticated:

    gcloud auth login
    gcloud auth configure-docker us-docker.pkg.dev

> **Important:** The address used here ( `us-docker.pkg.dev` ) is an example for an Artifact Registry repository. This address must match the hostname of the registry where your image is stored (for example, an Artifact Registry or Container Registry address). For example, if your image URI is `gcr.io/my-project/my-image` , you must use `gcr.io` .

Step 2: Create the conversion script.

Create a file named `enroot-convert.sh` and add the following script content. Before running this script, you must update the `REMOTE_IMG` and `LOCAL_IMG` variables to point to your container image and your chosen output path.

    #!/bin/bash
    
    #SBATCH --gpus-per-node=8
    #SBATCH --exclusive
    #SBATCH --mem=0
    #SBATCH --ntasks-per-node=1
    
    # Run this script on the slurm login node:
    # sbatch -N 1 enroot-convert.sh
    
    set -x
    set -e
    
    # The remote docker image URI.
    REMOTE_IMG="docker://us-docker.pkg.dev/{YOUR_CONTAINER_IMG_URI}:{YOUR_CONTAINER_IMAGE_TAG}"
    
    # The local path to the to be imported enroot squash file.
    LOCAL_IMG="${HOME}/my_nemo.sqsh"
    
    # The path to the enroot config file.
    TMP_ENROOT_CONFIG_PATH="/tmp/\$(id -u --name)/config/enroot"
    
    # Download the docker image to each node.
    srun -l -N "${SLURM_NNODES}" \
    bash -c "
    mkdir -p ${TMP_ENROOT_CONFIG_PATH};
    echo 'machine us-docker.pkg.dev login oauth2accesstoken password $(gcloud auth print-access-token)' > ${TMP_ENROOT_CONFIG_PATH}/.credentials;
    rm -f ${LOCAL_IMG};
    ENROOT_CONFIG_PATH=${TMP_ENROOT_CONFIG_PATH} ENROOT_MAX_PROCESSORS=$(( $(nproc) / 2 )) enroot import -o ${LOCAL_IMG} ${REMOTE_IMG};
    "

Step 3: Run the script and verify the output.

Execute the script on the Slurm login node.

    sbatch -N 1 enroot-convert.sh

After the job completes, find the conversion logs in a file named `slurm-<JOB_ID>` .out and the final container image at the path you specified for `LOCAL_IMG` .

#### Download the training recipes

The training recipes are stored in a private `googlesource.com` repository. To access them with the Git command line, you must first generate authentication credentials.

1.  **Generate authentication credentials** .
    
    Visit the following URL and follow the on-screen instructions. This configures your local environment to authenticate with the repository. <https://www.googlesource.com/new-password>

2.  **Clone the repository** .
    
    Once the credentials are authenticated, run the following command to download the recipes.
    
        git clone -b release-allowlist-ga https://vertex-model-garden.googlesource.com/vertex-oss-training

### Launch a training job

Once your environment is set up, you can launch a training job.

Step 1: Set environment variables

The following environment variables may be required for your job:

  - The `HF_TOKEN` is required to download models and datasets from Hugging Face.
  - The `WANDB_API_KEY` is required to use [Weights & Biases](https://docs.wandb.ai/) for experiment analysis.

<!-- end list -->

    export HF_TOKEN=YOUR_HF_TOKEN
    export WANDB_API_KEY=YOUR_WANDB_API_KEY

Step 2: Run the launch script

Navigate to your working directory and run the `run.py` script to start a job. This example kicks off a demo training job with Llama 3.1-2b.

    # Set the working directory
    export WORK_DIR=$HOME/vertex-oss-training/nemo
    cd $WORK_DIR
    
    gcloud storage cp
    gs://vmds-containers-<region>/vmds_nemo_squashfs/nemo-20250721.sqsh nemo-demo.sqsh
    
    # Launch the training job
    export NEMORUN_HOME=$WORK_DIR && \
    python3 run.py -e slurm --slurm-type hcc-a3m --partition a3m \
      -d $WORK_DIR -i $WORK_DIR/nemo-demo.sqsh \
      -s pretrain/llama3p1_2b_pt.py -n 2 \
      --experiment-name nemo-demo-run

### Launch parameters

  - `--slurm-type` is set based on the cluster type (for example, `hcc-a3m` , `hcc-a3u` , `hcc-a4` ).
  - `--partition` must be set to an available partition. You can check partition names with the `sinfo` command.
  - The `run.py` script automatically mounts several directories to the Docker container, including `--log-dir` , `--cache-dir` , and `--data-dir` , if they are set.

### Monitoring job status and logs

After you launch the job, a status block is displayed:

    Experiment Status for nemo-demo-run_1753123402
    
    Task 0: nemo-demo-run
    - Status: RUNNING
    - Executor: SlurmExecutor on @localhost
    - Job id: 75
    - Local Directory: $NEMORUN_HOME/experiments/nemo-demo-run/nemo-demo-run_1753123402/nemo-demo-run

The execution logs are written to the path shown in the `Local Directory` field from the status output. For example, you can find the log files at a path similar to this:

    $NEMORUN_HOME/experiments/nemo-demo-run/nemo-demo-run_1753123402/nemo-demo-run/<JOB_ID>.log

### Common errors and solutions

This section describes common issues that may arise during job execution and provides recommended steps to resolve them.

**Invalid partition error**

By default, jobs attempt to launch on the general partition. If the general partition doesn't exist or isn't available, the job will fail with the following error:

    sbatch: error: invalid partition specified: general
    sbatch: error: Batch job submission failed: Invalid partition name specified

Solution:

Specify an available partition using the `--partition` or `-p` argument in your launch command. To see a list of available partitions, run the `sinfo` command on the Slurm login node.

    sinfo

The output shows the available partition names, such as `a3u` in this example:

| PARTITION | AVAIL | TIMELIMIT | NODES | STATE  | NODELIST          |
| :-------- | :---- | :-------- | :---- | :----- | :---------------- |
| a3u\*     | up    | infinite  | 2     | idle\~ | alice-a3u-\[2-3\] |
| a3u\*     | up    | infinite  | 2     | idle   | alice-a3u-\[0-1\] |

**Tokenizer download error**

You may encounter an OSError related to a cross-device link when the script attempts to download the GPT2 tokenizer:

    OSError: [Errno 18] Invalid cross-device link: 'gpt2-vocab.json' -> '/root/.cache/torch/megatron/megatron-gpt-345m_vocab'

Solutions:

You have two options to resolve this issue:

  - Option \#1: Rerun the job. This error is often transient. Rerunning the job using the same `--cache-dir` may resolve the issue.
  - Option \#2: Manually download the tokenizer files. If rerunning the job fails, follow these steps:
      - Download the following two files:
          - `gpt2-vocab.json`
          - `gpt2-merges.txt`
      - Move the downloaded files into the `torch/megatron/` subdirectory within your cache directory (for example, `<var>YOUR_CACHE_DIR</var>/torch/megatron/` ).
      - Rename the files as follows:
          - Rename `gpt2-vocab.json` to `megatron-gpt-345m_vocab` .
          - Rename `gpt2-merges.txt` to `megatron-gpt-345m_merges` .

## NVIDIA NeMo-RL

The [NVIDIA NeMo-RL](https://docs.nvidia.com/nemo/rl/latest/about/overview.html) framework is designed to align large language models with human preferences and instructions. This section guides you through using NeMo-RL on a cluster to perform advanced alignment tasks, including supervised fine-tuning (SFT), preference-tuning (such as Direct Preference Optimization, or DPO), and Reinforcement Learning (RL).

The guide covers two primary workflows: running a standard batch training job and using the interactive development environment for debugging.

### Prerequisites

Before you begin, create a cluster by following the instructions on the [Create cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster) page, or use an existing Managed Training cluster, if you have one.

### Connect to the cluster login node

To connect to the cluster's login node, find the correct Google Cloud CLI command by navigating to the [Google Compute Engine Virtual Machine](https://console.cloud.google.com/compute/instances) page in the Google Google Cloud console and clicking SSH \> View Google Cloud CLI command. It will look similar to this:

    ssh $USER_NAME@machine-addr

Example:

    ssh $USER_NAME@nic0.sliua3m1-login-001.europe-north1-c.c.infinipod-shared-dev.internal.gcpnode.com

### Use the prebuilt Docker image

Converted `.sqsh` files are provided for prebuilt container images. You can select a container for your region and either set it directly as the container image parameter or download it to the cluster's file system.

To directly set it as the container image param, use one of the following paths. Note that you should replace `<region>` with your specific region (for example, `europe` , `asia` , `us` ):

    /gcs/vmds-containers-<region>/vmds_nemo_rl_squashfs/nemo_rl-h20260302.sqsh

To download the image to the cluster's lustre storage, use the following command:

    gs://vmds-containers-<region>/vmds_nemo_rl_squashfs/nemo_rl-h20260302.sqsh DESTINATION

### Download code

In order to get access to the training recipe with git CLI, visit <https://www.googlesource.com/new-password> . The recipe can be downloaded with the following command:

    cd $HOME
    git clone -b release-allowlist-ga https://vertex-model-garden.googlesource.com/vertex-oss-training

### Launch jobs

Step 1: Set environment variables.

To pull models and data from Hugging Face, the `HF_TOKEN` may need to be set. To use Weights & Biases for experiment analysis, the `WANDB_API_KEY` needs to be set. Update these variables in the following file:

File to update: `$HOME/vertex-oss-training/nemo_rl/configs/auth.sh`

If you don't want to use Weights & Biases, set the `logger.wandb_enabled` to `False` in your launch script.

Step 2: Download or copy the container file to your launch folder.

Here are some examples.

    gcloud storage cp \
      gs://vmds-containers-<region>/vmds_nemo_rl_squashfs/nemo_rl-h20260302.sqsh \
      $HOME/vertex-oss-training/nemo_rl/nemo_rl-h20260302.sqsh
    
    
    # OR
    
    /gcs/vmds-containers-<region>/vmds_nemo_rl_squashfs/nemo_rl-h20260302.sqsh \
      $HOME/vertex-oss-training/nemo_rl/nemo_rl-h20260302.sqsh
    
    cd $HOME/vertex-oss-training/nemo_rl/
    
    # Where region is either `us`, `asia`, or `europe`

Step 3: Prepare or Clone the NeMo-RL repository.

Create a clone of the NeMo-RL code if not already present. Note that you may need to use `git submodule update --init --recursive` if you've already cloned the repository without the `--recursive` flag.

    git clone https://github.com/NVIDIA-NeMo/RL --recursive

Step 4: Launch the training job.

    sbatch -N <num_nodes> launch.sh --cluster_type hcc-a3m --job_script algorithms/dpo.sh

Where:

  - `--cluster-type` is set based on the cluster type:
      - A3-Mega: `hcc-a3m`
      - A3-Ultra: `hcc-a3u`
      - A4: `hcc-a4`
      - A3H: `hcc-a3h`
  - `--partition` should be set accordingly, where `sinfo` can be used to check the slurm partitions.

After your job starts, a new directory named after its SLURM Job ID are created in your current location. Inside, you'll find all the logs and checkpoints belonging to this job. More precisely, inside that you'll find the following directories and files:

  - `checkpoints/` → This directory is mounted inside the NeMo-RL container and contains all of the checkpoints from the training.
  - `ray-logs/` → This directory contains the logs from ray head and ray workers.
  - `nemo_rl_output.log` → This file contains the Slurm logs from your submitted job.
  - `attach.sh` (Interactive jobs only) → This is a bash script which lets you attach to an interactive job. If your job is launched successfully, it might take a couple of minutes for this file to be created.

### Development with NeMo-RL

**Interactive Setup**

Two options are available for quick interactive development with NeMo-RL.

#### nemorlinteractive

This is a straightforward helper command which lets you choose a GPU node from the cluster (let's say node number 5), and then it takes you to a running container for NeMo-RL inside your selected node. This command is helpful for your single node workflows.

In order to use `nemorlinteractive` , you need to follow these prerequisite steps:

1.  Provide all auth tokens you want (for example, HF and WandB) loaded to the job in the `configs/auth.sh` file.

2.  Set the `CLUSTER_TYPE` environment variable according to the following guideline:
    
        export CLUSTER_TYPE="hcc-a3m" # --> if you have A3-Mega cluster
        export CLUSTER_TYPE="hcc-a3u" # --> if you have A3-Ultra cluster
        export CLUSTER_TYPE="hcc-a4"  # --> If you have A4 cluster
        export CLUSTER_TYPE="hcc-a3h" # --> If you have A3H cluster

3.  Import `nemorlinteractive` in your bash terminal by sourcing the `bash_utils.sh` :
    
        source bash_utils.sh

4.  Run the `nemorlinteractive` command. For example:
    
        # Assuming you want to take the compute node number 5.
        nemorlinteractive 5

#### Interactive launch

This option lets you run workloads interactively on multiple compute nodes. Interactive jobs are most suitable for debugging and verification use cases. These workloads reserve the node indefinitely until the developer decides that the debugging has concluded and they want to release the resources.

The following are the steps that need to be followed for this option:

Provide all auth tokens you want (for example HF and WandB) loaded to the job in the `configs/auth.sh` file.

    sbatch -N <num_nodes> launch.sh --cluster_type hcc-a3m --interactive

  - Wait for 2-5 minutes and you should see `<job_id>/attach.sh` created.

  - To monitor progress of the launch check `<job_id>/nemo_rl_output.log` to see the progress of the launch script and check `<job_id>/ray_logs/` to see the progress of ray head and workers launch.

  - Connect to the interactive job. This script lets you connect again even if you lose connection:

<!-- end list -->

    bash <job_id>/attach.sh

## What's next

Running a prebuilt workload verifies the cluster's operational status. The next step is to run your own custom training application.

  - Run your own custom workload: Package your training code into a container and submit the container as a `CustomJob` to your training cluster. This process includes configuring the job for a distributed environment.
      - [Learn how to run a distributed training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training)
  - Monitor your training jobs: Effectively track the progress, resource utilization, and logs for the jobs running on your cluster using the the Google Cloud console or Cloud Logging.
      - [Monitor training jobs on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/monitoring-metrics)
  - Manage your cluster: After running your tests, check the status of your cluster or delete it to manage costs.
      - [Learn how to manage your training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster)
  - Orchestrate jobs with Gemini Enterprise Agent Platform Pipelines: After running jobs manually, automate the process by creating a pipeline to orchestrate your training workflows.
      - [Learn about orchestrating jobs on a training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/orchestration)
