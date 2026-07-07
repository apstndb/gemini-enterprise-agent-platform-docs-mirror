---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/delete-cluster
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/delete-cluster
title: Delete the Ray cluster on Gemini Enterprise Agent Platform
description: Instructions for how to delete a Ray cluster, which avoids unnecessary billing, using the {{dynamic_data.site_values.cloud_name_short}} console or Agent Platform SDK for Python.
data_source: docs.cloud.google.com
---

When you finish [developing an application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/develop-application) for your Ray cluster on Gemini Enterprise Agent Platform, delete the cluster to avoid unnecessary billing.

> **Note:** You can't reuse the cluster name for up to two hours after deleting the cluster.

### Console

1.  In the Google Cloud console, go to the Ray on Agent Platform page.

2.  Select the Ray cluster on Gemini Enterprise Agent Platform you want to delete.

3.  Click **Delete** .

### Agent Platform SDK for Python

From the same Python environment where you connected to your Ray cluster on Gemini Enterprise Agent Platform, run the following:

    # Shut down the Ray on Agent Platform if currently connected
    ray.shutdown()
    
    # Delete cluster
    vertex_ray.delete_ray_cluster(CLUSTER_RESOURCE_NAME)

Where:

  - CLUSTER\_RESOURCE\_NAME : CLUSTER\_RESOURCE\_NAME='projects/{}/locations/{}/persistentResources/{}'.format( PROJECT\_ID , LOCATION , CLUSTER\_NAME ).
