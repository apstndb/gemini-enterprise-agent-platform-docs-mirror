---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging
title: Use online inference logging
description: Enable or disable inference logging for custom-trained models and AutoML tabular and image models.
data_source: docs.cloud.google.com
---

For AutoML tabular models, AutoML image models, and custom-trained models, you can enable or disable inference logs during model deployment or endpoint creation. This page explains the different types of inference logs available, and how to enable or disable these logs.

## Types of inference logs

There are several types of inference logs that you can use to get information from your inference nodes:

- **Container logging** , which logs the `stdout` and `stderr` streams from your inference nodes to [Cloud Logging](https://docs.cloud.google.com/logging/docs/overview) . These logs are required for debugging.

  - On the `v1` service endpoint, container logging is enabled by default. You can disable it when you deploy a model. You can also disable or enable logging when you [mutate](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/mutateDeployedModel) the deployed model.

  - On the `v1beta1` service endpoint, container logging is disabled by default. You can enable it when you deploy a model. You can also disable or enable logging when you [mutate](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/mutateDeployedModel) the deployed model.

  > **Note:** The default logging behavior in Python sends outputs to `stderr` , which will appear at the `ERROR` level in Cloud Logging. If you'd like for container logs to appear at the `INFO` level, configure your container logging to send outputs to `stdout` . For more information, see the Python [Logging handlers](https://docs.python.org/3/library/logging.handlers.html) tutorials and the Python [Logging Cookbook](https://docs.python.org/3/howto/logging-cookbook.html) .

  Container `stdout` and `stderr` collection runs asynchronously so that log writing doesn't delay or block inference requests. If an inference replica generates a high volume of logs, or experiences temporary delays sending logs to Cloud Logging, then some `stdout` and `stderr` entries might be dropped while the replica continues serving predictions. If your workload requires every inference log entry to be recorded, [write logs directly to Cloud Logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging#direct-cloud-logging) .

- **Access logging** , which logs information like timestamp and latency for each request to Cloud Logging.

  On both the `v1` and `v1beta1` service endpoints, access logging is disabled by default. You can enable access logging when you deploy a model to an endpoint.

- **Request-response logging** , which logs a sample of online inference requests and responses to a BigQuery table.

  You can enable request-response logging by creating or patching the inference endpoint.

You can enable or disable each type of log independently.

## Inference log settings

You can enable or disable online inference logs when you create an endpoint, deploy a model to the endpoint, or mutate a deployed model.

To update the settings for access logs, you must [undeploy your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/undeployModel) , and then redeploy the model with your new settings. You can update the settings for container logs without re-deploying your model.

Online inference at a high rate of queries per second (QPS) can produce a substantial number of logs, which are subject to [Cloud Logging pricing](https://cloud.google.com/stackdriver/pricing#logging-costs) . To estimate the pricing for your online inference logs, see [Estimating your bills](https://docs.cloud.google.com/stackdriver/estimating-bills) for logging. To reduce this cost, you can disable inference logging.

### Enable and disable inference logs

The following examples highlight where to modify the default log settings:

### Console

When you deploy a model to an endpoint or create a new endpoint in the Google Cloud console, you can specify which types of inference logs to enable in the **Logging** step. Select the checkboxes to enable **Access logging** or **Container logging** , or clear the checkboxes to disable these logs.

Use the REST API to update the settings for container logs.

Use the REST API to enable request-response logging. The Google Cloud console and gcloud CLI don't support request-response logging configuration.

To see more context about how to deploy models, read [Deploy a model using the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-console) .

### gcloud

To change the default behavior for which logs are enabled in deployed models, add flags to your `gcloud` command:

### `v1` service endpoint

Run [`gcloud ai endpoints deploy-model`](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/deploy-model) :

```
gcloud ai endpoints deploy-model ENDPOINT_ID\
  --region=LOCATION \
  --model=MODEL_ID \
  --display-name=DEPLOYED_MODEL_NAME \
  --machine-type=MACHINE_TYPE \
  --accelerator=count=2,type=nvidia-tesla-t4 \
  --disable-container-logging \
  --enable-access-logging
```

### `v1beta1` service endpoint

Run [`gcloud beta ai endpoints deploy-model`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/ai/endpoints/deploy-model) :

```
gcloud beta ai endpoints deploy-model ENDPOINT_ID\
  --region=LOCATION \
  --model=MODEL_ID \
  --display-name=DEPLOYED_MODEL_NAME \
  --machine-type=MACHINE_TYPE \
  --accelerator=count=2,type=nvidia-tesla-t4 \
  --enable-access-logging \
  --enable-container-logging
```

Use the REST API to update the settings for container logs.

Use the REST API to enable request-response logging. The Google Cloud console and gcloud CLI don't support request-response logging configuration.

To see more context about how to deploy models, read [Deploy a model using the Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api) .

### REST

To change the default behavior for which logs are enabled in deployed models, set the relevant fields to `True` :

### `v1` service endpoint

To disable **container logging** , set the `disableContainerLogging` field to `True` when you call either [`projects.locations.endpoints.deployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel) or [`projects.locations.endpoints.mutateDeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/mutateDeployedModel) .

To enable **access logging** , set `enableAccessLogging` to `True` when deploying your model with [`projects.locations.endpoints.deployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel) .

### `v1beta1` service endpoint

To enable **container logging** , set the `enableContainerLogging` field to `True` when you call either [`projects.locations.endpoints.deployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel) or [`projects.locations.endpoints.mutateDeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/mutateDeployedModel) .

To enable **access logging** , set `enableAccessLogging` to `True` when deploying your model with [`projects.locations.endpoints.deployModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/deployModel) .

To see more context about how to deploy models, read [Deploy a model using the Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api) .

**Request-response logging**

You can only enable request-response logging when you create an endpoint using [`projects.locations.endpoints.create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/create) or patch an existing endpoint using [`projects.locations.endpoints.patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/patch) .

Request-response logging is done at the endpoint level, so requests sent to any deployed models under the same endpoint are logged.

When you create or patch an endpoint, populate the `predictRequestResponseLoggingConfig` field of the [Endpoint resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints) with the following entries:

- `enabled` : set to `True` to enable request-response logging.

- `samplingPercentage` : a number between 0 or 1 defining the fraction of requests to log. For example, set this value to `1` in order to log all requests or to `0.1` to log 10% of requests.

- [`BigQueryDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BigQueryDestination) : the BigQuery table to be used for logging. If you only specify a project name, a new dataset is created with the name `logging_ `` ENDPOINT_DISPLAY_NAME `` _ `` ENDPOINT_ID` , where `ENDPOINT_DISPLAY_NAME` follows the [BigQuery naming rules](https://docs.cloud.google.com/bigquery/docs/datasets#dataset-naming) . If you don't specify a table name, a new table is created with the name `request_response_logging` .

  The schema for the BigQuery table should look like the following:

  | Field name          | Type      | Mode     |
  |---------------------|-----------|----------|
  | `endpoint`          | STRING    | NULLABLE |
  | `deployed_model_id` | STRING    | NULLABLE |
  | `logging_time`      | TIMESTAMP | NULLABLE |
  | `request_id`        | NUMERIC   | NULLABLE |
  | `request_payload`   | STRING    | REPEATED |
  | `response_payload`  | STRING    | REPEATED |

The following is an example configuration:

```
{
   "predict_request_response_logging_config": {
     "enabled": true,
     "sampling_rate": 0.5,
     "bigquery_destination": {
       "output_uri": "bq://PROJECT_ID.DATASET_NAME.TABLE_NAME"
     }
   }
}
```

## Inference request-response logging for dedicated endpoints and Private Service Connect endpoints

For [dedicated endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#create-dedicated-endpoint) and [Private Service Connect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/private-service-connect) endpoints, you can use request-response logging to record request and response payloads under 10 MB (larger payloads are skipped automatically) for TensorFlow, PyTorch, sklearn, and XGBoost models.

Request-response logging is available only for the [`predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) and [`rawPredict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/rawPredict) methods.

To enable request-response logging, populate the [`predictRequestResponseLoggingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#PredictRequestResponseLoggingConfig) field of the [Endpoint resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints) with the following entries:

- `enabled` : set to `True` to enable request-response logging.

- `samplingRate` : the fraction of requests and responses to log. Set to a number that is greater than 0 and less than or equal to 1. For example, set this value to `1` in order to log all requests or to `0.1` to log 10% of requests.

- [`BigQueryDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BigQueryDestination) : the BigQuery location for the output content, as a URI to a project or table.

The following is an example configuration for creating a dedicated endpoint with request-response logging enabled:

```
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer `gcloud auth print-access-token`" https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_NUMBER/locations/LOCATION_ID/endpoints \
-d '{displayName: "ENDPOINT_NAME", \
     dedicatedEndpointEnabled: true, \
     predictRequestResponseLoggingConfig: { \
       enabled: true, \
       samplingRate: 1.0, \
       bigqueryDestination: { \
          outputUri:"bq://PROJECT_ID" \
       } \
     } \
   }'
```

Replace the following:

- ` LOCATION_ID ` : The region where you are using Agent Platform.
- ` PROJECT_NUMBER ` : The project number for your Google Cloud project.
- ` ENDPOINT_NAME ` : The display name for the endpoint.
- ` PROJECT_ID ` : The project ID for your Google Cloud project.

The following is an example configuration for creating a Private Service Connect endpoint with request-response logging enabled:

```
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer `gcloud auth print-access-token`" https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_NUMBER/locations/LOCATION_ID/endpoints \
-d '{displayName: "ENDPOINT_NAME", \
     privateServiceConnectConfig: { \
       enablePrivateServiceConnect: true, \
       projectAllowlist: ["ALLOWED_PROJECTS"] \
     }, \
     predictRequestResponseLoggingConfig: { \
       enabled: true, \
       samplingRate: 1.0, \
       bigqueryDestination: { \
          outputUri:"bq://PROJECT_ID" \
       } \
     } \
   }'
