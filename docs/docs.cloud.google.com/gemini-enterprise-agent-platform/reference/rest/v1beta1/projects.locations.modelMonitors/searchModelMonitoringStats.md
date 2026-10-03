---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats
title: 'Method: modelMonitors.searchModelMonitoringStats'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelMonitors.searchModelMonitoringStats

Searches Model Monitoring Stats generated within a given time window.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{modelMonitor}:searchModelMonitoringStats`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`modelMonitor` `string`

Required. ModelMonitor resource name. Format: `projects/{project}/locations/{location}/modelMonitors/{modelMonitor}`

### Request body

The request body contains data with the following structure:

Fields

`statsFilter` `object ( `[`SearchModelMonitoringStatsFilter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#SearchModelMonitoringStatsFilter)` )`

Filter for search different stats.

`timeInterval` `object ( `[`Interval`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Interval)` )`

The time interval for which results should be returned.

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

A page token received from a previous [`ModelMonitoringService.SearchModelMonitoringStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#google.cloud.aiplatform.v1beta1.ModelMonitoringService.SearchModelMonitoringStats) call.

### Response body

Response message for [`ModelMonitoringService.SearchModelMonitoringStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#google.cloud.aiplatform.v1beta1.ModelMonitoringService.SearchModelMonitoringStats) .

If successful, the response body contains data with the following structure:

Fields

`monitoringStats[]` `object ( `[`ModelMonitoringStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#ModelMonitoringStats)` )`

Stats retrieved for requested objectives.

`nextPageToken` `string`

The page token that can be used by the next [`ModelMonitoringService.SearchModelMonitoringStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#google.cloud.aiplatform.v1beta1.ModelMonitoringService.SearchModelMonitoringStats) call.

**JSON representation**

```
{
  "monitoringStats": [
    {
      object (ModelMonitoringStats)
    }
  ],
  "nextPageToken": string
}
```

## SearchModelMonitoringStatsFilter

Filter for searching ModelMonitoringStats.

Fields

`filter` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`tabularStatsFilter` `object ( `[`TabularStatsFilter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#TabularStatsFilter)` )`

Tabular statistics filter.

End of mutually exclusive fields.

**JSON representation**

```
{

  // filter
  "tabularStatsFilter": {
    object (TabularStatsFilter)
  }
  // Union type
}
```

## TabularStatsFilter

Tabular statistics filter.

Fields

`statsName` `string`

If not specified, will return all the stats_names.

`objectiveType` `string`

One of the supported monitoring objectives: `raw-feature-drift` `prediction-output-drift` `feature-attribution`

`modelMonitoringJob` `string`

From a particular monitoring job.

`modelMonitoringSchedule` `string`

From a particular monitoring schedule.

`algorithm` `string`

Specify the algorithm type used for distance calculation, eg: jensen_shannon_divergence, l_infinity.

**JSON representation**

```
{
  "statsName": string,
  "objectiveType": string,
  "modelMonitoringJob": string,
  "modelMonitoringSchedule": string,
  "algorithm": string
}
```

## ModelMonitoringStats

Represents the collection of statistics for a metric.

Fields

`stats` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`tabularStats` `object ( `[`ModelMonitoringTabularStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#ModelMonitoringTabularStats)` )`

Generated tabular statistics.

End of mutually exclusive fields.

**JSON representation**

```
{

  // stats
  "tabularStats": {
    object (ModelMonitoringTabularStats)
  }
  // Union type
}
```

## ModelMonitoringTabularStats

A collection of data points that describes the time-varying values of a tabular metric.

Fields

`statsName` `string`

The stats name.

`objectiveType` `string`

One of the supported monitoring objectives: `raw-feature-drift` `prediction-output-drift` `feature-attribution`

`dataPoints[]` `object ( `[`ModelMonitoringStatsDataPoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#ModelMonitoringStatsDataPoint)` )`

The data points of this time series. When listing time series, points are returned in reverse time order.

**JSON representation**

```
{
  "statsName": string,
  "objectiveType": string,
  "dataPoints": [
    {
      object (ModelMonitoringStatsDataPoint)
    }
  ]
}
```

## ModelMonitoringStatsDataPoint

Represents a single statistics data point.

Fields

`currentStats` `object ( `[`TypedValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#TypedValue)` )`

Statistics from current dataset.

`baselineStats` `object ( `[`TypedValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#TypedValue)` )`

Statistics from baseline dataset.

`thresholdValue` `number`

Threshold value.

`hasAnomaly` `boolean`

Indicate if the statistics has anomaly.

`modelMonitoringJob` `string`

Model monitoring job resource name.

`schedule` `string`

Schedule resource name.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Statistics create time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`algorithm` `string`

algorithm used to calculated the metrics, eg: jensen_shannon_divergence, l_infinity.

**JSON representation**

```
{
  "currentStats": {
    object (TypedValue)
  },
  "baselineStats": {
    object (TypedValue)
  },
  "thresholdValue": number,
  "hasAnomaly": boolean,
  "modelMonitoringJob": string,
  "schedule": string,
  "createTime": string,
  "algorithm": string
}
```

## TypedValue

Typed value of the statistics.

Fields

`value` `Union type`

The typed value. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`doubleValue` `number`

Double.

`distributionValue` `object ( `[`DistributionDataValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringStats#DistributionDataValue)` )`

Distribution.

End of mutually exclusive fields.

**JSON representation**

```
{

  // value
  "doubleValue": number,
  "distributionValue": {
    object (DistributionDataValue)
  }
  // Union type
}
```

## DistributionDataValue

Summary statistics for a population of values.

Fields

`distribution` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Predictive monitoring drift distribution in `tensorflow.metadata.v0.DatasetFeatureStatistics` format.

`distributionDeviation` `number`

Distribution distance deviation from the current dataset's statistics to baseline dataset's statistics. \* For categorical feature, the distribution distance is calculated by L-inifinity norm or Jensen–Shannon divergence. \* For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence.

**JSON representation**

```
{
  "distribution": value,
  "distributionDeviation": number
}
```
