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

Dump the anomalies to Cloud Logging. The anomalies will be put to json payload encoded from proto [`ModelMonitoringStatsAnomalies`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#ModelMonitoringStatsAnomalies) . This can be further synced to Pub/Sub or any other services supported by Cloud Logging.

`notificationChannels[]` `string`

Resource names of the NotificationChannels to send alert. Must be of the format `projects/<project_id_or_number>/notificationChannels/<channelId>`

`alert` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`emailAlertConfig` `object ( `[`EmailAlertConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringAlertConfig#EmailAlertConfig)` )`

email alert config.

End of mutually exclusive fields.

**JSON representation**

```
{
  "enableLogging": boolean,
  "notificationChannels": [
    string
  ],

  // alert
  "emailAlertConfig": {
    object (EmailAlertConfig)
  }
  // Union type
}
```

## EmailAlertConfig

The config for email alert.

Fields

`userEmails[]` `string`

The email addresses to send the alert.

**JSON representation**

```
{
  "userEmails": [
    string
  ]
}
```
