---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringNotificationSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringNotificationSpec
title: ModelMonitoringNotificationSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Notification spec(email, notification channel) for model monitoring statistics/alerts.

Fields

`emailConfig` `object ( `[`EmailConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringNotificationSpec#EmailConfig)` )`

email alert config.

`enableCloudLogging` `boolean`

Dump the anomalies to Cloud Logging. The anomalies will be put to json payload encoded from proto \[google.cloud.aiplatform.logging.ModelMonitoringAnomaliesLogEntry\]\[\]. This can be further sinked to Pub/Sub or any other services supported by Cloud Logging.

`notificationChannelConfigs[]` `object ( `[`NotificationChannelConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringNotificationSpec#NotificationChannelConfig)` )`

Notification channel config.

**JSON representation**

```
{
  "emailConfig": {
    object (EmailConfig)
  },
  "enableCloudLogging": boolean,
  "notificationChannelConfigs": [
    {
      object (NotificationChannelConfig)
    }
  ]
}
```

## EmailConfig

The config for email alerts.

Fields

`userEmails[]` `string`

The email addresses to send the alerts.

**JSON representation**

```
{
  "userEmails": [
    string
  ]
}
```

## NotificationChannelConfig

Google Cloud Notification channel config.

Fields

`notificationChannel` `string`

Resource names of the NotificationChannels. Must be of the format `projects/<project_id_or_number>/notificationChannels/<channelId>`

**JSON representation**

```
{
  "notificationChannel": string
}
```
