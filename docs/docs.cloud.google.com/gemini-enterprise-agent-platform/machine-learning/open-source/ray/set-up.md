---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/set-up
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/set-up
title: Set up for Ray on Agent Platform
description: Instructions for how to set up Ray on Agent Platform.
data_source: docs.cloud.google.com
---

> To see an example of getting started with Ray on cluster management, run the "Ray on cluster management" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/ray_cluster_management.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fray_cluster_management.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fray_on_vertex_ai%2Fray_cluster_management.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ray_on_vertex_ai/ray_cluster_management.ipynb)

Before you begin with Ray on Agent Platform, follow these steps to set up your Google project and Agent Platform SDK for Python :

1.  Set up billing for your project, [install the gcloud CLI](https://docs.cloud.google.com/sdk/docs/install) , and enable the Agent Platform API. To do this, follow the steps at [Set up a project and a development environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/cloud-environment) .

2.  Prerequisite: You must know how to develop programs using [open source Ray](https://docs.ray.io/en/latest/ray-overview/index.html) .

3.  The Ray on Agent Platform SDK for Python used here is a version of the Agent Platform SDK for Python that includes the functionality of the [Ray Client](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/ray-client.html) , Ray BigQuery connector, Ray cluster management on Gemini Enterprise Agent Platform, and predictions on Gemini Enterprise Agent Platform.
    
      - If you use Ray on Agent Platform in the Google Cloud console, a Colab Enterprise notebook guides you through the Agent Platform SDK for Python installation process after you [create a Ray cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster) .
    
      - If you use Ray on Agent Platform in the Vertex AI Workbench or other interactive Python environment, install the Agent Platform SDK for Python:
        
            # The latest image in the Ray cluster includes Ray 2.47
            # The latest supported Python version is Python 3.11.
            $ pip install google-cloud-aiplatform[ray]
        
        After you install the SDK, restart the kernel before you import packages.
        
        > **Note:** If you use a Vertex AI Workbench notebook as the client environment and use the [Deep Learning VM](https://docs.cloud.google.com/deep-learning-vm/docs/introduction) as the machine image, Ray and the Agent Platform SDK for Python are pre-installed in the Python, TensorFlow Enterprise

4.  Optional: If you plan to read from BigQuery, create a new BigQuery dataset or use an existing dataset. To do this, see [create a new BigQuery dataset](https://docs.cloud.google.com/bigquery/docs/datasets) .
    
    > **Note:** If you run code on your Ray cluster on Gemini Enterprise Agent Platform that interacts with Google services like BigQuery, the [Gemini Enterprise Agent Platform Custom Code Service Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) authenticates.

5.  (Optional) To mitigate the risk of data exfiltration from Agent Platform, enable VPC Service Controls and specify a VPC network when you create a cluster. For more information, see [VPC Service Controls with Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls) .
    
    If you enable VPC Service Controls, you can't reach resources outside the perimeter, such as files in a Cloud Storage bucket.
    
    > **Note:** The best setup for Ray on Agent Platform is one auto mode VPC network per project. If you use a custom mode VPC network or use multiple VPC networks to create clusters in the same project, you might encounter issues.

6.  (Optional) To use a custom container image, host it on [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/overview) . A custom image lets you add Python dependencies that aren't included with the prebuilt container images. To build custom images, see Packing your software in the [Docker documentation](https://docs.docker.com/build/building/packaging/) .

7.  (Optional) If you specify a VPC network when creating a Ray cluster on Gemini Enterprise Agent Platform, it's highly recommended that you use an auto mode VPC network in your project. Custom mode VPC networks and multiple VPC networks in the same project aren't supported and may cause cluster creation to fail.

## Secure your clusters

Follow [Ray best practices and guidelines](https://docs.ray.io/en/latest/ray-security/index.html#best-practices) , including running trusted code on trusted networks, to secure your Ray workloads. Deployment of ray.io in your cloud instances falls under the model of [shared responsibility](https://docs.cloud.google.com/vertex-ai/docs/shared-responsibility) .

For more information about Google Cloud best practices, see the [GCP-2024-020 security bulletin](https://docs.cloud.google.com/support/bulletins#gcp-2024-020) .

## Supported locations

The [Feature availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#available-regions) table lists the available locations for Ray on Agent Platform for Custom model training.

## What's next

  - [Create a Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster)
