---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `create_notebook_execution_schedule`

Use this tool to create a notebook execution schedule to periodically launch scheduled runs of a notebook execution job. Format: 'projects/{project_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context. If no region is specified, prompt the user for one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `create_notebook_execution_schedule` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "create_notebook_execution_schedule",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `ScheduleService.CreateSchedule` .

### CreateScheduleRequest

**JSON representation**

```
{
  "parent": string,
  "schedule": {
    object (Schedule)
  }
}
```

| Fields     |                                                                                                                                                                                                                 |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. The resource name of the Location to create the Schedule in. Format: `projects/{project}/locations/{location}`                                                                               |
| `schedule` | `object ( `[`Schedule`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Schedule)` )` Required. The Schedule to create. |

### Schedule

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "startTime": string,
  "endTime": string,
  "maxRunCount": string,
  "startedRunCount": string,
  "state": enum (State),
  "createTime": string,
  "updateTime": string,
  "nextRunTime": string,
  "lastPauseTime": string,
  "lastResumeTime": string,
  "maxConcurrentRunCount": string,
  "maxConcurrentActiveRunCount": string,
  "allowQueueing": boolean,
  "catchUp": boolean,
  "lastScheduledRunResponse": {
    object (RunResponse)
  },

  // Union field time_specification can be only one of the following:
  "cron": string
  // End of list of possible types for union field time_specification.

  // Union field request can be only one of the following:
  "createPipelineJobRequest": {
    object (CreatePipelineJobRequest)
  },
  "createNotebookExecutionJobRequest": {
    object (CreateNotebookExecutionJobRequest)
  }
  // End of list of possible types for union field request.
}
```

| Fields                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                                           | `string` Immutable. The resource name of the Schedule.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `displayName`                                                                                                                                                                                    | `string` Required. User provided name of the Schedule. The name can be up to 128 characters long and can consist of any UTF-8 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `startTime`                                                                                                                                                                                      | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Optional. Timestamp after which the first run can be scheduled. Default to Schedule create time if not specified. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                      |
| `endTime`                                                                                                                                                                                        | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Optional. Timestamp after which no new runs can be scheduled. If specified, The schedule will be completed when either end_time is reached or when scheduled_run_count \>= max_run_count. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `maxRunCount`                                                                                                                                                                                    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Maximum run count of the schedule. If specified, The schedule will be completed when either started_run_count \>= max_run_count or when end_time is reached. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified.                                                                                                                                                                                                                                                                                                   |
| `startedRunCount`                                                                                                                                                                                | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The number of runs started by this schedule.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `state`                                                                                                                                                                                          | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.State_3)` )` Output only. The state of this Schedule.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `createTime`                                                                                                                                                                                     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Schedule was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                 |
| `updateTime`                                                                                                                                                                                     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Schedule was updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                 |
| `nextRunTime`                                                                                                                                                                                    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Schedule should schedule the next run. Having a next_run_time in the past means the runs are being started behind schedule. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                           |
| `lastPauseTime`                                                                                                                                                                                  | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Schedule was last paused. Unset if never paused. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                      |
| `lastResumeTime`                                                                                                                                                                                 | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Schedule was last resumed. Unset if never resumed from pause. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                         |
| `maxConcurrentRunCount`                                                                                                                                                                          | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Required. Maximum number of runs that can be started concurrently for this Schedule. This is the limit for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable).                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `maxConcurrentActiveRunCount`                                                                                                                                                                    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Specifies the maximum number of active runs that can be executed concurrently for this Schedule. This limits the number of runs that can be in a non-terminal state at the same time. Currently, this field is only supported for requests of type CreatePipelineJobRequest.                                                                                                                                                                                                                                                                                                                                                                |
| `allowQueueing`                                                                                                                                                                                  | `boolean` Optional. Whether new scheduled runs can be queued when max_concurrent_runs limit is reached. If set to true, new runs will be queued instead of skipped. Default to false.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `catchUp`                                                                                                                                                                                        | `boolean` Output only. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. Default to false.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `lastScheduledRunResponse`                                                                                                                                                                       | `object ( `[`RunResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.RunResponse)` )` Output only. Response of the last scheduled run. This is the response for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable). Unset if no run has been scheduled yet.                                                                                                                                                                                                                                                                                                                  |
| Union field `time_specification` . Required. The time specification to launch scheduled runs. `time_specification` can be only one of the following:                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `cron`                                                                                                                                                                                           | `string` Cron schedule ( <https://en.wikipedia.org/wiki/Cron> ) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON_TZ=\${IANA_TIME_ZONE}" or "TZ=\${IANA_TIME_ZONE}". The \${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 \* \* \* \*", or "TZ=America/New_York 1 \* \* \* \*".                                                                                                                                                                                                                                                                                                                              |
| Union field `request` . Required. The API request template to launch the scheduled runs. User-specified ID is not supported in the request template. `request` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `createPipelineJobRequest`                                                                                                                                                                       | `object ( `[`CreatePipelineJobRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.CreatePipelineJobRequest)` )` Request for `PipelineService.CreatePipelineJob` . CreatePipelineJobRequest.parent field is required (format: projects/{project}/locations/{location}).                                                                                                                                                                                                                                                                                                                                                                         |
| `createNotebookExecutionJobRequest`                                                                                                                                                              | `object ( `[`CreateNotebookExecutionJobRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.CreateNotebookExecutionJobRequest)` )` Request for `NotebookService.CreateNotebookExecutionJob` .                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### CreatePipelineJobRequest

**JSON representation**

```
{
  "parent": string,
  "pipelineJob": {
    object (PipelineJob)
  },
  "pipelineJobId": string
}
```

| Fields          |                                                                                                                                                                                                                                                              |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`        | `string` Required. The resource name of the Location to create the PipelineJob in. Format: `projects/{project}/locations/{location}`                                                                                                                         |
| `pipelineJob`   | `object ( `[`PipelineJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineJob)` )` Required. The PipelineJob to create.                                     |
| `pipelineJobId` | `string` The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are `/[a-z][0-9]-/` . |

### PipelineJob

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "createTime": string,
  "startTime": string,
  "endTime": string,
  "updateTime": string,
  "pipelineSpec": {
    object
  },
  "state": enum (PipelineState),
  "jobDetail": {
    object (PipelineJobDetail)
  },
  "error": {
    object (Status)
  },
  "labels": {
    string: string,
    ...
  },
  "runtimeConfig": {
    object (RuntimeConfig)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "serviceAccount": string,
  "network": string,
  "reservedIpRanges": [
    string
  ],
  "pscInterfaceConfig": {
    object (PscInterfaceConfig)
  },
  "templateUri": string,
  "templateMetadata": {
    object (PipelineTemplateMetadata)
  },
  "scheduleName": string,
  "preflightValidations": boolean
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                 | `string` Output only. The resource name of the PipelineJob.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `displayName`          | `string` The display name of the Pipeline. The name can be up to 128 characters long and can consist of any UTF-8 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `createTime`           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Pipeline creation time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                                                                                      |
| `startTime`            | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Pipeline start time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                                                                                         |
| `endTime`              | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Pipeline end time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                                                                                           |
| `updateTime`           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this PipelineJob was most recently updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                                                   |
| `pipelineSpec`         | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` A compiled definition of a pipeline, represented as a `JSON` object. Defines the structure of the pipeline, including its components, tasks, and parameters. This specification is generated by compiling a pipeline function defined in `Python` using the `Kubeflow Pipelines SDK` .                                                                                                                                                                                                                                                                                                                                                                                                         |
| `state`                | `enum ( `[`PipelineState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineState)` )` Output only. The detailed state of the job.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `jobDetail`            | `object ( `[`PipelineJobDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineJobDetail)` )` Output only. The details of pipeline run. Not available in the list view.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `error`                | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. The error that occurred during pipeline execution. Only populated when the pipeline's state is FAILED or CANCELLED.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `labels`               | `map (key: string, value: string)` The labels with user-defined metadata to organize PipelineJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See <https://goo.gl/xmQnxf> for more information and examples of labels. Note there is some reserved label key for Agent Platform Pipelines. - `vertex-ai-pipelines-run-billing-id` , user set value will get overrided. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                          |
| `runtimeConfig`        | `object ( `[`RuntimeConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.RuntimeConfig)` )` Runtime config of the pipeline.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `encryptionSpec`       | `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec)` )` Customer-managed encryption key spec for a pipelineJob. If set, this PipelineJob and all of its sub-resources will be secured by this key.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `serviceAccount`       | `string` The service account that the pipeline workload runs as. If not specified, the Compute Engine default service account in the project will be used. See <https://cloud.google.com/compute/docs/access/service-accounts#default_service_account> Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service account.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `network`              | `string` The full name of the Compute Engine [network](https://docs.cloud.google.com/compute/docs/networks-and-firewalls#networks) to which the Pipeline Job's workload should be peered. For example, `projects/12345/global/networks/myVPC` . [Format](https://docs.cloud.google.com/compute/docs/reference/rest/v1/networks/insert) is of the form `projects/{project}/global/networks/{network}` . Where {project} is a project number, as in `12345` , and {network} is a network name. Private services access must already be configured for the network. Pipeline job will apply the network configuration to the Google Cloud resources being launched, if applied, such as Agent Platform Training or Dataflow job. If left unspecified, the workload is not peered with any network. |
| `reservedIpRanges[]`   | `string` A list of names for the reserved ip ranges under the VPC network that can be used for this Pipeline Job's workload. If set, we will deploy the Pipeline Job's workload within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network. Example: \['vertex-ai-ip-range'\].                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `pscInterfaceConfig`   | `object ( `[`PscInterfaceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PscInterfaceConfig)` )` Optional. Configuration for PSC-I for PipelineJob.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `templateUri`          | `string` A template uri from where the `PipelineJob.pipeline_spec` , if empty, will be downloaded. Currently, only uri from Vertex Template Registry & Gallery is supported. Reference to <https://cloud.google.com/vertex-ai/docs/pipelines/create-pipeline-template> .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `templateMetadata`     | `object ( `[`PipelineTemplateMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineTemplateMetadata)` )` Output only. Pipeline template metadata. Will fill up fields if `PipelineJob.template_uri` is from supported template registry.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `scheduleName`         | `string` Output only. The schedule resource name. Only returned if the Pipeline is created by Schedule API.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `preflightValidations` | `boolean` Optional. Whether to do component level validations before job creation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### Struct

**JSON representation**

```
{
  "fields": {
    string: value,
    ...
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                          |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map (key: string, value: value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format))` Unordered map of dynamically typed values. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### FieldsEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### Value

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean,
  "structValue": {
    object
  },
  "listValue": array
  // End of list of possible types for union field kind.
}
```

| Fields                                                                           |                                                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . The kind of value. `kind` can be only one of the following: |                                                                                                                                                                                                                                                |
| `nullValue`                                                                      | `null` Represents a JSON `null` .                                                                                                                                                                                                              |
| `numberValue`                                                                    | `number` Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type. |
| `stringValue`                                                                    | `string` Represents a JSON string.                                                                                                                                                                                                             |
| `boolValue`                                                                      | `boolean` Represents a JSON boolean ( `true` or `false` literal in JSON).                                                                                                                                                                      |
| `structValue`                                                                    | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Represents a JSON object.                                                                                                                     |
| `listValue`                                                                      | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` Represents a JSON array.                                                                                                                |

### ListValue

**JSON representation**

```
{
  "values": [
    value
  ]
}
```

| Fields     |                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Repeated field of dynamically typed values. |

### PipelineJobDetail

**JSON representation**

```
{
  "pipelineContext": {
    object (Context)
  },
  "pipelineRunContext": {
    object (Context)
  },
  "taskDetails": [
    {
      object (PipelineTaskDetail)
    }
  ]
}
```

| Fields               |                                                                                                                                                                                                                                                                     |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pipelineContext`    | `object ( `[`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Context)` )` Output only. The context of the pipeline.                                               |
| `pipelineRunContext` | `object ( `[`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Context)` )` Output only. The context of the current pipeline run.                                   |
| `taskDetails[]`      | `object ( `[`PipelineTaskDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineTaskDetail)` )` Output only. The runtime details of the tasks under the pipeline. |

