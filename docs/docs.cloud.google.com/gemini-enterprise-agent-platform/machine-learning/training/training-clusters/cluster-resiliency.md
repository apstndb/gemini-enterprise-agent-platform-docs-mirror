---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/cluster-resiliency
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/cluster-resiliency
title: Cluster resiliency
description: Learn about Gemini Enterprise Agent Platform training clusters resiliency. Use automated health checks and `reportFaultyNodes` API for compute node and Slurm job stability.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters, contact your sales representative for access.

Gemini Enterprise Agent Platform training clusters integrates a comprehensive health check system to ensure the reliability of compute nodes and the stability of your Slurm jobs. This system features both automated and manual recovery options. An automated process runs during job execution to monitor critical components like GPU health and disk usage, automatically replacing nodes that fail. For situations requiring user intervention, your training cluster provides a `reportFaultyNodes` API, letting you manually delete a specific faulty node or to report a suspected hardware failure on its underlying host.

## Run a test workload to verify GPU functionality

### Step 1: Connect to the cluster nodes using SSH

From Cloud Shell or the Google Cloud console, connect to the Login Node using IAP. The following example shows the command for Cloud Shell:

    gcloud compute ssh --zone $ZONE "Login Node Name" --tunnel-through-iap --project $PROJECT_ID

### Step 2: Run a standard Slurm command

After connecting to a login node, run a few standard Slurm commands to verify that the cluster is functioning correctly.

    ~$ sinfo
    PARTITION   AVAIL  TIMELIMIT  NODES  STATE NODELIST
    partition1*    up   infinite      2   idle hcsa3m1236-a3mnodeset-[0-1]

Next, submit a batch job.

    ~$ sbatch --qos normal --wrap "echo start! && sleep 10s && echo done!"

You should see that a slurm- job-id .out file is created in your home directory.

### Step 3: Run a GPU workload

Save the following content as a script file named `test.sh` in your home directory.

    #!/bin/bash
    #SBATCH --nodes=2
    #SBATCH --ntasks-per-node=1
    #SBATCH --cpus-per-task=4
    #SBATCH --gres=gpu:8
    #SBATCH --job-name=nvidia_smi
    
    srun nvidia-smi -L

Set the script's permissions to 755 to make it executable, then submit the Slurm job:

    ~$ sbatch ./test.sh

Slurm saves the script's output to a file named slurm- job-id .out.

Expected output:

    GPU 0: NVIDIA H100 80GB HBM3 (UUID: GPU-f75045e8-4d87-49d1-2eb9-39ec2baddf9b)
    GPU 1: NVIDIA H100 80GB HBM3 (UUID: GPU-b91556d8-5215-d0ed-50b8-a88720e5b29c)
    GPU 2: NVIDIA H100 80GB HBM3 (UUID: GPU-7600155a-0036-35f5-9489-a7b4ed0ce887)
    GPU 3: NVIDIA H100 80GB HBM3 (UUID: GPU-a402e125-7841-033f-f08b-7921526c121f)
    GPU 4: NVIDIA H100 80GB HBM3 (UUID: GPU-20eef8f8-b2c7-1716-5ce7-7f64475bd2c0)
    GPU 5: NVIDIA H100 80GB HBM3 (UUID: GPU-65463286-e587-b52f-4d5b-8880eecbf0e7)
    GPU 6: NVIDIA H100 80GB HBM3 (UUID: GPU-d5ff75e7-dd54-edf6-a684-33c26fc365e1)
    GPU 7: NVIDIA H100 80GB HBM3 (UUID: GPU-26e81ae2-11fd-9d7e-95b6-c186e5173007)
    GPU 0: NVIDIA H100 80GB HBM3 (UUID: GPU-e66a185a-b40c-81d9-d35d-19cab811df34)
    GPU 1: NVIDIA H100 80GB HBM3 (UUID: GPU-d23e5cf7-afd8-bec2-1487-9e27eeb6aae0)
    GPU 2: NVIDIA H100 80GB HBM3 (UUID: GPU-4dde1b05-ea5e-01e9-5c1e-e1c0d3b4b113)
    GPU 3: NVIDIA H100 80GB HBM3 (UUID: GPU-3a0d734a-6fb8-d841-a97f-d6846553ea7f)
    GPU 4: NVIDIA H100 80GB HBM3 (UUID: GPU-76fe0d37-08b2-a3a6-8ddf-55501426bc7c)
    GPU 5: NVIDIA H100 80GB HBM3 (UUID: GPU-9e0a41e1-b399-8934-01af-6198b749c02a)
    GPU 6: NVIDIA H100 80GB HBM3 (UUID: GPU-dddd09ee-c944-1098-9c4e-d96f8762ecb1)
    GPU 7: NVIDIA H100 80GB HBM3 (UUID: GPU-df52c109-0ac1-30cc-226b-85b1a8a6bc16)

