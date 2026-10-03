---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringOutputSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringOutputSpec
title: ModelMonitoringOutputSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Specification for the export destination of monitoring results, including metrics, logs, etc.

Fields

`gcsBaseDirectory` `object ( ``GcsDestination`` )`

Google Cloud Storage base folder path for metrics, error logs, etc.

**JSON representation**

```
{
  "gcsBaseDirectory": {
    object (GcsDestination)
  }
}
```