### Context

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "parentContexts": [
    string
  ],
  "schemaTitle": string,
  "schemaVersion": string,
  "metadata": {
    object
  },
  "description": string
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`             | `string` Immutable. The resource name of the Context.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `displayName`      | `string` User provided display name of the Context. May be up to 128 Unicode characters.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `etag`             | `string` An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.                                                                                                                                                                                                                                                                                                                                                                                                       |
| `labels`           | `map (key: string, value: string)` The labels with user-defined metadata to organize your Contexts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Context (System labels are excluded). An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `createTime`       | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Context was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                  |
| `updateTime`       | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Context was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                             |
| `parentContexts[]` | `string` Output only. A list of resource names of Contexts that are parents of this Context. A Context may have at most 10 parent_contexts.                                                                                                                                                                                                                                                                                                                                                                                  |
| `schemaTitle`      | `string` The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                        |
| `schemaVersion`    | `string` The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                        |
| `metadata`         | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Properties of the Context. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.                                                                                                                                                                                                                                                                            |
| `description`      | `string` Description of the Context                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### PipelineTaskDetail

**JSON representation**

```
{
  "taskId": string,
  "parentTaskId": string,
  "taskName": string,
  "createTime": string,
  "startTime": string,
  "endTime": string,
  "executorDetail": {
    object (PipelineTaskExecutorDetail)
  },
  "state": enum (State),
  "execution": {
    object (Execution)
  },
  "error": {
    object (Status)
  },
  "pipelineTaskStatus": [
    {
      object (PipelineTaskStatus)
    }
  ],
  "inputs": {
    string: {
      object (ArtifactList)
    },
    ...
  },
  "outputs": {
    string: {
      object (ArtifactList)
    },
    ...
  },
  "taskUniqueName": string
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `taskId`               | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The system generated ID of the task.                                                                                                                                                                                                                                                                                                                                             |
| `parentTaskId`         | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The id of the parent task if the task is within a component scope. Empty if the task is at the root level.                                                                                                                                                                                                                                                                       |
| `taskName`             | `string` Output only. The user specified name of the task that is defined in `pipeline_spec` .                                                                                                                                                                                                                                                                                                                                                                                       |
| `createTime`           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Task create time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                 |
| `startTime`            | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Task start time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                  |
| `endTime`              | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Task end time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                    |
| `executorDetail`       | `object ( `[`PipelineTaskExecutorDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineTaskExecutorDetail)` )` Output only. The detailed execution info.                                                                                                                                                                                                                          |
| `state`                | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.State)` )` Output only. State of the task.                                                                                                                                                                                                                                                                                |
| `execution`            | `object ( `[`Execution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Execution)` )` Output only. The execution metadata of the task.                                                                                                                                                                                                                                                     |
| `error`                | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. The error that occurred during task execution. Only populated when the task's state is FAILED or CANCELLED.                                                                                                                                                                                                     |
| `pipelineTaskStatus[]` | `object ( `[`PipelineTaskStatus`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineTaskStatus)` )` Output only. A list of task status. This field keeps a record of task status evolving over time.                                                                                                                                                                                   |
| `inputs`               | `map (key: string, value: object ( `[`ArtifactList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.ArtifactList)` ))` Output only. The runtime input artifacts of the task. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                          |
| `outputs`              | `map (key: string, value: object ( `[`ArtifactList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.ArtifactList)` ))` Output only. The runtime output artifacts of the task. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                         |
| `taskUniqueName`       | `string` Output only. The unique name of a task. This field is used by rerun pipeline job. Console UI and Agent Platform SDK will support triggering pipeline job reruns. The name is constructed by concatenating all the parent tasks name with the task name. For example, if a task named "child_task" has a parent task named "parent_task_1" and parent task 1 has a parent task named "parent_task_2", the task unique name will be "parent_task_2.parent_task_1.child_task". |

### PipelineTaskExecutorDetail

**JSON representation**

```
{

  // Union field details can be only one of the following:
  "containerDetail": {
    object (ContainerDetail)
  },
  "customJobDetail": {
    object (CustomJobDetail)
  }
  // End of list of possible types for union field details.
}
```

| Fields                                                              |                                                                                                                                                                                                                                                       |
|---------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `details` . `details` can be only one of the following: |                                                                                                                                                                                                                                                       |
| `containerDetail`                                                   | `object ( `[`ContainerDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.ContainerDetail)` )` Output only. The detailed info for a container executor.  |
| `customJobDetail`                                                   | `object ( `[`CustomJobDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.CustomJobDetail)` )` Output only. The detailed info for a custom job executor. |

### ContainerDetail

**JSON representation**

```
{
  "mainJob": string,
  "preCachingCheckJob": string,
  "failedMainJobs": [
    string
  ],
  "failedPreCachingCheckJobs": [
    string
  ]
}
```

| Fields                        |                                                                                                                                                                                                                                                                                                               |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mainJob`                     | `string` Output only. The name of the `CustomJob` for the main container execution.                                                                                                                                                                                                                           |
| `preCachingCheckJob`          | `string` Output only. The name of the `CustomJob` for the pre-caching-check container execution. This job will be available if the `PipelineJob.pipeline_spec` specifies the `pre_caching_check` hook in the lifecycle events.                                                                                |
| `failedMainJobs[]`            | `string` Output only. The names of the previously failed `CustomJob` for the main container executions. The list includes the all attempts in chronological order.                                                                                                                                            |
| `failedPreCachingCheckJobs[]` | `string` Output only. The names of the previously failed `CustomJob` for the pre-caching-check container executions. This job will be available if the `PipelineJob.pipeline_spec` specifies the `pre_caching_check` hook in the lifecycle events. The list includes the all attempts in chronological order. |

### CustomJobDetail

**JSON representation**

```
{
  "job": string,
  "failedJobs": [
    string
  ]
}
```

| Fields         |                                                                                                                                   |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------|
| `job`          | `string` Output only. The name of the `CustomJob` .                                                                               |
| `failedJobs[]` | `string` Output only. The names of the previously failed `CustomJob` . The list includes the all attempts in chronological order. |

### Execution

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "state": enum (State),
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "schemaTitle": string,
  "schemaVersion": string,
  "metadata": {
    object
  },
  "description": string
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`          | `string` Output only. The resource name of the Execution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `displayName`   | `string` User provided display name of the Execution. May be up to 128 Unicode characters.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `state`         | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.State_1)` )` The state of this Execution. This is a property of the Execution, and does not imply or capture any ongoing process. This property is managed by clients (such as Agent Platform Pipelines) and the system does not prescribe or check the validity of state transitions.                                                                                |
| `etag`          | `string` An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.                                                                                                                                                                                                                                                                                                                                                                                                           |
| `labels`        | `map (key: string, value: string)` The labels with user-defined metadata to organize your Executions. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Execution (System labels are excluded). An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `createTime`    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Execution was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                    |
| `updateTime`    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Execution was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                               |
| `schemaTitle`   | `string` The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                            |
| `schemaVersion` | `string` The version of the schema in `schema_title` to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                         |
| `metadata`      | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Properties of the Execution. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.                                                                                                                                                                                                                                                                              |
| `description`   | `string` Description of the Execution                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### Status

**JSON representation**

```
{
  "code": integer,
  "message": string,
  "details": [
    {
      "@type": string,
      field1: ...,
      ...
    }
  ]
}
```

| Fields      |                                                                                                                                                                                                                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`      | `integer` The status code, which should be an enum value of `google.rpc.Code` .                                                                                                                                                                                                                              |
| `message`   | `string` A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.                                                                                                      |
| `details[]` | `object` A list of messages that carry the error details. There is a common set of message types for APIs to use. An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` . |

### Any

**JSON representation**

```
{
  "typeUrl": string,
  "value": string
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `typeUrl` | `string` Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name. Example: type.googleapis.com/google.protobuf.StringValue This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them. The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests. All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected. In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs. |
| `value`   | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Holds a Protobuf serialization of the type described by type_url. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### PipelineTaskStatus

**JSON representation**

```
{
  "updateTime": string,
  "state": enum (State),
  "error": {
    object (Status)
  }
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `updateTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Update time of this status. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                         |
| `state`      | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.State)` )` Output only. The state of the task.                                                                                                                                                                                                                                                                              |
| `error`      | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. The error that occurred during the state. May be set when the state is any of the non-final state (PENDING/RUNNING/CANCELLING) or FAILED state. If the state is FAILED, the error here is final and not going to be retried. If the state is a non-final state, the error indicates a system-error being retried. |

### InputsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (ArtifactList)
  }
}
```

| Fields  |                                                                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                              |
| `value` | `object ( `[`ArtifactList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.ArtifactList)` )` |

### ArtifactList

**JSON representation**

```
{
  "artifacts": [
    {
      object (Artifact)
    }
  ]
}
```

| Fields        |                                                                                                                                                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `artifacts[]` | `object ( `[`Artifact`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Artifact)` )` Output only. A list of artifact metadata. |

### Artifact

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "uri": string,
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "state": enum (State),
  "schemaTitle": string,
  "schemaVersion": string,
  "metadata": {
    object
  },
  "description": string
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`          | `string` Output only. The resource name of the Artifact.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `displayName`   | `string` User provided display name of the Artifact. May be up to 128 Unicode characters.                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `uri`           | `string` The uniform resource identifier of the artifact file. May be empty if there is no actual artifact file.                                                                                                                                                                                                                                                                                                                                                                                                               |
| `etag`          | `string` An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.                                                                                                                                                                                                                                                                                                                                                                                                         |
| `labels`        | `map (key: string, value: string)` The labels with user-defined metadata to organize your Artifacts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Artifact (System labels are excluded). An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `createTime`    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Artifact was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                   |
| `updateTime`    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Artifact was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                              |
| `state`         | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.State_2)` )` The state of this Artifact. This is a property of the Artifact, and does not imply or capture any ongoing process. This property is managed by clients (such as Agent Platform Pipelines), and the system does not prescribe or check the validity of state transitions.                                                                               |
| `schemaTitle`   | `string` The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                          |
| `schemaVersion` | `string` The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                          |
| `metadata`      | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Properties of the Artifact. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.                                                                                                                                                                                                                                                                             |
| `description`   | `string` Description of the Artifact                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### OutputsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (ArtifactList)
  }
}
```

| Fields  |                                                                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                              |
| `value` | `object ( `[`ArtifactList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.ArtifactList)` )` |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### RuntimeConfig

**JSON representation**

```
{
  "parameters": {
    string: {
      object (Value)
    },
    ...
  },
  "gcsOutputDirectory": string,
  "parameterValues": {
    string: value,
    ...
  },
  "failurePolicy": enum (PipelineFailurePolicy),
  "inputArtifacts": {
    string: {
      object (InputArtifact)
    },
    ...
  }
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parameters </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>map (key: string, value: object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Value_1"><code>Value</code></a><code> ))</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated. Use <code>RuntimeConfig.parameter_values</code> instead. The runtime parameters of the PipelineJob. The parameters will be passed into <code>PipelineJob.pipeline_spec</code> to replace the placeholders at runtime. This field is used by pipelines built using <code>PipelineJob.pipeline_spec.schema_version</code> 2.0.0 or lower, such as pipelines built using Kubeflow Pipelines SDK 1.8 or lower.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>gcsOutputDirectory</code></td>
<td><p><code>string</code></p>
<p>Required. A path in a Cloud Storage bucket, which will be treated as the root output directory of the pipeline. It is used by the system to generate the paths of output artifacts. The artifact paths are generated with a sub-path pattern <code>{job_id}/{task_id}/{output_key}</code> under the specified output directory. The service account specified in this pipeline must have the <code>storage.objects.get</code> and <code>storage.objects.create</code> permissions for this bucket.</p></td>
</tr>
<tr class="odd">
<td><code>parameterValues</code></td>
<td><p><code>map (key: string, value: value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format))</code></p>
<p>The runtime parameters of the PipelineJob. The parameters will be passed into <code>PipelineJob.pipeline_spec</code> to replace the placeholders at runtime. This field is used by pipelines built using <code>PipelineJob.pipeline_spec.schema_version</code> 2.1.0, such as pipelines built using Kubeflow Pipelines SDK 1.9 or higher and the v2 DSL.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>failurePolicy</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineFailurePolicy"><code>PipelineFailurePolicy</code></a><code> )</code></p>
<p>Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW. However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion.</p></td>
</tr>
<tr class="odd">
<td><code>inputArtifacts</code></td>
<td><p><code>map (key: string, value: object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.InputArtifact"><code>InputArtifact</code></a><code> ))</code></p>
<p>The runtime artifacts of the PipelineJob. The key will be the input artifact name and the value would be one of the InputArtifact.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
</tbody>
</table>

### ParametersEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (Value)
  }
}
```

