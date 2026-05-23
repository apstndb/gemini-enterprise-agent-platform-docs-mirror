---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/overview
title: Gemini Enterprise Agent Platform training clusters overview
description: Provides an overview of Gemini Enterprise Agent Platform training clusters.
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters, contact your sales representative for access.

Gemini Enterprise Agent Platform training clusters is a service from Google Cloud designed to simplify and accelerate the largest and most complex AI/ML workloads. It's specifically built to address challenges in large-scale training, such as complex cluster configuration, framework optimization, handling hardware failures, and integrating disparate toolsets.

## Key value proposition and features

Gemini Enterprise Agent Platform training clusters offers several core benefits:

  - **Open-source Slurm UX and cluster transparency** : Gemini Enterprise Agent Platform training clusters provides familiar, flexible tools to launch and manage jobs through an open-source Slurm user experience. Slurm is an industry standard known for optimized GPU scheduling, automated fault tolerance, and simplified parallel job launch.

  - **Automated cluster setup and configuration** : Gemini Enterprise Agent Platform training clusters automates the setup and configuration of clusters, aiming to transition from reservation to production training in hours. Users can create clusters using the Google Cloud console (using reference architectures or step-by-step configuration) or through API calls with JSON files.

  - **Preconfigured data science recipes and workflows** : Gemini Enterprise Agent Platform training clusters includes purpose-built tooling and optimized training recipes to jumpstart training for popular use cases like Llama and Gemma models, covering pre-training, SFT (Supervised Fine-Tuning), and Reinforcement Learning (RL). These recipes are preconfigured for state-of-the-art (SOTA) performance on Google Cloud Infrastructure, demonstrating significant performance gains.

  - **Hardware resiliency and high uptime** : Gemini Enterprise Agent Platform training clusters is designed with hardware resiliency to boost cluster uptime. It automatically resolves hardware issues, detects and triages various failure modes (for example, correctness checks, speed checks, Error-Correcting Code (ECC) errors, NVIDIA Data Center GPU Manager (DCGM) checks, disk space capacity), and triggers remediation actions such as restarting, reimaging, or replacing faulty nodes, and resuming from checkpoints. This helps mitigate the significant cost increase and delays caused by job interruptions and hardware failures in large-scale training.

  - **Architecture and components** : Gemini Enterprise Agent Platform training clusters runs on [Compute Engine infrastructure](https://docs.cloud.google.com/kubernetes-engine/distributed-cloud/bare-metal/docs/try/admin-user-gce-vms) supporting GPUs and CPUs. It leverages a managed Slurm orchestrator for deploying and managing compute nodes, including login and worker nodes. The service integrates with other Google Cloud services such as networking and storage.

  - **MLOps and Observability** : Integrates with Vertex ML Ops tools like Gemini Enterprise Agent Platform Model Registry for automatic registration, tracking, and versioning of trained workflows, and Vertex AI Inference for deployment with autoscaling and automated metrics. Training clusters also features automatic observability integration with Vertex AI TensorBoard to visualize training processes, track metrics, and identify issues early.

Training clusters can be created, retrieved, listed, updated and deleted using the Gemini Enterprise Agent Platform training clusters API. After cluster creation, users can validate its functionality by logging into nodes, running basic Slurm commands (for example, `sinfo` , `sbatch` ), and executing GPU-related workloads (for example, `nvidia-smi` ). The [Cluster Health Scanner (CHS) tool](https://docs.cloud.google.com/ai-hypercomputer/docs/troubleshooting/test-clusters) is pre-installed for running diagnostics like DCGM and NCCL tests to verify cluster readiness.

Gemini Enterprise Agent Platform training clusters provides an API for launching **prebuilt LLM jobs** using optimized recipes for models like Llama and Gemma, supporting pre-training and continuous pre-training from checkpoints. Job monitoring is possible by logging into the login node and examining output files and Slurm commands like `squeue` .

## Terminology

This section provides definitions for key terms and concepts essential to understanding and effectively utilizing Gemini Enterprise Agent Platform training clusters. These terms span core service components, architectural considerations, integrated storage technologies, and fundamental machine learning (ML) and MLOps concepts that underpin your training environment.

### Core service concepts

##### node

  - A single virtual machine (Compute Engine instance) within a cluster. In the context of Managed Training on reserved clusters, a node refers to an individual virtual machine (VM) that serves as a single unit of computation within your cluster. Think of it as one of the dedicated worker machines that runs a portion of your overall training job. Each node is equipped with specific resources like CPU, memory, and accelerators (for example, A3 or A4 GPUs), and they all work together in a coordinated way to handle large-scale, distributed training tasks.

##### login node

  - A login node is the main entry point for a user to access the cluster, submit jobs, and manage files. For more information, see [What is high performance computing?](https://cloud.google.com/discover/what-is-high-performance-computing) .

##### partition

  - In Slurm, a logical grouping of nodes, often used to separate nodes with different hardware configurations.

##### recipe

  - In the context of Managed Training, a recipe is a comprehensive and reusable package that contains everything needed to execute a specific large-scale training workload.

##### Slurm cluster

  - A collection of Compute Engine instances, managed by Slurm, that includes a login node and multiple worker nodes configured for running training jobs. For more information, see [Slurm workload manager](https://slurm.schedmd.com/overview.html) .

##### worker node

  - A worker node refers to an individual machine or computational instance within a cluster that's responsible for executing tasks or performing work. In systems like Kubernetes or Ray clusters, nodes are the fundamental units of compute. For more information, see [What is high performance computing (HPC)?](https://cloud.google.com/discover/what-is-high-performance-computing) .

### Architecture and networking

##### consumer VPC network

  - A consumer VPC network is a Google Cloud Virtual Private Cloud (VPC) that privately accesses a service hosted in another VPC (known as the producer VPC). For more information, see [Private Service Connect](https://cloud.google.com/vpc/docs/private-service-connect#producers-and-consumers) .

##### Maximum transmission unit (MTU)

  - The largest size of a data packet that a network-connected device can transmit. Larger MTU sizes (jumbo frames) can improve network performance for certain workloads. For more information, see [Maximum transmission unit](https://cloud.google.com/vpc/docs/mtu) .

##### private services access

  - Private services access is a private connection between your Virtual Private Cloud (VPC) network and networks owned by Google or third-party service providers. It allows virtual machine (VM) instances in your VPC network to communicate with these services using internal IP addresses, avoiding exposure to the public internet. For more information, see [Private services access](https://cloud.google.com/vpc/docs/private-services-access) .

##### VPC Network Peering

  - A networking connection that allows two VPC networks to communicate privately. In the context of Managed Training on reserved clusters, VPC Network Peering is a critical component for integrating essential services. For instance, it is the required method for connecting your cluster's VPC to a Filestore instance, which provides the necessary shared \`/home\` directory for all the nodes in your cluster.

##### zone

  - A specific deployment area within a Google Cloud region. In the context of Managed Training on reserved clusters, for best performance, all components of the service (the cluster, Filestore, and Managed Lustre instances) should be created in the same zone.

### Integrated storage technologies

##### Cloud Storage Fuse

  - An open-source FUSE adapter that lets you mount Cloud Storage buckets as a file system on Linux or macOS systems. For more information, see [Cloud Storage Fuse](https://cloud.google.com/storage/docs/cloud-storage-fuse/overview) .

##### Filestore

  - A fully managed, high-performance file storage service from Google Cloud, often used for applications that require a shared file system. For more information, see [Filestore overview](https://cloud.google.com/filestore/docs/overview) .

##### Managed Lustre

  - A parallel, distributed file system designed for high-performance computing. Google Cloud's Managed Lustre provides a high-throughput file system for demanding workloads. For more information, see [Managed Lustre overview](https://cloud.google.com/managed-lustre/docs/overview) .

##### performance tier

  - A configuration setting for a Managed Lustre instance that defines its throughput speed (in MBps per TiB) and affects its minimum and maximum capacity.

### Key ML and MLOps concepts

##### checkpoint

  - Data that captures the state of a model's parameters either during training or after training is completed. For example, during training, you can: 1. Stop training, perhaps intentionally or perhaps as the result of certain errors. 2. Capture the checkpoint. 3. Later, reload the checkpoint, possibly on different hardware. 4. Restart training. Within Gemini, a checkpoint refers to a specific version of a Gemini model trained on a specific dataset.

##### Supervised fine-tuning (SFT)

  - A machine learning technique where a pre-trained model is further trained on a smaller, labeled dataset to adapt it to a specific task.

##### Vertex AI Inference

  - A Vertex AI service that lets you use a trained machine learning (ML) model to make inferences from new, unseen data. Vertex AI provides services to deploy models for inference. For more information, see [Get inferences from a custom trained model](https://cloud.google.com/vertex-ai/docs/predictions/get-predictions) .

##### Vertex AI Model Registry

  - The Vertex AI Model Registry is a central repository where you can manage the lifecycle of your ML models. From the Vertex AI Model Registry, you have an overview of your models so you can better organize, track, and train new versions. When you have a model version you would like to deploy, you can assign it to an endpoint directly from the registry, or using aliases, deploy models to an endpoint. For more information, see [Introduction to the Vertex AI Model Registry](https://cloud.google.com/vertex-ai/docs/model-registry/introduction) .

##### Vertex AI TensorBoard

  - Vertex AI TensorBoard is a managed, scalable service on Google Cloud that enables data scientists and ML engineers to visualize their machine learning experiments, debug model training, and track performance metrics using the familiar open-source TensorBoard interface. It integrates seamlessly with Vertex AI Training and other services, providing persistent storage for experiment data and allowing collaborative analysis of model development. For more information, see [Introduction to Vertex AI TensorBoard](https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-introduction) .
