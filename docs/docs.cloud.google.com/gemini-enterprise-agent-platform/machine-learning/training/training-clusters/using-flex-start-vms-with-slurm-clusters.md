---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/using-flex-start-vms-with-slurm-clusters
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/using-flex-start-vms-with-slurm-clusters
title: Using Flex Start VMs with Slurm cluster
description: Configure Flex Start VMs with Slurm clusters on Agent Platform. Implement flexible VM provisioning models, manage IAM permissions, and define node pool specifications for training workloads.
data_source: docs.cloud.google.com
---

This guide provides instructions for configuring and using Flex Start VMs with Slurm on Gemini Enterprise Agent Platform. This integration lets you use flexible VM provisioning models for your training workloads.

## Configuration and cluster creation

Before defining the cluster's configuration, you must first complete the following one-time prerequisite step to ensure the necessary service accounts are authorized to manage Flex Start resources.

### Verify permissions for the Google APIs Service Agent

  - Context: Slurm on Gemini Enterprise Agent Platform uses managed instance groups to dynamically provision Flex Start VM instances and manage their lifecycle. The Google APIs Service Agent creates and manages the underlying Compute Engine resources for the managed instance group. As detailed in the [Managed instance groups and IAM documentation](https://docs.cloud.google.com/compute/docs/access/iam#managed-instance-groups-and-iam) , this service account requires permissions to create, delete, and list VM instances, as well as permission to attach a service account identity to them.
  - Action: Check if your Google APIs Service Agent ( `  PROJECT_NUMBER  ` @cloudservices.gserviceaccount.com) already has the Editor role ( `roles/editor` ).
      - If "yes": You likely don't need to take further action. The Editor role typically includes all necessary permissions.
      - If "no": If the default Editor role isn't granted, you have to explicitly grant the following roles to ensure the MIG can function:
          - Compute Instance Admin (v1) ( `roles/compute.instanceAdmin.v1` ) - Required for creating, listing, and deleting VM instances.
          - Service Account User ( `roles/iam.serviceAccountUser` ) - Required for attaching a service account to the new VMs.

### Creating a Slurm cluster with Flex Start provisioning model

To create a Slurm cluster that uses the Flex Start provisioning model, you must specify the `provisioning_model` within the node pool configuration of your cluster specification when submitting your cluster creation request using the API.

**Example Configuration Snippet:** Save the following JSON configuration to a file named `cluster_config.json` . This example explicitly uses a `slurm_spec` . Replace the placeholders (for example, `<project-id>, <region>, <zone>` ) with your actual values.

    {
      "display_name": "flexvm",
      "name": "projects/<project-id>/locations/<region>/modelDevelopmentClusters/",
      "network": {
        "network": "projects/<project-id>/global/networks/default",
        "subnetwork": "projects/<project-id>/regions/<region>/subnetworks/default"
      },
      "node_pools": [
        {
          "id": "login",
          "machine_spec": { "machine_type": "n2-standard-8" },
          "scaling_spec": { "min_node_count": 1, "max_node_count": 1 },
          "enable_public_ips": "true",
          "zone": "<zone>",
          "boot_disk": { "boot_disk_type": "pd-standard", "boot_disk_size_gb": 120 }
        },
        {
          "id": "a3u",
          "machine_spec": {
            "machine_type": "a3-ultragpu-8g",
            "accelerator_type": "NVIDIA_H200_141GB",
            "accelerator_count": 8
          },
          "provisioning_model": "FLEX_START",
          "flex_start_max_duration": "604800s",
          "scaling_spec": { "min_node_count": 0, "max_node_count": 2 },
          "zone": "<zone>",
          "enable_public_ips": "true",
          "boot_disk": { "boot_disk_type": "hyperdisk-balanced", "boot_disk_size_gb": 400 }
        }
      ],
      "orchestrator_spec": {
        "slurm_spec": {
          "home_directory_storage": "projects/<project-id>/locations/<zone>/instances/<filestore-id>",
          "partitions": [ { "id": "a3u", "node_pool_ids": [ "a3u" ] } ],
          "login_node_pool_id": "login"
        }
      }
    }

Follow the steps in [Create a Slurm cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster) to authenticate and submit the request.

**Maximum Flex Start Duration:** You can optionally set the maximum run duration for your Flex Start instances. Use the `flex_start_max_duration` field in your node pool configuration, specifying the value as a string in seconds, appended with an "s" (for example, "172800s" for 2 days). If omitted, the system defaults to 7 days.

## Operational lifecycle and resiliency

Understanding the lifecycle of Flex Start nodes in a Slurm on Gemini Enterprise Agent Platform environment is critical for planning your jobs.

### Flex Start constraints

All Flex Start VMs have a fixed maximum run duration, which is defined by the `flex_start_max_duration` setting.

  - Duration Limit: By default, the `flex_start_max_duration` is set to 7 days. You can override this limit by specifying a custom `flex_start_max_duration` between 30 seconds and a maximum of 7 days (604,800 seconds) in your node pool configuration to better match your expected job runtimes.
  - Termination: When this limit is reached, Compute Engine strictly terminates the instance.

### Node scaling behavior

The following sections describe the two available scaling strategies: static and dynamic.

#### Static node

Static nodes let you maintain a fixed pool of resources that are always available (for example, `min_node_count > 0` ).

  - Provisioning: Nodes are requested immediately upon cluster creation or resizing to meet the minimum node count.
  - Expiration and recovery: When a static Flex Start node reaches its `flex_start_max_duration` and is terminated by Compute Engine, the system automatically attempts to recreate the node to restore the defined cluster capacity. This cycle ensures the static pool remains populated, regardless of whether a Slurm job is waiting on the nodes.

#### Dynamic node

Dynamic nodes let the cluster scale up only when needed.

  - Provisioning: When a job is queued (entering a `PENDING` state), the Slurm Scheduler requests resources by creating a managed instance group and issuing a resize request.
  - Expiration and recovery: Upon expiration, the system provisions a new Flex Start node only if a Slurm job is pending on the nodes.

> **Note:** The system doesn't automatically save the application state. To resume progress from where it left off, your training job must implement checkpointing and restoration logic.

### Cluster resiliency and auto-repair

Slurm on Gemini Enterprise Agent Platform monitors node health at key stages of the job lifecycle. Health checks are run both before a job starts (the prolog) and after it completes (the epilog) to help maintain job stability.

  - Hardware error handling: If the service detects critical hardware issues (such as GPU errors), it's designed to automatically repair the unhealthy VM.
  - Automatic replacement: If the job is still in a PENDING state (or has been requeued to PENDING due to the node failure), the system automatically provisions a new Flex Start instance to replace the unhealthy VM. This lets your workload proceed on healthy hardware without manual intervention.
