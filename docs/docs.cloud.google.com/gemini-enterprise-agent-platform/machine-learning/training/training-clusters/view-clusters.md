---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/view-clusters
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/view-clusters
title: View clusters
description: 'View Gemini Enterprise Agent Platform training clusters in the {{dynamic_data.site_values.cloud_name_short}} console or with the Agent Platform API: list the clusters in a project, and inspect a single cluster''s configuration, nodes, and metrics.'
data_source: docs.cloud.google.com
---

If you're interested in Gemini Enterprise Agent Platform training clusters, contact your sales representative for access.

This page shows you how to list and view the training clusters in your project by using the Google Cloud console or the Agent Platform API (Google Cloud CLI not supported).

Viewing a cluster lets you confirm the following:

  - Cluster configuration
  - Cluster and node state
  - Login node information
  - Cluster resource usage

If you're looking for instructions on updating a cluster, see [Manage cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster) .

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

Select the tab for how you plan to use the samples on this page:

### Console

When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.

### REST

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

### Required roles

To get the permissions that you need to view training clusters, ask your administrator to grant you the [Agent Platform Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.viewer) ( `roles/aiplatform.viewer` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to view training clusters. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to view training clusters:

  - To view a list of clusters: `aiplatform.modelDevelopmentClusters.list`
  - To view the details of a single cluster: `aiplatform.modelDevelopmentClusters.get`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Console visibility

IAM permissions on their own don't make training clusters visible in the Google Cloud console. The **Training Clusters** page appears only for projects that are enrolled in Gemini Enterprise Agent Platform training clusters. If you don't see the page, contact your sales representative.

The Google Cloud console also requires the following APIs to be enabled in your project. If any of them are missing, the **Training Clusters** page shows an **Enable APIs** button instead of your clusters:

  - `aiplatform.googleapis.com`
  - `compute.googleapis.com`
  - `file.googleapis.com`
  - `hypercomputecluster.googleapis.com`
  - `lustre.googleapis.com`
  - `servicenetworking.googleapis.com`
  - `storage.googleapis.com`

### Authentication for the API

The Agent Platform API examples on this page use the following alias, which calls the Google Cloud CLI to mint an access token:

    alias gcurl='curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json"'

## View a list of clusters

Both interfaces list clusters one region at a time. In the Google Cloud console you choose the region from a list, and with the Agent Platform API the region is part of the request URL.

### Console

1.  In the Google Cloud console, go to the **Training Clusters** page.

2.  In the **Region** list, select the region that you want to view clusters in.
    
    The page lists the clusters in that region. Each column of the table describes a property of the cluster:
    
    | Column                 | Description                                                                                      |
    | ---------------------- | ------------------------------------------------------------------------------------------------ |
    | **ID**                 | The cluster ID, which you use as `CLUSTER_ID` in Agent Platform API requests.                    |
    | **Name**               | The display name of the cluster.                                                                 |
    | **Status**             | The state of the cluster: `Creating` , `Running` , `Updating` , `Stopping` , or `Error` .        |
    | **Nodes**              | The number of nodes in the cluster.                                                              |
    | **Date created**       | When the cluster was created.                                                                    |
    | **Machine types**      | The machine types used by the cluster's node pools.                                              |
    | **Consumption models** | How the cluster's capacity is obtained: `Reservation` , `Spot` , `Flex-start` , or `On-demand` . |
    

3.  To open a cluster, click its name in the **Name** column.

### REST

To view a list of the clusters in one region, send a `GET` request to the `modelDevelopmentClusters` collection:

    gcurl -X GET https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters

Replace the following:

  - PROJECT\_ID : the ID of your project.
  - REGION : the region where your clusters exist.

The `list` method supports the following optional query parameters to control pagination:

  - `pageSize` (integer, optional): The maximum number of clusters to return in the response. The service may return fewer than this value, even if more items exist. If unspecified, a default page size is used.
  - `pageToken` (string, optional): A token received from a previous list call. Provide this token to retrieve the subsequent page of results.

The following example requests the first page of results, with a maximum of five clusters per page:

    gcurl "https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters?pageSize=5"

A successful response contains a `modelDevelopmentClusters` array with up to five cluster resources, and may also include a `nextPageToken` string.

## View the details of a cluster

Both the Google Cloud console and the Agent Platform API report a cluster's configuration and its current state, including the state of each of its nodes. The Cloud Monitoring dashboards are available only in the Google Cloud console.

### Console

1.  In the Google Cloud console, go to the **Training Clusters** page.

2.  In the **Region** list, select the region that the cluster is in.

3.  In the **Name** column, click the name of the cluster that you want to view. The **Cluster details** page opens on the **Overview** tab.

4.  Select a tab to view the corresponding details:
    
      - **Overview** : the cluster's name, description, and location, along with its configured compute, network, and orchestration settings, its login node, and its Slurm partitions.
    
      - **Nodes** : two tables describing the nodes in the cluster.
    
      - **Login nodes** , with the columns **Status** , **Name** , **Zone** , **Machine type** , **Internal IP** , **External IP** , and **Connect** . Use **Connect** to open an SSH session on a login node.
    
      - **Compute nodes** , with the columns **Status** , **Name** , **Zone** , **Machine type** , **Internal IP** , and **Partition** .
    
      - **Observability** : prebuilt Cloud Monitoring dashboards covering CPU, memory, and network usage across the cluster, along with GPU utilization, NVIDIA Data Center GPU Manager (DCGM) metrics, GPU network, and GPU health.

To reload the page with the current state of the cluster, click refresh **Refresh** . To delete the cluster, click delete **Delete** .

> **Note:** You can't edit a cluster from the **Cluster details** page. To change a cluster, use the Agent Platform API, as described in [Manage cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster) .

### REST

To view the details of a single cluster, send a `GET` request to the cluster resource:

    gcurl -X GET https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID

Replace the following:

  - PROJECT\_ID : the ID of your project.
  - REGION : the region where your cluster exists.
  - CLUSTER\_ID : the ID of the cluster that you want to view. This is the value shown in the **ID** column of the **Training Clusters** page in the Google Cloud console.

The response is a `ModelDevelopmentCluster` resource. Alongside the cluster's configuration, its `clusterStatus` field reports the current state of the cluster and of each of its nodes:

  - `clusterStatus.state` : the state of the cluster, one of `PROVISIONING` , `RUNNING` , `UPDATING` , `STOPPING` , or `ERROR` . The Google Cloud console shows `PROVISIONING` as **Creating** .
  - `clusterStatus.nodesStatus[]` : one entry for each node in the cluster, giving the node's `nodeState` ( `PREPARING` , `RUNNING` , `UPDATING` , or `ERROR` ), its Compute Engine instance name, its node pool, and the time its state last changed.
  - `clusterStatus.detail` : a human-readable description of the cluster's status, when one is available.

For a description of the configuration fields, see the [parameter reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/create-cluster#param-reference) .

## What's next

  - [Modify or delete a cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-cluster)
  - [Connect to a cluster and recover from node failures](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/cluster-resiliency)
  - [Run prebuilt workloads on a cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/run-prebuilt-workloads)
  - [Orchestrate jobs on a training cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/orchestration)
