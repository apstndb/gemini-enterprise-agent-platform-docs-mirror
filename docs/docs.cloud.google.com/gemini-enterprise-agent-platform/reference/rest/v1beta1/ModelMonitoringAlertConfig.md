---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringAlertConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringAlertConfig
title: ModelMonitoringAlertConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The alert config for model monitoring.

Fields

`enableLogging` `boolean`

Dump the anomalies to Cloud Logging. The anomalies will be put to json payload encoded from proto `  ModelMonitoringStatsAnomalies  ` . This can be further synced to Pub/Sub or any other services supported by Cloud Logging.

`notificationChannels[]` `string`

Resource names of the NotificationChannels to send alert. Must be of the format `projects/<project_id_or_number>/notificationChannels/<channelId>`

`alert` `Union type`

`alert` can be only one of the following:

`emailAlertConfig` ` object ( EmailAlertConfig  ` )

email alert config.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enableLogging&quot;: boolean,&quot;notificationChannels&quot;: [string],// alert&quot;emailAlertConfig&quot;: {object (EmailAlertConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## EmailAlertConfig

The config for email alert.

Fields

`userEmails[]` `string`

The email addresses to send the alert.

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
  &quot;userEmails&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>
