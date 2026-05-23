---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/overview
title: Ray on Agent Platform overview
description: Scale AI and Python applications with Ray on Agent Platform. Take advantage of distributed computing, parallel processing, and MLOps integrations.
data_source: docs.cloud.google.com
---

[Ray](https://docs.ray.io/en/latest/ray-overview/index.html) is an open-source framework for scaling AI and Python applications. Ray provides the infrastructure to perform distributed computing and parallel processing for your machine learning (ML) workflow.

![Ray and Agent Platform comparison](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/images/manage-ray.png)

If you already use Ray, you can use the same open source Ray code to write programs and develop applications on Gemini Enterprise Agent Platform with minimal changes. You can then use Gemini Enterprise Agent Platform's integrations with other Google Cloud services such as [Vertex AI Inference](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#prediction-prices) and [BigQuery](https://docs.cloud.google.com/bigquery/docs/introduction) as part of your machine learning workflow.

If you already use Gemini Enterprise Agent Platform and need a simpler way to manage compute resources, you can use Ray code to scale training.

## Workflow for using Ray on Agent Platform

Use Colab Enterprise and Agent Platform SDK for Python to connect to the Ray Cluster.

| Steps                                                                                                                                                                            | Description                                                                                                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1\. [Set up for Ray on Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/set-up)                                                         | Set up your Google project, install the version of the Agent Platform SDK for Python that includes the functionality of the [Ray Client](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/ray-client.html) , and set up a VPC peering network, which is optional. |
| 2\. [Create a Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/create-cluster)                         | Create a Ray cluster on Gemini Enterprise Agent Platform. The Gemini Enterprise Agent Platform [Administrator role](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.admin) is required.                                                                     |
| 3\. [Develop a Ray application on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/develop-application)               | Connect to a Ray cluster on Gemini Enterprise Agent Platform and develop an application. Gemini Enterprise Agent Platform [User role](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) is required.                                                    |
| 4\. [(Optional) Use Ray on Agent Platform with BigQuery](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/bigquery-integration)                         | Read, write, and transform data with BigQuery.                                                                                                                                                                                                                                             |
| 5\. [(Optional) Deploy a model on Gemini Enterprise Agent Platform and get inferences](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/deploy-predict) | Deploy a model to a Gemini Enterprise Agent Platform online endpoint and get inferences.                                                                                                                                                                                                   |
| 6\. [Monitor your Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/view-logs)                          | Monitor generated logs in Cloud Logging and metrics in Cloud Monitoring.                                                                                                                                                                                                                   |
| 7\. [Delete a Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/delete-cluster)                         | Delete a Ray cluster on Gemini Enterprise Agent Platform to avoid unnecessary billing.                                                                                                                                                                                                     |

## Overview

Ray clusters are built in to ensure capacity availability for critical ML workloads or during peak seasons. Unlike custom jobs, where the training service releases the resource after job completion, Ray clusters remain available until deleted.

**Note** : Use long running Ray clusters in these scenarios:

  - If you submit the same Ray job multiple times, you can benefit from data and image caching by running the jobs on the same long-running Ray cluster.
  - If you run many short-lived Ray jobs where the actual processing time is shorter than the job startup time, it may be beneficial to have a long-running cluster.

Ray clusters on Gemini Enterprise Agent Platform can be set up either with public or private connectivity. The following diagrams show the architecture and workflow for Ray on Agent Platform. See [Public or private connectivity](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/create-cluster#private_and_public_connectivity) for more information.

### Architecture with public connectivity

![Ray on Agent Platform public connectivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/images/RoV-public-connectivity.png)

1.  Create the Ray cluster on Gemini Enterprise Agent Platform using the following options:
    
    a. Use the Google Cloud console to create the Ray cluster on Gemini Enterprise Agent Platform.
    
    b. Create the Ray cluster on Gemini Enterprise Agent Platform using the Agent Platform SDK for Python.

2.  Connect to the Ray cluster on Gemini Enterprise Agent Platform for interactive development using the following options:
    
    a. Use [Colab Enterprise](https://docs.cloud.google.com/colab/docs/introduction) in the Google Cloud console for seamless connection.
    
    b. Use any Python environment accessible to the public internet.

3.  Develop your application and train your model on the Ray cluster on Gemini Enterprise Agent Platform:
    
      - Use the Agent Platform SDK for Python in your preferred environment (Colab Enterprise or any Python notebook).
    
      - Write a Python script using your preferred environment.
    
      - Submit a Ray Job to the Ray cluster on Gemini Enterprise Agent Platform using the Agent Platform SDK for Python, Ray Job CLI, or Ray Job Submission API.

4.  Deploy the trained model to an online Gemini Enterprise Agent Platform endpoint for live inference.

5.  Use BigQuery to manage your data.

### Architecture with VPC

The following diagram shows the architecture and workflow for Ray on Agent Platform after you set up your Google Cloud project and VPC network, which is optional:

![Ray on Agent Platform VPC](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/images/RoV-architecture.png)

1.  Set up your (a) Google project and (b) VPC network.

2.  Create the Ray cluster on Gemini Enterprise Agent Platform using the following options:
    
    a. Use the Google Cloud console to create the Ray cluster on Gemini Enterprise Agent Platform.
    
    b. Create the Ray cluster on Gemini Enterprise Agent Platform using the Agent Platform SDK for Python.

3.  Connect to the Ray cluster on Gemini Enterprise Agent Platform through a VPC peered network using the following options:
    
      - Use [Colab Enterprise](https://docs.cloud.google.com/colab/docs/introduction) in the Google Cloud console.
    
      - Use a [Gemini Enterprise Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction) notebook.

4.  Develop your application and train your model on the Ray cluster on Gemini Enterprise Agent Platform using the following options:
    
      - Use the Agent Platform SDK for Python in your preferred environment (Colab Enterprise or a Agent Platform Workbench notebook).
    
      - Write a Python script using your preferred environment. Submit a Ray Job to the Ray cluster on Gemini Enterprise Agent Platform using the Agent Platform SDK for Python, Ray Job CLI, or Ray dashboard.

5.  Deploy the trained model to an online Gemini Enterprise Agent Platform endpoint for inferences.

6.  Use BigQuery to manage your data.

## Terminology

For a full list of terms see the [Agent Platform glossary for predictive AI](https://docs.cloud.google.com/vertex-ai/docs/glossary) .

  - ##### autoscaling
    
      - Autoscaling is the capability of a compute resource, like a Ray cluster's worker pool, to automatically adjust the number of nodes up or down based on the workload demands, optimizing resource utilization and cost. For more information, see [Scale Ray clusters on Vertex AI: Autoscaling](https://cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/scale-clusters#autoscaling) .

  - ##### batch inference
    
      - Batch inference takes a group of inference requests and outputs the results in one file. For more information, see [Overview of getting inferences on Vertex AI](https://cloud.google.com/vertex-ai/docs/predictions/overview#batch-inference) .

  - ##### BigQuery
    
      - BigQuery is a fully managed, serverless, and highly scalable enterprise data warehouse provided by Google Cloud, designed for analyzing massive datasets using SQL queries at incredibly high speeds. BigQuery enables powerful business intelligence and analytics without requiring users to manage any infrastructure. For more information, see [From data warehouse to autonomous data and AI platform](https://cloud.google.com/bigquery/docs) .

  - ##### Cloud Logging
    
      - Cloud Logging is a fully managed, real-time logging service provided by Google Cloud that lets you collect, store, analyze, and monitor logs from all your Google Cloud resources, on-premises applications, and even custom sources. Cloud Logging centralizes log management, which makes it easier to troubleshoot, audit, and understand the behavior and health of your applications and infrastructure. For more information, see [Cloud Logging overview](https://cloud.google.com/logging/docs/overview) .

  - ##### Colab Enterprise
    
      - Colab Enterprise is a collaborative, managed Jupyter notebook environment that brings the popular Google Colab user experience to Google Cloud, offering enterprise-level security and compliance capabilities. Colab Enterprise provides a notebook-centric, zero-configuration experience, with compute resources managed by Vertex AI, and integrates with other Google Cloud services like BigQuery. For more information, see [Introduction to Colab Enterprise](https://cloud.google.com/colab/docs/introduction) .

  - ##### custom container image
    
      - A custom container image is a self-contained, executable package that includes the user's application code, its runtime, libraries, dependencies, and environment configuration. In the context of Google Cloud, particularly Vertex AI, it lets the user package their machine learning training code or serving application with its exact dependencies, ensuring reproducibility and enabling the user to run a workload on managed services using specific software versions or unique configurations not provided by standard environments. For more information, see [Custom container requirements for inference](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements) .

  - ##### endpoint
    
      - Resources to which you can deploy trained models to serve inferences. For more information, see [Choose an endpoint type](https://cloud.google.com/vertex-ai/docs/predictions/choose-endpoint-type) .

  - ##### Identity and Access Management permissions (IAM)
    
      - Identity and Access Management (IAM) permissions are specific granular capabilities that define who can do what on which Google Cloud resources. They are assigned to principals (like users, groups, or service accounts) through roles, allowing precise control over access to services and data within a Google Cloud project or organization. For more information, see [Access control with IAM](https://cloud.google.com/support/docs/access-control) .

  - ##### inference
    
      - In the context of the Vertex AI platform, inference refers to the process of running data points through a machine learning model to calculate an output, such as a single numerical score. This process is also known as "operationalizing a machine learning model" or "putting a machine learning model into production." Inference is an important step in the machine learning workflow, since it enables models to be used to make inferences on new data. In Vertex AI, inference can be performed in various ways, including batch inference and online inference. Batch inference involves running a group of inference requests and outputting the results in one file, while online inference allows for real-time inferences on individual data points.

  - ##### Network File System (NFS)
    
      - A client/server system that lets users access files across a network and treat them as if they resided in a local file directory. For more information, see [Mount a Network File System share](https://cloud.google.com/vertex-ai/docs/training/train-nfs-share) .

  - ##### Online inference
    
      - Obtaining inferences on individual instances synchronously. For more information, see [Online inference](https://cloud.google.com/vertex-ai/docs/predictions/overview#online-inference) .

  - ##### persistent resource
    
      - A type of Vertex AI compute resource, such as a Ray cluster, that remains allocated and available until explicitly deleted, which is beneficial for iterative development and reduces startup overhead between jobs. For more information, see [Get persistent resource information](https://cloud.google.com/vertex-ai/docs/training/persistent-resource-get) .

  - ##### pipeline
    
      - ML pipelines are portable and scalable ML workflows that are based on containers. For more information, see [Introduction to Vertex AI Pipelines](https://cloud.google.com/vertex-ai/docs/pipelines/introduction) .

  - ##### Prebuilt container
    
      - Container images provided by Vertex AI that come pre-installed with common ML frameworks and dependencies, simplifying the setup for training and inference jobs. For more information, see [Prebuilt containers for serverless training](https://cloud.google.com/vertex-ai/docs/training/pre-built-containers) .

  - ##### Private Service Connect (PSC)
    
      - Private Service Connect is a technology that allows Compute Engine customers to map private IPs in their network to either another VPC network or to Google APIs. For more information, see [Private Service Connect](https://cloud.google.com/vpc/docs/private-service-connect) .

  - ##### Ray cluster on Vertex AI
    
      - A Ray cluster on Vertex AI is a managed cluster of compute nodes that can be used to run distributed machine learning (ML) and Python applications. It provides the infrastructure to perform distributed computing and parallel processing for your ML workflow. Ray clusters are built into Vertex AI to ensure capacity availability for critical ML workloads or during peak seasons. Unlike custom jobs, where the training service releases the resource after job completion, Ray clusters remain available until deleted. For more information, see [Ray on Vertex AI overview](https://cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/overview) .

  - ##### Ray on Vertex AI (RoV)
    
      - Ray on Vertex AI is designed so you can use the same open source Ray code to write programs and develop applications on Vertex AI with minimal changes. For more information, see [Ray on Vertex AI overview](https://cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/overview) .

  - ##### Ray on Vertex AI SDK for Python
    
      - Ray on Vertex AI SDK for Python is a version of the Vertex AI SDK for Python that includes the functionality of the Ray Client, Ray BigQuery connector, Ray cluster management on Vertex AI, and inferences on Vertex AI. For more information, see [Introduction to the Vertex AI SDK for Python](https://cloud.google.com/vertex-ai/docs/python-sdk/use-vertex-ai-python-sdk-ref) .

  - ##### Ray on Vertex AI SDK for Python
    
      - Ray on Vertex AI SDK for Python is a version of the Vertex AI SDK for Python that includes the functionality of the Ray Client, Ray BigQuery connector, Ray cluster management on Vertex AI, and inferences on Vertex AI. For more information, see [Introduction to the Vertex AI SDK for Python](https://cloud.google.com/vertex-ai/docs/python-sdk/use-vertex-ai-python-sdk-ref) .

  - ##### service account
    
      - Service accounts are special Google Cloud accounts used by applications or virtual machines to make authorized API calls to Google Cloud services. Unlike user accounts, they are not tied to an individual human but act as an identity for your code, enabling secure and programmatic access to resources without requiring human credentials. For more information, see [Service accounts overview](https://cloud.google.com/iam/docs/service-account-overview) .

  - ##### Vertex AI Workbench
    
      - Vertex AI Workbench is a unified, Jupyter notebook-based development environment that supports the entire data science workflow, from data exploration and analysis to model development, training, and deployment. Vertex AI Workbench provides a managed and scalable infrastructure with built-in integrations to other Google Cloud services like BigQuery and Cloud Storage, enabling data scientists to perform their machine learning tasks efficiently without managing underlying infrastructure. For more information, see [Introduction to Vertex AI Workbench](https://cloud.google.com/vertex-ai/docs/workbench/introduction) .

  - ##### worker node
    
      - A worker node refers to an individual machine or computational instance within a cluster that's responsible for executing tasks or performing work. In systems like Kubernetes or Ray clusters, nodes are the fundamental units of compute. For more information, see [What is high performance computing (HPC)?](https://cloud.google.com/discover/what-is-high-performance-computing) .

  - ##### worker pool
    
      - Components of a Ray cluster that execute distributed tasks. Worker pools can be configured with specific machine types and support both autoscaling and manual scaling. For more information, see [Structure of the training cluster](https://cloud.google.com/vertex-ai/docs/training/distributed-training#cluster-structure) .

## Pricing

Pricing for Ray on Agent Platform is calculated as follows:

  - The compute resources you use are charged based on the machine configuration you select when creating your Ray cluster on Gemini Enterprise Agent Platform. For Ray on Agent Platform pricing, see the [pricing page](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#ray-on-vertex-ai) .

  - Regarding Ray clusters, you are only charged during RUNNING and UPDATING [states](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.persistentResources#state) . No other states are charged. The amount charged is based on the actual cluster size at the moment.

  - When you perform tasks using the Ray cluster on Gemini Enterprise Agent Platform, logs are automatically generated and charged based on [Cloud Logging pricing](https://docs.cloud.google.com/stackdriver/pricing#logging-costs) .

  - If you deploy your model to an endpoint for online inferences, see the ["Prediction and explanation"](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#prediction-prices) section of the Gemini Enterprise Agent Platform pricing page.

  - If you use BigQuery with Ray on Agent Platform, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) .

## What's next

  - [Set up for Ray on Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/set-up)
