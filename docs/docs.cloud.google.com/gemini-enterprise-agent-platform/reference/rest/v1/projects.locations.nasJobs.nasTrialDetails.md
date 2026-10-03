---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails
title: 'REST Resource: projects.locations.nasJobs.nasTrialDetails'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: NasTrialDetail

Represents a NasTrial details along with its parameters. If there is a corresponding train NasTrial, the train NasTrial is also returned.

Fields

`name` `string`

Output only. Resource name of the NasTrialDetail.

`parameters` `string`

The parameters for the NasJob NasTrial.

`searchTrial` `object ( `[`NasTrial`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NasTrial)` )`

The requested search NasTrial.

`trainTrial` `object ( `[`NasTrial`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NasTrial)` )`

The train NasTrial corresponding to [`searchTrial`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails#NasTrialDetail.FIELDS.search_trial) . Only populated if [`searchTrial`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails#NasTrialDetail.FIELDS.search_trial) is used for training.

**JSON representation**

```
{
  "name": string,
  "parameters": string,
  "searchTrial": {
    object (NasTrial)
  },
  "trainTrial": {
    object (NasTrial)
  }
}
```

| Methods                                                                                                                                    |                                       |
|--------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails/get)   | Gets a NasTrialDetail.                |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails/list) | List top NasTrialDetails of a NasJob. |
