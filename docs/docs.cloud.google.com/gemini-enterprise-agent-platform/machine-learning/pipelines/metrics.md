---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics
title: View pipeline metrics
description: Learn how to view pipeline metrics in Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

After you define, build, and run a pipeline, you can view metrics related to the pipeline job or pipeline tasks in the Metrics Explorer. Additionally, you can create custom log-based metrics and alerts using Cloud Logging to monitor events such as pipeline failures.

This page describes how you can do the following:

  - [View standard Agent Platform Pipelines metrics in the Metrics Explorer](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#view_metrics_explorer)

  - [Create and view custom metrics in the Logs Explorer](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#build-custom-metrics) (preview)

Creating and viewing custom metrics in Cloud Logging has costs associated with it. For more information, see [Cloud Logging pricing](https://docs.cloud.google.com/logging#pricing) .

## View standard Agent Platform Pipelines metrics in the Metrics Explorer

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can view the following metrics related to Agent Platform Pipelines in the Metrics Explorer:

  - **Pipeline job-level metrics:**
    
      - Use the `Vertex Pipelines Job - PipelineJob duration` metric to [view the runtime duration of pipeline runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#pipelinejob_duration) .
    
      - Use the `Location - Executing PipelineJobs` metric to [view the number of pipeline runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#pipelinejob_runs) .

  - **Pipeline task-level metrics:**
    
      - Use the `Vertex Pipelines Job - Completed PipelineTasks` to [view the number of pipeline tasks completed](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#pipelinetask_completed) .
    
      - Use the `Location - Executing PipelineTasks` to [view the number of pipeline tasks executed in pipeline runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#pipelinetask_executed) .

### View the runtime duration of pipeline jobs

Use the following instructions to view the `Vertex Pipelines Job - PipelineJob duration` metric in the Google Cloud console:

1.  Navigate to the **Metrics Explorer** :

2.  In the **Metric** list, select **Vertex Pipelines Job** \> **Pipelinejob** \> **PipelineJob duration** .

3.  Click **Apply** .

4.  Optional: To filter the query, specify one or more criteria by clicking **Filter** . For example:
    
      - To view the runtime duration of a specific pipeline job, use the `pipeline_job_id` filter.
    
      - To view the runtime duration of pipeline jobs for a specific location, use the `location` filter.
    
      - To view the runtime duration of pipeline jobs in the `PIPELINE_STATE_CANCELLED` , `PIPELINE_STATE_CANCELLING` , `PIPELINE_STATE_FAILED` , `PIPELINE_STATE_PENDING` , `PIPELINE_STATE_RUNNING` , or `PIPELINE_STATE_SUCCEEDED` state, use the `run_state` filter.

### View the number of pipeline runs

Use the following instructions to view the `Location - Executing PipelineJobs` metric in the Google Cloud console:

1.  Navigate to the **Metrics Explorer** :

2.  In the **Metric** list, select **Location** \> **Executing\_vertexai\_pipeline\_jobs** \> **Executing PipelineJobs** .

3.  Click **Apply** .

4.  Optional: To filter the query, specify one or more criteria by clicking **Filter** . For example, to view the number of pipeline jobs for a specific location, use the `location` filter.

### View the number of pipeline tasks completed

Use the following instructions to view the `Vertex Pipelines Job - Completed PipelineTasks` metric in the Google Cloud console:

1.  Navigate to the **Metrics Explorer** :

2.  In the **Metric** list, select **Vertex Pipelines Job** \> **Pipelinejob** \> **Completed PipelineTasks** .

3.  Click **Apply** .

4.  Optional: To filter the query, specify one or more criteria by clicking **Filter** . For example:
    
      - To view the number of tasks completed in a specific pipeline run, use the `pipeline_job_id` filter.
    
      - To view the number of tasks completed in pipeline runs for a specific location, use the `location` filter.

### View the number of pipeline tasks executed

Use the following instructions to view the `Location - Executing PipelineTasks` metric in the Google Cloud console:

1.  Navigate to the **Metrics Explorer** :

2.  In the **Metric** list, select **Location** \> **Executing\_vertexai\_pipeline\_tasks** \> **Executing PipelineTasks** .

3.  Click **Apply** .

4.  Optional: To filter the query, specify one or more criteria by clicking **Filter** . For example, to view the number of pipeline tasks executed for a specific location, use the `location` filter.

## Create and view custom metrics in the Logs Explorer

You can [use the Logs Explorer](https://docs.cloud.google.com/logging/docs/view/logs-explorer-interface) in the Google Cloud console to create custom [log-based metrics](https://docs.cloud.google.com/logging/docs/logs-based-metrics) that track and analyze patterns within your pipeline logs.

### Examples of custom metrics

This section illustrates examples of custom metrics you can create. These include the following:

  - [Create a custom metric for failed pipeline jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#custom-metric-failed-jobs)

  - [Create a custom metric for final pipeline state](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#custom-metric-final-state)

  - [View pipeline job failure rate](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#pipeline-job-failure-rate)

#### Create a custom metric for failed pipeline jobs

To create a custom log-based [counter metric](https://docs.cloud.google.com/logging/docs/logs-based-metrics/counter-metrics#create_a_counter_metric) that monitors failed pipeline jobs, do the following:

1.  Navigate to the **Logs Explorer** :

2.  Select the appropriate Google Cloud project.

3.  In the **Resource** drop-down menu, select **Vertex Pipelines Job** .

4.  In the **Location** drop-down menu, select your pipeline's location.

5.  In the **All pipeline\_job\_id** drop-down menu, select the ID of your pipeline job.

6.  Click **Apply** .

7.  Click **Create Metric** .

8.  In the **Create logs metric** screen:
    
    1.  Set the **Metric type** : Select **Counter** .
    
    2.  Set the following fields in the **Details** section:
        
          - **Log metric name** : Enter a name for your log metric, for example, `pipelinejob_failed` . Choose a name that is unique among the logs-based metrics in your Google Cloud project. Some naming restrictions apply. For more information, see [Troubleshooting](https://docs.cloud.google.com/logging/docs/logs-based-metrics/troubleshooting#metric-name-restrictions) .
          - **Description** : Enter a description for the metric.
          - **Units** : Leave this field blank or enter the digit **1** .
    
    3.  Define your metric filter in the **Filter selection** section. Create a filter that collects only the log entries that you want to count in your metric using the [logging query language](https://docs.cloud.google.com/logging/docs/view/logging-query-language) , for example:
        
            resource.type="aiplatform.googleapis.com/PipelineJob"
            jsonPayload.state="PIPELINE_STATE_FAILED"
        
        You can also use regular expressions to create your metric's filters.
        
        To open a panel showing you the log entries that match your filter, click **Preview logs** .
    
    4.  Optional: Add a label in the **Labels** section. For instructions on creating labels, see [Create a label](https://docs.cloud.google.com/logging/docs/logs-based-metrics/labels#create-label) .
    
    5.  To create the metric, click **Create metric** .

#### Create a custom metric for final pipeline state

To create a custom log-based [counter metric](https://docs.cloud.google.com/logging/docs/logs-based-metrics/counter-metrics#create_a_counter_metric) that monitors the final state of your pipeline jobs, do the following:

1.  Navigate to the Logs Explorer:

2.  Select the appropriate Google Cloud project.

3.  In the **Resource** drop-down menu, select **Vertex Pipelines Job** .

4.  In the **Location** drop-down menu, select your pipeline's location.

5.  In the **All pipeline\_job\_id** drop-down menu, select the ID of your pipeline job.

6.  Click **Apply** .

7.  Click **Create Metric** .

8.  In the **Create logs metric** screen:
    
    1.  Set the **Metric type** : Select **Counter** .
    
    2.  Set the following fields in the **Details** section:
        
          - **Log metric name** : Enter a name for your log metric, for example, `Pipeline_state_final` . Choose a name that is unique among the logs-based metrics in your Google Cloud project. Some naming restrictions apply. For more information, see [Troubleshooting](https://docs.cloud.google.com/logging/docs/logs-based-metrics/troubleshooting#metric-name-restrictions) .
          - **Description** : Enter a description for the metric.
          - **Units** : Leave this field blank or enter the digit **1** .
    
    3.  Define your metric filter in the **Filter selection** section. Create a filter that collects only the log entries that you want to count in your metric using the [logging query language](https://docs.cloud.google.com/logging/docs/view/logging-query-language) , for example:
        
            resource.type="aiplatform.googleapis.com/PipelineJob"
            jsonPayload.state="PIPELINE_STATE_SUCCEEDED" OR
            "PIPELINE_STATE_FAILED" OR "PIPELINE_STATE_CANCELLED"
        
        You can also use regular expressions to create your metric's filters.
        
        To open a panel showing you the log entries that match your filter, click **Preview logs** .
    
    4.  Optional: Add a label in the **Labels** section. For instructions on creating labels, see [Create a label](https://docs.cloud.google.com/logging/docs/logs-based-metrics/labels#create-label) .
    
    5.  To create the metric, click **Create metric** .

#### View pipeline job failure rate

The pipeline job failure rate is calculated as the ratio of the number of pipeline jobs in the final state to the number of failed pipeline jobs. To create a dashboard to monitor the pipeline job failure rate, do the following:

1.  Create a metric for monitoring the pipeline jobs in the final state. For more information, see [Create a custom metric for final pipeline state](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#custom-metric-final-state) .

2.  Create a metric for monitoring the pipeline jobs in the failed state. For more information, see [Create a custom metric for failed pipeline jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/metrics#custom-metric-failed-jobs) .

3.  In the **Monitoring** section of the Google Cloud console, go to the Metrics Explorer page.

4.  In the **Configuration** tab, do the following:
    
    1.  Click **Add another metric** .
    
    2.  Select the **Display metrics as ratio** option. When you select this option:
        
          - The **Time series A** pane is renamed **Numerator** .
        
          - The **Time series B** pane is renamed **Denominator** .
    
    3.  In the **Numerator** pane, click **Select a metric** to select the metric created for failed pipeline jobs.
    
    4.  In the **Denominator** pane, click **Select a metric** to select the metric created for final state pipeline jobs.
    
    5.  (Optional) Configure the numerator and denominator by adding filters, or by updating the grouping fields and alignment parameters.
        
        For more information about how to add filters, or update the grouping fields and alignment parameters, see [Chart a ratio of metrics](https://docs.cloud.google.com/monitoring/charts/metrics-explorer#chart-ratio) .
        
        > **Note:** The two metrics selected as the numerator and denominator must have the same resource type. If you select the same metric as the numerator and the denominator, use different filters or groupings to make the numerator distinct from the denominator.
    
    After you select the numerator and the denominator, the pipeline job failure rate is displayed in the graph.
    
      - After you generate the pipeline job failure rate graph, you can add it to your custom dashboard. For more information, see [Save a chart for future reference](https://docs.cloud.google.com/monitoring/charts/metrics-explorer#save) .
    
      - To copy the URL containing the graph configuration, click the ellipsis icon on the top right corner of the graph, and then click **Share by URL** .
