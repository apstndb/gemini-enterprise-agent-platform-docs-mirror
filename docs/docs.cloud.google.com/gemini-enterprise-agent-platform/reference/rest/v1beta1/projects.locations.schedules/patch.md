---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.schedules/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.schedules/patch
title: 'Method: schedules.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.schedules.patch

Updates an active or paused Schedule.

When the Schedule is updated, new runs will be scheduled starting from the updated next execution time after the update time based on the time\_specification in the updated Schedule. All unstarted runs before the update time will be skipped while already created runs will NOT be paused or canceled.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{schedule.name}`  

`PATCH https://{service-endpoint}/v1beta1/{schedule.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`schedule.name` `string`

Immutable. The resource name of the Schedule.

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. The update mask applies to the resource. See `  google.protobuf.FieldMask  ` .

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  Schedule  ` .

### Response body

If successful, the response body contains an instance of `  Schedule  ` .