| Fields  |                                                                                                                                                                           |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                  |
| `value` | `object ( `[`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Value_1)` )` |

### Value

**JSON representation**

```
{

  // Union field value can be only one of the following:
  "intValue": string,
  "doubleValue": number,
  "stringValue": string
  // End of list of possible types for union field value.
}
```

| Fields                                                          |                                                                                                          |
|-----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Union field `value` . `value` can be only one of the following: |                                                                                                          |
| `intValue`                                                      | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` An integer value. |
| `doubleValue`                                                   | `number` A double value.                                                                                 |
| `stringValue`                                                   | `string` A string value.                                                                                 |

### ParameterValuesEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### InputArtifactsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (InputArtifact)
  }
}
```

| Fields  |                                                                                                                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                                |
| `value` | `object ( `[`InputArtifact`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.InputArtifact)` )` |

### InputArtifact

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "artifactId": string
  // End of list of possible types for union field kind.
}
```

| Fields                                                        |                                                                                                                                                                                                                                                                                                 |
|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . `kind` can be only one of the following: |                                                                                                                                                                                                                                                                                                 |
| `artifactId`                                                  | `string` Artifact resource id from MLMD. Which is the last portion of an artifact resource name: `projects/{project}/locations/{location}/metadataStores/default/artifacts/{artifact_id}` . The artifact must stay within the same project, location and default metadatastore as the pipeline. |

### EncryptionSpec

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Required. Resource name of the Cloud KMS key used to protect the resource. The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

### PscInterfaceConfig

**JSON representation**

```
{
  "networkAttachment": string,
  "dnsPeeringConfigs": [
    {
      object (DnsPeeringConfig)
    }
  ]
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `networkAttachment`   | `string` Optional. The name of the Compute Engine [network attachment](https://cloud.google.com/vpc/docs/about-network-attachments) to attach to the resource within the region and user project. To specify this field, you must have already [created a network attachment](https://cloud.google.com/vpc/docs/create-manage-network-attachments#create-network-attachments) . This field is only used for resources using PSC-I.                                                                               |
| `dnsPeeringConfigs[]` | `object ( `[`DnsPeeringConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.DnsPeeringConfig)` )` Optional. DNS peering configurations. When specified, Agent Platform will attempt to configure DNS peering zones in the tenant project VPC to resolve the specified domains using the target network's Cloud DNS. The user must grant the dns.peer role to the Agent Platform Service Agent on the target project. |

### DnsPeeringConfig

**JSON representation**

```
{
  "domain": string,
  "targetProject": string,
  "targetNetwork": string
}
```

| Fields          |                                                                                                                                                                               |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `domain`        | `string` Required. The DNS name suffix of the zone being peered to, e.g., "my-internal-domain.corp.". Must end with a dot.                                                    |
| `targetProject` | `string` Required. The project ID hosting the Cloud DNS managed zone that contains the 'domain'. The Agent Platform Service Agent requires the dns.peer role on this project. |
| `targetNetwork` | `string` Required. The VPC network name in the target_project where the DNS zone specified by 'domain' is visible.                                                            |

### PipelineTemplateMetadata

**JSON representation**

```
{
  "version": string
}
```

| Fields    |                                                                                                                                                                                               |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `version` | `string` The version_name in artifact registry. Will always be presented in output if the `PipelineJob.template_uri` is from supported template registry. Format is "sha256:abcdef123456...". |

### CreateNotebookExecutionJobRequest

**JSON representation**

```
{
  "parent": string,
  "notebookExecutionJob": {
    object (NotebookExecutionJob)
  },
  "notebookExecutionJobId": string
}
```

| Fields                   |                                                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                 | `string` Required. The resource name of the Location to create the NotebookExecutionJob. Format: `projects/{project}/locations/{location}`                                                                                                     |
| `notebookExecutionJob`   | `object ( `[`NotebookExecutionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.NotebookExecutionJob)` )` Required. The NotebookExecutionJob to create. |
| `notebookExecutionJobId` | `string` Optional. User specified ID for the NotebookExecutionJob.                                                                                                                                                                             |

### NotebookExecutionJob

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "executionTimeout": string,
  "scheduleResourceName": string,
  "jobState": enum (JobState),
  "status": {
    object (Status)
  },
  "createTime": string,
  "updateTime": string,
  "labels": {
    string: string,
    ...
  },
  "kernelName": string,
  "encryptionSpec": {
    object (EncryptionSpec)
  },

  // Union field notebook_source can be only one of the following:
  "dataformRepositorySource": {
    object (DataformRepositorySource)
  },
  "gcsNotebookSource": {
    object (GcsNotebookSource)
  },
  "directNotebookSource": {
    object (DirectNotebookSource)
  }
  // End of list of possible types for union field notebook_source.

  // Union field environment_spec can be only one of the following:
  "notebookRuntimeTemplateResourceName": string,
  "customEnvironmentSpec": {
    object (CustomEnvironmentSpec)
  }
  // End of list of possible types for union field environment_spec.

  // Union field execution_sink can be only one of the following:
  "gcsOutputUri": string
  // End of list of possible types for union field execution_sink.

  // Union field execution_identity can be only one of the following:
  "executionUser": string,
  "serviceAccount": string
  // End of list of possible types for union field execution_identity.

  // Union field runtime_environment can be only one of the following:
  "workbenchRuntime": {
    object (WorkbenchRuntime)
  }
  // End of list of possible types for union field runtime_environment.
}
```

| Fields                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                                                | `string` Output only. The resource name of this NotebookExecutionJob. Format: `projects/{project_id}/locations/{location}/notebookExecutionJobs/{job_id}`                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `displayName`                                                                                                                                                                                         | `string` The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `executionTimeout`                                                                                                                                                                                    | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Max running time of the execution job in seconds (default 86400s / 24 hrs). A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .                                                                                                                                                                                                                                                                                                                            |
| `scheduleResourceName`                                                                                                                                                                                | `string` The Schedule resource name if this job is triggered by one. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `jobState`                                                                                                                                                                                            | `enum ( `[`JobState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.JobState)` )` Output only. The state of the NotebookExecutionJob.                                                                                                                                                                                                                                                                                                                                                                                                |
| `status`                                                                                                                                                                                              | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated.                                                                                                                                                                                                                                                                                                 |
| `createTime`                                                                                                                                                                                          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this NotebookExecutionJob was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                      |
| `updateTime`                                                                                                                                                                                          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this NotebookExecutionJob was most recently updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                        |
| `labels`                                                                                                                                                                                              | `map (key: string, value: string)` The labels with user-defined metadata to organize NotebookExecutionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `kernelName`                                                                                                                                                                                          | `string` The name of the kernel to use during notebook execution. If unset, the default kernel is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `encryptionSpec`                                                                                                                                                                                      | `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec)` )` Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the [`NotebookRuntimeTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookRuntimeTemplate) has an encryption spec.                                                                                              |
| Union field `notebook_source` . The input notebook. `notebook_source` can be only one of the following:                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `dataformRepositorySource`                                                                                                                                                                            | `object ( `[`DataformRepositorySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.DataformRepositorySource)` )` The Dataform Repository pointing to a single file notebook repository.                                                                                                                                                                                                                                                                                                                               |
| `gcsNotebookSource`                                                                                                                                                                                   | `object ( `[`GcsNotebookSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.GcsNotebookSource)` )` The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`                                                                                                                                                                                                                                                                                                                        |
| `directNotebookSource`                                                                                                                                                                                | `object ( `[`DirectNotebookSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.DirectNotebookSource)` )` The contents of an input notebook file.                                                                                                                                                                                                                                                                                                                                                                      |
| Union field `environment_spec` . The compute config to use for an execution job. `environment_spec` can be only one of the following:                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `notebookRuntimeTemplateResourceName`                                                                                                                                                                 | `string` The NotebookRuntimeTemplate to source compute configuration from.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `customEnvironmentSpec`                                                                                                                                                                               | `object ( `[`CustomEnvironmentSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.CustomEnvironmentSpec)` )` The custom compute configuration for an execution job.                                                                                                                                                                                                                                                                                                                                                     |
| Union field `execution_sink` . The location to store the notebook execution result. `execution_sink` can be only one of the following:                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `gcsOutputUri`                                                                                                                                                                                        | `string` The Cloud Storage location to upload the result to. Format: `gs://bucket-name`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `execution_identity` . The identity to run the execution as. `execution_identity` can be only one of the following:                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `executionUser`                                                                                                                                                                                       | `string` The user email to run the execution as. Only supported by Colab runtimes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `serviceAccount`                                                                                                                                                                                      | `string` The service account to run the execution as.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Union field `runtime_environment` . Runtime environment for the notebook execution job. If unspecified, the default runtime of Colab is used. `runtime_environment` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `workbenchRuntime`                                                                                                                                                                                    | `object ( `[`WorkbenchRuntime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.WorkbenchRuntime)` )` The Workbench runtime configuration to use for the notebook execution.                                                                                                                                                                                                                                                                                                                                               |

### DataformRepositorySource

**JSON representation**

```
{
  "dataformRepositoryResourceName": string,
  "commitSha": string
}
```

| Fields                           |                                                                                                                                          |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| `dataformRepositoryResourceName` | `string` The resource name of the Dataform Repository. Format: `projects/{project_id}/locations/{location}/repositories/{repository_id}` |
| `commitSha`                      | `string` The commit SHA to read repository with. If unset, the file will be read at HEAD.                                                |

### GcsNotebookSource

**JSON representation**

```
{
  "uri": string,
  "generation": string
}
```

| Fields       |                                                                                                                                                                                         |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uri`        | `string` The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`                                                                                    |
| `generation` | `string` The version of the Cloud Storage object to read. If unset, the current version of the object is read. See <https://cloud.google.com/storage/docs/metadata#generation-number> . |

### DirectNotebookSource

**JSON representation**

```
{
  "content": string
}
```

| Fields    |                                                                                                                                                                         |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `content` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The base64-encoded contents of the input notebook file. A base64-encoded string. |

### CustomEnvironmentSpec

**JSON representation**

```
{
  "machineSpec": {
    object (MachineSpec)
  },
  "persistentDiskSpec": {
    object (PersistentDiskSpec)
  },
  "networkSpec": {
    object (NetworkSpec)
  },
  "shieldedInstanceConfig": {
    object (ShieldedInstanceConfig)
  }
}
```

| Fields                   |                                                                                                                                                                                                                                                                                           |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineSpec`            | `object ( `[`MachineSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.MachineSpec)` )` The specification of a single machine for the execution job.                           |
| `persistentDiskSpec`     | `object ( `[`PersistentDiskSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.PersistentDiskSpec)` )` The specification of a persistent disk to attach for the execution job.  |
| `networkSpec`            | `object ( `[`NetworkSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NetworkSpec)` )` The network configuration to use for the execution job.                                |
| `shieldedInstanceConfig` | `object ( `[`ShieldedInstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.ShieldedInstanceConfig)` )` Optional. Shielded VM configuration (for example, Secure Boot) for the execution VM. |

### MachineSpec

**JSON representation**

```
{
  "machineType": string,
  "acceleratorType": enum (AcceleratorType),
  "acceleratorCount": integer,
  "gpuPartitionSize": string,
  "tpuTopology": string,
  "reservationAffinity": {
    object (ReservationAffinity)
  }
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineType`         | `string` Immutable. The type of the machine. See the [list of machine types supported for prediction](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#machine-types) See the [list of machine types supported for custom training](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . For `DeployedModel` this field is optional, and the default value is `n1-standard-2` . For `BatchPredictionJob` or as part of `WorkerPoolSpec` this field is required.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `acceleratorType`     | `enum ( `[`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.AcceleratorType)` )` Immutable. The type of accelerator(s) that may be attached to the machine as per `accelerator_count` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `acceleratorCount`    | `integer` The number of accelerators to attach to the machine. For [accelerator optimized machine types](https://cloud.google.com/compute/docs/accelerator-optimized-machines) , One may set the accelerator_count from 1 to N for machine with N GPUs. If accelerator_count is less than or equal to N / 2, Agent Platform co-schedules the replicas of the model into the same VM to save cost. For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set accelerator_count to 1 to 8. If accelerator_count is 1, 2, 3, or 4, Agent Platform co-schedules 8, 4, 2, or 2 replicas of the model into the same VM to save cost. When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM. Note that the feature is not compatible with \[multihost_gpu_node_count\]\[\]. When multihost_gpu_node_count is set, the co-scheduling will not be enabled. |
| `gpuPartitionSize`    | `string` Optional. Immutable. The Nvidia GPU partition size. When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu_partition_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances. The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes. If set, the accelerator_count should be set to 1.                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `tpuTopology`         | `string` Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu_topology: "2x2x1").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `reservationAffinity` | `object ( `[`ReservationAffinity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.ReservationAffinity)` )` Optional. Immutable. Configuration controlling how this resource pool consumes reservation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### ReservationAffinity

**JSON representation**

```
{
  "reservationAffinityType": enum (Type),
  "key": string,
  "values": [
    string
  ]
}
```

| Fields                    |                                                                                                                                                                                                                                       |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservationAffinityType` | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.Type)` )` Required. Specifies the reservation affinity type. |
| `key`                     | `string` Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.  |
| `values[]`                | `string` Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.                                                                            |

