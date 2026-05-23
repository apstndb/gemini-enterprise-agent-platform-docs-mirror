---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs/patch
title: 'Method: runs.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.runs.patch

Updates a TensorboardRun.

### Endpoint

patch `https: / /{service-endpoint} /v1beta1 /{tensorboardRun.name}`  

`PATCH https://{service-endpoint}/v1beta1/{tensorboardRun.name}`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`tensorboardRun.name` `string`

Output only. name of the TensorboardRun. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`

### Query parameters

`updateMask` ` string ( FieldMask  ` format)

Required. Field mask is used to specify the fields to be overwritten in the TensorboardRun resource by the update. The fields specified in the updateMask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  TensorboardRun  ` .

### Response body

If successful, the response body contains an instance of `  TensorboardRun  ` .
