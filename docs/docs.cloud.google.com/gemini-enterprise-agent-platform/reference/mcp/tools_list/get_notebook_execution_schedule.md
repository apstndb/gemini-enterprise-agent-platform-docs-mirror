---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_notebook_execution_schedule
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_notebook_execution_schedule
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `get_notebook_execution_schedule`

Use this tool to get the details and status of a specific notebook execution schedule. Format: 'projects/{project\_id}/locations/{region}/schedules/{schedule\_id}'. CRITICAL: For {region}, use the region specified in the current context. If no region is specified, prompt the user for one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `get_notebook_execution_schedule` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://aiplatform.googleapis.com/mcp/generate&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;get_notebook_execution_schedule&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for `ScheduleService.GetSchedule` .

### GetScheduleRequest

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The name of the Schedule resource. Format: `projects/{project}/locations/{location}/schedules/{schedule}`

## Output Schema

An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type.

### Schedule

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;maxRunCount&quot;: string,&quot;startedRunCount&quot;: string,&quot;state&quot;: enum (State),&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;nextRunTime&quot;: string,&quot;lastPauseTime&quot;: string,&quot;lastResumeTime&quot;: string,&quot;maxConcurrentRunCount&quot;: string,&quot;maxConcurrentActiveRunCount&quot;: string,&quot;allowQueueing&quot;: boolean,&quot;catchUp&quot;: boolean,&quot;lastScheduledRunResponse&quot;: {object (RunResponse)},// Union field time_specification can be only one of the following:&quot;cron&quot;: string// End of list of possible types for union field time_specification.// Union field request can be only one of the following:&quot;createPipelineJobRequest&quot;: {object (CreatePipelineJobRequest)},&quot;createNotebookExecutionJobRequest&quot;: {object (CreateNotebookExecutionJobRequest)}// End of list of possible types for union field request.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Immutable. The resource name of the Schedule.

`displayName`

`string`

Required. User provided name of the Schedule. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`startTime`

` string ( Timestamp  ` format)

Optional. Timestamp after which the first run can be scheduled. Default to Schedule create time if not specified.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime`

` string ( Timestamp  ` format)

Optional. Timestamp after which no new runs can be scheduled. If specified, The schedule will be completed when either end\_time is reached or when scheduled\_run\_count \>= max\_run\_count. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`maxRunCount`

`string ( int64 format)`

Optional. Maximum run count of the schedule. If specified, The schedule will be completed when either started\_run\_count \>= max\_run\_count or when end\_time is reached. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified.

`startedRunCount`

`string ( int64 format)`

Output only. The number of runs started by this schedule.

`state`

`enum ( State` )

Output only. The state of this Schedule.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Schedule was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Schedule was updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`nextRunTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Schedule should schedule the next run. Having a next\_run\_time in the past means the runs are being started behind schedule.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`lastPauseTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Schedule was last paused. Unset if never paused.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`lastResumeTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Schedule was last resumed. Unset if never resumed from pause.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`maxConcurrentRunCount`

`string ( int64 format)`

Required. Maximum number of runs that can be started concurrently for this Schedule. This is the limit for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable).

`maxConcurrentActiveRunCount`

`string ( int64 format)`

Optional. Specifies the maximum number of active runs that can be executed concurrently for this Schedule. This limits the number of runs that can be in a non-terminal state at the same time. Currently, this field is only supported for requests of type CreatePipelineJobRequest.

`allowQueueing`

`boolean`

Optional. Whether new scheduled runs can be queued when max\_concurrent\_runs limit is reached. If set to true, new runs will be queued instead of skipped. Default to false.

`catchUp`

`boolean`

Output only. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. Default to false.

`lastScheduledRunResponse`

` object ( RunResponse  ` )

Output only. Response of the last scheduled run. This is the response for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable). Unset if no run has been scheduled yet.

Union field `time_specification` . Required. The time specification to launch scheduled runs. `time_specification` can be only one of the following:

`cron`

`string`