### PersistentDiskSpec

**JSON representation**

```
{
  "diskType": string,
  "diskSizeGb": string
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `diskType`   | `string` Type of the disk (default is "pd-standard"). Valid values: "pd-ssd" (Persistent Disk Solid State Drive) "pd-standard" (Persistent Disk Hard Disk Drive) "pd-balanced" (Balanced Persistent Disk) "pd-extreme" (Extreme Persistent Disk) "hyperdisk-balanced" (Hyperdisk Balanced) "hyperdisk-extreme" (Hyperdisk Extreme) "hyperdisk-balanced-high-availability" (Hyperdisk Balanced High Availability) "hyperdisk-ml" (Hyperdisk ML) "hyperdisk-throughput" (Hyperdisk Throughput) |
| `diskSizeGb` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Size in GB of the disk (default is 100GB).                                                                                                                                                                                                                                                                                                                                                            |

### NetworkSpec

**JSON representation**

```
{
  "enableInternetAccess": boolean,
  "network": string,
  "subnetwork": string
}
```

| Fields                 |                                                                                                                                                  |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableInternetAccess` | `boolean` Whether to enable public internet access. Default false.                                                                               |
| `network`              | `string` The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks)            |
| `subnetwork`           | `string` The name of the subnet that this instance is in. Format: `projects/{project_id_or_number}/regions/{region}/subnetworks/{subnetwork_id}` |

### ShieldedInstanceConfig

**JSON representation**

```
{
  "enableSecureBoot": boolean,
  "enableVtpm": boolean,
  "enableIntegrityMonitoring": boolean
}
```

| Fields                      |                                                                                           |
|-----------------------------|-------------------------------------------------------------------------------------------|
| `enableSecureBoot`          | `boolean` Optional. Whether the VM instance has Secure Boot enabled. Disabled by default. |
| `enableVtpm`                | `boolean` Optional. Whether the VM instance has vTPM enabled.                             |
| `enableIntegrityMonitoring` | `boolean` Optional. Whether the VM instance has integrity monitoring enabled.             |

### WorkbenchRuntime

**JSON representation**

```
{

  // Union field image_environment can be only one of the following:
  "vmImage": {
    object (VmImage)
  },
  "customContainerImage": {
    object (ContainerImage)
  }
  // End of list of possible types for union field image_environment.
}
```

| Fields                                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                                                         |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `image_environment` . The image environment to run the notebook execution in. Optional: if unset, the service defaults to a managed `workbench-instances-2603` VM image (Python 3.12). `image_environment` can be only one of the following: |                                                                                                                                                                                                                                                                                                         |
| `vmImage`                                                                                                                                                                                                                                                | `object ( `[`VmImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.VmImage)` )` A specific Compute Engine VM image to run the notebook on.                                                                       |
| `customContainerImage`                                                                                                                                                                                                                                   | `object ( `[`ContainerImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.ContainerImage)` )` A user-provided container image. The notebook executes inside this container on a managed container-host (COS) VM. |

### VmImage

**JSON representation**

```
{
  "project": string,

  // Union field image can be only one of the following:
  "name": string,
  "family": string
  // End of list of possible types for union field image.
}
```

| Fields                                                                                                      |                                                                                                                 |
|-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| `project`                                                                                                   | `string` Required. The name of the Google Cloud project that this VM image belongs to. Format: `{project_id}` . |
| Union field `image` . The reference to a Compute Engine VM image. `image` can be only one of the following: |                                                                                                                 |
| `name`                                                                                                      | `string` Use this VM image name to find the image.                                                              |
| `family`                                                                                                    | `string` Use this VM image family to find the image; the newest image in this family is used.                   |

### ContainerImage

**JSON representation**

```
{
  "repository": string,
  "tag": string
}
```

| Fields       |                                                                                                                  |
|--------------|------------------------------------------------------------------------------------------------------------------|
| `repository` | `string` Required. The path to the container image repository. For example: `gcr.io/{project_id}/{image_name}` . |
| `tag`        | `string` Optional. The tag of the container image. If unset, defaults to `latest` .                              |

### Duration

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years                                                                                    |
| `nanos`   | `integer` Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive. |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### RunResponse

**JSON representation**

```
{
  "scheduledRunTime": string,
  "runResponse": string
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `scheduledRunTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The scheduled run time based on the user-specified schedule. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `runResponse`      | `string` The response of the scheduled run.                                                                                                                                                                                                                                                                                                                                                                                        |

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### PipelineState

Describes the state of a pipeline.

| Enums                        |                                                                                                                                                                   |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `PIPELINE_STATE_UNSPECIFIED` | The pipeline state is unspecified.                                                                                                                                |
| `PIPELINE_STATE_QUEUED`      | The pipeline has been created or resumed, and processing has not yet begun.                                                                                       |
| `PIPELINE_STATE_PENDING`     | The service is preparing to run the pipeline.                                                                                                                     |
| `PIPELINE_STATE_RUNNING`     | The pipeline is in progress.                                                                                                                                      |
| `PIPELINE_STATE_SUCCEEDED`   | The pipeline completed successfully.                                                                                                                              |
| `PIPELINE_STATE_FAILED`      | The pipeline failed.                                                                                                                                              |
| `PIPELINE_STATE_CANCELLING`  | The pipeline is being cancelled. From this state, the pipeline may only go to either PIPELINE_STATE_SUCCEEDED, PIPELINE_STATE_FAILED or PIPELINE_STATE_CANCELLED. |
| `PIPELINE_STATE_CANCELLED`   | The pipeline has been cancelled.                                                                                                                                  |
| `PIPELINE_STATE_PAUSED`      | The pipeline has been stopped, and can be resumed.                                                                                                                |

### State

Specifies state of TaskExecution

| Enums               |                                                                                                                                                                                         |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified.                                                                                                                                                                            |
| `PENDING`           | Specifies pending state for the task.                                                                                                                                                   |
| `RUNNING`           | Specifies task is being executed.                                                                                                                                                       |
| `SUCCEEDED`         | Specifies task completed successfully.                                                                                                                                                  |
| `CANCEL_PENDING`    | Specifies Task cancel is in pending state.                                                                                                                                              |
| `CANCELLING`        | Specifies task is being cancelled.                                                                                                                                                      |
| `CANCELLED`         | Specifies task was cancelled.                                                                                                                                                           |
| `FAILED`            | Specifies task failed.                                                                                                                                                                  |
| `SKIPPED`           | Specifies task was skipped due to cache hit.                                                                                                                                            |
| `NOT_TRIGGERED`     | Specifies that the task was not triggered because the task's trigger policy is not satisfied. The trigger policy is specified in the `condition` field of `PipelineJob.pipeline_spec` . |

### State

Describes the state of the Execution.

| Enums               |                                            |
|---------------------|--------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified Execution state                |
| `NEW`               | The Execution is new                       |
| `RUNNING`           | The Execution is running                   |
| `COMPLETE`          | The Execution has finished running         |
| `FAILED`            | The Execution has failed                   |
| `CACHED`            | The Execution completed through Cache hit. |
| `CANCELLED`         | The Execution was cancelled.               |

### State

Describes the state of the Artifact.

| Enums               |                                                                                                                                                |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified state for the Artifact.                                                                                                            |
| `PENDING`           | A state used by systems like Agent Platform Pipelines to indicate that the underlying data item represented by this Artifact is being created. |
| `LIVE`              | A state indicating that the Artifact should exist, unless something external to the system deletes it.                                         |

### PipelineFailurePolicy

Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW. However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion.

| Enums                                 |                                                                                                                |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------|
| `PIPELINE_FAILURE_POLICY_UNSPECIFIED` | Default value, and follows fail slow behavior.                                                                 |
| `PIPELINE_FAILURE_POLICY_FAIL_SLOW`   | Indicates that the pipeline should continue to run until all possible tasks have been scheduled and completed. |
| `PIPELINE_FAILURE_POLICY_FAIL_FAST`   | Indicates that the pipeline should stop scheduling new tasks after a task has failed.                          |

### AcceleratorType

Represents a hardware accelerator type.

| Enums                          |                                                                                                                        |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------|
| `ACCELERATOR_TYPE_UNSPECIFIED` | Unspecified accelerator type, which means no accelerator.                                                              |
| `NVIDIA_TESLA_K80`             | Deprecated: Nvidia Tesla K80 GPU has reached end of support, see <https://cloud.google.com/compute/docs/eol/k80-eol> . |
| `NVIDIA_TESLA_P100`            | Nvidia Tesla P100 GPU.                                                                                                 |
| `NVIDIA_TESLA_V100`            | Nvidia Tesla V100 GPU.                                                                                                 |
| `NVIDIA_TESLA_P4`              | Nvidia Tesla P4 GPU.                                                                                                   |
| `NVIDIA_TESLA_T4`              | Nvidia Tesla T4 GPU.                                                                                                   |
| `NVIDIA_TESLA_A100`            | Nvidia Tesla A100 GPU.                                                                                                 |
| `NVIDIA_A100_80GB`             | Nvidia A100 80GB GPU.                                                                                                  |
| `NVIDIA_L4`                    | Nvidia L4 GPU.                                                                                                         |
| `NVIDIA_H100_80GB`             | Nvidia H100 80Gb GPU.                                                                                                  |
| `NVIDIA_H100_MEGA_80GB`        | Nvidia H100 Mega 80Gb GPU.                                                                                             |
| `NVIDIA_H200_141GB`            | Nvidia H200 141Gb GPU.                                                                                                 |
| `NVIDIA_B200`                  | Nvidia B200 GPU.                                                                                                       |
| `NVIDIA_GB200`                 | Nvidia GB200 GPU.                                                                                                      |
| `NVIDIA_RTX_PRO_6000`          | Nvidia RTX Pro 6000 GPU.                                                                                               |
| `TPU_V2`                       | TPU v2.                                                                                                                |
| `TPU_V3`                       | TPU v3.                                                                                                                |
| `TPU_V4_POD`                   | TPU v4.                                                                                                                |
| `TPU_V5_LITEPOD`               | TPU v5.                                                                                                                |

### Type

Identifies a type of reservation affinity.

| Enums                  |                                                                                                                         |
|------------------------|-------------------------------------------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED`     | Default value. This should not be used.                                                                                 |
| `NO_RESERVATION`       | Do not consume from any reserved capacity, only use on-demand.                                                          |
| `ANY_RESERVATION`      | Consume any reservation available, falling back to on-demand.                                                           |
| `SPECIFIC_RESERVATION` | Consume from a specific reservation. When chosen, the reservation must be identified via the `key` and `values` fields. |

### JobState

Describes the state of a job.

| Enums                           |                                                                                                                                                 |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `JOB_STATE_UNSPECIFIED`         | The job state is unspecified.                                                                                                                   |
| `JOB_STATE_QUEUED`              | The job has been just created or resumed and processing has not yet begun.                                                                      |
| `JOB_STATE_PENDING`             | The service is preparing to run the job.                                                                                                        |
| `JOB_STATE_RUNNING`             | The job is in progress.                                                                                                                         |
| `JOB_STATE_SUCCEEDED`           | The job completed successfully.                                                                                                                 |
| `JOB_STATE_FAILED`              | The job failed.                                                                                                                                 |
| `JOB_STATE_CANCELLING`          | The job is being cancelled. From this state the job may only go to either `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` . |
| `JOB_STATE_CANCELLED`           | The job has been cancelled.                                                                                                                     |
| `JOB_STATE_PAUSED`              | The job has been stopped, and can be resumed.                                                                                                   |
| `JOB_STATE_EXPIRED`             | The job has expired.                                                                                                                            |
| `JOB_STATE_UPDATING`            | The job is being updated. Only jobs in the `RUNNING` state can be updated. After updating, the job goes back to the `RUNNING` state.            |
| `JOB_STATE_PARTIALLY_SUCCEEDED` | The job is partially succeeded, some results may be missing due to errors.                                                                      |

### State

Possible state of the schedule.

| Enums               |                                                                                                                                                                       |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified.                                                                                                                                                          |
| `ACTIVE`            | The Schedule is active. Runs are being scheduled on the user-specified timespec.                                                                                      |
| `PAUSED`            | The schedule is paused. No new runs will be created until the schedule is resumed. Already started runs will be allowed to complete.                                  |
| `COMPLETED`         | The Schedule is completed. No new runs will be scheduled. Already started runs will be allowed to complete. Schedules in completed state cannot be paused or resumed. |

## Output Schema

An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type.

### Schedule

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "startTime": string,
  "endTime": string,
  "maxRunCount": string,
  "startedRunCount": string,
  "state": enum (State),
  "createTime": string,
  "updateTime": string,
  "nextRunTime": string,
  "lastPauseTime": string,
  "lastResumeTime": string,
  "maxConcurrentRunCount": string,
  "maxConcurrentActiveRunCount": string,
  "allowQueueing": boolean,
  "catchUp": boolean,
  "lastScheduledRunResponse": {
    object (RunResponse)
  },

  // Union field time_specification can be only one of the following:
  "cron": string
  // End of list of possible types for union field time_specification.

  // Union field request can be only one of the following:
  "createPipelineJobRequest": {
    object (CreatePipelineJobRequest)
  },
  "createNotebookExecutionJobRequest": {
    object (CreateNotebookExecutionJobRequest)
  }
  // End of list of possible types for union field request.
}
```

