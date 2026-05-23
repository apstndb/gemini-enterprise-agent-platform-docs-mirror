---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/view-endpoint-metrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/view-endpoint-metrics
title: View Vertex AI Inference endpoints dashboard and endpoint metrics
description: Learn about viewing metrics for Vertex AI Inference endpoints.
data_source: docs.cloud.google.com
---

This page covers how to view the [Cloud Monitoring](https://docs.cloud.google.com/monitoring/docs/monitoring-overview) dashboard associated with your Vertex AI Inference endpoints and how to use [Metrics Explorer](https://docs.cloud.google.com/monitoring/charts/metrics-explorer) to explore endpoint metric data.

For an explanation of the Gemini Enterprise Agent Platform metrics, see `aiplatform` in [Google Cloud metrics](https://docs.cloud.google.com/monitoring/api/metrics_gcp_a_b#gcp-aiplatform) .

## View the predefined Gemini Enterprise Agent Platform endpoints overview dashboard

To view the predefined dashboard for Vertex AI Inference endpoints, do the following:

1.  Go to the **Dashboards** page in the Google Cloud console.
    
    If you use the search bar to find this page, then select the result whose subheading is **Monitoring** .

2.  In the toolbar of the Google Cloud console, select your Google Cloud project.

3.  In the list of dashboards, select the **Gemini Enterprise Agent Platform Endpoint Overview** dashboard.

## View endpoint metrics in Metrics Explorer

To view metrics for your endpoint in Metrics Explorer, do the following:

1.  Go to the **Metrics explorer** page in the Google Cloud console.

2.  Under **Select a metric** , select **Gemini Enterprise Agent Platform Endpoint** .

3.  Under **Active metric categories** , select **Log-based metrics** or **Prediction** .

4.  Under **Active metrics** , select the desired metric.

5.  Click **Apply** .

## What's next

  - Learn how to [View and customize Google Cloud dashboards](https://docs.cloud.google.com/monitoring/charts/predefined-dashboards) .
  - Learn how to [Create and manage custom dashboards](https://docs.cloud.google.com/monitoring/charts/dashboards) .
  - Learn more about the [Metrics Explorer](https://docs.cloud.google.com/monitoring/charts/metrics-selector#basic-advanced-mode) .
  - Learn more about [logs-based metrics](https://docs.cloud.google.com/stackdriver/docs/solutions/slo-monitoring/sli-metrics/logs-based-metrics) .