Cron schedule ( <https://en.wikipedia.org/wiki/Cron> ) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON\_TZ=${IANA\_TIME\_ZONE}" or "TZ=${IANA\_TIME\_ZONE}". The ${IANA\_TIME\_ZONE} may only be a valid string from IANA time zone database. For example, "CRON\_TZ=America/New\_York 1 \* \* \* \*", or "TZ=America/New\_York 1 \* \* \* \*".

Union field `request` . Required. The API request template to launch the scheduled runs. User-specified ID is not supported in the request template. `request` can be only one of the following:

`createPipelineJobRequest`

` object ( CreatePipelineJobRequest  ` )

Request for `PipelineService.CreatePipelineJob` . CreatePipelineJobRequest.parent field is required (format: projects/{project}/locations/{location}).

`createNotebookExecutionJobRequest`

` object ( CreateNotebookExecutionJobRequest  ` )

Request for `NotebookService.CreateNotebookExecutionJob` .

### CreatePipelineJobRequest

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;pipelineJob&quot;: {object (PipelineJob)},&quot;pipelineJobId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. The resource name of the Location to create the PipelineJob in. Format: `projects/{project}/locations/{location}`

`pipelineJob`

` object ( PipelineJob  ` )

Required. The PipelineJob to create.

`pipelineJobId`

`string`

The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated.

This value should be less than 128 characters, and valid characters are `/[a-z][0-9]-/` .

### PipelineJob

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;createTime&quot;: string,&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;updateTime&quot;: string,&quot;pipelineSpec&quot;: {object},&quot;state&quot;: enum (PipelineState),&quot;jobDetail&quot;: {object (PipelineJobDetail)},&quot;error&quot;: {object (Status)},&quot;labels&quot;: {string: string,...},&quot;runtimeConfig&quot;: {object (RuntimeConfig)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;serviceAccount&quot;: string,&quot;network&quot;: string,&quot;reservedIpRanges&quot;: [string],&quot;pscInterfaceConfig&quot;: {object (PscInterfaceConfig)},&quot;templateUri&quot;: string,&quot;templateMetadata&quot;: {object (PipelineTemplateMetadata)},&quot;scheduleName&quot;: string,&quot;preflightValidations&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. The resource name of the PipelineJob.

`displayName`

`string`

The display name of the Pipeline. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`createTime`

` string ( Timestamp  ` format)

Output only. Pipeline creation time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime`

` string ( Timestamp  ` format)

Output only. Pipeline start time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime`

` string ( Timestamp  ` format)

Output only. Pipeline end time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this PipelineJob was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`pipelineSpec`

` object ( Struct  ` format)

A compiled definition of a pipeline, represented as a `JSON` object. Defines the structure of the pipeline, including its components, tasks, and parameters. This specification is generated by compiling a pipeline function defined in `Python` using the `Kubeflow Pipelines SDK` .

`state`

`enum ( PipelineState` )

Output only. The detailed state of the job.

`jobDetail`

` object ( PipelineJobDetail  ` )

Output only. The details of pipeline run. Not available in the list view.

`error`

` object ( Status  ` )

Output only. The error that occurred during pipeline execution. Only populated when the pipeline's state is FAILED or CANCELLED.

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize PipelineJob.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

Note there is some reserved label key for Agent Platform Pipelines. - `vertex-ai-pipelines-run-billing-id` , user set value will get overrided.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`runtimeConfig`

` object ( RuntimeConfig  ` )

Runtime config of the pipeline.

`encryptionSpec`

` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for a pipelineJob. If set, this PipelineJob and all of its sub-resources will be secured by this key.

`serviceAccount`

`string`

The service account that the pipeline workload runs as. If not specified, the Compute Engine default service account in the project will be used. See <https://cloud.google.com/compute/docs/access/service-accounts#default_service_account>

Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service account.

`network`

`string`

The full name of the Compute Engine [network](https://docs.cloud.google.com/compute/docs/networks-and-firewalls#networks) to which the Pipeline Job's workload should be peered. For example, `projects/12345/global/networks/myVPC` . [Format](https://docs.cloud.google.com/compute/docs/reference/rest/v1/networks/insert) is of the form `projects/{project}/global/networks/{network}` . Where {project} is a project number, as in `12345` , and {network} is a network name.

Private services access must already be configured for the network. Pipeline job will apply the network configuration to the Google Cloud resources being launched, if applied, such as Agent Platform Training or Dataflow job. If left unspecified, the workload is not peered with any network.

`reservedIpRanges[]`

`string`

A list of names for the reserved ip ranges under the VPC network that can be used for this Pipeline Job's workload.

If set, we will deploy the Pipeline Job's workload within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network.

Example: \['vertex-ai-ip-range'\].

`pscInterfaceConfig`

` object ( PscInterfaceConfig  ` )

Optional. Configuration for PSC-I for PipelineJob.

`templateUri`

`string`

A template uri from where the `PipelineJob.pipeline_spec` , if empty, will be downloaded. Currently, only uri from Vertex Template Registry & Gallery is supported. Reference to <https://cloud.google.com/vertex-ai/docs/pipelines/create-pipeline-template> .

`templateMetadata`

` object ( PipelineTemplateMetadata  ` )

Output only. Pipeline template metadata. Will fill up fields if `PipelineJob.template_uri` is from supported template registry.

`scheduleName`

`string`

Output only. The schedule resource name. Only returned if the Pipeline is created by Schedule API.

`preflightValidations`

`boolean`

Optional. Whether to do component level validations before job creation.

### Timestamp

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`nanos`

`integer`

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### Struct

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;fields&quot;: {
    string: value,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fields`

` map (key: string, value: value ( Value  ` format))

Unordered map of dynamically typed values.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### FieldsEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` value ( Value  ` format)

### Value

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field kind can be only one of the following:&quot;nullValue&quot;: null,&quot;numberValue&quot;: number,&quot;stringValue&quot;: string,&quot;boolValue&quot;: boolean,&quot;structValue&quot;: {object},&quot;listValue&quot;: array// End of list of possible types for union field kind.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `kind` . The kind of value. `kind` can be only one of the following:

`nullValue`

`null`

Represents a JSON `null` .

`numberValue`

`number`

Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type.

`stringValue`

`string`

Represents a JSON string.

`boolValue`

`boolean`

Represents a JSON boolean ( `true` or `false` literal in JSON).

`structValue`

` object ( Struct  ` format)

Represents a JSON object.

`listValue`

` array ( ListValue  ` format)

Represents a JSON array.

### ListValue

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;values&quot;: [
    value
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`values[]`

` value ( Value  ` format)

Repeated field of dynamically typed values.

### PipelineJobDetail

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;pipelineContext&quot;: {object (Context)},&quot;pipelineRunContext&quot;: {object (Context)},&quot;taskDetails&quot;: [{object (PipelineTaskDetail)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`pipelineContext`

` object ( Context  ` )

Output only. The context of the pipeline.

`pipelineRunContext`

` object ( Context  ` )

Output only. The context of the current pipeline run.

`taskDetails[]`

` object ( PipelineTaskDetail  ` )

Output only. The runtime details of the tasks under the pipeline.

### Context

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;displayName&quot;: string,
  &quot;etag&quot;: string,
  &quot;labels&quot;: {
    string: string,
    ...
  },
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;parentContexts&quot;: [
    string
  ],
  &quot;schemaTitle&quot;: string,
  &quot;schemaVersion&quot;: string,
  &quot;metadata&quot;: {
    object
  },
  &quot;description&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Immutable. The resource name of the Context.

`displayName`

`string`

User provided display name of the Context. May be up to 128 Unicode characters.

`etag`

`string`

An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize your Contexts.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Context (System labels are excluded).

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Context was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Context was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`parentContexts[]`

`string`

Output only. A list of resource names of Contexts that are parents of this Context. A Context may have at most 10 parent\_contexts.

`schemaTitle`

`string`

The title of the schema describing the metadata.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`schemaVersion`

`string`

The version of the schema in schema\_name to use.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`metadata`

` object ( Struct  ` format)

Properties of the Context. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.

`description`

`string`

Description of the Context

### LabelsEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### PipelineTaskDetail

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;taskId&quot;: string,&quot;parentTaskId&quot;: string,&quot;taskName&quot;: string,&quot;createTime&quot;: string,&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;executorDetail&quot;: {object (PipelineTaskExecutorDetail)},&quot;state&quot;: enum (State),&quot;execution&quot;: {object (Execution)},&quot;error&quot;: {object (Status)},&quot;pipelineTaskStatus&quot;: [{object (PipelineTaskStatus)}],&quot;inputs&quot;: {string: {object (ArtifactList)},...},&quot;outputs&quot;: {string: {object (ArtifactList)},...},&quot;taskUniqueName&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`taskId`

