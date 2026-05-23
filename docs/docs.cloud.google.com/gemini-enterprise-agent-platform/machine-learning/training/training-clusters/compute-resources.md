---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/compute-resources
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/compute-resources
title: Compute resources
description: Optimize AI/ML workloads. Select Vertex Model Development Service compute resources and configure cluster node pools with a4, a3, n2 machine types.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters, contact your sales representative for access.

Gemini Enterprise Agent Platform training clusters supports a variety of machine types to accommodate different workloads. You can choose from the following options when configuring your cluster node pools:

  - a4-highgpu-8g
  - a4x-highgpu-4g
  - a3-ultragpu-8g
  - a3-megagpu-8g
  - n2 CPU family

## A4X machine type

Gemini Enterprise Agent Platform training clusters support the [A4X accelerator-optimized machine type](https://docs.cloud.google.com/compute/docs/accelerator-optimized-machines#a4x-machine-type) (a4x-highgpu-4g), an exascale platform based on the [NVIDIA GB200 NVL72](https://www.nvidia.com/en-us/data-center/gb200-nvl72/) rack-scale architecture.

### Architectural comparison

The following table outlines the fundamental hardware differences between the A4X family and other accelerator-optimized families.

| Feature              | A4X (a4x-highgpu-4g) | A3 / A4H        |
| :------------------- | :------------------- | :-------------- |
| **CPU Architecture** | ARM                  | X86             |
| **GPU Count**        | 4 GPUs per node      | 8 GPUs per node |
| **Reservation Type** | All capacity mode    | Managed Mode    |
| **Placement Policy** | Strict (Compact)     | Flexible        |

### A4X specific guidelines

  - Your A4X node pool VM count must be a multiple of 18 (for example, 18, 36, 54). This is required because A4X capacity is provisioned in fixed, non-shareable 18-node blocks called NVLink domains. These domains are bound by a strict Compact Placement Policy, and any partially allocated blocks cannot be used by other clusters.
  - Due to the ARM-based architecture of A4X nodes, you must make two key changes to your training workloads:
      - Use ARM-Compatible images: All training jobs must use a container image that is built for the ARM architecture.
      - Adapt for 4 GPUs: Your distributed training logic must be updated to correctly recognize and use the 4 GPUs available on each A4X node.
  - Host Fault Reporting process and downtime When you report a host as faulty, be aware of the following recovery process:
      - No standby capacity: The system doesn't use a standby spare pool for an instant node replacement.
      - Repair-based recovery: The node remains unavailable until the underlying physical host is repaired.
      - Extended downtime: This repair process typically takes 3 to 14 days.

## Capacity provisioning

Choosing the right provisioning model is critical for balancing cost, speed, and resource availability. See the following provisioning options:

  - `RESERVATION` : Allocates nodes from a specific Compute Engine reservation that you've created in advance. This model ensures capacity and is the recommended choice for high-demand resources.

  - `FLEX_START` : Utilizes the Dynamic Workload Scheduler to queue your job. The job begins automatically as soon as the requested compute resources become available, offering a flexible start time without requiring a reservation.

  - `SPOT` : Provisions the node pool using Spot VMs. This is the most cost-effective option, but it should only be used for workloads that are fault-tolerant and can handle interruptions, as the VMs may be preempted at any time.

  - `ON_DEMAND` : This is the default option for CPU-only node pools and is best suited for machine types that are not scarce. It provides standard VM instances with predictable, pay-as-you-go pricing.

Use the following guidance to make your selection:

  - For high-demand GPU resources (like A3 and A4): The `RESERVATION` model is strongly recommended. It ensures you have dedicated access to the capacity you need for critical training jobs.

  - For bursty or flexible workloads: Consider `FLEX_START` or `SPOT` . `FLEX_START` queues your job until resources are available, while `SPOT` offers significant cost savings for fault-tolerant jobs that can handle preemption.

  - For abundant machine types: The `ON_DEMAND` model is the preferred choice. Use it for machine types that are not scarce and where immediate availability isn't a concern.

## Using a shared reservation (optional)

If you'd like to use a shared reservation, rather than a local reservation, there are additional steps to take before you can create a cluster.

Before using a shared reservation with Gemini Enterprise Agent Platform training clusters, make sure the shared reservation works by manually creating a VM that uses the shared reservation. If this VM creation works, move on to the next step. In the cluster creation configuration, use the reservation name in the following format: ` projects/ RESERVATION_HOST_PROJECT_ID /zones/ RESERVATION_ZONE /reservations/ RESERVATION_NAME  ` .

## What's next

After selecting the compute and provisioning options for your training cluster, you are ready to create the cluster and run a workload on it.

  - Create a Compute Engine reservation: The `RESERVATION` model is used for allocating high-demand resources like GPUs. Learn how to create a new reservation in Compute Engine to get dedicated access to your required resources.
      - [Learn how to create a reservation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-reservations)
  - Create your training cluster: Apply the configurations you've learned about by following the step-by-step guide to create your first persistent training cluster using the Agent Platform API or `gcloud` .
      - [Learn how to create a training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster)
  - Submit a training job to your cluster: Once your cluster is active, the next step is to run a workload. Submit a `CustomJob` that targets your persistent cluster for execution.
      - [Learn how to run a job on a training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job)
  - Adapt your code for distributed training: To take full advantage of a multi-node cluster, adapt your training code for a distributed environment.
      - [Learn about distributed training on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training)
