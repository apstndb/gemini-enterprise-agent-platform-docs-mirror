---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials/complete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials/complete
title: 'Method: trials.complete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.trials.complete

Marks a Trial as complete.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:complete`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`

### Request body

The request body contains data with the following structure:

Fields

`finalMeasurement` ` object ( Measurement  ` )

Optional. If provided, it will be used as the completed Trial's finalMeasurement; Otherwise, the service will auto-select a previously reported measurement as the final-measurement

`trialInfeasible` `boolean`

Optional. True if the Trial cannot be run with the given Parameter, and finalMeasurement will be ignored.

`infeasibleReason` `string`

Optional. A human readable reason why the trial was infeasible. This should only be provided if `trialInfeasible` is true.

### Response body

If successful, the response body contains an instance of `  Trial  ` .
