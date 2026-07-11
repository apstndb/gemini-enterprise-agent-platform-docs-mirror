---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/change-machine-type
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/change-machine-type
title: Change machine type and configure GPUs of an Agent Platform Workbench instance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page shows you how to change the machine type and GPU configuration of a Gemini Enterprise Agent Platform Workbench instance.

## Overview

The machine type determines some specifications of your Agent Platform Workbench instance, such as the amount of memory, virtual cores, and persistent disk limits. Changing the machine type can improve performance or help avoid errors caused by high memory utilization.

GPUs provide hardware acceleration that can improve the performance of your notebook code. You may want to add or increase the number of GPUs for greater performance, or, to reduce the cost of running your Agent Platform Workbench instance, you may want to remove GPUs.

## Before you change a machine type or GPU configuration

Consider the following before you make any changes to your Agent Platform Workbench instance's machine types or GPU configuration.

### Billing implications

Each machine type and GPU configuration is billed at a different rate. Make sure you understand the [pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#notebooks) implications of making a change. For example, an `e2-highmem-2` machine type costs more than an `e2-standard-2` machine type.

### Changing between G2 and non-G2 machine types not supported

Changing between a [G2 machine type](https://docs.cloud.google.com/compute/docs/accelerator-optimized-machines#g2-vms) and a non-G2 machine type isn't supported. If your instance has a G2 machine type, you can only change the machine type to a different G2 machine type. If your instance has a non-G2 machine type, you can change the machine type to a different non-G2 machine type, such as an E2 or N2 machine type.

### Moving to a smaller machine type

If you move from a machine type with more resources to a machine type with fewer resources, such as moving from an `e2-standard-8` machine type to an `e2-standard-2` , you might run into hardware resource issues or performance limitations because smaller machine types are less powerful than larger machine types.

### Make a backup

It's good practice to make regular backups of your instance's persistent disk data using snapshots. Consider [taking a snapshot](https://docs.cloud.google.com/compute/docs/disks/create-snapshots#creating_snapshots) of your persistent disk data before you change the machine type. If you want to make sure the new machine type is able to support the data on the existing instance, you can take a persistent disk snapshot and use it to start a second instance with the new machine type to confirm that the instance starts up successfully.

## Change the machine type and configure GPUs

> **Note:** To change the machine type or GPUs for an Agent Platform Workbench instance, you must [shut down the Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/shut-down) .

To change the machine type or configure the GPUs on an Agent Platform Workbench instance, complete the following steps.

1.  In the Google Cloud console, go to the **Instances** page.

2.  In the **Notebook name** column, click the name of the instance that you want to modify.
    
    The **Notebook details** page opens.

3.  Click the **Hardware** tab.

4.  In the **Modify hardware configuration** section, select the **Machine type** that you want to use.

5.  If there are GPUs available for your instance's combination of zone, environment, and machine type, you can configure the GPUs. In the **GPUs** section, select the **GPU type** and **Number of GPUs** that you want to use. [Learn more about GPU regions and zone availability](https://docs.cloud.google.com/compute/docs/gpus/gpu-regions-zones) .

6.  If you haven't already installed the required GPU drivers on your instance, select **Install NVIDIA GPU driver automatically for me** to install the drivers automatically on next startup.

7.  After Agent Platform Workbench has finished updating the machine type and GPU configuration, you can start your Agent Platform Workbench instance.

## What's next

  - Learn more about the available [GPU platforms](https://docs.cloud.google.com/compute/docs/gpus) .
