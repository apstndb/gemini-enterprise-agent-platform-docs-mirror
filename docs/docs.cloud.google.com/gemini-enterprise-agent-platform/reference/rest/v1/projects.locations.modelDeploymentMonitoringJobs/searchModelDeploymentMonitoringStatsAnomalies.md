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

Required. The DeployedModel id of the \[ModelDeploymentMonitoringObjectiveConfig.deployed\_model\_id\].

`featureDisplayName` `string`

The feature display name. If specified, only return the stats belonging to this feature. Format: `  ModelMonitoringStatsAnomalies.FeatureHistoricStatsAnomalies.feature_display_name  ` , example: "user\_destination".

`objectives[]` ` object ( StatsAnomaliesObjective  ` )

Required. Objectives of the stats to retrieve.

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

A page token received from a previous `  JobService.SearchModelDeploymentMonitoringStatsAnomalies  ` call.

`startTime` ` string ( Timestamp  ` format)

The earliest timestamp of stats being generated. If not set, indicates fetching stats till the earliest possible one.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

The latest timestamp of stats being generated. If not set, indicates feching stats till the latest possible one.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

### Response body

Response message for `  JobService.SearchModelDeploymentMonitoringStatsAnomalies  ` .

If successful, the response body contains data with the following structure:

Fields

`monitoringStats[]` ` object ( ModelMonitoringStatsAnomalies  ` )

Stats retrieved for requested objectives. There are at most 1000 `  ModelMonitoringStatsAnomalies.FeatureHistoricStatsAnomalies.prediction_stats  ` in the response.

`nextPageToken` `string`

The page token that can be used by the next `  JobService.SearchModelDeploymentMonitoringStatsAnomalies  ` call.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;monitoringStats&quot;: [{object (ModelMonitoringStatsAnomalies)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## StatsAnomaliesObjective

Stats requested for specific objective.

Fields

`type` ` enum ( ModelDeploymentMonitoringObjectiveType  ` )

`topFeatureCount` `integer`

If set, all attribution scores between `  SearchModelDeploymentMonitoringStatsAnomaliesRequest.start_time  ` and `  SearchModelDeploymentMonitoringStatsAnomaliesRequest.end_time  ` are fetched, and page token doesn't take effect in this case. Only used to retrieve attribution score for the top Features which has the highest attribution score in the latest monitoring run.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (ModelDeploymentMonitoringObjectiveType),&quot;topFeatureCount&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

## ModelDeploymentMonitoringObjectiveType

The Model Monitoring Objective types.

Enums

`MODEL_DEPLOYMENT_MONITORING_OBJECTIVE_TYPE_UNSPECIFIED`

Default value, should not be set.

`RAW_FEATURE_SKEW`

Raw feature values' stats to detect skew between Training-Prediction datasets.

`RAW_FEATURE_DRIFT`

Raw feature values' stats to detect drift between Serving-Prediction datasets.

`FEATURE_ATTRIBUTION_SKEW`

feature attribution scores to detect skew between Training-Prediction datasets.

`FEATURE_ATTRIBUTION_DRIFT`

feature attribution scores to detect skew between Prediction datasets collected within different time windows.

## ModelMonitoringStatsAnomalies

Statistics and anomalies generated by Model Monitoring.

Fields

`objective` ` enum ( ModelDeploymentMonitoringObjectiveType  ` )

Model Monitoring Objective those stats and anomalies belonging to.

`deployedModelId` `string`

Deployed Model id.

`anomalyCount` `integer`

Number of anomalies within all stats.

`featureStats[]` ` object ( FeatureHistoricStatsAnomalies  ` )

A list of historical Stats and Anomalies generated for all Features.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;objective&quot;: enum (ModelDeploymentMonitoringObjectiveType),&quot;deployedModelId&quot;: string,&quot;anomalyCount&quot;: integer,&quot;featureStats&quot;: [{object (FeatureHistoricStatsAnomalies)}]}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureHistoricStatsAnomalies

Historical Stats (and Anomalies) for a specific feature.

Fields

`featureDisplayName` `string`

Display name of the feature.

`threshold` ` object ( ThresholdConfig  ` )

Threshold for anomaly detection.

`trainingStats` ` object ( FeatureStatsAnomaly  ` )

Stats calculated for the Training Dataset.

`predictionStats[]` ` object ( FeatureStatsAnomaly  ` )

A list of historical stats generated by different time window's Prediction Dataset.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureDisplayName&quot;: string,&quot;threshold&quot;: {object (ThresholdConfig)},&quot;trainingStats&quot;: {object (FeatureStatsAnomaly)},&quot;predictionStats&quot;: [{object (FeatureStatsAnomaly)}]}</code></pre></td>
</tr>
</tbody>
</table>