| Fields                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                                           | `string` Immutable. The resource name of the Schedule.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `displayName`                                                                                                                                                                                    | `string` Required. User provided name of the Schedule. The name can be up to 128 characters long and can consist of any UTF-8 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `startTime`                                                                                                                                                                                      | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Optional. Timestamp after which the first run can be scheduled. Default to Schedule create time if not specified. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                      |
| `endTime`                                                                                                                                                                                        | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Optional. Timestamp after which no new runs can be scheduled. If specified, The schedule will be completed when either end_time is reached or when scheduled_run_count \>= max_run_count. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `maxRunCount`                                                                                                                                                                                    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Maximum run count of the schedule. If specified, The schedule will be completed when either started_run_count \>= max_run_count or when end_time is reached. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified.                                                                                                                                                                                                                                                                                                   |
| `startedRunCount`                                                                                                                                                                                | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The number of runs started by this schedule.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `state`                                                                                                                                                                                          | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.State_3)` )` Output only. The state of this Schedule.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `createTime`                                                                                                                                                                                     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Schedule was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                 |
| `updateTime`                                                                                                                                                                                     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Schedule was updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                 |
| `nextRunTime`                                                                                                                                                                                    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Schedule should schedule the next run. Having a next_run_time in the past means the runs are being started behind schedule. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                           |
| `lastPauseTime`                                                                                                                                                                                  | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Schedule was last paused. Unset if never paused. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                      |
| `lastResumeTime`                                                                                                                                                                                 | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Schedule was last resumed. Unset if never resumed from pause. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                         |
| `maxConcurrentRunCount`                                                                                                                                                                          | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Required. Maximum number of runs that can be started concurrently for this Schedule. This is the limit for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable).                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `maxConcurrentActiveRunCount`                                                                                                                                                                    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Specifies the maximum number of active runs that can be executed concurrently for this Schedule. This limits the number of runs that can be in a non-terminal state at the same time. Currently, this field is only supported for requests of type CreatePipelineJobRequest.                                                                                                                                                                                                                                                                                                                                                                |
| `allowQueueing`                                                                                                                                                                                  | `boolean` Optional. Whether new scheduled runs can be queued when max_concurrent_runs limit is reached. If set to true, new runs will be queued instead of skipped. Default to false.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `catchUp`                                                                                                                                                                                        | `boolean` Output only. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. Default to false.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `lastScheduledRunResponse`                                                                                                                                                                       | `object ( `[`RunResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.RunResponse)` )` Output only. Response of the last scheduled run. This is the response for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable). Unset if no run has been scheduled yet.                                                                                                                                                                                                                                                                                                                  |
| Union field `time_specification` . Required. The time specification to launch scheduled runs. `time_specification` can be only one of the following:                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `cron`                                                                                                                                                                                           | `string` Cron schedule ( <https://en.wikipedia.org/wiki/Cron> ) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON_TZ=\${IANA_TIME_ZONE}" or "TZ=\${IANA_TIME_ZONE}". The \${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 \* \* \* \*", or "TZ=America/New_York 1 \* \* \* \*".                                                                                                                                                                                                                                                                                                                              |
| Union field `request` . Required. The API request template to launch the scheduled runs. User-specified ID is not supported in the request template. `request` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `createPipelineJobRequest`                                                                                                                                                                       | `object ( `[`CreatePipelineJobRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.CreatePipelineJobRequest)` )` Request for `PipelineService.CreatePipelineJob` . CreatePipelineJobRequest.parent field is required (format: projects/{project}/locations/{location}).                                                                                                                                                                                                                                                                                                                                                                         |
| `createNotebookExecutionJobRequest`                                                                                                                                                              | `object ( `[`CreateNotebookExecutionJobRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.CreateNotebookExecutionJobRequest)` )` Request for `NotebookService.CreateNotebookExecutionJob` .                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### CreatePipelineJobRequest

**JSON representation**

```
{
  "parent": string,
  "pipelineJob": {
    object (PipelineJob)
  },
  "pipelineJobId": string
}
```

| Fields          |                                                                                                                                                                                                                                                              |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`        | `string` Required. The resource name of the Location to create the PipelineJob in. Format: `projects/{project}/locations/{location}`                                                                                                                         |
| `pipelineJob`   | `object ( `[`PipelineJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineJob)` )` Required. The PipelineJob to create.                                     |
| `pipelineJobId` | `string` The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are `/[a-z][0-9]-/` . |

### PipelineJob

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "createTime": string,
  "startTime": string,
  "endTime": string,
  "updateTime": string,
  "pipelineSpec": {
    object
  },
  "state": enum (PipelineState),
  "jobDetail": {
    object (PipelineJobDetail)
  },
  "error": {
    object (Status)
  },
  "labels": {
    string: string,
    ...
  },
  "runtimeConfig": {
    object (RuntimeConfig)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "serviceAccount": string,
  "network": string,
  "reservedIpRanges": [
    string
  ],
  "pscInterfaceConfig": {
    object (PscInterfaceConfig)
  },
  "templateUri": string,
  "templateMetadata": {
    object (PipelineTemplateMetadata)
  },
  "scheduleName": string,
  "preflightValidations": boolean
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                 | `string` Output only. The resource name of the PipelineJob.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `displayName`          | `string` The display name of the Pipeline. The name can be up to 128 characters long and can consist of any UTF-8 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `createTime`           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Pipeline creation time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                                                                                      |
| `startTime`            | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Pipeline start time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                                                                                         |
| `endTime`              | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Pipeline end time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                                                                                           |
| `updateTime`           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this PipelineJob was most recently updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                                                                                                   |
| `pipelineSpec`         | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` A compiled definition of a pipeline, represented as a `JSON` object. Defines the structure of the pipeline, including its components, tasks, and parameters. This specification is generated by compiling a pipeline function defined in `Python` using the `Kubeflow Pipelines SDK` .                                                                                                                                                                                                                                                                                                                                                                                                         |
| `state`                | `enum ( `[`PipelineState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineState)` )` Output only. The detailed state of the job.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `jobDetail`            | `object ( `[`PipelineJobDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineJobDetail)` )` Output only. The details of pipeline run. Not available in the list view.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `error`                | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. The error that occurred during pipeline execution. Only populated when the pipeline's state is FAILED or CANCELLED.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `labels`               | `map (key: string, value: string)` The labels with user-defined metadata to organize PipelineJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See <https://goo.gl/xmQnxf> for more information and examples of labels. Note there is some reserved label key for Agent Platform Pipelines. - `vertex-ai-pipelines-run-billing-id` , user set value will get overrided. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                          |
| `runtimeConfig`        | `object ( `[`RuntimeConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.RuntimeConfig)` )` Runtime config of the pipeline.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `encryptionSpec`       | `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec)` )` Customer-managed encryption key spec for a pipelineJob. If set, this PipelineJob and all of its sub-resources will be secured by this key.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `serviceAccount`       | `string` The service account that the pipeline workload runs as. If not specified, the Compute Engine default service account in the project will be used. See <https://cloud.google.com/compute/docs/access/service-accounts#default_service_account> Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service account.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `network`              | `string` The full name of the Compute Engine [network](https://docs.cloud.google.com/compute/docs/networks-and-firewalls#networks) to which the Pipeline Job's workload should be peered. For example, `projects/12345/global/networks/myVPC` . [Format](https://docs.cloud.google.com/compute/docs/reference/rest/v1/networks/insert) is of the form `projects/{project}/global/networks/{network}` . Where {project} is a project number, as in `12345` , and {network} is a network name. Private services access must already be configured for the network. Pipeline job will apply the network configuration to the Google Cloud resources being launched, if applied, such as Agent Platform Training or Dataflow job. If left unspecified, the workload is not peered with any network. |
| `reservedIpRanges[]`   | `string` A list of names for the reserved ip ranges under the VPC network that can be used for this Pipeline Job's workload. If set, we will deploy the Pipeline Job's workload within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network. Example: \['vertex-ai-ip-range'\].                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `pscInterfaceConfig`   | `object ( `[`PscInterfaceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PscInterfaceConfig)` )` Optional. Configuration for PSC-I for PipelineJob.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `templateUri`          | `string` A template uri from where the `PipelineJob.pipeline_spec` , if empty, will be downloaded. Currently, only uri from Vertex Template Registry & Gallery is supported. Reference to <https://cloud.google.com/vertex-ai/docs/pipelines/create-pipeline-template> .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `templateMetadata`     | `object ( `[`PipelineTemplateMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineTemplateMetadata)` )` Output only. Pipeline template metadata. Will fill up fields if `PipelineJob.template_uri` is from supported template registry.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `scheduleName`         | `string` Output only. The schedule resource name. Only returned if the Pipeline is created by Schedule API.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `preflightValidations` | `boolean` Optional. Whether to do component level validations before job creation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### Struct

**JSON representation**

```
{
  "fields": {
    string: value,
    ...
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                          |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map (key: string, value: value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format))` Unordered map of dynamically typed values. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### FieldsEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### Value

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean,
  "structValue": {
    object
  },
  "listValue": array
  // End of list of possible types for union field kind.
}
```

| Fields                                                                           |                                                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . The kind of value. `kind` can be only one of the following: |                                                                                                                                                                                                                                                |
| `nullValue`                                                                      | `null` Represents a JSON `null` .                                                                                                                                                                                                              |
| `numberValue`                                                                    | `number` Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type. |
| `stringValue`                                                                    | `string` Represents a JSON string.                                                                                                                                                                                                             |
| `boolValue`                                                                      | `boolean` Represents a JSON boolean ( `true` or `false` literal in JSON).                                                                                                                                                                      |
| `structValue`                                                                    | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Represents a JSON object.                                                                                                                     |
| `listValue`                                                                      | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` Represents a JSON array.                                                                                                                |

### ListValue

**JSON representation**

```
{
  "values": [
    value
  ]
}
```

| Fields     |                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Repeated field of dynamically typed values. |

### PipelineJobDetail

**JSON representation**

```
{
  "pipelineContext": {
    object (Context)
  },
  "pipelineRunContext": {
    object (Context)
  },
  "taskDetails": [
    {
      object (PipelineTaskDetail)
    }
  ]
}
```

| Fields               |                                                                                                                                                                                                                                                                     |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pipelineContext`    | `object ( `[`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Context)` )` Output only. The context of the pipeline.                                               |
| `pipelineRunContext` | `object ( `[`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Context)` )` Output only. The context of the current pipeline run.                                   |
| `taskDetails[]`      | `object ( `[`PipelineTaskDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineTaskDetail)` )` Output only. The runtime details of the tasks under the pipeline. |