## Cluster health verification

This section shows how to test your training cluster using the Cluster Health Scanner (CHS) tool, which is pre-installed on the training cluster image. The CHS tool checks the health of the cluster, running tests such as DCGM diagnostics and NCCL tests to verify that the cluster is ready to run your workloads.

> **Important:** The compute nodes must have outbound internet access for the DCGM diagnostic and cluster validation tests to succeed. Ensure that either public IP addresses are enabled for the compute nodes ( `"enable_public_ips": "true"` ) or a Cloud NAT gateway is deployed in the cluster's network.

From the login node of the cluster, you can run the following script to run tests using the CHS tool.

> **Note:** This script is written for a cluster with two A3 Ultra nodes, but it can be modified to fit your cluster setup.

    export CLUSTER_ID=<your_cluster_id>
    export PARTITION=a3u
    export MACHINE_TYPE=a3-ultragpu-8g
    cd ~
    /opt/cluster-health-scanner/deploy/slurm/cluster-validation.sh \
    --nodelist=${CLUSTER_ID}-${PARTITION}-[0-1] \
    --nodes=2 \
    --partition=${PARTITION} \
    --machine-type=${MACHINE_TYPE} \
    --relative-exec-path=../../opt/cluster-health-scanner/deploy/slurm \
    --results-dir=results

A successful test run provides two sets of results:

  - Summary Output: A brief summary is printed to the console, which should resemble the following example.
  - Detailed Logs: For a complete report, see the detailed logs saved in the `~/results` directory.

<!-- end list -->

    Starting DCGM Diagnostics...
    DCGM diagnostics passing on all nodes!
    Starting NCCL all_reduce_perf...
    CURR_NODES:  cluster-id-0
    cluster-id-1
    NCCL test passing on all nodes!

## Automated health checks and recovery

To ensure node reliability, training clusters continuously monitors node health using the following suite of automated checks. Training clusters runs health checks during the Slurm prolog (before a job starts) and epilog (after a job completes).

### Health check suite

  - GPU Health: Performs detailed, individual GPU diagnostics including `nvidia-smi` , `dcgmi` , and `xid` code monitoring.
  - Disk Usage: Checks for high disk usage on critical partitions ( `/` , `/mnt/localssd` , `/mnt/localdisk` ) to prevent jobs from failing due to lack of space.
  - Network Health: Verifies that primary network interfaces have an IPv4 address. If an issue is found, it attempts to self-heal by resetting the interface.
  - CPU Load: Monitors the system's load average and logs a warning if it exceeds a predefined threshold.

### Failure recovery process

If a check detects a severe, unrecoverable error, Gemini Enterprise Agent Platform training clusters automatically initiates a failure recovery process. The standard process involves draining the faulty nodes, requeuing the affected Slurm job, and then deleting and recreating the drained nodes to restore them to a healthy state.

This automated recovery is subject to the following conditions:

  - **Restart Limit** : The recovery process is skipped if the affected Slurm job has already been restarted a set number of times.

  - **GPU Utilization** : Node deletion and recreation is also skipped if the job running on the node doesn't use all of the available GPUs. In this case, the node is only drained to prevent new jobs from being scheduled on it.

## Manually managing faulty compute nodes

Training clusters provides APIs for manually reporting and managing faulty compute nodes, which is particularly useful if automated health checks don't resolve an issue. You can only run these operations on one node at a time.

| Action                    | Description                                                                               | Best For                                                                  |
| :------------------------ | :---------------------------------------------------------------------------------------- | :------------------------------------------------------------------------ |
| **Delete Node**           | Removes a specified faulty node from the cluster. This is the default action.             | General errors or when a node is unresponsive and needs to be recycled.   |
| **Report Host as Faulty** | Reports the underlying physical host as faulty, triggering a repair or migration process. | Suspected hardware failures on the physical machine hosting the GPU node. |

### Action 1: Delete a faulty node

This action deletes the specified node. The outcome of this operation depends on whether the node is classified as "static" or "dynamic" by Slurm:

  - Static Nodes: If a deleted node's index is less than the minimum node count of the node pool, a new compute node is recreated with the same name and specifications.

  - Dynamic Nodes: If a deleted node's index is greater than the minimum node count, it's only recreated if there is a pending workload scheduled for it. Otherwise, it is removed.

