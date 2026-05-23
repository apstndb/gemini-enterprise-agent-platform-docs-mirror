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

`statsFilter` ` object ( SearchModelMonitoringStatsFilter  ` )

Filter for search different stats.

`timeInterval` ` object ( Interval  ` )

The time interval for which results should be returned.

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

A page token received from a previous `  ModelMonitoringService.SearchModelMonitoringStats  ` call.

### Response body

Response message for `  ModelMonitoringService.SearchModelMonitoringStats  ` .

If successful, the response body contains data with the following structure:

Fields

`monitoringStats[]` ` object ( ModelMonitoringStats  ` )

Stats retrieved for requested objectives.

`nextPageToken` `string`

The page token that can be used by the next `  ModelMonitoringService.SearchModelMonitoringStats  ` call.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;monitoringStats&quot;: [{object (ModelMonitoringStats)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## SearchModelMonitoringStatsFilter

Filter for searching ModelMonitoringStats.

Fields

`filter` `Union type`

`filter` can be only one of the following:

`tabularStatsFilter` ` object ( TabularStatsFilter  ` )

Tabular statistics filter.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// filter&quot;tabularStatsFilter&quot;: {object (TabularStatsFilter)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TabularStatsFilter

Tabular statistics filter.

Fields

`statsName` `string`

If not specified, will return all the stats\_names.

`objectiveType` `string`

One of the supported monitoring objectives: `raw-feature-drift` `prediction-output-drift` `feature-attribution`

`modelMonitoringJob` `string`

From a particular monitoring job.

`modelMonitoringSchedule` `string`

From a particular monitoring schedule.

`algorithm` `string`

Specify the algorithm type used for distance calculation, eg: jensen\_shannon\_divergence, l\_infinity.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;statsName&quot;: string,
  &quot;objectiveType&quot;: string,
  &quot;modelMonitoringJob&quot;: string,
  &quot;modelMonitoringSchedule&quot;: string,
  &quot;algorithm&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ModelMonitoringStats

Represents the collection of statistics for a metric.

Fields

`stats` `Union type`

`stats` can be only one of the following:

`tabularStats` ` object ( ModelMonitoringTabularStats  ` )

Generated tabular statistics.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// stats&quot;tabularStats&quot;: {object (ModelMonitoringTabularStats)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ModelMonitoringTabularStats

A collection of data points that describes the time-varying values of a tabular metric.

Fields

`statsName` `string`

The stats name.

`objectiveType` `string`

One of the supported monitoring objectives: `raw-feature-drift` `prediction-output-drift` `feature-attribution`

`dataPoints[]` ` object ( ModelMonitoringStatsDataPoint  ` )

The data points of this time series. When listing time series, points are returned in reverse time order.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;statsName&quot;: string,&quot;objectiveType&quot;: string,&quot;dataPoints&quot;: [{object (ModelMonitoringStatsDataPoint)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ModelMonitoringStatsDataPoint

Represents a single statistics data point.

Fields

`currentStats` ` object ( TypedValue  ` )

Statistics from current dataset.

`baselineStats` ` object ( TypedValue  ` )

Statistics from baseline dataset.

`thresholdValue` `number`

Threshold value.

`hasAnomaly` `boolean`

Indicate if the statistics has anomaly.

`modelMonitoringJob` `string`

Model monitoring job resource name.

`schedule` `string`

Schedule resource name.

`createTime` ` string ( Timestamp  ` format)

Statistics create time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`algorithm` `string`

algorithm used to calculated the metrics, eg: jensen\_shannon\_divergence, l\_infinity.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;currentStats&quot;: {object (TypedValue)},&quot;baselineStats&quot;: {object (TypedValue)},&quot;thresholdValue&quot;: number,&quot;hasAnomaly&quot;: boolean,&quot;modelMonitoringJob&quot;: string,&quot;schedule&quot;: string,&quot;createTime&quot;: string,&quot;algorithm&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## TypedValue

Typed value of the statistics.

Fields

`value` `Union type`

The typed value. `value` can be only one of the following:

`doubleValue` `number`

Double.

`distributionValue` ` object ( DistributionDataValue  ` )

Distribution.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// value&quot;doubleValue&quot;: number,&quot;distributionValue&quot;: {object (DistributionDataValue)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## DistributionDataValue

Summary statistics for a population of values.

Fields

`distribution` ` value ( Value  ` format)

Predictive monitoring drift distribution in `tensorflow.metadata.v0.DatasetFeatureStatistics` format.

`distributionDeviation` `number`

Distribution distance deviation from the current dataset's statistics to baseline dataset's statistics. \* For categorical feature, the distribution distance is calculated by L-inifinity norm or Jensen–Shannon divergence. \* For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;distribution&quot;: value,
  &quot;distributionDeviation&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
