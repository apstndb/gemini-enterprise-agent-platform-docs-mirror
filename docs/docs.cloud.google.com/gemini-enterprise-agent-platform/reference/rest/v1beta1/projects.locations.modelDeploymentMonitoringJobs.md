---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelDeploymentMonitoringJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelDeploymentMonitoringJobs
title: 'REST Resource: projects.locations.modelDeploymentMonitoringJobs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ModelDeploymentMonitoringJob

Represents a job that runs periodically to monitor the deployed models in an endpoint. It will analyze the logged training & prediction data to detect any abnormal behaviors.

Fields

`name` `string`

Output only. Resource name of a ModelDeploymentMonitoringJob.

`displayName` `string`

Required. The user-defined name of the ModelDeploymentMonitoringJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. Display name of a ModelDeploymentMonitoringJob.

`endpoint` `string`

Required. Endpoint resource name. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

`state` ` enum ( JobState  ` )

Output only. The detailed state of the monitoring job. When the job is still creating, the state will be 'PENDING'. Once the job is successfully created, the state will be 'RUNNING'. Pause the job, the state will be 'PAUSED'. Resume the job, the state will return to 'RUNNING'.

`scheduleState` ` enum ( MonitoringScheduleState  ` )

Output only. Schedule state when the monitoring job is in Running state.

`latestMonitoringPipelineMetadata` ` object ( LatestMonitoringPipelineMetadata  ` )

Output only. Latest triggered monitoring pipeline metadata.

`modelDeploymentMonitoringObjectiveConfigs[]` ` object ( ModelDeploymentMonitoringObjectiveConfig  ` )

Required. The config for monitoring objectives. This is a per DeployedModel config. Each DeployedModel needs to be configured separately.

`modelDeploymentMonitoringScheduleConfig` ` object ( ModelDeploymentMonitoringScheduleConfig  ` )

Required. Schedule config for running the monitoring job.

`loggingSamplingStrategy` ` object ( SamplingStrategy  ` )

Required. Sample Strategy for logging.

`modelMonitoringAlertConfig` ` object ( ModelMonitoringAlertConfig  ` )

Alert config for model monitoring.

`predictInstanceSchemaUri` `string`

YAML schema file uri describing the format of a single instance, which are given to format this Endpoint's prediction (and explanation). If not set, we will generate predict schema from collected predict requests.

`samplePredictInstance` ` value ( Value  ` format)

Sample Predict instance, same format as `  PredictRequest.instances  ` , this can be set as a replacement of `  ModelDeploymentMonitoringJob.predict_instance_schema_uri  ` . If not set, we will generate predict schema from collected predict requests.

`analysisInstanceSchemaUri` `string`

YAML schema file uri describing the format of a single instance that you want Tensorflow data Validation (TFDV) to analyze.

If this field is empty, all the feature data types are inferred from `  predictInstanceSchemaUri  ` , meaning that TFDV will use the data in the exact format(data type) as prediction request/response. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Agent Platform, this field must be set as all the fields in predict instance formatted as string.

`bigqueryTables[]` ` object ( ModelDeploymentMonitoringBigQueryTable  ` )

Output only. The created bigquery tables for the job under customer project. Customer could do their own query & analysis. There could be 4 log tables in maximum: 1. Training data logging predict request/response 2. Serving data logging predict request/response

`logTtl` ` string ( Duration  ` format)

The TTL of BigQuery tables in user projects which stores logs. A day is the basic unit of the TTL and we take the ceil of TTL/86400(a day). e.g. { second: 3600} indicates ttl = 1 day.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your ModelDeploymentMonitoringJob.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ModelDeploymentMonitoringJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ModelDeploymentMonitoringJob was updated most recently.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`nextScheduleTime` ` string ( Timestamp  ` format)

Output only. timestamp when this monitoring pipeline will be scheduled to run for the next round.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`statsAnomaliesBaseDirectory` `object ( GcsDestination` )

Stats anomalies base folder path.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for a ModelDeploymentMonitoringJob. If set, this ModelDeploymentMonitoringJob and all sub-resources of this ModelDeploymentMonitoringJob will be secured by this key.

`enableMonitoringPipelineLogs` `boolean`

If true, the scheduled monitoring pipeline logs are sent to Google Cloud Logging, including pipeline status and anomalies detected. Please note the logs incur cost, which are subject to [Cloud Logging pricing](https://cloud.google.com/logging#pricing) .

`error` ` object ( Status  ` )

