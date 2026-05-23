---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs
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

`statsAnomaliesBaseDirectory` ` object ( GcsDestination  ` )

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

## ModelMonitoringObjectiveConfig

The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.

Fields

`trainingDataset` ` object ( TrainingDataset  ` )

Training dataset for models. This field has to be set only if TrainingPredictionSkewDetectionConfig is specified.

`trainingPredictionSkewDetectionConfig` ` object ( TrainingPredictionSkewDetectionConfig  ` )

The config for skew between training data and prediction data.

`predictionDriftDetectionConfig` ` object ( PredictionDriftDetectionConfig  ` )

The config for drift of prediction data.

`explanationConfig` ` object ( ExplanationConfig  ` )

The config for integrating with Vertex Explainable AI.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trainingDataset&quot;: {object (TrainingDataset)},&quot;trainingPredictionSkewDetectionConfig&quot;: {object (TrainingPredictionSkewDetectionConfig)},&quot;predictionDriftDetectionConfig&quot;: {object (PredictionDriftDetectionConfig)},&quot;explanationConfig&quot;: {object (ExplanationConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## TrainingDataset

Training Dataset information.

Fields

`dataFormat` `string`

data format of the dataset, only applicable if the input is from Google Cloud Storage. The possible formats are:

"tf-record" The source file is a TFRecord file.

"csv" The source file is a CSV file. "jsonl" The source file is a JSONL file.

`targetField` `string`

The target field name the model is to predict. This field will be excluded when doing Predict and (or) Explain for the training data.

`loggingSamplingStrategy` ` object ( SamplingStrategy  ` )

Strategy to sample data from Training Dataset. If not set, we process the whole dataset.

`data_source` `Union type`

`data_source` can be only one of the following:

`dataset` `string`

The resource name of the Dataset used to train this Model.

`gcsSource` ` object ( GcsSource  ` )

The Google Cloud Storage uri of the unmanaged Dataset used to train this Model.

`bigquerySource` ` object ( BigQuerySource  ` )

The BigQuery table of the unmanaged Dataset used to train this Model.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataFormat&quot;: string,&quot;targetField&quot;: string,&quot;loggingSamplingStrategy&quot;: {object (SamplingStrategy)},// data_source&quot;dataset&quot;: string,&quot;gcsSource&quot;: {object (GcsSource)},&quot;bigquerySource&quot;: {object (BigQuerySource)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## SamplingStrategy

Sampling Strategy for logging, can be for both training and prediction dataset.

Fields

`randomSampleConfig` ` object ( RandomSampleConfig  ` )

Random sample config. Will support more sampling strategies later.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;randomSampleConfig&quot;: {object (RandomSampleConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## RandomSampleConfig

Requests are randomly selected.

Fields

`sampleRate` `number`

Sample rate (0, 1\]

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
  &quot;sampleRate&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## TrainingPredictionSkewDetectionConfig

The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

Fields

`skewThresholds` ` map (key: string, value: object ( ThresholdConfig  ` ))

Key is the feature name and value is the threshold. If a feature needs to be monitored for skew, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between the training and prediction feature.

`attributionScoreSkewThresholds` ` map (key: string, value: object ( ThresholdConfig  ` ))

Key is the feature name and value is the threshold. The threshold here is against attribution score distance between the training and prediction feature.

`defaultSkewThreshold` ` object ( ThresholdConfig  ` )

Skew anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;skewThresholds&quot;: {string: {object (ThresholdConfig)},...},&quot;attributionScoreSkewThresholds&quot;: {string: {object (ThresholdConfig)},...},&quot;defaultSkewThreshold&quot;: {object (ThresholdConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## ThresholdConfig

The config for feature monitoring threshold.

Fields

`threshold` `Union type`

`threshold` can be only one of the following:

`value` `number`

Specify a threshold value that can trigger the alert. If this threshold config is for feature distribution distance: 1. For categorical feature, the distribution distance is calculated by L-inifinity norm. 2. For numerical feature, the distribution distance is calculated by Jensen–Shannon divergence. Each feature must have a non-zero threshold if they need to be monitored. Otherwise no alert will be triggered for that feature.

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

  // threshold
  &quot;value&quot;: number
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## PredictionDriftDetectionConfig

The config for Prediction data drift detection.

Fields

`driftThresholds` ` map (key: string, value: object ( ThresholdConfig  ` ))

Key is the feature name and value is the threshold. If a feature needs to be monitored for drift, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between different time windws.

`attributionScoreDriftThresholds` ` map (key: string, value: object ( ThresholdConfig  ` ))

Key is the feature name and value is the threshold. The threshold here is against attribution score distance between different time windows.

`defaultDriftThreshold` ` object ( ThresholdConfig  ` )

Drift anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;driftThresholds&quot;: {string: {object (ThresholdConfig)},...},&quot;attributionScoreDriftThresholds&quot;: {string: {object (ThresholdConfig)},...},&quot;defaultDriftThreshold&quot;: {object (ThresholdConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## ExplanationConfig

The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanationSpec populated.

Fields

`enableFeatureAttributes` `boolean`

If want to analyze the Vertex Explainable AI feature attribute scores or not. If set to true, Agent Platform will log the feature attributions from explain response and do the skew/drift detection for them.

`explanationBaseline` ` object ( ExplanationBaseline  ` )

Predictions generated by the BatchPredictionJob using baseline dataset.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enableFeatureAttributes&quot;: boolean,&quot;explanationBaseline&quot;: {object (ExplanationBaseline)}}</code></pre></td>
</tr>
</tbody>
</table>

## ExplanationBaseline

Output from `  BatchPredictionJob  ` for Model Monitoring baseline dataset, which can be used to generate baseline attribution scores.

Fields

`predictionFormat` ` enum ( PredictionFormat  ` )

The storage format of the predictions generated BatchPrediction job.

`destination` `Union type`

The configuration specifying of BatchExplain job output. This can be used to generate the baseline of feature attribution scores. `destination` can be only one of the following:

`gcs` ` object ( GcsDestination  ` )

Cloud Storage location for BatchExplain output.

`bigquery` ` object ( BigQueryDestination  ` )

BigQuery location for BatchExplain output.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;predictionFormat&quot;: enum (PredictionFormat),// destination&quot;gcs&quot;: {object (GcsDestination)},&quot;bigquery&quot;: {object (BigQueryDestination)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## PredictionFormat

The storage format of the predictions generated BatchPrediction job.

Enums

`PREDICTION_FORMAT_UNSPECIFIED`

Should not be set.

`JSONL`

Predictions are in JSONL files.

`BIGQUERY`

Predictions are in BigQuery.

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

## ModelMonitoringAlertConfig

The alert config for model monitoring.

Fields

`enableLogging` `boolean`

Dump the anomalies to Cloud Logging. The anomalies will be put to json payload encoded from proto `  ModelMonitoringStatsAnomalies  ` . This can be further synced to Pub/Sub or any other services supported by Cloud Logging.

`notificationChannels[]` `string`

Resource names of the NotificationChannels to send alert. Must be of the format `projects/<project_id_or_number>/notificationChannels/<channelId>`

`alert` `Union type`

`alert` can be only one of the following:

`emailAlertConfig` ` object ( EmailAlertConfig  ` )

email alert config.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enableLogging&quot;: boolean,&quot;notificationChannels&quot;: [string],// alert&quot;emailAlertConfig&quot;: {object (EmailAlertConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## EmailAlertConfig

The config for email alert.

Fields

`userEmails[]` `string`

The email addresses to send the alert.

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
  &quot;userEmails&quot;: [
    string
  ]
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
