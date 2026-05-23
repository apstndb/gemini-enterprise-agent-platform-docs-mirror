---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/view-autometrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/view-autometrics
title: View Vertex AI Inference AI AutoMetrics
description: Learn about viewing AI AutoMetrics for Vertex AI Inference endpoints.
data_source: docs.cloud.google.com
---

This document describes how to use AI AutoMetrics to monitor your AI workloads on Gemini Enterprise Agent Platform.

AI AutoMetrics lets you to monitor the performance and health of your models with minimal configuration. This feature is designed to give you immediate insights into your custom containers and models running on Vertex AI Inference.

## Before you begin

1.  Make sure you have a [Gemini Enterprise Agent Platform endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/choose-endpoint-type) with a [deployed model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) that uses a container with supported frameworks.
2.  Make sure your project has enabled Cloud Monitoring. See For more information, see [Enable the Monitoring API](https://docs.cloud.google.com/monitoring/api/enable-api) .

## Use AI AutoMetrics

To view AI AutoMetrics on Metrics Explorer, do the following:

1.  Go to the **Metrics Explorer** page in the Google Cloud console.

2.  Under **Select a metric** , select **Prometheus Target** .

3.  Under **Active metric categories** , select **Vertex** .

4.  Under **Active metrics** , select the desired metric.

5.  Click **Apply** .

You can also query metrics using [Grafana](https://docs.cloud.google.com/stackdriver/docs/managed-prometheus/query) , or [Prometheus API or UI](https://docs.cloud.google.com/stackdriver/docs/managed-prometheus/query-api-ui) .

## Supported Frameworks

AI AutoMetrics supports the following frameworks:

| Framework                               | Qualified endpoint                        | Qualified metrics           |
| --------------------------------------- | ----------------------------------------- | --------------------------- |
| [vLLM](https://docs.vllm.ai/en/latest/) | Prometheus-compatible `/metrics` endpoint | Metrics with `vllm:` prefix |

## How it works

Gemini Enterprise Agent Platform automatically scrapes the `/metrics` endpoint of your container at a predefined interval. All qualified metrics are then exported to Google Cloud [Google Cloud Managed Service for Prometheus](https://docs.cloud.google.com/stackdriver/docs/managed-prometheus) , where you can analyze and visualize them.

## Metric naming and labels

The metrics collected by AI AutoMetrics are ingested into Cloud Monitoring under the `vertex_*` naming convention.

For easier filtering and grouping, AI AutoMetrics automatically attaches the following additional Gemini Enterprise Agent Platform labels to each metric:

  - `deployed_model_id` : the ID of a deployed model which serves inference requests.
  - `model_display_name` : the display name of a deployed model.
  - `replica_id` : the unique ID corresponding to the deployed model replica (pod name).
  - `endpoint_id` : the ID of a model endpoint.
  - `endpoint_display_name` : the display name of a model endpoint.
  - `product` : the name of the feature under Gemini Enterprise Agent Platform. This is always **Online Inference** .

## What's next

  - Learn more about the [Metrics Explorer](https://docs.cloud.google.com/monitoring/charts/metrics-selector#basic-advanced-mode) .
