---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringAlerts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/searchModelMonitoringAlerts
title: 'Method: modelMonitors.searchModelMonitoringAlerts'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelMonitors.searchModelMonitoringAlerts

Returns the Model Monitoring alerts.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{modelMonitor}:searchModelMonitoringAlerts`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`modelMonitor` `string`

Required. ModelMonitor resource name. Format: `projects/{project}/locations/{location}/modelMonitors/{modelMonitor}`

### Request body

The request body contains data with the following structure:

Fields

`modelMonitoringJob` `string`

If non-empty, returns the alerts of this model monitoring job.

`alertTimeInterval` ` object ( Interval  ` )

If non-empty, returns the alerts in this time interval.

`statsName` `string`

If non-empty, returns the alerts of this statsName.

`objectiveType` `string`

If non-empty, returns the alerts of this objective type. Supported monitoring objectives: `raw-feature-drift` `prediction-output-drift` `feature-attribution`

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

A page token received from a previous `  ModelMonitoringService.SearchModelMonitoringAlerts  ` call.

### Response body

Response message for `  ModelMonitoringService.SearchModelMonitoringAlerts  ` .

If successful, the response body contains data with the following structure:

Fields

`modelMonitoringAlerts[]` ` object ( ModelMonitoringAlert  ` )

Alerts retrieved for the requested objectives. Sorted by alert time descendingly.

`totalNumberAlerts` `string ( int64 format)`

The total number of alerts retrieved by the requested objectives.

`nextPageToken` `string`

The page token that can be used by the next `  ModelMonitoringService.SearchModelMonitoringAlerts  ` call.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelMonitoringAlerts&quot;: [{object (ModelMonitoringAlert)}],&quot;totalNumberAlerts&quot;: string,&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## ModelMonitoringAlert

Represents a single monitoring alert. This is currently used in the modelMonitors.searchModelMonitoringAlerts api, thus the alert wrapped in this message belongs to the resource asked in the request.

Fields

`statsName` `string`

The stats name.

`objectiveType` `string`

One of the supported monitoring objectives: `raw-feature-drift` `prediction-output-drift` `feature-attribution`

`alertTime` ` string ( Timestamp  ` format)

Alert creation time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`anomaly` ` object ( ModelMonitoringAnomaly  ` )

Anomaly details.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;statsName&quot;: string,&quot;objectiveType&quot;: string,&quot;alertTime&quot;: string,&quot;anomaly&quot;: {object (ModelMonitoringAnomaly)}}</code></pre></td>
</tr>
</tbody>
</table>

## ModelMonitoringAnomaly

Represents a single model monitoring anomaly.

Fields

`modelMonitoringJob` `string`

Model monitoring job resource name.

`algorithm` `string`

algorithm used to calculated the metrics, eg: jensen\_shannon\_divergence, l\_infinity.

`anomaly` `Union type`

`anomaly` can be only one of the following:

`tabularAnomaly` ` object ( TabularAnomaly  ` )

Tabular anomaly.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelMonitoringJob&quot;: string,&quot;algorithm&quot;: string,// anomaly&quot;tabularAnomaly&quot;: {object (TabularAnomaly)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TabularAnomaly

Tabular anomaly details.

Fields

`anomalyUri` `string`

Additional anomaly information. e.g. Google Cloud Storage uri.

`summary` `string`

Overview of this anomaly.

`anomaly` ` value ( Value  ` format)

Anomaly body.

`triggerTime` ` string ( Timestamp  ` format)

The time the anomaly was triggered.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`condition` ` object ( ModelMonitoringAlertCondition  ` )

The alert condition associated with this anomaly.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;anomalyUri&quot;: string,&quot;summary&quot;: string,&quot;anomaly&quot;: value,&quot;triggerTime&quot;: string,&quot;condition&quot;: {object (ModelMonitoringAlertCondition)}}</code></pre></td>
</tr>
</tbody>
</table>