`string ( int64 format)`

Output only. The system generated ID of the task.

`parentTaskId`

`string ( int64 format)`

Output only. The id of the parent task if the task is within a component scope. Empty if the task is at the root level.

`taskName`

`string`

Output only. The user specified name of the task that is defined in `pipeline_spec` .

`createTime`

` string ( Timestamp  ` format)

Output only. Task create time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime`

` string ( Timestamp  ` format)

Output only. Task start time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime`

` string ( Timestamp  ` format)

Output only. Task end time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`executorDetail`

` object ( PipelineTaskExecutorDetail  ` )

Output only. The detailed execution info.

`state`

`enum ( State` )

Output only. State of the task.

`execution`

` object ( Execution  ` )

Output only. The execution metadata of the task.

`error`

` object ( Status  ` )

Output only. The error that occurred during task execution. Only populated when the task's state is FAILED or CANCELLED.

`pipelineTaskStatus[]`

` object ( PipelineTaskStatus  ` )

Output only. A list of task status. This field keeps a record of task status evolving over time.

`inputs`

` map (key: string, value: object ( ArtifactList  ` ))

Output only. The runtime input artifacts of the task.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`outputs`

` map (key: string, value: object ( ArtifactList  ` ))

Output only. The runtime output artifacts of the task.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`taskUniqueName`

`string`

Output only. The unique name of a task. This field is used by rerun pipeline job. Console UI and Agent Platform SDK will support triggering pipeline job reruns. The name is constructed by concatenating all the parent tasks name with the task name. For example, if a task named "child\_task" has a parent task named "parent\_task\_1" and parent task 1 has a parent task named "parent\_task\_2", the task unique name will be "parent\_task\_2.parent\_task\_1.child\_task".

### PipelineTaskExecutorDetail

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field details can be only one of the following:&quot;containerDetail&quot;: {object (ContainerDetail)},&quot;customJobDetail&quot;: {object (CustomJobDetail)}// End of list of possible types for union field details.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `details` .

`details` can be only one of the following:

`containerDetail`

` object ( ContainerDetail  ` )

Output only. The detailed info for a container executor.

`customJobDetail`

` object ( CustomJobDetail  ` )

Output only. The detailed info for a custom job executor.

