---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HyperparameterTuningJobSpec
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HyperparameterTuningJobSpec
title: HyperparameterTuningJobSpec
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`studySpec` `object ( `[`StudySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/StudySpec)` )`

Study configuration of the HyperparameterTuningJob.

`trialJobSpec` `object ( `[`CustomJobSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec)` )`

The spec of a trial job. The same spec applies to the CustomJobs created in all the trials.

`maxTrialCount` `integer`

The desired total number of Trials.

`parallelTrialCount` `integer`

The desired number of Trials to run in parallel.

`maxFailedTrialCount` `integer`

The number of failed Trials that need to be seen before failing the HyperparameterTuningJob.

If set to 0, Agent Platform decides how many Trials must fail before the whole job fails.

**JSON representation**

```
{
  "studySpec": {
    object (StudySpec)
  },
  "trialJobSpec": {
    object (CustomJobSpec)
  },
  "maxTrialCount": integer,
  "parallelTrialCount": integer,
  "maxFailedTrialCount": integer
}
```
