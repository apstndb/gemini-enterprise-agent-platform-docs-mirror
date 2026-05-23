---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/develop-application
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/develop-application
title: Develop an application on the Ray cluster on Gemini Enterprise Agent Platform
description: Connect to a Ray cluster on Agent Platform using Ray client or submit jobs programmatically with the Ray Jobs API.
data_source: docs.cloud.google.com
---

Connect to a Ray cluster on Gemini Enterprise Agent Platform and develop an application using the following methods:

  - Connect to the Ray cluster on Gemini Enterprise Agent Platform through Ray Client using the version of the Agent Platform SDK for Python that includes the functionality of the [Ray Client](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/ray-client.html) . Use this option if you prefer an interactive Python development environment.
    
      - Use the Agent Platform SDK for Python within the Colab Enterprise notebook in the Google Cloud console.
    
      - Use the Agent Platform SDK for Python within a Python session, shell, or Jupyter notebook.

  - Write a Python script and submit the script to the Ray cluster on Gemini Enterprise Agent Platform using the [Ray Jobs API](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/index.html) . If you prefer to submit jobs programmatically, use this option.

Before you begin, make sure to read the [Ray on Agent Platform overview](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/overview) and [set up](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/set-up) all the prerequisite tools you need.

## Connect to a Ray cluster through Ray Client

To use the interactive Ray client, connect to your Ray cluster on Gemini Enterprise Agent Platform. The connecting environment's network depends on the cluster's network configuration. No restrictions apply to the connecting environment as long as the cluster has public internet access. That is, you didn't specify a VPC network during cluster creation. If, however, the cluster is on a private VPC network that peers with Gemini Enterprise Agent Platform, the connecting environment must be on the same VPC network as the cluster.

The Ray version on the client side must match the cluster's Ray version. `pip install "google-cloud-aiplatform[ray]"` installs Ray version 2.47 on the client side by default. If the cluster's Ray version is older than, for example, 2.42, then use `pip install ray==2.42.0` to match the client side's Ray version to the cluster's Ray version.

### Console

