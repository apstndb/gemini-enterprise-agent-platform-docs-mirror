---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/patch
title: 'Method: projects.locations.runtimes.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Update Notebook Runtime configuration.

### HTTP request

`PATCH https://notebooks.googleapis.com/v1/{runtime.name}`

### Path parameters

Parameters

`runtime.name`

`string`

Output only. The resource name of the runtime. Format: `projects/{project}/locations/{location}/runtimes/{runtimeId}`

### Query parameters

Parameters

`updateMask`

` string ( FieldMask  ` format)

Required. Specifies the path, relative to `Runtime` , of the field to update. For example, to change the software configuration kernels, the `updateMask` parameter would be specified as `softwareConfig.kernels` , and the `PATCH` request body would specify the new value, as follows:

    {
      "softwareConfig":{
        "kernels": [{
           'repository':
           'gcr.io/deeplearning-platform-release/pytorch-gpu', 'tag':
           'latest' }],
        }
    }

Currently, only the following fields can be updated:

  - `softwareConfig.kernels`
  - `softwareConfig.post_startup_script`
  - `softwareConfig.custom_gpu_driver_path`
  - `softwareConfig.idle_shutdown`
  - `softwareConfig.idle_shutdown_timeout`
  - `softwareConfig.disable_terminal`
  - `labels`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`requestId`

`string`

Idempotent request UUID.

### Request body

The request body contains an instance of `  Runtime  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