### ContainerDetail

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;mainJob&quot;: string,
  &quot;preCachingCheckJob&quot;: string,
  &quot;failedMainJobs&quot;: [
    string
  ],
  &quot;failedPreCachingCheckJobs&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mainJob`

`string`

Output only. The name of the `CustomJob` for the main container execution.

`preCachingCheckJob`

`string`

Output only. The name of the `CustomJob` for the pre-caching-check container execution. This job will be available if the `PipelineJob.pipeline_spec` specifies the `pre_caching_check` hook in the lifecycle events.

`failedMainJobs[]`

`string`

Output only. The names of the previously failed `CustomJob` for the main container executions. The list includes the all attempts in chronological order.

`failedPreCachingCheckJobs[]`

`string`

Output only. The names of the previously failed `CustomJob` for the pre-caching-check container executions. This job will be available if the `PipelineJob.pipeline_spec` specifies the `pre_caching_check` hook in the lifecycle events. The list includes the all attempts in chronological order.

### CustomJobDetail

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;job&quot;: string,
  &quot;failedJobs&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`job`

`string`

Output only. The name of the `CustomJob` .

`failedJobs[]`

`string`

Output only. The names of the previously failed `CustomJob` . The list includes the all attempts in chronological order.

### Execution

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;state&quot;: enum (State),&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;schemaTitle&quot;: string,&quot;schemaVersion&quot;: string,&quot;metadata&quot;: {object},&quot;description&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. The resource name of the Execution.

`displayName`

`string`

User provided display name of the Execution. May be up to 128 Unicode characters.

`state`

`enum ( State` )

The state of this Execution. This is a property of the Execution, and does not imply or capture any ongoing process. This property is managed by clients (such as Agent Platform Pipelines) and the system does not prescribe or check the validity of state transitions.

`etag`

`string`

An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize your Executions.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Execution (System labels are excluded).

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Execution was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Execution was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`schemaTitle`

`string`

The title of the schema describing the metadata.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`schemaVersion`

`string`

The version of the schema in `schema_title` to use.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`metadata`

` object ( Struct  ` format)

Properties of the Execution. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.

`description`

`string`

Description of the Execution

### LabelsEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### Status

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;code&quot;: integer,
  &quot;message&quot;: string,
  &quot;details&quot;: [
    {
      &quot;@type&quot;: string,
      field1: ...,
      ...
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`code`

`integer`

The status code, which should be an enum value of `google.rpc.Code` .

`message`

`string`

A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.

`details[]`

`object`

A list of messages that carry the error details. There is a common set of message types for APIs to use.

An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .

### Any

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;typeUrl&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`typeUrl`

`string`

Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name.

Example: type.googleapis.com/google.protobuf.StringValue

This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them.

The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests.

All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected.

In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs.

`value`

`string ( bytes format)`

Holds a Protobuf serialization of the type described by type\_url.

A base64-encoded string.

### PipelineTaskStatus

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;updateTime&quot;: string,&quot;state&quot;: enum (State),&quot;error&quot;: {object (Status)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`updateTime`

` string ( Timestamp  ` format)

Output only. Update time of this status.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state`

`enum ( State` )

Output only. The state of the task.

`error`

` object ( Status  ` )

Output only. The error that occurred during the state. May be set when the state is any of the non-final state (PENDING/RUNNING/CANCELLING) or FAILED state. If the state is FAILED, the error here is final and not going to be retried. If the state is a non-final state, the error indicates a system-error being retried.

### InputsEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (ArtifactList)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( ArtifactList  ` )

### ArtifactList

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;artifacts&quot;: [{object (Artifact)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`artifacts[]`

` object ( Artifact  ` )

Output only. A list of artifact metadata.

### Artifact

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;uri&quot;: string,&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;state&quot;: enum (State),&quot;schemaTitle&quot;: string,&quot;schemaVersion&quot;: string,&quot;metadata&quot;: {object},&quot;description&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. The resource name of the Artifact.

`displayName`

`string`

User provided display name of the Artifact. May be up to 128 Unicode characters.

`uri`

`string`

The uniform resource identifier of the artifact file. May be empty if there is no actual artifact file.

`etag`

`string`

An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize your Artifacts.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Artifact (System labels are excluded).

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Artifact was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Artifact was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state`

`enum ( State` )

The state of this Artifact. This is a property of the Artifact, and does not imply or capture any ongoing process. This property is managed by clients (such as Agent Platform Pipelines), and the system does not prescribe or check the validity of state transitions.

`schemaTitle`

`string`

The title of the schema describing the metadata.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`schemaVersion`

`string`

The version of the schema in schema\_name to use.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`metadata`

` object ( Struct  ` format)

Properties of the Artifact. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.

`description`

`string`

Description of the Artifact

### LabelsEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### OutputsEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (ArtifactList)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( ArtifactList  ` )

### LabelsEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### RuntimeConfig

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parameters&quot;: {string: {object (Value)},...},&quot;gcsOutputDirectory&quot;: string,&quot;parameterValues&quot;: {string: value,...},&quot;failurePolicy&quot;: enum (PipelineFailurePolicy),&quot;inputArtifacts&quot;: {string: {object (InputArtifact)},...}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` parameters (deprecated)  `

` map (key: string, value: object ( Value  ` ))

> This item is deprecated\!

Deprecated. Use `RuntimeConfig.parameter_values` instead. The runtime parameters of the PipelineJob. The parameters will be passed into `PipelineJob.pipeline_spec` to replace the placeholders at runtime. This field is used by pipelines built using `PipelineJob.pipeline_spec.schema_version` 2.0.0 or lower, such as pipelines built using Kubeflow Pipelines SDK 1.8 or lower.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`gcsOutputDirectory`

`string`

Required. A path in a Cloud Storage bucket, which will be treated as the root output directory of the pipeline. It is used by the system to generate the paths of output artifacts. The artifact paths are generated with a sub-path pattern `{job_id}/{task_id}/{output_key}` under the specified output directory. The service account specified in this pipeline must have the `storage.objects.get` and `storage.objects.create` permissions for this bucket.

`parameterValues`

` map (key: string, value: value ( Value  ` format))

