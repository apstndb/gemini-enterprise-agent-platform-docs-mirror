---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/nas-client
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/neural-architecture-search/nas-client
title: Neural Architecture Search client library
description: Learn about the Agent Platform Neural Architecture Search Neural Architecture Search client library.
data_source: docs.cloud.google.com
---

This document describes the Agent Platform Neural Architecture Search Neural Architecture Search client library.

Agent Platform Neural Architecture Search client (in [`vertex_nas_cli.py`](https://github.com/google/vertex-ai-nas/blob/main/vertex_nas_cli.py) ) wraps the job management API and facilitates the Agent Platform Neural Architecture Search development. It provides the following subcommands:

  - `vertex_nas_cli.py build` : builds Agent Platform Neural Architecture Search containers and pushes to [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/overview) .
  - `vertex_nas_cli.py run_latency_calculator_local` : runs latency calculator locally for Agent Platform Neural Architecture Search stage-1 search job.
  - `vertex_nas_cli.py search_in_local` : runs Agent Platform Neural Architecture Search job locally on your machine with a randomly sampled architecture.
  - `vertex_nas_cli.py search` : runs Agent Platform Neural Architecture Search job with stage-1 search and stage-2 training on Google Cloud.
  - `vertex_nas_cli.py search_resume` : resumes a previous Agent Platform Neural Architecture Search job on Google Cloud.
  - `vertex_nas_cli.py list_trials` : lists Agent Platform Neural Architecture Search trials for specific job.
  - `vertex_nas_cli.py train` : trains searched model architecture (trial) in Google Cloud.

## Build

Run the following command to see the list of arguments supported by `vertex_nas_cli.py build` :

    python3 vertex_nas_cli.py build -h

> **Note:** Instead of building with Dockerfile, you can also use other tools like `bazel` to build the trainer, and use it with the Agent Platform Neural Architecture Search service.

If `--trainer_docker_id` is specified, it builds the trainer docker from the docker file specified by the flag `--trainer_docker_file` . The docker is built with full URI `gcr.io/project_id/trainer_docker_id` and pushed to [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/overview) .

If `--latency_calculator_docker_id` is specified, it builds the latency calculator docker from the docker file specified by the flag `--latency_calculator_docker_file` . The docker is built with full URI `gcr.io/project_id/latency_calculator_docker_id` and pushed to [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/overview) .

Instead of building with Dockerfile, you can also use other tools like `bazel` to build the trainer, and use it with the Agent Platform Neural Architecture Search service.

## Run latency calculator local

Run the following command to see the list of arguments supported by `vertex_nas_cli.py run_latency_calculator_local` :

    python3 vertex_nas_cli.py run_latency_calculator_local -h

## Search in local

Run the following command to see the list of arguments supported by `vertex_nas_cli.py search_in_local` :

    python3 vertex_nas_cli.py search_in_local -h

You need to specify either `--search_space_module` or `--prebuilt_search_space` so that [`vertex_nas_cli.py`](https://github.com/google/vertex-ai-nas/blob/main/vertex_nas_cli.py) internally generates a random model architecture to use.

This command will run the docker `gcr.io/project_id/trainer_docker_id:latest` on your local machine with a randomly sampled architecture.

You can pass through the flags to be used by the container after `--search_docker_flags` . For example, you can pass through `--training_data_path` and `validation_data_path` to the container:

    python3 vertex_nas_cli.py search_in_local \
    --project_id=${PROJECT_ID} \
    --trainer_docker_id=${TRAINER_DOCKER_ID} \
    --prebuilt_search_space=spinenet \
    --use_prebuilt_trainer=True \
    --local_output_dir=${JOB_DIR} \
    --search_docker_flags \
    training_data_path=/test_data/test-coco.tfrecord \
    validation_data_path=/test_data/test-coco.tfrecord \
    model=retinanet

## Search

Run the following command to see the list of arguments supported by `vertex_nas_cli.py search` :

    python3 vertex_nas_cli.py search -h

You need to specify either `--search_space_module` or `--prebuilt_search_space` so that [`vertex_nas_cli.py`](https://github.com/google/vertex-ai-nas/blob/main/vertex_nas_cli.py) internally creates `search_space_spec` .

The machines to run Agent Platform Neural Architecture Search jobs can be specified by `--accelerator_type` . For more information or to customize for your own needs, like using more GPUs, see `add_machine_configurations` .

Use the flags with prefix `train_` to set the stage-2 training related parameters.

## Search Resume

Run the following command to see the list of arguments supported by `vertex_nas_cli.py search_resume` :

    python3 vertex_nas_cli.py search_resume -h

You can resume a previously run search job by passing `previous_nas_job_id` and optionally `previous_latency_job_id` . The `previous_latency_job_id` flag is needed only if your previous search job involved a Google Cloud latency job. If instead of a Google Cloud latency job you used an on-premises latency calculator, then you have to run that on-premises latency calculator job separately again. The previous search job should not itself be a resume job. The region for the search resume job should be the same as for the previous search job. An example `search_resume` command looks like the following:

    python3 vertex_nas_cli.py search_resume \
      --project_id=${PROJECT} \
      --region=${REGION} \
      --job_name="${JOB_NAME}" \
      --previous_nas_job_id=${previous_nas_job_id} \
      --previous_latency_job_id=${previous_latency_job_id} \
      --root_output_dir=${GCS_ROOT_DIR} \
      --max_nas_trial=2 \
      --max_parallel_nas_trial=2 \
      --max_failed_nas_trial=2

## List trials

Run the following command to see the list of arguments supported by `vertex_nas_cli.py list_trials` :

    python3 vertex_nas_cli.py list_trials -h

> **Note:** The `job_id` flag is different from the `job_name` flag. The `job_id` is a unique numeric number assigned to the Agent Platform Neural Architecture Search job.

## Train

Run the following command to see the list of arguments supported by `vertex_nas_cli.py train` :

    python3 vertex_nas_cli.py train -h

## Proxy-task variance measurement

Run the following command to see the list of arguments supported by `vertex_nas_cli.py measure_proxy_task_variance` :

    python3 vertex_nas_cli.py measure_proxy_task_variance -h

## Proxy-task model selection

Run the following command to see the list of arguments supported by `vertex_nas_cli.py select_proxy_task_models` :

    python3 vertex_nas_cli.py select_proxy_task_models -h

## Proxy-task search

Run the following command to see the list of arguments supported by `vertex_nas_cli.py search_proxy_task` :

    python3 vertex_nas_cli.py search_proxy_task -h