These examples use a `gcurl` alias, which is a convenient, authenticated shortcut for interacting with the API endpoints. The following command creates an alias for `curl` that includes the required authorization headers.  

    alias gcurl='curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json"'

##### API request to delete a node

To delete a faulty node, execute the following POST request. The `NODE_ID` should be in the format `  CLUSTER_ID - NODEPOOL_ID - INDEX  ` .

``` 
  gcurl -X POST https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID:reportFaultyNodes -d '{"nodeActions": [{"nodeId": "NODE_ID"}]}'
  
```

##### Check operation status

You can monitor the result of the `reportFaultyNodes` action by checking the operation status.

``` 
  gcurl https://REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/REGION/operations/OPERATION_ID
  
```

### Action 2: Report a host as faulty

> **Caution:** This is a pre-GA feature. Before reporting a host, thoroughly investigate the issue to identify the root cause. Only use this action if you have no other alternatives. Consult the report [faulty host documentation report](https://docs.cloud.google.com/ai-hypercomputer/docs/manage/report-faulty-host) and the Google Cloud support team before proceeding.

You can report the physical host of a GPU node as faulty if you suspect a hardware failure.

  - Supported VMs: A3 Ultra and A4 High-GPU

  - Node State: The target node must be in a `RUNNING` state before you call the API. It will transition to `REPAIRING` upon a successful call and return to `RUNNING` after the host is repaired or the node is recreated on a new host. This is a best-effort operation.

##### Prerequisite: Grant IAM role

To use this feature, you must grant the Compute Instance Admin (v1) ( `roles/compute.instanceAdmin.v1` ) role to the Agent Platform Service Agent.

``` 
  PROJECT_NUMBER=$(gcloud projects describe PROJECT_ID --format="value(projectNumber)")

  gcloud projects add-iam-policy-binding PROJECT_ID\
  --member="serviceAccount:service-PROJECT_NUMBER@gcp-sa-aiplatform.iam.iam.gserviceaccount.com" \
  --role="roles/compute.instanceAdmin.v1"
  
```

##### API request to report a host

Execute the following POST request to report the underlying host as faulty. When doing so, you must provide one or more observed behaviors and descriptions for the `faultReasons` .  
For the `behavior` field, you should use one of the following values:

| Behavior                  | Description                                                                                                                                                                                                              |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `PERFORMANCE`             | The GPUs attached to the VM have performance issues compared to other GPUs in the cluster, you see no XID errors in the logs, and Compute Engine detects no other usual failure patterns such as silent data corruption. |
| `SILENT_DATA_CORRUPTION`  | You see data corruption in your VM, but the VM keeps running. This can be due to issues like vCPU defects, software bugs, or kernel issues.                                                                              |
| `UNRECOVERABLE_GPU_ERROR` | You have identified an unrecoverable GPU error with an XID.                                                                                                                                                              |
| `BEHAVIOR_UNSPECIFIED`    | You are not sure what the issue with your VM is.                                                                                                                                                                         |

Here is an example of the API request.

``` 
gcurl -X POST \
  https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID:reportFaultyNodes \
  -d '{"nodeActions": [{"nodeId": "NODE_ID", "reportFaultyHost": {"faultReasons": [{"behavior": "BEHAVIOR_1", "description": "DESCRIPTION_1"}, {"behavior": "BEHAVIOR_2", "description": "DESCRIPTION_2"}]}}]}'
  
```

## Putting it all together

By leveraging both automated health checks and the manual controls detailed on this page, you're able to maintain a highly resilient training environment. Proactively managing the health of your cluster by deleting faulty nodes or reporting hardware issues ensures maximum uptime and the successful completion of your training jobs. For persistent or complex issues, always consider consulting with the Google Cloud support team for in-depth diagnostics and assistance.

## What's next

Configuring your training cluster for fault tolerance is a key step in building a complete, production-ready MLOps workflow.

  - Monitor and debug your training jobs: Track the progress, resource utilization, and health of your training jobs, including how to identify when a node has been recovered or a job has been restarted due to a failure.
      - [Monitor training jobs on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/monitoring-metrics)
  - Orchestrate your resilient jobs with Gemini Enterprise Agent Platform Pipelines: For production environments, use Gemini Enterprise Agent Platform Pipelines to create an automated, repeatable workflow that submits your resilient training jobs to your cluster.
      - [Learn about orchestrating jobs on a training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/orchestration)
  - Manage and deploy your model: Once your resilient training job is complete, use Gemini Enterprise Agent Platform Model Registry to version your model artifact before deploying the model to an endpoint to serve online inference requests.
      - [Introduction to Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction)
      - [Deploy a model to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment)