The runtime parameters of the PipelineJob. The parameters will be passed into `PipelineJob.pipeline_spec` to replace the placeholders at runtime. This field is used by pipelines built using `PipelineJob.pipeline_spec.schema_version` 2.1.0, such as pipelines built using Kubeflow Pipelines SDK 1.9 or higher and the v2 DSL.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`failurePolicy`

`enum ( PipelineFailurePolicy` )

Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE\_FAILURE\_POLICY\_FAIL\_SLOW. However, if a pipeline is set to PIPELINE\_FAILURE\_POLICY\_FAIL\_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion.

`inputArtifacts`

` map (key: string, value: object ( InputArtifact  ` ))

The runtime artifacts of the PipelineJob. The key will be the input artifact name and the value would be one of the InputArtifact.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### ParametersEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (Value)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( Value  ` )

### Value

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field value can be only one of the following:&quot;intValue&quot;: string,&quot;doubleValue&quot;: number,&quot;stringValue&quot;: string// End of list of possible types for union field value.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `value` .

`value` can be only one of the following:

`intValue`

`string ( int64 format)`

An integer value.

`doubleValue`

`number`

A double value.

`stringValue`

`string`

A string value.

### ParameterValuesEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` value ( Value  ` format)

### InputArtifactsEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (InputArtifact)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( InputArtifact  ` )

### InputArtifact

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field kind can be only one of the following:&quot;artifactId&quot;: string// End of list of possible types for union field kind.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `kind` .

`kind` can be only one of the following:

`artifactId`

`string`

Artifact resource id from MLMD. Which is the last portion of an artifact resource name: `projects/{project}/locations/{location}/metadataStores/default/artifacts/{artifact_id}` . The artifact must stay within the same project, location and default metadatastore as the pipeline.

### EncryptionSpec

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;kmsKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kmsKeyName`

`string`

Required. Resource name of the Cloud KMS key used to protect the resource.

The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` .