Output only. Only populated when the job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;endpoint&quot;: string,&quot;state&quot;: enum (JobState),&quot;scheduleState&quot;: enum (MonitoringScheduleState),&quot;latestMonitoringPipelineMetadata&quot;: {object (LatestMonitoringPipelineMetadata)},&quot;modelDeploymentMonitoringObjectiveConfigs&quot;: [{object (ModelDeploymentMonitoringObjectiveConfig)}],&quot;modelDeploymentMonitoringScheduleConfig&quot;: {object (ModelDeploymentMonitoringScheduleConfig)},&quot;loggingSamplingStrategy&quot;: {object (SamplingStrategy)},&quot;modelMonitoringAlertConfig&quot;: {object (ModelMonitoringAlertConfig)},&quot;predictInstanceSchemaUri&quot;: string,&quot;samplePredictInstance&quot;: value,&quot;analysisInstanceSchemaUri&quot;: string,&quot;bigqueryTables&quot;: [{object (ModelDeploymentMonitoringBigQueryTable)}],&quot;logTtl&quot;: string,&quot;labels&quot;: {string: string,...},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;nextScheduleTime&quot;: string,&quot;statsAnomaliesBaseDirectory&quot;: {object (GcsDestination)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;enableMonitoringPipelineLogs&quot;: boolean,&quot;error&quot;: {object (Status)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## MonitoringScheduleState

The state to Specify the monitoring pipeline.

Enums

`MONITORING_SCHEDULE_STATE_UNSPECIFIED`

Unspecified state.

`PENDING`

The pipeline is picked up and wait to run.

`OFFLINE`

The pipeline is offline and will be scheduled for next run.

`RUNNING`

The pipeline is running.

## LatestMonitoringPipelineMetadata

All metadata of most recent monitoring pipelines.

Fields

`runTime` ` string ( Timestamp  ` format)

The time that most recent monitoring pipelines that is related to this run.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`status` ` object ( Status  ` )

The status of the most recent monitoring pipeline.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;runTime&quot;: string,&quot;status&quot;: {object (Status)}}</code></pre></td>
</tr>
</tbody>
</table>

## ModelDeploymentMonitoringObjectiveConfig

ModelDeploymentMonitoringObjectiveConfig contains the pair of deployedModelId to ModelMonitoringObjectiveConfig.

Fields

`deployedModelId` `string`

The DeployedModel id of the objective config.

`objectiveConfig` ` object ( ModelMonitoringObjectiveConfig  ` )

The objective config of for the modelmonitoring job of this deployed model.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;deployedModelId&quot;: string,&quot;objectiveConfig&quot;: {object (ModelMonitoringObjectiveConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## ModelDeploymentMonitoringScheduleConfig

The config for scheduling monitoring job.

Fields

`monitorInterval` ` string ( Duration  ` format)

Required. The model monitoring job scheduling interval. It will be rounded up to next full hour. This defines how often the monitoring jobs are triggered.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`monitorWindow` ` string ( Duration  ` format)

The time window of the prediction data being included in each prediction dataset. This window specifies how long the data should be collected from historical model results for each run. If not set, `  ModelDeploymentMonitoringScheduleConfig.monitor_interval  ` will be used. e.g. If currently the cutoff time is 2022-01-08 14:30:00 and the monitorWindow is set to be 3600, then data from 2022-01-08 13:30:00 to 2022-01-08 14:30:00 will be retrieved and aggregated to calculate the monitoring statistics.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

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
  &quot;monitorInterval&quot;: string,
  &quot;monitorWindow&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ModelDeploymentMonitoringBigQueryTable

ModelDeploymentMonitoringBigQueryTable specifies the BigQuery table name as well as some information of the logs stored in this table.

Fields

`logSource` ` enum ( LogSource  ` )

The source of log.

`logType` ` enum ( LogType  ` )

The type of log.

`bigqueryTablePath` `string`

The created BigQuery table to store logs. Customer could do their own query & analysis. Format: `bq://<projectId>.model_deployment_monitoring_<endpointId>.<tolower(logSource)>_<tolower(logType)>`

`requestResponseLoggingSchemaVersion` `string`

Output only. The schema version of the request/response logging BigQuery table. Default to v1 if unset.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;logSource&quot;: enum (LogSource),&quot;logType&quot;: enum (LogType),&quot;bigqueryTablePath&quot;: string,&quot;requestResponseLoggingSchemaVersion&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## LogSource

Indicates where does the log come from.

Enums

`LOG_SOURCE_UNSPECIFIED`

Unspecified source.

`TRAINING`

Logs coming from Training dataset.

`SERVING`

Logs coming from Serving traffic.

## LogType

Indicates what type of traffic does the log belong to.

Enums

`LOG_TYPE_UNSPECIFIED`

Unspecified type.

`PREDICT`

Predict logs.

`EXPLAIN`

Explain logs.

## Methods

### `            create           `

Creates a ModelDeploymentMonitoringJob.

### `            delete           `

Deletes a ModelDeploymentMonitoringJob.

### `            get           `

Gets a ModelDeploymentMonitoringJob.

### `            list           `

Lists ModelDeploymentMonitoringJobs in a Location.

### `            patch           `

Updates a ModelDeploymentMonitoringJob.

### `            pause           `

Pauses a ModelDeploymentMonitoringJob.

### `            resume           `

Resumes a paused ModelDeploymentMonitoringJob.

### `            searchModelDeploymentMonitoringStatsAnomalies           `

Searches Model Monitoring Statistics generated within a given time window.
