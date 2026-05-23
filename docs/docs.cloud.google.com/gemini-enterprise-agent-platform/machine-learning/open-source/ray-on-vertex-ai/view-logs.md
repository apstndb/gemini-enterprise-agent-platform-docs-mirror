---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/view-logs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/view-logs
title: Monitor your Ray cluster on Gemini Enterprise Agent Platform
description: View the tracking logs associated with your Ray clusters and monitor the Ray on Agent Platform metrics. Debugging guidance for Ray clusters is also provided.
data_source: docs.cloud.google.com
---

This page covers how to view the tracking logs associated with your Ray clusters and monitor the Ray on Agent Platform metrics. Guidance for debugging Ray clusters is also provided.

## View logs

When you perform tasks with your Ray cluster on Gemini Enterprise Agent Platform, tracking logs are automatically generated and stored in both Cloud Logging and [open source Ray dashboard](https://docs.ray.io/en/latest/ray-observability/getting-started.html#logs-view) . This section describes how to access the generated logs through the Google Cloud console.

Before you begin, make sure to read the [Ray on Agent Platform overview](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/overview) and [set up](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/set-up) all the prerequisite tools you need.

### Ray OSS dashboard

You can view the open source Ray log files through the Ray OSS dashboard:

1.  In the Google Cloud console, go to the Ray on Agent Platform page.

2.  In the row for the cluster you created, select more\_vert **more actions** menu.

3.  Select the Ray OSS dashboard link. The dashboard opens in another tab.

4.  Navigate to the **Logs** view in the top right corner in the menu:
    
    ![Ray dashboard logs](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/open-source/images/Ray-dashboard-logs.png)

5.  Click each node to see the log files associated with that node.

### Cloud Logging console

1.  In the Google Cloud console, go to the segment **Logs Explorer** page:
    
    If you use the search bar to find this page, then select the result whose subheading is **Logging** .

2.  Select an existing Google Cloud project, folder, or organization.

3.  To display all Ray logs, enter the following query into the query-editor field, and then click **Run query** :
    
        resource.labels.task_name="ray-cluster-logs"

4.  To narrow down the logs to a specific Ray cluster, add the following line to the query and then click **Run query** :
    
        labels."ml.googleapis.com/ray_cluster_id"=CLUSTER_NAME
    
    Replace CLUSTER\_NAME with the name for your Ray cluster. In the Google Cloud console go to **Gemini Enterprise Agent Platform** \> **Ray on Agent Platform** where you see a list of cluster names in each region.

5.  To further narrow down the logs to a specific log file like `raylet.out` , click the name of the log under **Log fields** -\> **Log name** .

6.  You can group similar log entries together:
    
    1.  In the **Query results** , click a log entry to expand the log.
    
    2.  In the `jsonPayload` , click the `tailed_path` value. A drop-down menu appears.
    
    3.  Click **Show matching entries** .

## Disable logs

By default, Ray on Vertex AI Cloud Logging is enabled.

  - To disable the export of Ray logs to Cloud Logging, use the following Agent Platform SDK for Python command:
    
        vertex_ray.create_ray_cluster(..., enable_logging=False, ...)

You can view the Ray log files on the Ray dashboard even if the Ray on Agent Platform Cloud Logging feature is disabled.

## Monitor metrics

You can view the Ray on Agent Platform metrics in different ways using [Google Cloud Monitoring (GCM)](https://docs.cloud.google.com/monitoring) . Alternatively, you can export the metrics from GCM to your own Grafana server.

> **Note:** See [Google Cloud Managed Service for Prometheus (GMP)](https://docs.cloud.google.com/stackdriver/docs/managed-prometheus) for [pricing](https://docs.cloud.google.com/stackdriver/docs/managed-prometheus/cost-controls) and [data storage](https://docs.cloud.google.com/stackdriver/docs/managed-prometheus#gmp-data-storage) information.

### Monitor Metrics in GCM

There are two ways you can view the Ray on Agent Platform metrics in GCM.

  - Use the direct view under **Metrics Explorer** .

  - Import the Grafana dashboard.

### **Metrics Explorer**

To use the direct view under **Metrics Explorer** , follow these steps:

1.  Go to the Google Cloud Monitoring console.

2.  Under [**Explore**](http://console.cloud.google.com/monitoring/metrics-explorer) select **Metrics explorer** .

3.  Under **Active Resources** , select **Prometheus Target** . **Active Metric Categories** appears.

4.  Select **Ray** .
    
    A list of metrics appears:
    
    ![select metric](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/open-source/images/monitor-metrics-prometheus.png)

5.  Select the metrics you want to monitor. For example:
    
    1.  Choose the cpu utilization percentage as a monitored metric:  
        ![utilization-target](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/open-source/images/ray-cpu-utilization-target.png)  
    2.  Select a filter. For example, select cluster:  
        ![add necessary filter](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/open-source/images/ray-add-filter.png) Use the cluster ID to only monitor the above metrics for a specific cluster. To locate your cluster ID, follow these steps:
        1.  In the Google Cloud console, go to the **Ray** page.
        
        2.  Be sure you're in the project you want to create the experiment in.  
            ![Vertex AI select project](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/project-select.png)
        
        3.  Under **Name** a list of cluster IDs appears.
        ![select metric](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/open-source/images/ray-cluster-id.png)
    3.  Select the **Aggregation** method to view the metrics. That is, you can choose to view unaggregated metrics, which show each Ray process's CPU utilization:  
        ![unaggregated metrics](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/open-source/images/ray-unaggregated-metrics.png)

### **GCM** dashboard

To import a Grafana dashboard for Ray on Vertex AI follow the guidelines on the cloud monitoring dashboard, [Import your own grafana dashboard](https://cloud.google.com/monitoring/dashboards/import-grafana-dashboards) .

![monitoring dashboard](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/open-source/images/ray-cloud-monitoring-dashboard.png)

All you need is a Grafana dashboard JSON file. OSS Ray supports this [manual setup](https://docs.ray.io/en/releases-2.5.1/cluster/metrics.html?highlight=simplist#recommended-use-ray-dashboard-with-embedded-grafana-visualizations) by providing the default dashboard Grafana JSON file.

### Monitor metrics

from user-owned Grafana

If you already have a Grafana server running, then there's also a way to export all the Ray cluster on Vertex AI Prometheus metrics to your existing Grafana server. To do so, follow the GMP [Query using Grafana](https://docs.cloud.google.com/stackdriver/docs/managed-prometheus/query#begin) guidance. This lets you add a new Grafana data source to your existing Grafana server and use the data source syncer to sync the new Grafana Prometheus data source to Ray on Vertex AI metrics.

It's important that you configure and authenticate the newly added Grafana data source using the data source syncer. Follow the steps provided in [Configure and authenticate the Grafana data source](https://docs.cloud.google.com/stackdriver/docs/managed-prometheus/query#grafana-oauth) .

Once synced, you can create and add any dashboard you need based on the Ray on Vertex AI metrics.

By default, the Ray on Vertex AI metrics collections are enabled. Here's how to disable them using Agent Platform SDK for Python:

    vertex_ray.create_ray_cluster(..., enable_metrics_collection=False, ...)

## Debug Ray clusters

To debug Ray clusters, use the **Head node interactive shell** :

> **Note:** Only use the interactive shell for debugging purposes or other advanced operations not supported in other ways. It's **not recommended** for normal operations like running workloads.

### Google Cloud console

To access the **Head node interactive shell** , do the following:

1.  In the Google Cloud console, go to the **Ray on Vertex AI** page.  
2.  Be sure you're in the correct project.  
    ![Vertex AI select project](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/open-source/images/project-select.png)
3.  Select the cluster you want to examine. **Basic info** section appears.
4.  In the **Access links** section, click the link for **Head node interactive shell** . The head node interactive shell appears.
5.  Follow the instructions outlined in [Monitor and debug training with an interactive shell](https://docs.cloud.google.com/vertex-ai/machine-learning/training/monitor-debug-interactive-shell) .

## What's next

  - [Delete a Ray cluster](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/delete-cluster)