In accordance with the [OSS Ray best practice](https://docs.ray.io/en/latest/cluster/vms/user-guides/large-cluster-best-practices.html#configuring-the-head-node) recommendation, setting the logical CPU count to 0 on the Ray head node is enforced in order to avoid running any workload on the head node.

1.  In the Google Cloud console, go to the Ray on Agent Platform page.

2.  In the row for the cluster you created, click **Open in Colab Enterprise** .

3.  The Colab Enterprise notebook opens. Follow the instructions on how to use the Agent Platform SDK for Python to connect to the Ray cluster on Gemini Enterprise Agent Platform.
    
      - If a dialog screen asks you to enable APIs, click **Enable** .
    
      - If you're connecting to the cluster for the first time, then click **Connect** . If you're reconnecting to the cluster, then **Reconnect** . The notebook takes a few minutes to connect to the Runtime.
    
      - Click the **+CREATE** to create a new notebook.
    
      - Click ![Ray on Agent Platform panel](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/images/RoV-panel-icon.png) to open the Ray on Agent Platform panel.  
        Existing clusters display.
    
      - Select a cluster and click **CONNECT** .  
        Code appears in your open notebook that connects to your chosen cluster.
    
      - Other actions (Optional): To open the Ray on Agent Platform cluster list page, click **Manage clusters** in the Ray on Agent Platform panel.
        
          - Select a cluster and click more\_vert **more actions** menu.  
            More options appear:  
            ![more options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/images/ray-more-options.png)
    
      - Run the **Getting started** code cell to import the Agent Platform SDK for Python and connect to the Ray cluster on Gemini Enterprise Agent Platform.

### Python

In accordance with the [OSS Ray best practice](https://docs.ray.io/en/latest/cluster/vms/user-guides/large-cluster-best-practices.html#configuring-the-head-node) recommendation, setting the logical CPU count to 0 on the Ray head node is enforced in order to avoid running any workload on the head node.

From an interactive Python environment:

    import ray
    
    # Necessary even if aiplatform.* symbol is not directly used in your program.
    from google.cloud import aiplatform
    import vertex_ray
    
    import vertexai
    vertexai.init()
    # The CLUSTER_RESOURCE_NAME is the one returned from vertex_ray.create_ray_cluster.
    CLUSTER_RESOURCE_NAME='projects/{}/locations/{}/persistentResources/{}'.format(PROJECT_ID, LOCATION, CLUSTER_NAME)
    
    ray.init('vertex_ray://{}'.format(CLUSTER_RESOURCE_NAME))

Where:

  - **LOCATION** : The location you specify for your Ray cluster on Gemini Enterprise Agent Platform.

  - PROJECT\_ID : Your Google Cloud project ID. Find the project ID in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.

  - CLUSTER\_NAME : The name of your Ray cluster on Gemini Enterprise Agent Platform, specified when you create the cluster. Go to the [Google Cloud console](https://console.cloud.google.com/vertex-ai/ray) to view the list of cluster names for a project.

You get output similar to the following:

    Python version:  3.10.12
    Ray version: 2.47
    Vertex SDK version: 1.46.0
    Dashboard: xxxx-dot-us-central1.aiplatform-training.googleusercontent.com

Use the `Dashboard` URL to access the Ray dashboard from a browser. The URI is in the format of `https://xxxx-dot-us-central1.aiplatform-training.googleusercontent.com/` . The dashboard shows submitted jobs, the number of GPU or CPUs, and disk space of each machine in the cluster.

After you connect to the Ray cluster on Gemini Enterprise Agent Platform, develop a Ray program the same way you develop one for a normal OSS Ray backend.

    @ray.remote
    def square(x):
      print(x)
      return x * x
    
    # Launch four parallel square tasks.
    futures = [square.remote(i) for i in range(4)]
    
    print(ray.get(futures))
    # Returns [0, 1, 4, 9]

## Develop an application using the Ray Jobs API

This section describes how to submit a Python program to the Ray cluster on Gemini Enterprise Agent Platform using the [Ray Jobs API](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/api.html) .

### Write a Python script

Develop your application as a Python script in any text editor. For example, place the following script in a `my_script.py` file:

> **Note:** Code in the entrypoint of the program executes on the head node. Wrap functions with `@ray.remote` for proper parallelization.

    import ray
    import time
    
    @ray.remote
    def hello_world():
        return "hello world"
    
    @ray.remote
    def square(x):
        print(x)
        time.sleep(100)
        return x * x
    
    ray.init()  # No need to specify address="vertex_ray://...."
    print(ray.get(hello_world.remote()))
    print(ray.get([square.remote(i) for i in range(4)]))

### Submit a Ray job using the Ray Jobs API

Submit a Ray job using Python, the Ray Jobs CLI, or the public [Ray dashboard](https://docs.ray.io/en/latest/ray-observability/getting-started.html) address.

> **Note:** All content within the `working_dir` directory is sent to the Ray cluster, which may cause a timeout if the directory is too large. We recommend that you specify a `working_dir` directory that contains only the files that you want to send.

### Python - cluster resource name

Submit a Ray job using a Python environment:

    import ray
    import vertex_ray
    from ray.job_submission import JobSubmissionClient
    from google.cloud import aiplatform  # Necessary even if aiplatform.* symbol is not directly used in your program.
    
    CLUSTER_RESOURCE_NAME='projects/{}/locations/REGION/persistentResources/{}'.format(PROJECT_ID, CLUSTER_NAME)
    
    client = JobSubmissionClient("vertex_ray://{}".format(CLUSTER_RESOURCE_NAME))
    
    job_id = client.submit_job(
      # Entrypoint shell command to execute
      entrypoint="python my_script.py",
      # Path to the local directory that contains the my_script.py file.
      runtime_env={
        "working_dir": "./directory-containing-my-script",
        "pip": ["numpy",
                "setuptools<70.0.0",
                "xgboost",
                "ray==CLUSTER_RAY_VERSION", # pin the Ray version to the same version as the cluster
               ]
      }
    )
    
    # Ensure that the Ray job has been created.
    print(job_id)

Where:

  - REGION : The region you specify for your Ray cluster on Gemini Enterprise Agent Platform.

  - PROJECT\_ID : Your Google Cloud project number. Find the project ID in the Google Cloud console [welcome](https://console.cloud.google.com/welcome) page.

  - CLUSTER\_NAME : The name of your Ray cluster on Gemini Enterprise Agent Platform, specified when you created the cluster. Go to the [Google Cloud console](https://console.cloud.google.com/vertex-ai/ray) to view the list of cluster names for a project.

  - CLUSTER\_RAY\_VERSION : Pin the Ray version to the same version as the cluster. For example, 2.47.1.

### Python - Ray dashboard

The Ray dashboard address is accessible from outside the VPC, including the public internet. Note that `vertex_ray` is required to obtain authentication automatically.

    from ray.job_submission import JobSubmissionClient
    import vertex_ray
    
    DASHBOARD_ADDRESS=DASHBOARD_ADDRESS
    
    client = JobSubmissionClient(
      "vertex_ray://{}".format(DASHBOARD_ADDRESS),
    )
    
    job_id = client.submit_job(
      # Entrypoint shell command to execute
      entrypoint="python my_script.py",
      # Path to the local directory that contains the my_script.py file
      runtime_env={
        "working_dir": "./directory-containing-my-script",
        "pip": ["numpy",
                "setuptools<70.0.0",
                "xgboost",
                "ray==CLUSTER_RAY_VERSION", # pin the Ray version to the same version as the cluster
               ]
      }
    )
    print(job_id)

Where:

DASHBOARD\_ADDRESS : The Ray dashboard address for your cluster. Find the dashboard address [using the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/develop-application#sdk) .

### Ray Jobs CLI

Use the Ray Jobs CLI commands only within the peered VPC network.

    $ ray job submit --working-dir ./ --address vertex_ray://{CLUSTER_RESOURCE_NAME} -- python my_script.py

After submitting a long running Ray Job, if you want to monitor your job status using `client.get_job_status(job_id)` , re-instantiate `JobSubmissionClient(client = JobSubmissionClient("vertex_ray://{}".format(CLUSTER_RESOURCE_NAME)) )` to refresh the authentication token.

## Support for VPC peering and custom service account

Ray on Agent Platform supports Ray Client and Ray Jobs API (JobSubmissionClient) in a public network for default service agent and custom service accounts.

The following table shows Ray on Agent Platform support for VPC peering when you create the Ray cluster with the VPC network:

| VPC peering                   | Default service agent | Custom service account |
| ----------------------------- | --------------------- | ---------------------- |
| Ray Client (interactive mode) | Yes                   | No                     |
| Ray JobSubmissionClient       | Yes                   | Yes                    |

VPC Service Controls (VPC-SC) requires additional configurations. See [Private and public connectivity](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/create-cluster#private_and_public_connectivity) for more details.

## Use Network File System (NFS) in your Ray code

If you set an [NFS mount](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/create-cluster#use_the_network_file_system_nfs) when creating the Ray cluster, read and write those NFS volumes in your application code.

#### RayClient

This section shows you how to use Network File System (NFS) in your Ray code.

1.  Initialize the RayClient in a Python environment
    
        import ray
        from google.cloud import aiplatform
        import vertex_ray
        aiplatform.init(project=PROJECT_ID, location=REGION)
        ray.init(address='vertex_ray://projects/{}/locations/us-central1/persistentResources/{}'.format(PROJECT_NUMBER, PERSISTENT_RESOURCE_ID))

2.  Run job script
    
        import ray
        import logging
        import os
        import sys
        
        @ray.remote
        def main():
        logging.info("list all files in mounted folder")
        return os.listdir("/mnt/nfs/test")
        
        print(''.join(ray.get(main.remote())))

Submit a Ray job using Python, the Ray Jobs CLI, or the public Ray dashboard address. For more information, see [Develop an application on the Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/develop-application#submit-ray-job-with-API) ).

## What's next

  - [Use Ray on Agent Platform with BigQuery](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/bigquery-integration)

  - [Deploy a model on Gemini Enterprise Agent Platform and get inferences](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/deploy-predict)

  - [View logs for your Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/view-logs)

  - [Delete a Ray cluster](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/delete-cluster)
