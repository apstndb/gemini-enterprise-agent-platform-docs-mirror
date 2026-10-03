---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies
title: 'Method: modelDeploymentMonitoringJobs.searchModelDeploymentMonitoringStatsAnomalies'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelDeploymentMonitoringJobs.searchModelDeploymentMonitoringStatsAnomalies

Searches Model Monitoring Statistics generated within a given time window.

### Endpoint

post `https: / /{service-endpoint} /v1 /{modelDeploymentMonitoringJob}:searchModelDeploymentMonitoringStatsAnomalies`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`modelDeploymentMonitoringJob` `string`

Required. ModelDeploymentMonitoring Job resource name. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{modelDeploymentMonitoringJob}`

### Request body

The request body contains data with the following structure:

Fields

`deployedModelId` `string`

Required. The DeployedModel id of the \[ModelDeploymentMonitoringObjectiveConfig.deployed_model_id\].

`featureDisplayName` `string`

The feature display name. If specified, only return the stats belonging to this feature. Format: [`ModelMonitoringStatsAnomalies.FeatureHistoricStatsAnomalies.feature_display_name`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#FeatureHistoricStatsAnomalies.FIELDS.feature_display_name) , example: "user_destination".

`objectives[]` `object ( `[`StatsAnomaliesObjective`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#StatsAnomaliesObjective)` )`

Required. Objectives of the stats to retrieve.

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

A page token received from a previous [`JobService.SearchModelDeploymentMonitoringStatsAnomalies`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#google.cloud.aiplatform.v1.JobService.SearchModelDeploymentMonitoringStatsAnomalies) call.

`startTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

The earliest timestamp of stats being generated. If not set, indicates fetching stats till the earliest possible one.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

The latest timestamp of stats being generated. If not set, indicates feching stats till the latest possible one.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

### Response body

Response message for [`JobService.SearchModelDeploymentMonitoringStatsAnomalies`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#google.cloud.aiplatform.v1.JobService.SearchModelDeploymentMonitoringStatsAnomalies) .

If successful, the response body contains data with the following structure:

Fields

`monitoringStats[]` `object ( `[`ModelMonitoringStatsAnomalies`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#ModelMonitoringStatsAnomalies)` )`

Stats retrieved for requested objectives. There are at most 1000 [`ModelMonitoringStatsAnomalies.FeatureHistoricStatsAnomalies.prediction_stats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#FeatureHistoricStatsAnomalies.FIELDS.prediction_stats) in the response.

`nextPageToken` `string`

The page token that can be used by the next [`JobService.SearchModelDeploymentMonitoringStatsAnomalies`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#google.cloud.aiplatform.v1.JobService.SearchModelDeploymentMonitoringStatsAnomalies) call.

**JSON representation**

```
{
  "monitoringStats": [
    {
      object (ModelMonitoringStatsAnomalies)
    }
  ],
  "nextPageToken": string
}
```

## StatsAnomaliesObjective

Stats requested for specific objective.

Fields

`type` `enum ( `[`ModelDeploymentMonitoringObjectiveType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#ModelDeploymentMonitoringObjectiveType)` )`

`topFeatureCount` `integer`

If set, all attribution scores between [`SearchModelDeploymentMonitoringStatsAnomaliesRequest.start_time`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#body.request_body.FIELDS.start_time) and [`SearchModelDeploymentMonitoringStatsAnomaliesRequest.end_time`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#body.request_body.FIELDS.end_time) are fetched, and page token doesn't take effect in this case. Only used to retrieve attribution score for the top Features which has the highest attribution score in the latest monitoring run.

**JSON representation**

```
{
  "type": enum (ModelDeploymentMonitoringObjectiveType),
  "topFeatureCount": integer
}
```

## ModelDeploymentMonitoringObjectiveType

The Model Monitoring Objective types.

| Enums                                                    |                                                                                                                |
|----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| `MODEL_DEPLOYMENT_MONITORING_OBJECTIVE_TYPE_UNSPECIFIED` | Default value, should not be set.                                                                              |
| `RAW_FEATURE_SKEW`                                       | Raw feature values' stats to detect skew between Training-Prediction datasets.                                 |
| `RAW_FEATURE_DRIFT`                                      | Raw feature values' stats to detect drift between Serving-Prediction datasets.                                 |
| `FEATURE_ATTRIBUTION_SKEW`                               | feature attribution scores to detect skew between Training-Prediction datasets.                                |
| `FEATURE_ATTRIBUTION_DRIFT`                              | feature attribution scores to detect skew between Prediction datasets collected within different time windows. |

## ModelMonitoringStatsAnomalies

Statistics and anomalies generated by Model Monitoring.

Fields

`objective` `enum ( `[`ModelDeploymentMonitoringObjectiveType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#ModelDeploymentMonitoringObjectiveType)` )`

Model Monitoring Objective those stats and anomalies belonging to.

`deployedModelId` `string`

Deployed Model id.

`anomalyCount` `integer`

Number of anomalies within all stats.

`featureStats[]` `object ( `[`FeatureHistoricStatsAnomalies`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/searchModelDeploymentMonitoringStatsAnomalies#FeatureHistoricStatsAnomalies)` )`

A list of historical Stats and Anomalies generated for all Features.

**JSON representation**

```
{
  "objective": enum (ModelDeploymentMonitoringObjectiveType),
  "deployedModelId": string,
  "anomalyCount": integer,
  "featureStats": [
    {
      object (FeatureHistoricStatsAnomalies)
    }
  ]
}
```

## FeatureHistoricStatsAnomalies

Historical Stats (and Anomalies) for a specific feature.

Fields

`featureDisplayName` `string`

Display name of the feature.

`threshold` `object ( `[`ThresholdConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs#ThresholdConfig)` )`

Threshold for anomaly detection.

`trainingStats` `object ( `[`FeatureStatsAnomaly`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features#Feature.FeatureStatsAnomaly)` )`

Stats calculated for the Training Dataset.

`predictionStats[]` `object ( `[`FeatureStatsAnomaly`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features#Feature.FeatureStatsAnomaly)` )`

A list of historical stats generated by different time window's Prediction Dataset.

**JSON representation**

```
{
  "featureDisplayName": string,
  "threshold": {
    object (ThresholdConfig)
  },
  "trainingStats": {
    object (FeatureStatsAnomaly)
  },
  "predictionStats": [
    {
      object (FeatureStatsAnomaly)
    }
  ]
}
```