```

Replace the following:

- ` ``ALLOWED_PROJECTS`` ` : a comma-separated list of Google Cloud project IDs, each enclosed in quotation marks. For example, `["PROJECTID1", "PROJECTID2"]` . If a project isn't contained in this list, you won't be able to send inference requests to the Agent Platform endpoint from it. Make sure to include ` VERTEX_AI_PROJECT_ID ` in this list so that you can call the endpoint from the same project it's in.

## Request-response logging and Model Monitoring v1

Request-response logging and [Model Monitoring v1](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview) use the same BigQuery table on the backend to log incoming requests. To prevent unexpected changes to this BigQuery table, the following limitations are enforced when using both features at the same time:

- If an endpoint has Model Monitoring enabled, you can't enable request-response logging for the same endpoint.

- If you enable request-response logging and then Model Monitoring on the same endpoint, you won't be able to change the request-response logging configuration.

## Write logs directly to Cloud Logging

Standard container `stdout` and `stderr` logging is designed for operational debugging. If an inference replica generates a high volume of logs, or experiences temporary delays sending logs to Cloud Logging, then it might drop some `stdout` and `stderr` entries rather than delaying or blocking inference requests. If your [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements) workload requires every per-request log entry to be recorded without gaps, configure your deployed model to use a [custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) and send the log entries directly to Cloud Logging.

To ensure that your deployed model's custom service account has the necessary permissions to write log entries directly to Cloud Logging, ask your administrator to grant the [Logs Writer](https://docs.cloud.google.com/iam/docs/roles-permissions/logging#logging.logWriter) ( `roles/logging.logWriter` ) IAM role to your deployed model's custom service account on your project.

> **Important:** You must grant this role to your deployed model's custom service account, *not* to your user account. Failure to grant the role to the correct principal might result in permission errors.

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

Your administrator might also be able to give your deployed model's custom service account the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

After you attach the custom service account to your deployed model, use a background thread or asynchronous task in your custom container to write structured log entries using the [`entries.write`](https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/entries/write) method in the Cloud Logging API.

Standard Cloud Logging client libraries don't detect [Agent Platform `AIP_*` environment variables](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#aip-variables) automatically, so they record a generic resource type such as `global` . As a result, those entries don't match queries or [log sinks](https://docs.cloud.google.com/logging/docs/routing/overview#sinks) , which route matching logs to supported destinations, when filtering on `resource.type="aiplatform.googleapis.com/Endpoint"` .

In your `entries.write` requests, pass an explicit [`aiplatform.googleapis.com/Endpoint`](https://docs.cloud.google.com/monitoring/api/resources#tag_aiplatform.googleapis.com/Endpoint) monitored resource and set the following `resource.labels` fields:

- Set `endpoint_id` to the value of `AIP_ENDPOINT_ID` .
- Set `resource_container` to `projects/ `` PROJECT_NUMBER` using `AIP_PROJECT_NUMBER` .
- Set `location` to the endpoint's region, such as `us-central1` .

Because Agent Platform doesn't automatically set an `AIP_*` environment variable for the region, pass the region to your container explicitly, such as through [`containerSpec.env`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelContainerSpec#FIELDS.env) when you upload the model. To match standard Agent Platform container log filters, also set the `LogEntry` `labels` field with the key `deployed_model_id` set to the value of `AIP_DEPLOYED_MODEL_ID` and the key `replica_id` set to the value of `HOSTNAME` .

If your custom container pins specific `protobuf` or `grpcio` versions, or runs an asynchronous HTTP stack, you can avoid client library package conflicts by sending batched JSON requests over HTTPS to `https://logging.googleapis.com/v2/entries:write` . Authenticate these requests using your container's existing HTTP and authentication libraries with the `https://www.googleapis.com/auth/logging.write` OAuth 2.0 scope, or configure the Cloud Logging client library to use REST transport by setting `GOOGLE_CLOUD_DISABLE_GRPC=true` .

## What's next

- [Estimate pricing](https://docs.cloud.google.com/stackdriver/estimating-bills) for online inference logging.
- Deploy a model [using the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-console) or [using the Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api) .
- Learn [how to create a BigQuery table](https://docs.cloud.google.com/bigquery/docs/tables) .