### Context

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "parentContexts": [
    string
  ],
  "schemaTitle": string,
  "schemaVersion": string,
  "metadata": {
    object
  },
  "description": string
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`             | `string` Immutable. The resource name of the Context.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `displayName`      | `string` User provided display name of the Context. May be up to 128 Unicode characters.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `etag`             | `string` An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.                                                                                                                                                                                                                                                                                                                                                                                                       |
| `labels`           | `map (key: string, value: string)` The labels with user-defined metadata to organize your Contexts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Context (System labels are excluded). An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `createTime`       | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Context was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                  |
| `updateTime`       | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Context was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                             |
| `parentContexts[]` | `string` Output only. A list of resource names of Contexts that are parents of this Context. A Context may have at most 10 parent_contexts.                                                                                                                                                                                                                                                                                                                                                                                  |
| `schemaTitle`      | `string` The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                        |
| `schemaVersion`    | `string` The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                        |
| `metadata`         | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Properties of the Context. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.                                                                                                                                                                                                                                                                            |
| `description`      | `string` Description of the Context                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### PipelineTaskDetail

**JSON representation**

```
{
  "taskId": string,
  "parentTaskId": string,
  "taskName": string,
  "createTime": string,
  "startTime": string,
  "endTime": string,
  "executorDetail": {
    object (PipelineTaskExecutorDetail)
  },
  "state": enum (State),
  "execution": {
    object (Execution)
  },
  "error": {
    object (Status)
  },
  "pipelineTaskStatus": [
    {
      object (PipelineTaskStatus)
    }
  ],
  "inputs": {
    string: {
      object (ArtifactList)
    },
    ...
  },
  "outputs": {
    string: {
      object (ArtifactList)
    },
    ...
  },
  "taskUniqueName": string
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `taskId`               | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The system generated ID of the task.                                                                                                                                                                                                                                                                                                                                             |
| `parentTaskId`         | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The id of the parent task if the task is within a component scope. Empty if the task is at the root level.                                                                                                                                                                                                                                                                       |
| `taskName`             | `string` Output only. The user specified name of the task that is defined in `pipeline_spec` .                                                                                                                                                                                                                                                                                                                                                                                       |
| `createTime`           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Task create time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                 |
| `startTime`            | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Task start time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                  |
| `endTime`              | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Task end time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                    |
| `executorDetail`       | `object ( `[`PipelineTaskExecutorDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineTaskExecutorDetail)` )` Output only. The detailed execution info.                                                                                                                                                                                                                          |
| `state`                | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.State)` )` Output only. State of the task.                                                                                                                                                                                                                                                                                |
| `execution`            | `object ( `[`Execution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Execution)` )` Output only. The execution metadata of the task.                                                                                                                                                                                                                                                     |
| `error`                | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. The error that occurred during task execution. Only populated when the task's state is FAILED or CANCELLED.                                                                                                                                                                                                     |
| `pipelineTaskStatus[]` | `object ( `[`PipelineTaskStatus`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineTaskStatus)` )` Output only. A list of task status. This field keeps a record of task status evolving over time.                                                                                                                                                                                   |
| `inputs`               | `map (key: string, value: object ( `[`ArtifactList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.ArtifactList)` ))` Output only. The runtime input artifacts of the task. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                          |
| `outputs`              | `map (key: string, value: object ( `[`ArtifactList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.ArtifactList)` ))` Output only. The runtime output artifacts of the task. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                         |
| `taskUniqueName`       | `string` Output only. The unique name of a task. This field is used by rerun pipeline job. Console UI and Agent Platform SDK will support triggering pipeline job reruns. The name is constructed by concatenating all the parent tasks name with the task name. For example, if a task named "child_task" has a parent task named "parent_task_1" and parent task 1 has a parent task named "parent_task_2", the task unique name will be "parent_task_2.parent_task_1.child_task". |

### PipelineTaskExecutorDetail

**JSON representation**

```
{

  // Union field details can be only one of the following:
  "containerDetail": {
    object (ContainerDetail)
  },
  "customJobDetail": {
    object (CustomJobDetail)
  }
  // End of list of possible types for union field details.
}
```

| Fields                                                              |                                                                                                                                                                                                                                                       |
|---------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `details` . `details` can be only one of the following: |                                                                                                                                                                                                                                                       |
| `containerDetail`                                                   | `object ( `[`ContainerDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.ContainerDetail)` )` Output only. The detailed info for a container executor.  |
| `customJobDetail`                                                   | `object ( `[`CustomJobDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.CustomJobDetail)` )` Output only. The detailed info for a custom job executor. |

### ContainerDetail

**JSON representation**

```
{
  "mainJob": string,
  "preCachingCheckJob": string,
  "failedMainJobs": [
    string
  ],
  "failedPreCachingCheckJobs": [
    string
  ]
}
```

| Fields                        |                                                                                                                                                                                                                                                                                                               |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mainJob`                     | `string` Output only. The name of the `CustomJob` for the main container execution.                                                                                                                                                                                                                           |
| `preCachingCheckJob`          | `string` Output only. The name of the `CustomJob` for the pre-caching-check container execution. This job will be available if the `PipelineJob.pipeline_spec` specifies the `pre_caching_check` hook in the lifecycle events.                                                                                |
| `failedMainJobs[]`            | `string` Output only. The names of the previously failed `CustomJob` for the main container executions. The list includes the all attempts in chronological order.                                                                                                                                            |
| `failedPreCachingCheckJobs[]` | `string` Output only. The names of the previously failed `CustomJob` for the pre-caching-check container executions. This job will be available if the `PipelineJob.pipeline_spec` specifies the `pre_caching_check` hook in the lifecycle events. The list includes the all attempts in chronological order. |

### CustomJobDetail

**JSON representation**

```
{
  "job": string,
  "failedJobs": [
    string
  ]
}
```

| Fields         |                                                                                                                                   |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------|
| `job`          | `string` Output only. The name of the `CustomJob` .                                                                               |
| `failedJobs[]` | `string` Output only. The names of the previously failed `CustomJob` . The list includes the all attempts in chronological order. |

### Execution

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "state": enum (State),
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "schemaTitle": string,
  "schemaVersion": string,
  "metadata": {
    object
  },
  "description": string
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`          | `string` Output only. The resource name of the Execution.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `displayName`   | `string` User provided display name of the Execution. May be up to 128 Unicode characters.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `state`         | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.State_1)` )` The state of this Execution. This is a property of the Execution, and does not imply or capture any ongoing process. This property is managed by clients (such as Agent Platform Pipelines) and the system does not prescribe or check the validity of state transitions.                                                                                |
| `etag`          | `string` An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.                                                                                                                                                                                                                                                                                                                                                                                                           |
| `labels`        | `map (key: string, value: string)` The labels with user-defined metadata to organize your Executions. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Execution (System labels are excluded). An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `createTime`    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Execution was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                    |
| `updateTime`    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Execution was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                               |
| `schemaTitle`   | `string` The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                            |
| `schemaVersion` | `string` The version of the schema in `schema_title` to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                         |
| `metadata`      | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Properties of the Execution. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.                                                                                                                                                                                                                                                                              |
| `description`   | `string` Description of the Execution                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### Status

**JSON representation**

```
{
  "code": integer,
  "message": string,
  "details": [
    {
      "@type": string,
      field1: ...,
      ...
    }
  ]
}
```

| Fields      |                                                                                                                                                                                                                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`      | `integer` The status code, which should be an enum value of `google.rpc.Code` .                                                                                                                                                                                                                              |
| `message`   | `string` A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.                                                                                                      |
| `details[]` | `object` A list of messages that carry the error details. There is a common set of message types for APIs to use. An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` . |

### Any

**JSON representation**

```
{
  "typeUrl": string,
  "value": string
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `typeUrl` | `string` Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name. Example: type.googleapis.com/google.protobuf.StringValue This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them. The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests. All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected. In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs. |
| `value`   | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Holds a Protobuf serialization of the type described by type_url. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### PipelineTaskStatus

**JSON representation**

```
{
  "updateTime": string,
  "state": enum (State),
  "error": {
    object (Status)
  }
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `updateTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Update time of this status. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                         |
| `state`      | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.State)` )` Output only. The state of the task.                                                                                                                                                                                                                                                                              |
| `error`      | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. The error that occurred during the state. May be set when the state is any of the non-final state (PENDING/RUNNING/CANCELLING) or FAILED state. If the state is FAILED, the error here is final and not going to be retried. If the state is a non-final state, the error indicates a system-error being retried. |

### InputsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (ArtifactList)
  }
}
```

| Fields  |                                                                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                              |
| `value` | `object ( `[`ArtifactList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.ArtifactList)` )` |

### ArtifactList

**JSON representation**

```
{
  "artifacts": [
    {
      object (Artifact)
    }
  ]
}
```

| Fields        |                                                                                                                                                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `artifacts[]` | `object ( `[`Artifact`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Artifact)` )` Output only. A list of artifact metadata. |

### Artifact

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "uri": string,
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "state": enum (State),
  "schemaTitle": string,
  "schemaVersion": string,
  "metadata": {
    object
  },
  "description": string
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`          | `string` Output only. The resource name of the Artifact.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `displayName`   | `string` User provided display name of the Artifact. May be up to 128 Unicode characters.                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `uri`           | `string` The uniform resource identifier of the artifact file. May be empty if there is no actual artifact file.                                                                                                                                                                                                                                                                                                                                                                                                               |
| `etag`          | `string` An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.                                                                                                                                                                                                                                                                                                                                                                                                         |
| `labels`        | `map (key: string, value: string)` The labels with user-defined metadata to organize your Artifacts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Artifact (System labels are excluded). An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `createTime`    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Artifact was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                   |
| `updateTime`    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this Artifact was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                              |
| `state`         | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.State_2)` )` The state of this Artifact. This is a property of the Artifact, and does not imply or capture any ongoing process. This property is managed by clients (such as Agent Platform Pipelines), and the system does not prescribe or check the validity of state transitions.                                                                               |
| `schemaTitle`   | `string` The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                          |
| `schemaVersion` | `string` The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.                                                                                                                                                                                                                                                                          |
| `metadata`      | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Properties of the Artifact. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.                                                                                                                                                                                                                                                                             |
| `description`   | `string` Description of the Artifact                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### OutputsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (ArtifactList)
  }
}
```

| Fields  |                                                                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                              |
| `value` | `object ( `[`ArtifactList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.ArtifactList)` )` |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### RuntimeConfig

**JSON representation**

```
{
  "parameters": {
    string: {
      object (Value)
    },
    ...
  },
  "gcsOutputDirectory": string,
  "parameterValues": {
    string: value,
    ...
  },
  "failurePolicy": enum (PipelineFailurePolicy),
  "inputArtifacts": {
    string: {
      object (InputArtifact)
    },
    ...
  }
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parameters </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>map (key: string, value: object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Value_1"><code>Value</code></a><code> ))</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated. Use <code>RuntimeConfig.parameter_values</code> instead. The runtime parameters of the PipelineJob. The parameters will be passed into <code>PipelineJob.pipeline_spec</code> to replace the placeholders at runtime. This field is used by pipelines built using <code>PipelineJob.pipeline_spec.schema_version</code> 2.0.0 or lower, such as pipelines built using Kubeflow Pipelines SDK 1.8 or lower.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>gcsOutputDirectory</code></td>
<td><p><code>string</code></p>
<p>Required. A path in a Cloud Storage bucket, which will be treated as the root output directory of the pipeline. It is used by the system to generate the paths of output artifacts. The artifact paths are generated with a sub-path pattern <code>{job_id}/{task_id}/{output_key}</code> under the specified output directory. The service account specified in this pipeline must have the <code>storage.objects.get</code> and <code>storage.objects.create</code> permissions for this bucket.</p></td>
</tr>
<tr class="odd">
<td><code>parameterValues</code></td>
<td><p><code>map (key: string, value: value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format))</code></p>
<p>The runtime parameters of the PipelineJob. The parameters will be passed into <code>PipelineJob.pipeline_spec</code> to replace the placeholders at runtime. This field is used by pipelines built using <code>PipelineJob.pipeline_spec.schema_version</code> 2.1.0, such as pipelines built using Kubeflow Pipelines SDK 1.9 or higher and the v2 DSL.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>failurePolicy</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.PipelineFailurePolicy"><code>PipelineFailurePolicy</code></a><code> )</code></p>
<p>Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW. However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion.</p></td>
</tr>
<tr class="odd">
<td><code>inputArtifacts</code></td>
<td><p><code>map (key: string, value: object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.InputArtifact"><code>InputArtifact</code></a><code> ))</code></p>
<p>The runtime artifacts of the PipelineJob. The key will be the input artifact name and the value would be one of the InputArtifact.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
</tbody>
</table>

### ParametersEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (Value)
  }
}
```

| Fields  |                                                                                                                                                                           |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                  |
| `value` | `object ( `[`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.Value_1)` )` |

### Value

**JSON representation**

```
{

  // Union field value can be only one of the following:
  "intValue": string,
  "doubleValue": number,
  "stringValue": string
  // End of list of possible types for union field value.
}
```

| Fields                                                          |                                                                                                          |
|-----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Union field `value` . `value` can be only one of the following: |                                                                                                          |
| `intValue`                                                      | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` An integer value. |
| `doubleValue`                                                   | `number` A double value.                                                                                 |
| `stringValue`                                                   | `string` A string value.                                                                                 |

### ParameterValuesEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### InputArtifactsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (InputArtifact)
  }
}
```

| Fields  |                                                                                                                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                                |
| `value` | `object ( `[`InputArtifact`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.InputArtifact)` )` |

### InputArtifact

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "artifactId": string
  // End of list of possible types for union field kind.
}
```

| Fields                                                        |                                                                                                                                                                                                                                                                                                 |
|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . `kind` can be only one of the following: |                                                                                                                                                                                                                                                                                                 |
| `artifactId`                                                  | `string` Artifact resource id from MLMD. Which is the last portion of an artifact resource name: `projects/{project}/locations/{location}/metadataStores/default/artifacts/{artifact_id}` . The artifact must stay within the same project, location and default metadatastore as the pipeline. |

### EncryptionSpec

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Required. Resource name of the Cloud KMS key used to protect the resource. The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

### PscInterfaceConfig

**JSON representation**

```
{
  "networkAttachment": string,
  "dnsPeeringConfigs": [
    {
      object (DnsPeeringConfig)
    }
  ]
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `networkAttachment`   | `string` Optional. The name of the Compute Engine [network attachment](https://cloud.google.com/vpc/docs/about-network-attachments) to attach to the resource within the region and user project. To specify this field, you must have already [created a network attachment](https://cloud.google.com/vpc/docs/create-manage-network-attachments#create-network-attachments) . This field is only used for resources using PSC-I.                                                                               |
| `dnsPeeringConfigs[]` | `object ( `[`DnsPeeringConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_notebook_execution_schedule#Input.Schema.DnsPeeringConfig)` )` Optional. DNS peering configurations. When specified, Agent Platform will attempt to configure DNS peering zones in the tenant project VPC to resolve the specified domains using the target network's Cloud DNS. The user must grant the dns.peer role to the Agent Platform Service Agent on the target project. |

### DnsPeeringConfig

**JSON representation**

```
{
  "domain": string,
  "targetProject": string,
  "targetNetwork": string
}
```

| Fields          |                                                                                                                                                                               |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `domain`        | `string` Required. The DNS name suffix of the zone being peered to, e.g., "my-internal-domain.corp.". Must end with a dot.                                                    |
| `targetProject` | `string` Required. The project ID hosting the Cloud DNS managed zone that contains the 'domain'. The Agent Platform Service Agent requires the dns.peer role on this project. |
| `targetNetwork` | `string` Required. The VPC network name in the target_project where the DNS zone specified by 'domain' is visible.                                                            |

### PipelineTemplateMetadata

**JSON representation**

```
{
  "version": string
}
```

| Fields    |                                                                                                                                                                                               |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `version` | `string` The version_name in artifact registry. Will always be presented in output if the `PipelineJob.template_uri` is from supported template registry. Format is "sha256:abcdef123456...". |

### CreateNotebookExecutionJobRequest

**JSON representation**

```
{
  "parent": string,
  "notebookExecutionJob": {
    object (NotebookExecutionJob)
  },
  "notebookExecutionJobId": string
}
```

| Fields                   |                                                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                 | `string` Required. The resource name of the Location to create the NotebookExecutionJob. Format: `projects/{project}/locations/{location}`                                                                                                     |
| `notebookExecutionJob`   | `object ( `[`NotebookExecutionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.NotebookExecutionJob)` )` Required. The NotebookExecutionJob to create. |
| `notebookExecutionJobId` | `string` Optional. User specified ID for the NotebookExecutionJob.                                                                                                                                                                             |

### NotebookExecutionJob

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "executionTimeout": string,
  "scheduleResourceName": string,
  "jobState": enum (JobState),
  "status": {
    object (Status)
  },
  "createTime": string,
  "updateTime": string,
  "labels": {
    string: string,
    ...
  },
  "kernelName": string,
  "encryptionSpec": {
    object (EncryptionSpec)
  },

  // Union field notebook_source can be only one of the following:
  "dataformRepositorySource": {
    object (DataformRepositorySource)
  },
  "gcsNotebookSource": {
    object (GcsNotebookSource)
  },
  "directNotebookSource": {
    object (DirectNotebookSource)
  }
  // End of list of possible types for union field notebook_source.

  // Union field environment_spec can be only one of the following:
  "notebookRuntimeTemplateResourceName": string,
  "customEnvironmentSpec": {
    object (CustomEnvironmentSpec)
  }
  // End of list of possible types for union field environment_spec.

  // Union field execution_sink can be only one of the following:
  "gcsOutputUri": string
  // End of list of possible types for union field execution_sink.

  // Union field execution_identity can be only one of the following:
  "executionUser": string,
  "serviceAccount": string
  // End of list of possible types for union field execution_identity.

  // Union field runtime_environment can be only one of the following:
  "workbenchRuntime": {
    object (WorkbenchRuntime)
  }
  // End of list of possible types for union field runtime_environment.
}
```

| Fields                                                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                                                | `string` Output only. The resource name of this NotebookExecutionJob. Format: `projects/{project_id}/locations/{location}/notebookExecutionJobs/{job_id}`                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `displayName`                                                                                                                                                                                         | `string` The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `executionTimeout`                                                                                                                                                                                    | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Max running time of the execution job in seconds (default 86400s / 24 hrs). A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .                                                                                                                                                                                                                                                                                                                            |
| `scheduleResourceName`                                                                                                                                                                                | `string` The Schedule resource name if this job is triggered by one. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `jobState`                                                                                                                                                                                            | `enum ( `[`JobState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.JobState)` )` Output only. The state of the NotebookExecutionJob.                                                                                                                                                                                                                                                                                                                                                                                                |
| `status`                                                                                                                                                                                              | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated.                                                                                                                                                                                                                                                                                                 |
| `createTime`                                                                                                                                                                                          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this NotebookExecutionJob was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                      |
| `updateTime`                                                                                                                                                                                          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this NotebookExecutionJob was most recently updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                        |
| `labels`                                                                                                                                                                                              | `map (key: string, value: string)` The labels with user-defined metadata to organize NotebookExecutionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `kernelName`                                                                                                                                                                                          | `string` The name of the kernel to use during notebook execution. If unset, the default kernel is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `encryptionSpec`                                                                                                                                                                                      | `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec)` )` Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the [`NotebookRuntimeTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookRuntimeTemplate) has an encryption spec.                                                                                              |
| Union field `notebook_source` . The input notebook. `notebook_source` can be only one of the following:                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `dataformRepositorySource`                                                                                                                                                                            | `object ( `[`DataformRepositorySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.DataformRepositorySource)` )` The Dataform Repository pointing to a single file notebook repository.                                                                                                                                                                                                                                                                                                                               |
| `gcsNotebookSource`                                                                                                                                                                                   | `object ( `[`GcsNotebookSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.GcsNotebookSource)` )` The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`                                                                                                                                                                                                                                                                                                                        |
| `directNotebookSource`                                                                                                                                                                                | `object ( `[`DirectNotebookSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.DirectNotebookSource)` )` The contents of an input notebook file.                                                                                                                                                                                                                                                                                                                                                                      |
| Union field `environment_spec` . The compute config to use for an execution job. `environment_spec` can be only one of the following:                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `notebookRuntimeTemplateResourceName`                                                                                                                                                                 | `string` The NotebookRuntimeTemplate to source compute configuration from.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `customEnvironmentSpec`                                                                                                                                                                               | `object ( `[`CustomEnvironmentSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.CustomEnvironmentSpec)` )` The custom compute configuration for an execution job.                                                                                                                                                                                                                                                                                                                                                     |
| Union field `execution_sink` . The location to store the notebook execution result. `execution_sink` can be only one of the following:                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `gcsOutputUri`                                                                                                                                                                                        | `string` The Cloud Storage location to upload the result to. Format: `gs://bucket-name`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `execution_identity` . The identity to run the execution as. `execution_identity` can be only one of the following:                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `executionUser`                                                                                                                                                                                       | `string` The user email to run the execution as. Only supported by Colab runtimes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `serviceAccount`                                                                                                                                                                                      | `string` The service account to run the execution as.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Union field `runtime_environment` . Runtime environment for the notebook execution job. If unspecified, the default runtime of Colab is used. `runtime_environment` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `workbenchRuntime`                                                                                                                                                                                    | `object ( `[`WorkbenchRuntime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.WorkbenchRuntime)` )` The Workbench runtime configuration to use for the notebook execution.                                                                                                                                                                                                                                                                                                                                               |

### DataformRepositorySource

**JSON representation**

```
{
  "dataformRepositoryResourceName": string,
  "commitSha": string
}
```

| Fields                           |                                                                                                                                          |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| `dataformRepositoryResourceName` | `string` The resource name of the Dataform Repository. Format: `projects/{project_id}/locations/{location}/repositories/{repository_id}` |
| `commitSha`                      | `string` The commit SHA to read repository with. If unset, the file will be read at HEAD.                                                |

### GcsNotebookSource

**JSON representation**

```
{
  "uri": string,
  "generation": string
}
```

| Fields       |                                                                                                                                                                                         |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uri`        | `string` The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`                                                                                    |
| `generation` | `string` The version of the Cloud Storage object to read. If unset, the current version of the object is read. See <https://cloud.google.com/storage/docs/metadata#generation-number> . |

### DirectNotebookSource

**JSON representation**

```
{
  "content": string
}
```

| Fields    |                                                                                                                                                                         |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `content` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The base64-encoded contents of the input notebook file. A base64-encoded string. |

### CustomEnvironmentSpec

**JSON representation**

```
{
  "machineSpec": {
    object (MachineSpec)
  },
  "persistentDiskSpec": {
    object (PersistentDiskSpec)
  },
  "networkSpec": {
    object (NetworkSpec)
  },
  "shieldedInstanceConfig": {
    object (ShieldedInstanceConfig)
  }
}
```

| Fields                   |                                                                                                                                                                                                                                                                                           |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineSpec`            | `object ( `[`MachineSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.MachineSpec)` )` The specification of a single machine for the execution job.                           |
| `persistentDiskSpec`     | `object ( `[`PersistentDiskSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.PersistentDiskSpec)` )` The specification of a persistent disk to attach for the execution job.  |
| `networkSpec`            | `object ( `[`NetworkSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NetworkSpec)` )` The network configuration to use for the execution job.                                |
| `shieldedInstanceConfig` | `object ( `[`ShieldedInstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.ShieldedInstanceConfig)` )` Optional. Shielded VM configuration (for example, Secure Boot) for the execution VM. |

### MachineSpec

**JSON representation**

```
{
  "machineType": string,
  "acceleratorType": enum (AcceleratorType),
  "acceleratorCount": integer,
  "gpuPartitionSize": string,
  "tpuTopology": string,
  "reservationAffinity": {
    object (ReservationAffinity)
  }
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineType`         | `string` Immutable. The type of the machine. See the [list of machine types supported for prediction](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#machine-types) See the [list of machine types supported for custom training](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . For `DeployedModel` this field is optional, and the default value is `n1-standard-2` . For `BatchPredictionJob` or as part of `WorkerPoolSpec` this field is required.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `acceleratorType`     | `enum ( `[`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.AcceleratorType)` )` Immutable. The type of accelerator(s) that may be attached to the machine as per `accelerator_count` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `acceleratorCount`    | `integer` The number of accelerators to attach to the machine. For [accelerator optimized machine types](https://cloud.google.com/compute/docs/accelerator-optimized-machines) , One may set the accelerator_count from 1 to N for machine with N GPUs. If accelerator_count is less than or equal to N / 2, Agent Platform co-schedules the replicas of the model into the same VM to save cost. For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set accelerator_count to 1 to 8. If accelerator_count is 1, 2, 3, or 4, Agent Platform co-schedules 8, 4, 2, or 2 replicas of the model into the same VM to save cost. When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM. Note that the feature is not compatible with \[multihost_gpu_node_count\]\[\]. When multihost_gpu_node_count is set, the co-scheduling will not be enabled. |
| `gpuPartitionSize`    | `string` Optional. Immutable. The Nvidia GPU partition size. When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu_partition_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances. The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes. If set, the accelerator_count should be set to 1.                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `tpuTopology`         | `string` Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu_topology: "2x2x1").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `reservationAffinity` | `object ( `[`ReservationAffinity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.ReservationAffinity)` )` Optional. Immutable. Configuration controlling how this resource pool consumes reservation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### ReservationAffinity

**JSON representation**

```
{
  "reservationAffinityType": enum (Type),
  "key": string,
  "values": [
    string
  ]
}
```

| Fields                    |                                                                                                                                                                                                                                       |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservationAffinityType` | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.Type)` )` Required. Specifies the reservation affinity type. |
| `key`                     | `string` Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.  |
| `values[]`                | `string` Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.                                                                            |

