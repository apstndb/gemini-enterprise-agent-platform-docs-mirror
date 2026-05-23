---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelDeploymentMonitoringJobs/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelDeploymentMonitoringJobs/patch
title: 'Method: modelDeploymentMonitoringJobs.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelDeploymentMonitoringJobs.patch

Updates a ModelDeploymentMonitoringJob.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{modelDeploymentMonitoringJob.name}`  

`PATCH https://{service-endpoint}/v1beta1/{modelDeploymentMonitoringJob.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`modelDeploymentMonitoringJob.name` `string`

Output only. Resource name of a ModelDeploymentMonitoringJob.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. The update mask is used to specify the fields to be overwritten in the ModelDeploymentMonitoringJob resource by the update. The fields specified in the updateMask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the updateMask to `*` to override all fields. For the objective config, the user can either provide the update mask for modelDeploymentMonitoringObjectiveConfigs or any combination of its nested fields, such as: modelDeploymentMonitoringObjectiveConfigs.objective\_config.training\_dataset.

Updatable fields:

  - `displayName`
  - `modelDeploymentMonitoringScheduleConfig`
  - `modelMonitoringAlertConfig`
  - `loggingSamplingStrategy`
  - `labels`
  - `logTtl`
  - `enableMonitoringPipelineLogs` . and
  - `modelDeploymentMonitoringObjectiveConfigs` . or
  - `modelDeploymentMonitoringObjectiveConfigs.objective_config.training_dataset`
  - `modelDeploymentMonitoringObjectiveConfigs.objective_config.training_prediction_skew_detection_config`
  - `modelDeploymentMonitoringObjectiveConfigs.objective_config.prediction_drift_detection_config`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  ModelDeploymentMonitoringJob  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .
