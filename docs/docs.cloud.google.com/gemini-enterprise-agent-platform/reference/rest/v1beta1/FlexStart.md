---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FlexStart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FlexStart
title: FlexStart
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

FlexStart is used to schedule the deployment workload on DWS resource. It contains the max duration of the deployment.

Fields

`maxRuntimeDuration` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

The max duration of the deployment is maxRuntimeDuration. The deployment will be terminated after the duration. The maxRuntimeDuration can be set up to 7 days.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

**JSON representation**

```
{
  "maxRuntimeDuration": string
}
```
