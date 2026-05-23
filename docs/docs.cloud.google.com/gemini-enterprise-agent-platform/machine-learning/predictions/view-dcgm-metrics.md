---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/view-dcgm-metrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/view-dcgm-metrics
title: View Vertex AI Inference DCGM metrics
description: Learn about viewing metrics for Vertex AI Inference endpoints.
data_source: docs.cloud.google.com
---

This page covers how to explore [NVIDIA Data Center GPU Manager (DCGM)](https://developer.nvidia.com/dcgm) metrics associated with your Vertex AI Inference endpoints.

## What is DCGM

NVIDIA Data Center GPU Manager (DCGM) is a set of tools from NVIDIA that let you manage and monitor NVIDIA GPUs. Vertex AI Inference automatically exports [Gemini Enterprise Agent Platform DCGM metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/view-dcgm-metrics#dcgm_metrics) to Cloud Monitoring if your endpoints utilize [supported GPUs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/view-dcgm-metrics#supported_gpus) . Those metrics provide a comprehensive view of GPU utilization, performance, and health.

## Prerequisites

Before you start, make sure your project has enabled Cloud Monitoring. See [Enable the Monitoring API](https://docs.cloud.google.com/monitoring/api/enable-api) for more information.

## Use DCGM metrics

To view DCGM metrics on Metrics Explorer, do the following:

1.  Go to the **Metrics Explorer** page in the Google Cloud console.

2.  Under **Select a metric** , select **Prometheus Target** .

3.  Under **Active metric categories** , select **Vertex** .

4.  Under **Active metrics** , select the desired metric.

5.  Click **Apply** .

You can also query metrics using [Grafana](https://docs.cloud.google.com/stackdriver/docs/managed-prometheus/query) , or [Prometheus API or UI](https://docs.cloud.google.com/stackdriver/docs/managed-prometheus/query-api-ui) .

## Quota

DCGM metrics consume the **Time series ingestion requests per minute** quota of the Cloud Monitoring API. Before enabling the metrics packages, [check your recent peak usage](https://console.cloud.google.com/iam-admin/quotas) of that quota. If you are already approaching that quota limit, you can [request a quota-limit increase](https://docs.cloud.google.com/compute/quotas#requesting_additional_quota) .

## Gemini Enterprise Agent Platform DCGM metrics

The Cloud Monitoring metric names in this table must be prefixed with `prometheus.googleapis.com/` . That prefix has been omitted from the entries in the table.

Along with labels on the `prometheus_target` monitored resource, all collected DCGM metrics on Gemini Enterprise Agent Platform have the following labels attached to them:

GPU labels:

  - `gpu_model` : the GPU device model, such as `NVIDIA L4` .
  - `gpu_uuid` : the GPU device UUID.
  - `gpu_i_id` : the NVIDIA Multi-Instance GPU (MIG) instance ID.

Gemini Enterprise Agent Platform labels:

  - `deployed_model_id` : the ID of a deployed model which serves inference requests.
  - `model_display_name` : the display name of a deployed model.
  - `replica_id` : the unique ID corresponding to the deployed model replica (pod name).
  - `endpoint_id` : the ID of a model endpoint.
  - `endpoint_display_name` : the display name of a model endpoint.
  - `product` : the name of the feature under Gemini Enterprise Agent Platform. This is always `Online Inference` .

PromQL metric name  
Cloud Monitoring metric name

Kind, Type, Unit  
Monitored resources

*Description*

`vertex_dcgm_fi_dev_fb_free`  
`vertex_dcgm_fi_dev_fb_free/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

Free Frame Buffer in MB.

`vertex_dcgm_fi_dev_fb_total`  
`vertex_dcgm_fi_dev_fb_total/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

Total Frame Buffer of the GPU in MB.

`vertex_dcgm_fi_dev_fb_used`  
`vertex_dcgm_fi_dev_fb_used/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

Used Frame Buffer in MB.

`vertex_dcgm_fi_dev_gpu_temp`  
`vertex_dcgm_fi_dev_gpu_temp/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

Current temperature readings for the device (in °C).

`vertex_dcgm_fi_dev_gpu_util`  
`vertex_dcgm_fi_dev_gpu_util/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

GPU utilization (in %).

`vertex_dcgm_fi_dev_mem_copy_util`  
`vertex_dcgm_fi_dev_mem_copy_util/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

Memory utilization (in %).

`vertex_dcgm_fi_dev_memory_temp`  
`vertex_dcgm_fi_dev_memory_temp/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

Memory temperature for the device (in °C).

`vertex_dcgm_fi_dev_power_usage`  
`vertex_dcgm_fi_dev_power_usage/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

Power usage for the device (in Watts).

`vertex_dcgm_fi_dev_sm_clock`  
`vertex_dcgm_fi_dev_sm_clock/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

SM clock frequency (in MHz).

`vertex_dcgm_fi_dev_total_energy_consumption`  
`vertex_dcgm_fi_dev_total_energy_consumption/counter`  
  

`CUMULATIVE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

Total energy consumption for the GPU in mJ since the driver was last reloaded.

`vertex_dcgm_fi_prof_dram_active`  
`vertex_dcgm_fi_prof_dram_active/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The ratio of cycles the device memory interface is active sending or receiving data.

`vertex_dcgm_fi_prof_gr_engine_active`  
`vertex_dcgm_fi_prof_gr_engine_active/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The ratio of time the graphics engine is active.

`vertex_dcgm_fi_prof_nvlink_rx_bytes`  
`vertex_dcgm_fi_prof_nvlink_rx_bytes/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The rate of active NvLink rx (read) data in bytes including both header and payload.

`vertex_dcgm_fi_prof_nvlink_tx_bytes`  
`vertex_dcgm_fi_prof_nvlink_tx_bytes/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The rate of active NvLink tx (transmit) data in bytes including both header and payload.

`vertex_dcgm_fi_prof_pcie_rx_bytes`  
`vertex_dcgm_fi_prof_pcie_rx_bytes/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The rate of active PCIe rx (read) data in bytes including both header and payload.

`vertex_dcgm_fi_prof_pcie_tx_bytes`  
`vertex_dcgm_fi_prof_pcie_tx_bytes/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The rate of active PCIe tx (transmit) data in bytes including both header and payload.

`vertex_dcgm_fi_prof_pipe_fp16_active`  
`vertex_dcgm_fi_prof_pipe_fp16_active/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The ratio of cycles that the fp16 pipe is active.

`vertex_dcgm_fi_prof_pipe_fp32_active`  
`vertex_dcgm_fi_prof_pipe_fp32_active/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The ratio of cycles that the fp32 pipe is active.

`vertex_dcgm_fi_prof_pipe_fp64_active`  
`vertex_dcgm_fi_prof_pipe_fp64_active/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The ratio of cycles that the fp64 pipe is active.

`vertex_dcgm_fi_prof_pipe_tensor_active`  
`vertex_dcgm_fi_prof_pipe_tensor_active/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The ratio of cycles that any tensor pipe is active.

`vertex_dcgm_fi_prof_sm_active`  
`vertex_dcgm_fi_prof_sm_active/gauge`  
  

`GAUGE` , `DOUBLE` , `1` **[prometheus\_target](https://docs.cloud.google.com/monitoring/api/resources#tag_prometheus_target)**

The ratio of cycles an SM has at least 1 warp assigned.

## Supported GPUs

All NVIDIA GPUs are supported, except the following, due to resource constraints:

1.  [NVIDIA P100](https://docs.cloud.google.com/compute/docs/gpus#p100-gpus)
2.  [NVIDIA V100](https://docs.cloud.google.com/compute/docs/gpus#v100-gpus)
3.  [NVIDIA P4](https://docs.cloud.google.com/compute/docs/gpus#p4-gpus)
4.  [NVIDIA T4](https://docs.cloud.google.com/compute/docs/gpus#t4-gpus)

## What's next

  - Learn more about the [Metrics Explorer](https://docs.cloud.google.com/monitoring/charts/metrics-selector#basic-advanced-mode) .
