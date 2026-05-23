---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-train
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-train
title: Run Gemini Enterprise Agent Platform serverless training jobs on a persistent resource
description: Run a Gemini Enterprise Agent Platform serverless training job on a persistent resource using the {{dynamic_data.site_values.cloud_name_short}} console, Google Cloud CLI, Agent Platform SDK for Python, or the REST API.
data_source: docs.cloud.google.com
---

This page shows you how to run a serverless training job on a persistent resource by using the Google Cloud CLI, Agent Platform SDK for Python, and the REST API.

Normally, when you [create a serverless training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) , you need to specify compute resources that the job creates and runs on. After you create a persistent resource, you can instead configure the serverless trainingjob to run on one or more resource pools of that persistent resource. Running a custom training job on a persistent resource significantly reduces the job startup time that's otherwise needed for compute resource creation.

## Required roles

To get the permission that you need to run serverless trainingjobs on a persistent resource, ask your administrator to grant you the [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `aiplatform.customJobs.create` permission, which is required to run serverless trainingjobs on a persistent resource.

You might also be able to get this permission with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create a training job that runs on a persistent resource

To create a serverless training job that runs on a persistent resource, make the following modifications to the standard instructions for [creating a serverless training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) :

### gcloud

  - Specify the `--persistent-resource-id` flag and set the value to the ID of the persistent resource ( PERSISTENT\_RESOURCE\_ID ) that you want to use.
  - Specify the `--worker-pool-spec` flag such that the values for `machine-type` and `disk-type` matches exactly with a corresponding resource pool from the persistent resource. Specify one `--worker-pool-spec` for single node training and multiple for distributed training.
  - Specify a `replica-count` less than or equal to the `replica-count` or `max-replica-count` of the corresponding resource pool.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def create_custom_job_on_persistent_resource_sample(
        project: str,
        location: str,
        staging_bucket: str,
        display_name: str,
        container_uri: str,
        persistent_resource_id: str,
        service_account: Optional[str] = None,
    ) -> None:
        aiplatform.init(
            project=project, location=location, staging_bucket=staging_bucket
        )
    
        worker_pool_specs = [{
            "machine_spec": {
                "machine_type": "n1-standard-4",
                "accelerator_type": "NVIDIA_TESLA_K80",
                "accelerator_count": 1,
            },
            "replica_count": 1,
            "container_spec": {
                "image_uri": container_uri,
                "command": [],
                "args": [],
            },
        }]
    
        custom_job = aiplatform.CustomJob(
            display_name=display_name,
            worker_pool_specs=worker_pool_specs,
            persistent_resource_id=persistent_resource_id,
        )
    
        custom_job.run(service_account=service_account)

### REST

  - Specify the `persistent_resource_id` parameter and set the value to the ID of the persistent resource ( PERSISTENT\_RESOURCE\_ID ) that you want to use.
  - Specify the `worker_pool_specs` parameter such that the values of `machine_spec` and `disk_spec` for each resource pool matches exactly with a corresponding resource pool from the persistent resource. Specify one `machine_spec` for single node training and multiple for distributed training.
  - Specify a `replica_count` less than or equal to the `replica_count` or `max_replica_count` of the corresponding resource pool, excluding the replica count of any other jobs running on that resource pool.

## What's next

  - [Learn about persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-overview) .
  - [Create and use a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-create) .
  - [Get information about a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-get) .
  - [Reboot a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-reboot) .
  - [Delete a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-delete) .