### PscInterfaceConfig

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;networkAttachment&quot;: string,&quot;dnsPeeringConfigs&quot;: [{object (DnsPeeringConfig)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`networkAttachment`

`string`

Optional. The name of the Compute Engine [network attachment](https://cloud.google.com/vpc/docs/about-network-attachments) to attach to the resource within the region and user project. To specify this field, you must have already [created a network attachment](https://cloud.google.com/vpc/docs/create-manage-network-attachments#create-network-attachments) . This field is only used for resources using PSC-I.

`dnsPeeringConfigs[]`

` object ( DnsPeeringConfig  ` )

Optional. DNS peering configurations. When specified, Agent Platform will attempt to configure DNS peering zones in the tenant project VPC to resolve the specified domains using the target network's Cloud DNS. The user must grant the dns.peer role to the Agent Platform Service Agent on the target project.

### DnsPeeringConfig

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;domain&quot;: string,
  &quot;targetProject&quot;: string,
  &quot;targetNetwork&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`domain`

`string`

Required. The DNS name suffix of the zone being peered to, e.g., "my-internal-domain.corp.". Must end with a dot.

`targetProject`

`string`

Required. The project ID hosting the Cloud DNS managed zone that contains the 'domain'. The Agent Platform Service Agent requires the dns.peer role on this project.

`targetNetwork`

`string`

Required. The VPC network name in the target\_project where the DNS zone specified by 'domain' is visible.

### PipelineTemplateMetadata

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;version&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`version`

`string`

The version\_name in artifact registry.

Will always be presented in output if the `PipelineJob.template_uri` is from supported template registry.

Format is "sha256:abcdef123456...".

### CreateNotebookExecutionJobRequest

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;notebookExecutionJob&quot;: {object (NotebookExecutionJob)},&quot;notebookExecutionJobId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. The resource name of the Location to create the NotebookExecutionJob. Format: `projects/{project}/locations/{location}`

`notebookExecutionJob`

` object ( NotebookExecutionJob  ` )

Required. The NotebookExecutionJob to create.

`notebookExecutionJobId`

`string`

Optional. User specified ID for the NotebookExecutionJob.

### NotebookExecutionJob

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;executionTimeout&quot;: string,&quot;scheduleResourceName&quot;: string,&quot;jobState&quot;: enum (JobState),&quot;status&quot;: {object (Status)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;labels&quot;: {string: string,...},&quot;kernelName&quot;: string,&quot;encryptionSpec&quot;: {object (EncryptionSpec)},// Union field notebook_source can be only one of the following:&quot;dataformRepositorySource&quot;: {object (DataformRepositorySource)},&quot;gcsNotebookSource&quot;: {object (GcsNotebookSource)},&quot;directNotebookSource&quot;: {object (DirectNotebookSource)}// End of list of possible types for union field notebook_source.// Union field environment_spec can be only one of the following:&quot;notebookRuntimeTemplateResourceName&quot;: string,&quot;customEnvironmentSpec&quot;: {object (CustomEnvironmentSpec)}// End of list of possible types for union field environment_spec.// Union field execution_sink can be only one of the following:&quot;gcsOutputUri&quot;: string// End of list of possible types for union field execution_sink.// Union field execution_identity can be only one of the following:&quot;executionUser&quot;: string,&quot;serviceAccount&quot;: string// End of list of possible types for union field execution_identity.// Union field runtime_environment can be only one of the following:&quot;workbenchRuntime&quot;: {object (WorkbenchRuntime)}// End of list of possible types for union field runtime_environment.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. The resource name of this NotebookExecutionJob. Format: `projects/{project_id}/locations/{location}/notebookExecutionJobs/{job_id}`

`displayName`

`string`

The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`executionTimeout`

` string ( Duration  ` format)

Max running time of the execution job in seconds (default 86400s / 24 hrs).

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`scheduleResourceName`

`string`

The Schedule resource name if this job is triggered by one. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`

`jobState`

`enum ( JobState` )

Output only. The state of the NotebookExecutionJob.

`status`

` object ( Status  ` )

Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this NotebookExecutionJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this NotebookExecutionJob was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize NotebookExecutionJobs.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`kernelName`

`string`

The name of the kernel to use during notebook execution. If unset, the default kernel is used.

`encryptionSpec`

` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the `  NotebookRuntimeTemplate  ` has an encryption spec.

Union field `notebook_source` . The input notebook. `notebook_source` can be only one of the following:

`dataformRepositorySource`

` object ( DataformRepositorySource  ` )

The Dataform Repository pointing to a single file notebook repository.

`gcsNotebookSource`

` object ( GcsNotebookSource  ` )

The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`

`directNotebookSource`

` object ( DirectNotebookSource  ` )

The contents of an input notebook file.

Union field `environment_spec` . The compute config to use for an execution job. `environment_spec` can be only one of the following:

`notebookRuntimeTemplateResourceName`

`string`

The NotebookRuntimeTemplate to source compute configuration from.

`customEnvironmentSpec`

` object ( CustomEnvironmentSpec  ` )

The custom compute configuration for an execution job.

Union field `execution_sink` . The location to store the notebook execution result. `execution_sink` can be only one of the following:

`gcsOutputUri`

`string`

The Cloud Storage location to upload the result to. Format: `gs://bucket-name`

Union field `execution_identity` . The identity to run the execution as. `execution_identity` can be only one of the following:

`executionUser`

`string`

The user email to run the execution as. Only supported by Colab runtimes.

`serviceAccount`

`string`

The service account to run the execution as.

Union field `runtime_environment` . Runtime environment for the notebook execution job. If unspecified, the default runtime of Colab is used. `runtime_environment` can be only one of the following:

`workbenchRuntime`

`object ( WorkbenchRuntime` )

The Workbench runtime configuration to use for the notebook execution.

### DataformRepositorySource

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;dataformRepositoryResourceName&quot;: string,
  &quot;commitSha&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataformRepositoryResourceName`

`string`

The resource name of the Dataform Repository. Format: `projects/{project_id}/locations/{location}/repositories/{repository_id}`

`commitSha`

`string`

The commit SHA to read repository with. If unset, the file will be read at HEAD.

### GcsNotebookSource

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;uri&quot;: string,
  &quot;generation&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`uri`

`string`

The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`

`generation`

`string`

The version of the Cloud Storage object to read. If unset, the current version of the object is read. See <https://cloud.google.com/storage/docs/metadata#generation-number> .

### DirectNotebookSource

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;content&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`content`

`string ( bytes format)`

The base64-encoded contents of the input notebook file.

A base64-encoded string.

### CustomEnvironmentSpec

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineSpec&quot;: {object (MachineSpec)},&quot;persistentDiskSpec&quot;: {object (PersistentDiskSpec)},&quot;networkSpec&quot;: {object (NetworkSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`machineSpec`

` object ( MachineSpec  ` )

The specification of a single machine for the execution job.

`persistentDiskSpec`

` object ( PersistentDiskSpec  ` )

The specification of a persistent disk to attach for the execution job.

`networkSpec`

` object ( NetworkSpec  ` )

The network configuration to use for the execution job.

### MachineSpec

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineType&quot;: string,&quot;acceleratorType&quot;: enum (AcceleratorType),&quot;acceleratorCount&quot;: integer,&quot;gpuPartitionSize&quot;: string,&quot;tpuTopology&quot;: string,&quot;reservationAffinity&quot;: {object (ReservationAffinity)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`machineType`

`string`

Immutable. The type of the machine.

See the [list of machine types supported for prediction](https://cloud.google.com/vertex-ai/docs/predictions/configure-compute#machine-types)

See the [list of machine types supported for custom training](https://cloud.google.com/vertex-ai/docs/training/configure-compute#machine-types) .

For `DeployedModel` this field is optional, and the default value is `n1-standard-2` . For `BatchPredictionJob` or as part of `WorkerPoolSpec` this field is required.

`acceleratorType`

`enum ( AcceleratorType` )

Immutable. The type of accelerator(s) that may be attached to the machine as per `accelerator_count` .

`acceleratorCount`

`integer`

The number of accelerators to attach to the machine.

For accelerator optimized machine types ( <https://cloud.google.com/compute/docs/accelerator-optimized-machines> , One may set the accelerator\_count from 1 to N for machine with N GPUs. If accelerator\_count is less than or equal to N / 2, Vertex will co-schedule the replicas of the model into the same VM to save cost.

For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set accelerator\_count to 1 to 8. If accelerator\_count is 1, 2, 3, or 4, Vertex will co-schedule 8, 4, 2, or 2 replicas of the model into the same VM to save cost.

When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM.

Note that the feature is not compatible with \[multihost\_gpu\_node\_count\]\[\]. When multihost\_gpu\_node\_count is set, the co-scheduling will not be enabled.

`gpuPartitionSize`

`string`

Optional. Immutable. The Nvidia GPU partition size.

When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu\_partition\_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances.

The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes.

If set, the accelerator\_count should be set to 1.

`tpuTopology`

`string`

Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu\_topology: "2x2x1").

`reservationAffinity`

` object ( ReservationAffinity  ` )

Optional. Immutable. Configuration controlling how this resource pool consumes reservation.

### ReservationAffinity

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;reservationAffinityType&quot;: enum (Type),&quot;key&quot;: string,&quot;values&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`reservationAffinityType`

`enum ( Type` )

Required. Specifies the reservation affinity type.

`key`

`string`

Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC\_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.

`values[]`

`string`

Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.

### PersistentDiskSpec

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;diskType&quot;: string,
  &quot;diskSizeGb&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`diskType`

`string`

Type of the disk (default is "pd-standard"). Valid values: "pd-ssd" (Persistent Disk Solid State Drive) "pd-standard" (Persistent Disk Hard Disk Drive) "pd-balanced" (Balanced Persistent Disk) "pd-extreme" (Extreme Persistent Disk)

`diskSizeGb`

`string ( int64 format)`

Size in GB of the disk (default is 100GB).

### NetworkSpec

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;enableInternetAccess&quot;: boolean,
  &quot;network&quot;: string,
  &quot;subnetwork&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enableInternetAccess`

`boolean`

Whether to enable public internet access. Default false.

`network`

`string`

The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks)

`subnetwork`

`string`

The name of the subnet that this instance is in. Format: `projects/{project_id_or_number}/regions/{region}/subnetworks/{subnetwork_id}`

### Duration

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years

`nanos`

`integer`

Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive.

### LabelsEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### RunResponse

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;scheduledRunTime&quot;: string,
  &quot;runResponse&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`scheduledRunTime`

` string ( Timestamp  ` format)

The scheduled run time based on the user-specified schedule.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`runResponse`

`string`

The response of the scheduled run.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
