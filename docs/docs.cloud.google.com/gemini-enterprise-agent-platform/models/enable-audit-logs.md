---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/enable-audit-logs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/enable-audit-logs
title: Enable Data Access audit logs
description: Learn how to enable Data Access audit logs for generative models and endpoints on Agent Platform, compare inference logging options, and understand caller attribution.
data_source: docs.cloud.google.com
---

To get audit logs about the usage of your generative models and model endpoints, enable [Data Access audit logs](https://docs.cloud.google.com/logging/docs/audit#data-access) for Gemini Enterprise Agent Platform. Data Access audit logs include `ADMIN_READ` operations that read metadata or configuration information, as well as `DATA_READ` and `DATA_WRITE` operations that read or write user-provided data.

After you enable Data Access audit logs for Agent Platform, grant the Private Logs Viewer role ( `roles/logging.privateLogViewer` ) to view the `data_access` log stream ( `projects/ `` PROJECT_ID `` /logs/cloudaudit.googleapis.com%2Fdata_access` ) in Cloud Logging in the Google Cloud console.

For instructions on enabling and viewing Data Access audit logs, see [Agent Platform audit logging information](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/audit-logging) .

## Audited generative model operations

When you enable `DATA_READ` audit logs for `aiplatform.googleapis.com` , Agent Platform records Data Access audit log entries for the following generative model and prediction operations on both publisher models ( `publishers.models.*` ) and deployed endpoints ( `endpoints.*` ):

- **Content and chat generation** : `generateContent` , `streamGenerateContent` , and `chatCompletions`

- **Embeddings** : `embedContent` and `batchEmbedContents`

- **Token counting** : `countTokens` and `computeTokens`

- **Online prediction and explanation** : `predict` , `rawPredict` , `streamRawPredict` , `directPredict` , `directRawPredict` , `streamDirectPredict` , `streamDirectRawPredict` , `serverStreamingPredict` , `predictLongRunning` , `fetchPredictOperation` , and `explain`

For the complete list of audited methods across all categories, see [Agent Platform audit logging information](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/audit-logging#audited_operations) .

## Authentication and caller attribution

The authentication method that your application uses determines how `DATA_READ` audit logs record the caller's identity ( `protoPayload.authenticationInfo.principalEmail` ) and IP address ( `protoPayload.requestMetadata.callerIp` ):

- **[Application Default Credentials (ADC) and Identity and Access Management (IAM) principals](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/gcp-auth)** : Requests authenticated with ADC, user credentials, or workload-specific service accounts record both the caller's IP address ( `callerIp` ) and the individual caller's authenticated principal ( `principalEmail` ) in `DATA_READ` audit logs. Use ADC when you need per-user or per-workload audit attribution in production.

- **[Standard Google Cloud API keys](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/api-keys?usertype=standard)** : Standard Google Cloud API keys authenticate API calls through a single bound service account. `DATA_READ` audit logs record the caller's IP address ( `callerIp` ), but attribute `principalEmail` to that single bound service account for every request made with the API key rather than to individual users or workloads.

- **[Express mode API keys](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/api-keys?usertype=expressmode)** : Requests sent in [express mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/express-mode/overview) target projectless endpoints and don't generate customer-accessible `DATA_READ` audit logs in Logging.

## Compare audit logs and inference logs

Agent Platform provides multiple logging mechanisms for model inference. The following table compares Data Access ( `DATA_READ` ) audit logs with other inference logging options:

| Logging feature                                                                                                                                                         | Destination                                                 | Recorded fields                                                                                                                                     | Prompt and response payloads                        | Caller IP and IAM principal                                                                  |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|----------------------------------------------------------------------------------------------|
| **Data Access ( `DATA_READ` ) audit logs**                                                                                                                              | Logging ( `cloudaudit.googleapis.com%2Fdata_access` )       | API method name, target model or endpoint resource, and request metadata                                                                            | Not recorded                                        | Records `callerIp` and `principalEmail` (or the bound service account for standard API keys) |
| **[Inference request metadata logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/inference-metadata-logging)**                    | Logging ( `aiplatform.googleapis.com%2Finference_request` ) | Token counts ( `usageMetadata` ), request latency ( `requestDuration` ), consumption option ( `trafficType` ), and custom headers ( `httpHeaders` ) | Not recorded                                        | Records service account ( `principal` , when available); doesn't record `callerIp`           |
| **[Request-response logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/request-response-logging)**                             | BigQuery table                                              | Sampled inference requests, responses, token counts, and latency metadata                                                                           | Records `full_request` and `full_response` payloads | Doesn't record `callerIp` or `principalEmail`                                                |
| **[Online inference access and container logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging)** | Logging ( `prediction_access` and `prediction_container` )  | Endpoint access status, latency, and container `stdout` and `stderr` streams for custom-trained and AutoML models                                   | Container output only                               | Doesn't record `callerIp`                                                                    |

## What's next

Overview

### [Introduction to tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-3)

Learn how to tune a model by providing a training dataset that contains a set of examples of specific downstream tasks.

Overview

### [Responsible AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai)

Learn about some of the limitations to generative AI and recommended practices for using generative AI.
