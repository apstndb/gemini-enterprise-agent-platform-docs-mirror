---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.schedules/resume
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.schedules/resume
title: 'Method: schedules.resume'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.schedules.resume

Resumes a paused Schedule to start scheduling new runs. Will mark `  Schedule.state  ` to 'ACTIVE'. Only paused Schedule can be resumed.

When the Schedule is resumed, new runs will be scheduled starting from the next execution time after the current time based on the time\_specification in the Schedule. If `  Schedule.catch_up  ` is set up true, all missed runs will be scheduled for backfill first.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:resume`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the Schedule resource to be resumed. Format: `projects/{project}/locations/{location}/schedules/{schedule}`

### Request body

The request body contains data with the following structure:

Fields

`catchUp` `boolean`

Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update `  Schedule.catch_up  ` field. Default to false.

### Response body

If successful, the response body is an empty JSON object.
