---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards/readUsage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards/readUsage
title: 'Method: tensorboards.readUsage'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.readUsage

Returns a list of monthly active users for a given TensorBoard instance.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{tensorboard}:readUsage`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`tensorboard` `string`

Required. The name of the Tensorboard resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`

### Request body

The request body must be empty.

### Response body

Response message for [`TensorboardService.ReadTensorboardUsage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards/readUsage#google.cloud.aiplatform.v1beta1.TensorboardService.ReadTensorboardUsage) .

If successful, the response body contains data with the following structure:

Fields

`monthlyUsageData` `map (key: string, value: object ( `[`PerMonthUsageData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards/readUsage#PerMonthUsageData)` ))`

Maps year-month (YYYYMM) string to per month usage data.

**JSON representation**

```
{
  "monthlyUsageData": {
    string: {
      object (PerMonthUsageData)
    },
    ...
  }
}
```

## PerMonthUsageData

Per month usage data

Fields

`userUsageData[]` `object ( `[`PerUserUsageData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards/readUsage#PerUserUsageData)` )`

Usage data for each user in the given month.

**JSON representation**

```
{
  "userUsageData": [
    {
      object (PerUserUsageData)
    }
  ]
}
```

## PerUserUsageData

Per user usage data.

Fields

`username` `string`

user's username

`viewCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of times the user has read data within the Tensorboard.

**JSON representation**

```
{
  "username": string,
  "viewCount": string
}
```