### PersistentDiskSpec

**JSON representation**

```
{
  "diskType": string,
  "diskSizeGb": string
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `diskType`   | `string` Type of the disk (default is "pd-standard"). Valid values: "pd-ssd" (Persistent Disk Solid State Drive) "pd-standard" (Persistent Disk Hard Disk Drive) "pd-balanced" (Balanced Persistent Disk) "pd-extreme" (Extreme Persistent Disk) "hyperdisk-balanced" (Hyperdisk Balanced) "hyperdisk-extreme" (Hyperdisk Extreme) "hyperdisk-balanced-high-availability" (Hyperdisk Balanced High Availability) "hyperdisk-ml" (Hyperdisk ML) "hyperdisk-throughput" (Hyperdisk Throughput) |
| `diskSizeGb` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Size in GB of the disk (default is 100GB).                                                                                                                                                                                                                                                                                                                                                            |

### NetworkSpec

**JSON representation**

```
{
  "enableInternetAccess": boolean,
  "network": string,
  "subnetwork": string
}
```

| Fields                 |                                                                                                                                                  |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableInternetAccess` | `boolean` Whether to enable public internet access. Default false.                                                                               |
| `network`              | `string` The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks)            |
| `subnetwork`           | `string` The name of the subnet that this instance is in. Format: `projects/{project_id_or_number}/regions/{region}/subnetworks/{subnetwork_id}` |

### ShieldedInstanceConfig

**JSON representation**

```
{
  "enableSecureBoot": boolean,
  "enableVtpm": boolean,
  "enableIntegrityMonitoring": boolean
}
```

| Fields                      |                                                                                           |
|-----------------------------|-------------------------------------------------------------------------------------------|
| `enableSecureBoot`          | `boolean` Optional. Whether the VM instance has Secure Boot enabled. Disabled by default. |
| `enableVtpm`                | `boolean` Optional. Whether the VM instance has vTPM enabled.                             |
| `enableIntegrityMonitoring` | `boolean` Optional. Whether the VM instance has integrity monitoring enabled.             |

### WorkbenchRuntime

**JSON representation**

```
{

  // Union field image_environment can be only one of the following:
  "vmImage": {
    object (VmImage)
  },
  "customContainerImage": {
    object (ContainerImage)
  }
  // End of list of possible types for union field image_environment.
}
```

| Fields                                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                                                         |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `image_environment` . The image environment to run the notebook execution in. Optional: if unset, the service defaults to a managed `workbench-instances-2603` VM image (Python 3.12). `image_environment` can be only one of the following: |                                                                                                                                                                                                                                                                                                         |
| `vmImage`                                                                                                                                                                                                                                                | `object ( `[`VmImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.VmImage)` )` A specific Compute Engine VM image to run the notebook on.                                                                       |
| `customContainerImage`                                                                                                                                                                                                                                   | `object ( `[`ContainerImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_create_job#Input.Schema.ContainerImage)` )` A user-provided container image. The notebook executes inside this container on a managed container-host (COS) VM. |

### VmImage

**JSON representation**

```
{
  "project": string,

  // Union field image can be only one of the following:
  "name": string,
  "family": string
  // End of list of possible types for union field image.
}
```

| Fields                                                                                                      |                                                                                                                 |
|-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| `project`                                                                                                   | `string` Required. The name of the Google Cloud project that this VM image belongs to. Format: `{project_id}` . |
| Union field `image` . The reference to a Compute Engine VM image. `image` can be only one of the following: |                                                                                                                 |
| `name`                                                                                                      | `string` Use this VM image name to find the image.                                                              |
| `family`                                                                                                    | `string` Use this VM image family to find the image; the newest image in this family is used.                   |

### ContainerImage

**JSON representation**

```
{
  "repository": string,
  "tag": string
}
```

| Fields       |                                                                                                                  |
|--------------|------------------------------------------------------------------------------------------------------------------|
| `repository` | `string` Required. The path to the container image repository. For example: `gcr.io/{project_id}/{image_name}` . |
| `tag`        | `string` Optional. The tag of the container image. If unset, defaults to `latest` .                              |

### Duration

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years                                                                                    |
| `nanos`   | `integer` Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive. |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### RunResponse

**JSON representation**

```
{
  "scheduledRunTime": string,
  "runResponse": string
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `scheduledRunTime` | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` The scheduled run time based on the user-specified schedule. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `runResponse`      | `string` The response of the scheduled run.                                                                                                                                                                                                                                                                                                                                                                                        |

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### PipelineState

Describes the state of a pipeline.

| Enums                        |                                                                                                                                                                   |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `PIPELINE_STATE_UNSPECIFIED` | The pipeline state is unspecified.                                                                                                                                |
| `PIPELINE_STATE_QUEUED`      | The pipeline has been created or resumed, and processing has not yet begun.                                                                                       |
| `PIPELINE_STATE_PENDING`     | The service is preparing to run the pipeline.                                                                                                                     |
| `PIPELINE_STATE_RUNNING`     | The pipeline is in progress.                                                                                                                                      |
| `PIPELINE_STATE_SUCCEEDED`   | The pipeline completed successfully.                                                                                                                              |
| `PIPELINE_STATE_FAILED`      | The pipeline failed.                                                                                                                                              |
| `PIPELINE_STATE_CANCELLING`  | The pipeline is being cancelled. From this state, the pipeline may only go to either PIPELINE_STATE_SUCCEEDED, PIPELINE_STATE_FAILED or PIPELINE_STATE_CANCELLED. |
| `PIPELINE_STATE_CANCELLED`   | The pipeline has been cancelled.                                                                                                                                  |
| `PIPELINE_STATE_PAUSED`      | The pipeline has been stopped, and can be resumed.                                                                                                                |

### State

Specifies state of TaskExecution

| Enums               |                                                                                                                                                                                         |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified.                                                                                                                                                                            |
| `PENDING`           | Specifies pending state for the task.                                                                                                                                                   |
| `RUNNING`           | Specifies task is being executed.                                                                                                                                                       |
| `SUCCEEDED`         | Specifies task completed successfully.                                                                                                                                                  |
| `CANCEL_PENDING`    | Specifies Task cancel is in pending state.                                                                                                                                              |
| `CANCELLING`        | Specifies task is being cancelled.                                                                                                                                                      |
| `CANCELLED`         | Specifies task was cancelled.                                                                                                                                                           |
| `FAILED`            | Specifies task failed.                                                                                                                                                                  |
| `SKIPPED`           | Specifies task was skipped due to cache hit.                                                                                                                                            |
| `NOT_TRIGGERED`     | Specifies that the task was not triggered because the task's trigger policy is not satisfied. The trigger policy is specified in the `condition` field of `PipelineJob.pipeline_spec` . |

### State

Describes the state of the Execution.

| Enums               |                                            |
|---------------------|--------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified Execution state                |
| `NEW`               | The Execution is new                       |
| `RUNNING`           | The Execution is running                   |
| `COMPLETE`          | The Execution has finished running         |
| `FAILED`            | The Execution has failed                   |
| `CACHED`            | The Execution completed through Cache hit. |
| `CANCELLED`         | The Execution was cancelled.               |

### State

Describes the state of the Artifact.

| Enums               |                                                                                                                                                |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified state for the Artifact.                                                                                                            |
| `PENDING`           | A state used by systems like Agent Platform Pipelines to indicate that the underlying data item represented by this Artifact is being created. |
| `LIVE`              | A state indicating that the Artifact should exist, unless something external to the system deletes it.                                         |

### PipelineFailurePolicy

Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW. However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion.

| Enums                                 |                                                                                                                |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------|
| `PIPELINE_FAILURE_POLICY_UNSPECIFIED` | Default value, and follows fail slow behavior.                                                                 |
| `PIPELINE_FAILURE_POLICY_FAIL_SLOW`   | Indicates that the pipeline should continue to run until all possible tasks have been scheduled and completed. |
| `PIPELINE_FAILURE_POLICY_FAIL_FAST`   | Indicates that the pipeline should stop scheduling new tasks after a task has failed.                          |

### AcceleratorType

Represents a hardware accelerator type.

| Enums                          |                                                                                                                        |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------|
| `ACCELERATOR_TYPE_UNSPECIFIED` | Unspecified accelerator type, which means no accelerator.                                                              |
| `NVIDIA_TESLA_K80`             | Deprecated: Nvidia Tesla K80 GPU has reached end of support, see <https://cloud.google.com/compute/docs/eol/k80-eol> . |
| `NVIDIA_TESLA_P100`            | Nvidia Tesla P100 GPU.                                                                                                 |
| `NVIDIA_TESLA_V100`            | Nvidia Tesla V100 GPU.                                                                                                 |
| `NVIDIA_TESLA_P4`              | Nvidia Tesla P4 GPU.                                                                                                   |
| `NVIDIA_TESLA_T4`              | Nvidia Tesla T4 GPU.                                                                                                   |
| `NVIDIA_TESLA_A100`            | Nvidia Tesla A100 GPU.                                                                                                 |
| `NVIDIA_A100_80GB`             | Nvidia A100 80GB GPU.                                                                                                  |
| `NVIDIA_L4`                    | Nvidia L4 GPU.                                                                                                         |
| `NVIDIA_H100_80GB`             | Nvidia H100 80Gb GPU.                                                                                                  |
| `NVIDIA_H100_MEGA_80GB`        | Nvidia H100 Mega 80Gb GPU.                                                                                             |
| `NVIDIA_H200_141GB`            | Nvidia H200 141Gb GPU.                                                                                                 |
| `NVIDIA_B200`                  | Nvidia B200 GPU.                                                                                                       |
| `NVIDIA_GB200`                 | Nvidia GB200 GPU.                                                                                                      |
| `NVIDIA_RTX_PRO_6000`          | Nvidia RTX Pro 6000 GPU.                                                                                               |
| `TPU_V2`                       | TPU v2.                                                                                                                |
| `TPU_V3`                       | TPU v3.                                                                                                                |
| `TPU_V4_POD`                   | TPU v4.                                                                                                                |
| `TPU_V5_LITEPOD`               | TPU v5.                                                                                                                |

### Type

Identifies a type of reservation affinity.

| Enums                  |                                                                                                                         |
|------------------------|-------------------------------------------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED`     | Default value. This should not be used.                                                                                 |
| `NO_RESERVATION`       | Do not consume from any reserved capacity, only use on-demand.                                                          |
| `ANY_RESERVATION`      | Consume any reservation available, falling back to on-demand.                                                           |
| `SPECIFIC_RESERVATION` | Consume from a specific reservation. When chosen, the reservation must be identified via the `key` and `values` fields. |

### JobState

Describes the state of a job.

| Enums                           |                                                                                                                                                 |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `JOB_STATE_UNSPECIFIED`         | The job state is unspecified.                                                                                                                   |
| `JOB_STATE_QUEUED`              | The job has been just created or resumed and processing has not yet begun.                                                                      |
| `JOB_STATE_PENDING`             | The service is preparing to run the job.                                                                                                        |
| `JOB_STATE_RUNNING`             | The job is in progress.                                                                                                                         |
| `JOB_STATE_SUCCEEDED`           | The job completed successfully.                                                                                                                 |
| `JOB_STATE_FAILED`              | The job failed.                                                                                                                                 |
| `JOB_STATE_CANCELLING`          | The job is being cancelled. From this state the job may only go to either `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` . |
| `JOB_STATE_CANCELLED`           | The job has been cancelled.                                                                                                                     |
| `JOB_STATE_PAUSED`              | The job has been stopped, and can be resumed.                                                                                                   |
| `JOB_STATE_EXPIRED`             | The job has expired.                                                                                                                            |
| `JOB_STATE_UPDATING`            | The job is being updated. Only jobs in the `RUNNING` state can be updated. After updating, the job goes back to the `RUNNING` state.            |
| `JOB_STATE_PARTIALLY_SUCCEEDED` | The job is partially succeeded, some results may be missing due to errors.                                                                      |

### State

Possible state of the schedule.

| Enums               |                                                                                                                                                                       |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified.                                                                                                                                                          |
| `ACTIVE`            | The Schedule is active. Runs are being scheduled on the user-specified timespec.                                                                                      |
| `PAUSED`            | The schedule is paused. No new runs will be created until the schedule is resumed. Already started runs will be allowed to complete.                                  |
| `COMPLETED`         | The Schedule is completed. No new runs will be scheduled. Already started runs will be allowed to complete. Schedules in completed state cannot be paused or resumed. |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ❌ \| Read Only Hint: ❌ \| Open World Hint: ❌
