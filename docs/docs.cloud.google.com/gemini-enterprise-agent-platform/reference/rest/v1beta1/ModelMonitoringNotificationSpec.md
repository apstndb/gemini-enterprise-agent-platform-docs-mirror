---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringNotificationSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringNotificationSpec
title: ModelMonitoringNotificationSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Notification spec(email, notification channel) for model monitoring statistics/alerts.

Fields

`emailConfig` ` object ( EmailConfig  ` )

email alert config.

`enableCloudLogging` `boolean`

Dump the anomalies to Cloud Logging. The anomalies will be put to json payload encoded from proto \[google.cloud.aiplatform.logging.ModelMonitoringAnomaliesLogEntry\]\[\]. This can be further sinked to Pub/Sub or any other services supported by Cloud Logging.

`notificationChannelConfigs[]` ` object ( NotificationChannelConfig  ` )

Notification channel config.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;emailConfig&quot;: {object (EmailConfig)},&quot;enableCloudLogging&quot;: boolean,&quot;notificationChannelConfigs&quot;: [{object (NotificationChannelConfig)}]}</code></pre></td>
</tr>
</tbody>
</table>

## EmailConfig

The config for email alerts.

Fields

`userEmails[]` `string`

The email addresses to send the alerts.

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

## NotificationChannelConfig

Google Cloud Notification channel config.

Fields

`notificationChannel` `string`

Resource names of the NotificationChannels. Must be of the format `projects/<project_id_or_number>/notificationChannels/<channelId>`

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
  &quot;notificationChannel&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
