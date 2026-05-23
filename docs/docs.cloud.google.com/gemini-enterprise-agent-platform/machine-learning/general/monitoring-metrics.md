---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/monitoring-metrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/monitoring-metrics
title: Cloud Monitoring metrics for Agent Platform
description: Learn about Cloud Monitoring metrics that are available in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform exports metrics to [Cloud Monitoring](https://docs.cloud.google.com/monitoring/docs) . Agent Platform also shows some of these metrics in the Agent Platform Google Cloud console. You can use Cloud Monitoring to create dashboards or configure alerts based on the metrics. For example, you can receive alerts if a model's prediction latency in Agent Platform gets too high.

The following sections describe the metrics provided in the Agent Platform Google Cloud console, which might be direct or calculated metrics that Agent Platform sends to Cloud Monitoring.

To view a list of most metrics that Agent Platform exports to Cloud Monitoring, see [`aiplatform`](https://docs.cloud.google.com/monitoring/api/metrics_gcp_a_b#gcp-aiplatform) . For custom training metrics, see metric types that start with `training` in the [`ml`](https://docs.cloud.google.com/monitoring/api/metrics_gcp_i_o#gcp-ml) section.

## Custom training monitoring metrics

When you [perform custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) , you can monitor the following types of resource usage for each training node:

  - CPU or GPU utilization of each training node
  - Memory utilization of each training node
  - Network usage (bytes sent per second and bytes received per second)

If you are using [hyperparameter tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) , you can see the metrics for each trial.

To view these metrics after you have initiated custom training, do the following:

1.  In the Google Cloud console, go to one of the following pages, depending on whether you are using hyperparameter tuning:
    
      - If you aren't using hyperparameter tuning, go to the **Custom jobs** page.
    
      - If you are using hyperparameter tuning, go to the **Hyperparameter tuning jobs** page.

2.  Click the name of your custom training resource.
    
    If you created a [custom `TrainingPipeline` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) , then click the name of the job created by the `TrainingPipeline` ; for example, `  TRAINING_PIPELINE_NAME -custom-job ` or `  TRAINING_PIPELINE_NAME -hyperparameter-tuning-job ` .

3.  Click the **CPU** , **GPU** , or **Network** tab to view utilization charts for the metric that you are interested in.
    
    If you are using hyperparameter tuning, you can click a row in the **Hyperparamater tuning trials** table to view metrics for a specific trial.

To see older metrics or to customize how you view metrics, use Monitoring. Agent Platform exports custom training metrics to Monitoring as [metric types with the prefix `ml.googleapis.com/training`](https://docs.cloud.google.com/monitoring/api/metrics_gcp_i_o#gcp-ml) . The monitored resource type is [`cloudml_job`](https://docs.cloud.google.com/monitoring/api/resources#tag_cloudml_job) .

Note that [AI Platform Training](https://docs.cloud.google.com/ai-platform/training/docs) exports metrics to Monitoring with the same metric types and resource type.

## Endpoint monitoring metrics

After you deploy a model to an [endpoint](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-console) , you can monitor the endpoint to understand your model's performance and resource usage. You can track metrics such as traffic patterns, error rates, latency, and resource utilization to ensure that your model consistently and predictably responds to requests. For example, you might redeploy your model with a different machine type to optimize for cost. After you make the change, you can monitor the model to check whether your changes adversely affected its performance.

In Cloud Monitoring, the monitored resource type for deployed models is [`aiplatform.googleapis.com/Endpoint`](https://docs.cloud.google.com/monitoring/api/resources#tag_aiplatform.googleapis.com/Endpoint) .

### Performance metrics

Performance metrics can help you find information about your model's traffic patterns, errors, and latency. You can view the following performance metrics in the Google Cloud console.

  - **Predictions per second** : The number of predictions per second across both online and batch predictions. If you have more than one instance per request, each instance is counted in this chart.
  - **Prediction error percentage** : The rate of errors that your model is producing. A high error rate might indicate an issue with the model or with the requests to the model. View the response codes chart to determine which errors are occurring.
  - **Model latency (for tabular and custom models only)** : The time spent performing computation.
  - **Overhead latency (for tabular and custom models only)** : The total time spent processing a request, outside of computation.
  - **Total latency duration** : The total time that a request spends in the service, which is the model latency plus the overhead latency.

### Resource usage

Resource usage metrics can help you track your model's CPU usage, memory usage, and network usage. You can view the following usage metrics in the Google Cloud console.

  - **Replica count** : The number of active replicas used by the deployed model.
  - **Replica target** : The number of active replicas required for the deployed model.
  - **CPU usage** : Current CPU core usage rate of the deployed model replica. 100% represents one fully utilized CPU core, so a replica may achieve more than 100% utilization if its machine type has multiple cores.
  - **Memory usage** : The amount of memory allocated by the deployed model replica and currently in use.
  - **Network bytes sent** : The number of bytes sent over the network by the deployed model replica.
  - **Network bytes received** : The number of bytes received over the network by the deployed model replica.
  - **Accelerator average duty cycle** : The average fraction of time over the past sample period during which one or more accelerators were actively processing.
  - **Accelerator memory usage** : The amount of memory allocated by the deployed model replica.

### View endpoint monitoring metric charts

1.  Go to the Agent Platform **Endpoints** page in the Google Cloud console.

2.  Click the name of an endpoint to view its metrics.

3.  Below the chart intervals, click **Performance** or **Resource usage** to view the performance or resource usage metrics.
    
    You can select different chart intervals to see metric values over a particular time period, such as 1 hour, 12 hours, or 14 days.
    
    If you have multiple models deployed to the endpoint, you can select or deselect models to view or hide metrics for particular models. If you select multiple models, the console groups some model metrics into a single chart. For example, if a metric provides only one value per model, the console groups the model metrics into a single chart, such as CPU usage. For metrics that can have multiple values per model, the console provides a chart for each model. For example, the console provides a response code chart for each model.

## Vertex AI Feature Store (Legacy) monitoring metrics

After you [build a feature store using Vertex AI Feature Store (Legacy)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore#vaifs_legacy) , you can monitor its performance and resource utilization, such as the online storage serving latencies or the number of online storage nodes. For example, you might want to monitor the changes to the online storage serving metrics after updating the number of online storage nodes of a featurestore.

In Cloud Monitoring, the monitored resource type for a featurestore is [`aiplatform.googleapis.com/Featurestore`](https://docs.cloud.google.com/monitoring/api/resources#tag_aiplatform.googleapis.com/Featurestore) .

### Metrics

  - **Request size** : The request size by entity type in your featurestore.
  - **Offline storage write for streaming write** : The number of streaming write requests processed for the offline storage.
  - **Streaming write to offline storage delay time** : The time elapsed (in seconds) between calling the write API and writing to the offline storage.
  - **Node count** : The number of online serving nodes for your featurestore.
  - **Latency** : The total time that an online serving or streaming ingestion request spends in the service.
  - **Queries per second** : The number of online serving or streaming ingestion queries that your featurestore handles.
  - **Errors percentage** : The percentage of errors that your featurestore produces when handling online serving or streaming ingestion requests.
  - **CPU utilization** : The fraction of CPU allocated by the featurestore that's being utilized by the online storage. This number can exceed 100% if the online serving storage is overloaded. Consider increasing the featurestore's number of online serving nodes to reduce CPU utilization.
  - **CPU utilization - hottest node** : The CPU load for the hottest node in the featurestore's online storage.
  - **Total offline storage** : Amount of data stored in the featurestore's [offline storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/concepts#storage) .
  - **Total online storage** : Amount of data stored in the featurestore's [online storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/concepts#storage) .
  - **Online serving throughput** : In MBps, the throughput for online serving requests.

### View featurestore monitoring metric charts

1.  Go to the Agent Platform **Features** page in the Google Cloud console.

2.  In the **Featurestore** column, click the name of a featurestore to view its metrics.
    
    You can select different chart intervals to see metric values over a particular time period, such as 1 hour, 1 day, or 1 week.
    
    For some online serving metrics, you can choose to view metrics for a particular method, which further breaks down metrics by entity type. For example, you can view the latency for the `ReadFeatureValues` method or the `StreamingReadFeatureValues` method.

## Vertex AI Feature Store monitoring metrics

After you [set up online serving using Vertex AI Feature Store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore#vaifs) , you can monitor its performance and resource utilization. For example, you can monitor the CPU loads, the number of nodes for Optimized online serving, and the number of serving requests.

In Cloud Monitoring, the monitored resource type for an online store instance is [`aiplatform.googleapis.com/FeatureOnlineStore`](https://docs.cloud.google.com/monitoring/api/resources#tag_aiplatform.googleapis.com/FeatureOnlineStore) .

### Metrics

  - **Bytes stored** : The amount of data in bytes in the online store instance.

  - **CPU load** : The average CPU load of nodes in the online store instance.

  - **CPU load (hottest node)** : The CPU load of the hottest node in the online store instance.

  - **Node count** : The number of online serving nodes for an online store instance configured for Bigtable online serving.

  - **Optimized node count** : The number of online serving nodes for an online store instance configured for Optimized online serving.

  - **Request count** : The number of requests received by the online store instance.

  - **Request latency** : The server-side request latency of the online store instance.

  - **Response byte count** : The amount of data in bytes sent in online serving responses.

  - **Serving data ages** : The serving data age in seconds, measured as the difference between the current time and the time of the last sync.

  - **Running syncs** : The number of running syncs at a given point of time.

  - **Serving data by synced time** : Breakdown of data in the online store instance by the synced timestamp.
