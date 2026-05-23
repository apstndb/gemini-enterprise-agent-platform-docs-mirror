---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials/checkTrialEarlyStoppingState
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials/checkTrialEarlyStoppingState
title: 'Method: trials.checkTrialEarlyStoppingState'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.trials.checkTrialEarlyStoppingState

Checks whether a Trial should stop or not. Returns a long-running operation. When the operation is successful, it will contain a `  CheckTrialEarlyStoppingStateResponse  ` .

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{trialName}:checkTrialEarlyStoppingState`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`trialName` `string`

Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
