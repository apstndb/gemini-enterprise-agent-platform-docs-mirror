---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Measurement
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Measurement
title: Measurement
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A message representing a Measurement of a Trial. A Measurement contains the Metrics got by executing a Trial using suggested hyperparameter values.

Fields

`elapsedDuration` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Output only. time that the Trial has been running at the point of this Measurement.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`stepCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The number of steps the machine learning model has been trained for. Must be non-negative.

`metrics[]` `object ( `[`Metric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Measurement#Metric)` )`

Output only. A list of metrics got by evaluating the objective functions using suggested Parameter values.

**JSON representation**

```
{
  "elapsedDuration": string,
  "stepCount": string,
  "metrics": [
    {
      object (Metric)
    }
  ]
}
```

## Metric

A message representing a metric in the measurement.

Fields

`metricId` `string`

Output only. The id of the Metric. The Metric should be defined in [`StudySpec's Metrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/StudySpec#FIELDS.metrics) .

`value` `number`

Output only. The value for this metric.

**JSON representation**

```
{
  "metricId": string,
  "value": number
}
```
