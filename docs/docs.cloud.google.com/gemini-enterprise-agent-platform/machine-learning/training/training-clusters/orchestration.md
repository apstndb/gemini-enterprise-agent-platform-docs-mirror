---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/orchestration
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/orchestration
title: Orchestration
description: Orchestrate Gemini Enterprise Agent Platform training clusters workloads with Slurm. Configure job scheduling, preemption, and resource accounting parameters.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters, contact your sales representative for access.

Gemini Enterprise Agent Platform training clusters uses [Simple Linux Utility for Resource Management](https://slurm.schedmd.com/documentation.html) (Slurm) as the orchestrator for managing and scheduling jobs on your cluster.

Slurm is a widely-used, open-source cluster management and job scheduling system known for its scalability and fault tolerance.

## Key capabilities of Slurm

  - Slurm allocates a set of compute nodes for the exclusive use of a specific job for a defined period. This ensures a job has dedicated access to the resources it needs to run without interference.
  - Slurm provides a framework for managing the complete lifecycle of a job—from submission and execution to monitoring and completion. This system is specifically designed to handle parallel jobs that run across a set of allocated nodes.
  - Slurm maintains a queue of pending jobs, using a sophisticated prioritization engine to arbitrate access to compute resources. By considering factors like job size, user priority, and wait time, this system ensures fair and efficient resource utilization across the cluster.

## Basic cluster configuration

Before you can run jobs, you must define the fundamental structure of your Slurm cluster. This section details the essential configuration settings, including how to organize compute nodes into partitions, specify a dedicated login node pool, and configure a shared home directory for your users.

### Partitions

Partitions group nodes into logical sets, which can be useful for managing different machine types or access tiers. They are defined as a list within the partitions field of the `slurm_spec` .

Each partition object has the following required fields:

  - `id` : A unique identifier for the partition.
  - `node_pool_ids` : A list containing the IDs of one or more node pools that belong to this partition.

For example:

    "partitions": [
      {
        "id": "a4",
        "node_pool_ids": [ "a4" ]
      }
    ]

### Login nodes

The login node pool provides dedicated nodes that serve as the primary entry point for users to interact with the cluster. The `login_node_pool_id` field specifies the unique identifier for this pool.

For example:

    "login_node_pool_id": "login"

### Home directory storage

The `home_directory_storage` field specifies the Filestore instance to be mounted as the `/home` directory on all nodes in the cluster. This provides a shared, persistent home directory for all users.

You must provide the full resource name of the Filestore instance for this value.

For example:

    "home_directory_storage": "projects/PROJECT_ID/locations/REGION-ZONE/instances/FILESTORE_INSTANCE_NAME"

## Advanced Slurm configuration

Gemini Enterprise Agent Platform training clusters lets you customize a select set of `slurm.conf` parameters, but be aware that these settings can only be configured during initial cluster creation and can't be changed afterward.

### Accounting

Gemini Enterprise Agent Platform training clusters lets you use built-in accounting features to track resource usage within your cluster. For a complete guide on how to monitor metrics like job-specific CPU time and memory usage, review the official [Slurm accounting documentation](https://slurm.schedmd.com/accounting.html) .

| Parameter                                                                                          | Value                   | Example                   |
| :------------------------------------------------------------------------------------------------- | :---------------------- | :------------------------ |
| [AccountingStorageEnforce](https://slurm.schedmd.com/slurm.conf.html#OPT_AccountingStorageEnforce) | Comma-separated strings | `associations,limits,qos` |

### Preemption and priority

To manage how jobs are scheduled and prioritized, Gemini Enterprise Agent Platform training clusters lets you configure Slurm's job preemption. Preemption works with the multifactor priority plugin to determine if running jobs should be paused to make way for higher-priority work.

For a complete conceptual overview, review the official Slurm documentation on the [multifactor priority plugin](https://slurm.schedmd.com/priority_multifactor.html) and [preemption](https://slurm.schedmd.com/preempt.html) .

#### Preemption parameters

| Parameter                                                                                | Value                   | Example                  |
| :--------------------------------------------------------------------------------------- | :---------------------- | :----------------------- |
| [PREEMPT\_TYPE](https://slurm.schedmd.com/slurm.conf.html#OPT_PreemptType)               | String                  | `preempt/partition_prio` |
| [PREEMPT\_MODE](https://slurm.schedmd.com/slurm.conf.html#OPT_PreemptMode_1)             | Comma-separated strings | `SUSPEND,GANG`           |
| [PREEMPT\_EXEMPT\_TIME](https://slurm.schedmd.com/slurm.conf.html#OPT_PreemptExemptTime) | String                  | `00:00:00`               |

#### Priority parameters

| Parameter                                                                                            | Value                   | Example                |
| :--------------------------------------------------------------------------------------------------- | :---------------------- | :--------------------- |
| [PRIORITY\_TYPE](https://slurm.schedmd.com/slurm.conf.html#OPT_PriorityType)                         | String                  | `priority/multifactor` |
| [PRIORITY\_WEIGHT\_AGE](https://slurm.schedmd.com/slurm.conf.html#OPT_PriorityWeightAge)             | Integer                 | `0`                    |
| [PRIORITY\_WEIGHT\_ASSOC](https://slurm.schedmd.com/slurm.conf.html#OPT_PriorityWeightAssoc)         | Integer                 | `0`                    |
| [PRIORITY\_WEIGHT\_FAIRSHARE](https://slurm.schedmd.com/slurm.conf.html#OPT_PriorityWeightFairshare) | Integer                 | `0`                    |
| [PRIORITY\_WEIGHT\_JOB\_SIZE](https://slurm.schedmd.com/slurm.conf.html#OPT_PriorityWeightJobSize)   | Integer                 | `0`                    |
| [PRIORITY\_WEIGHT\_PARTITION](https://slurm.schedmd.com/slurm.conf.html#OPT_PriorityWeightPartition) | Integer                 | `0`                    |
| [PRIORITY\_WEIGHT\_QOS](https://slurm.schedmd.com/slurm.conf.html#OPT_PriorityWeightQOS)             | Integer                 | `0`                    |
| [PRIORITY\_WEIGHT\_TRES](https://slurm.schedmd.com/slurm.conf.html#OPT_PriorityWeightTRES)           | Comma-separated strings | `cpu=100,mem=150`      |

### Prolog and epilog scripts

You can configure custom Bash scripts to run automatically at the start (prolog) and end (epilog) of each job using the following fields:

  - `prolog_bash_scripts` : A list of strings, where each string contains the full content of a Bash script to be executed before the job begins.
  - `epilog_bash_scripts` : A list of strings, where each string contains the full content of a Bash script to be executed after the job completes.

This is useful for setting up a unique job environment or performing automated cleanup tasks.

### Example cluster specification

The following example shows a complete JSON configuration for creating a training cluster. You can adapt this specification for your own needs.

    {
      // ... other cluster configurations ...
      "orchestratorSpec": {
        "slurmSpec": {
          "partitions": [
            {
              "id": "a4",
              "node_pool_ids": ["a4"]
            }
          ],
          "login_node_pool_id": "login",
          "home_directory_storage": "projects/PROJECT_ID/locations/REGION-ZONE/instances/FILESTORE_INSTANCE_ID",
          "accounting": {
            "accounting_storage_enforce": "ACCOUNTING_STORAGE_ENFORCE"
          },
          "scheduling": {
            "priority_type": "PRIORITY_TYPE",
            "priority_weight_age": PRIORITY_WEIGHT_AGE,
            "priority_weight_assoc": PRIORITY_WEIGHT_ASSOC,
            "priority_weight_fairshare": PRIORITY_WEIGHT_FAIRSHARE,
            "priority_weight_job_size": PRIORITY_WEIGHT_JOB_SIZE,
            "priority_weight_partition": PRIORITY_WEIGHT_PARTITION,
            "priority_weight_qos": PRIORITY_WEIGHT_QOS,
            "priority_weight_tres": "PRIORITY_WEIGHT_TRES",
            "preempt_type": "PREEMPT_TYPE",
            "preempt_mode": "PREEMPT_MODE",
            "preempt_exempt_time": "PREEMPT_EXEMPT_TIME"
          },
          "prolog_bash_scripts": [
            "#!/bin/bash\necho 'First prolog script running'",
            "#!/bin/bash\necho 'Second prolog script running'"
          ],
          "epilog_bash_scripts": [
            "#!/bin/bash\necho 'Epilog script running'"
          ]
          // ... other Slurm settings ...
        }
      }
    }

### Cluster management and operations

**Managing a running cluster**

Once your cluster is created with the chosen accounting and preemption settings, you can use Slurm's command-line tools to manage user accounts and monitor job scheduling.

**Account management with `sacctmgr`**

The `sacctmgr` command is the primary tool for managing user and account information in the Slurm database. For example, to add a new user to an account and grant them access to a partition, run the following command:

    sudo sacctmgr add User Accounts=<account> Partition=<partition> <user>

For a comprehensive list of all `sacctmgr` options, review the official [Slurm accounting documentation](https://slurm.schedmd.com/sacctmgr.html) .

**Checking job priority**

To check the priority components of each job in the queue, use the `sprio` utility. This is useful for understanding why certain jobs are scheduled to run before others.

See the [`sprio` utility](https://slurm.schedmd.com/sprio.html) documentation for detailed usage.

**Preemption examples**

The official Slurm documentation provides several working examples of different preemption strategies. You can find these on the [Slurm Preemption](https://slurm.schedmd.com/preempt.html#example1) page.

## What's next

The following focuses on the final steps of the machine learning lifecycle: managing, deploying, and monitoring your trained models.

  - Deploy your model for inference: Deploy your trained model to a Vertex AI endpoint to serve online inference requests at scale.
      - [Deploy a model to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment)
  - Manage your model's lifecycle: Use Gemini Enterprise Agent Platform Model Registry to version, compare, and manage your models. A pipeline can be configured to automatically register a new model upon successful training.
      - [Introduction to Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/vertex-ai/machine-learning/model-registry/introduction)
  - Monitor your pipeline runs and model performance:
      - Pipeline Monitoring: Track the execution graph, artifacts, and performance of your pipeline runs to debug issues and optimize your orchestration.
          - [Visualize and analyze pipeline results](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/visualize-pipeline)
      - Model Monitoring: After deployment, set up monitoring to detect drift and anomalies in your model's prediction performance, which helps maintain the model's accuracy over time.
          - [Introduction to Gemini Enterprise Agent Platform Model Monitoring](https://docs.cloud.google.com/vertex-ai/machine-learning/model-monitoring/overview)
  - Optimize costs and manage the cluster lifecycle: When using automated pipelines, manage the cluster's lifecycle by considering run frequency.
      - For infrequent runs, add a final pipeline step to [delete the cluster](https://docs.cloud.google.com/vertex-ai/machine-learning/training/training-clusters/manage-cluster#delete-a-cluster:) to save costs. This typically involves creating a [custom pipeline component](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-own-components) that calls the delete function.
      - For frequent runs, leave the cluster active to reduce job startup time.
