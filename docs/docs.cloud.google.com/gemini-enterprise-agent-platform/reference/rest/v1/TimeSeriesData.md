---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/TimeSeriesData
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/TimeSeriesData
title: TimeSeriesData
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

All the data stored in a TensorboardTimeSeries.

Fields

`tensorboardTimeSeriesId` `string`

Required. The id of the TensorboardTimeSeries, which will become the final component of the TensorboardTimeSeries' resource name

`valueType` `enum ( `[`ValueType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs.timeSeries#ValueType)` )`

Required. Immutable. The value type of this time series. All the values in this time series data must match this value type.

`values[]` `object ( `[`TimeSeriesDataPoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/TimeSeriesDataPoint)` )`

Required. data points in this time series.

**JSON representation**

```
{
  "tensorboardTimeSeriesId": string,
  "valueType": enum (ValueType),
  "values": [
    {
      object (TimeSeriesDataPoint)
    }
  ]
}
```
