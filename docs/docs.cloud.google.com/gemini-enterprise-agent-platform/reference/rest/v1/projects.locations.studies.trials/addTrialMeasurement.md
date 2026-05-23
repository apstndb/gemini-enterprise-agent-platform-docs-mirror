---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/addTrialMeasurement
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies.trials/addTrialMeasurement
title: 'Method: trials.addTrialMeasurement'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.trials.addTrialMeasurement

Adds a measurement of the objective metrics to a Trial. This measurement is assumed to have been taken before the Trial is complete.

### Endpoint

post `https: / /{service-endpoint} /v1 /{trialName}:addTrialMeasurement`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`trialName` `string`

Required. The name of the trial to add measurement. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`

### Request body

The request body contains data with the following structure:

Fields

`measurement` ` object ( Measurement  ` )

Required. The measurement to be added to a Trial.

### Response body

If successful, the response body contains an instance of `  Trial  ` .
