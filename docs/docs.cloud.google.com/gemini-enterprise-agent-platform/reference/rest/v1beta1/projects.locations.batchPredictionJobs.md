---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs
title: 'REST Resource: projects.locations.batchPredictionJobs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: BatchPredictionJob

A job that uses a [`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.model) to produce predictions on multiple [`input instances`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.input_config) . If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances.

Fields

`name` `string`

Output only. Resource name of the BatchPredictionJob.

`displayName` `string`

Required. The user-defined name of this BatchPredictionJob.

`model` `string`

The name of the Model resource that produces the predictions via this job, must share the same ancestor Location. Starting this job has no impact on any existing deployments of the Model and their resources. Exactly one of model, unmanagedContainerModel, or endpoint must be set.

The model resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2` or `projects/{project}/locations/{location}/models/{model}@golden` if no version is specified, the default version will be deployed.

The model resource could also be a publisher model. Example: `publishers/{publisher}/models/{model}` or `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}`

`modelVersionId` `string`

Output only. The version id of the Model that produces the predictions via this job.

`unmanagedContainerModel` `object ( `[`UnmanagedContainerModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#UnmanagedContainerModel)` )`

Contains model information necessary to perform batch prediction without requiring uploading to model registry. Exactly one of model, unmanagedContainerModel, or endpoint must be set.

`endpoint` `string`

For Bring-Your-Own-Endpoint (BYOE), the name of the Endpoint resource that produces the predictions via this job, must share the same ancestor Location. Exactly one of model, unmanagedContainerModel, or endpoint must be set. Example: `projects/193595526740/locations/us-central1/endpoints/4203439000301600768`

`inputConfig` `object ( `[`InputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InputConfig)` )`

Required. Input configuration of the instances on which predictions are performed. The schema of any single instance may be specified via the [`Model's`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.model) [`PredictSchemata's`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.predict_schemata) [`instanceSchemaUri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata#FIELDS.instance_schema_uri) .

`instanceConfig` `object ( `[`InstanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InstanceConfig)` )`

Configuration for how to convert batch prediction input instances to the prediction instances that are sent to the Model.

`modelParameters` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

The parameters that govern the predictions. The schema of the parameters may be specified via the [`Model's`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.model) [`PredictSchemata's`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.predict_schemata) [`parametersSchemaUri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata#FIELDS.parameters_schema_uri) .

`outputConfig` `object ( `[`OutputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#OutputConfig)` )`

Required. The Configuration specifying where output predictions should be written. The schema of any single prediction may be specified as a concatenation of [`Model's`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.model) [`PredictSchemata's`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.predict_schemata) [`instanceSchemaUri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata#FIELDS.instance_schema_uri) and [`predictionSchemaUri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata#FIELDS.prediction_schema_uri) .

`dedicatedResources` `object ( `[`BatchDedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchDedicatedResources)` )`

The config of resources used by the Model during the batch prediction. If the Model [`supports`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.supported_deployment_resources_types) DEDICATED_RESOURCES this config may be provided (and the job will use these resources), if the Model doesn't support AUTOMATIC_RESOURCES, this config must be provided.

`serviceAccount` `string`

The service account that the DeployedModel's container runs as. If not specified, a system generated one will be used, which has minimal permissions and the custom container, if used, may not have enough permission to access other Google Cloud resources.

Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service account.

`manualBatchTuningParameters` `object ( `[`ManualBatchTuningParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#ManualBatchTuningParameters)` )`

Immutable. Parameters configuring the batch behavior. Currently only applicable when [`dedicatedResources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.dedicated_resources) are used (in other cases Agent Platform does the tuning itself).

`generateExplanation` `boolean`

Generate explanation with the batch prediction results.

When set to `true` , the batch prediction output changes based on the `predictionsFormat` field of the [`BatchPredictionJob.output_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.output_config) object:

- `bigquery` : output includes a column named `explanation` . The value is a struct that conforms to the [`Explanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Explanation) object.
- `jsonl` : The JSON objects on each line include an additional entry keyed `explanation` . The value of the entry is a JSON object that conforms to the [`Explanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Explanation) object.
- `csv` : Generating explanations for CSV format is not supported.

If this field is set to true, either the [`Model.explanation_spec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.explanation_spec) or [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.explanation_spec) must be populated.

`explanationSpec` `object ( `[`ExplanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExplanationSpec)` )`

Explanation configuration for this BatchPredictionJob. Can be specified only if [`generateExplanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.generate_explanation) is set to `true` .

This value overrides the value of [`Model.explanation_spec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.explanation_spec) . All fields of [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.explanation_spec) are optional in the request. If a field of the [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.explanation_spec) object is not populated, the corresponding field of the [`Model.explanation_spec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.explanation_spec) object is inherited.

`outputInfo` `object ( `[`OutputInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#OutputInfo)` )`

Output only. Information further describing the output of this job.

`state` `enum ( `[`JobState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/JobState)` )`

Output only. The detailed state of the job.

`error` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. Only populated when the job's state is JOB_STATE_FAILED or JOB_STATE_CANCELLED.

`partialFailures[]` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. Partial failures encountered. For example, single files that can't be read. This field never exceeds 20 entries. status details fields contain standard Google Cloud error details.

`resourcesConsumed` `object ( `[`ResourcesConsumed`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#ResourcesConsumed)` )`

Output only. Information about resources that had been consumed by this job. Provided in real time at best effort basis, as well as a final value once the job completes.

Note: This field currently may be not populated for batch predictions that use AutoML Models.

`completionStats` `object ( `[`CompletionStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#CompletionStats)` )`

Output only. Statistics on completed and failed prediction instances.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the BatchPredictionJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the BatchPredictionJob for the first time entered the `JOB_STATE_RUNNING` state.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the BatchPredictionJob entered any of the following states: `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the BatchPredictionJob was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize BatchPredictionJobs.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/EncryptionSpec)` )`

Customer-managed encryption key options for a BatchPredictionJob. If this is set, then all resources created by the BatchPredictionJob will be encrypted with the provided encryption key.

`modelMonitoringConfig` `object ( `[`ModelMonitoringConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#ModelMonitoringConfig)` )`

Model monitoring config will be used for analysis model behaviors, based on the input and output to the batch prediction job, as well as the provided training dataset.

`modelMonitoringStatsAnomalies[]` `object ( `[`ModelMonitoringStatsAnomalies`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#ModelMonitoringStatsAnomalies)` )`

Get batch prediction job monitoring statistics.

`modelMonitoringStatus` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. The running status of the model monitoring pipeline.

`disableContainerLogging` `boolean`

For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by default. Please note that the logs incur cost, which are subject to [Cloud Logging pricing](https://cloud.google.com/logging/pricing) .

user can disable container logging by setting this flag to true.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "model": string,
  "modelVersionId": string,
  "unmanagedContainerModel": {
    object (UnmanagedContainerModel)
  },
  "endpoint": string,
  "inputConfig": {
    object (InputConfig)
  },
  "instanceConfig": {
    object (InstanceConfig)
  },
  "modelParameters": value,
  "outputConfig": {
    object (OutputConfig)
  },
  "dedicatedResources": {
    object (BatchDedicatedResources)
  },
  "serviceAccount": string,
  "manualBatchTuningParameters": {
    object (ManualBatchTuningParameters)
  },
  "generateExplanation": boolean,
  "explanationSpec": {
    object (ExplanationSpec)
  },
  "outputInfo": {
    object (OutputInfo)
  },
  "state": enum (JobState),
  "error": {
    object (Status)
  },
  "partialFailures": [
    {
      object (Status)
    }
  ],
  "resourcesConsumed": {
    object (ResourcesConsumed)
  },
  "completionStats": {
    object (CompletionStats)
  },
  "createTime": string,
  "startTime": string,
  "endTime": string,
  "updateTime": string,
  "labels": {
    string: string,
    ...
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "modelMonitoringConfig": {
    object (ModelMonitoringConfig)
  },
  "modelMonitoringStatsAnomalies": [
    {
      object (ModelMonitoringStatsAnomalies)
    }
  ],
  "modelMonitoringStatus": {
    object (Status)
  },
  "disableContainerLogging": boolean,
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean
}
```

## UnmanagedContainerModel

Contains model information necessary to perform batch prediction without requiring a full model import.

Fields

`artifactUri` `string`

The path to the directory containing the Model artifact and any of its supporting files.

`predictSchemata` `object ( `[`PredictSchemata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata)` )`

Contains the schemata used in Model's predictions and explanations

`containerSpec` `object ( `[`ModelContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelContainerSpec)` )`

Input only. The specification of the container that is to be used when deploying this Model.

**JSON representation**

```
{
  "artifactUri": string,
  "predictSchemata": {
    object (PredictSchemata)
  },
  "containerSpec": {
    object (ModelContainerSpec)
  }
}
```

## InputConfig

Configures the input to [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob) . See [`Model.supported_input_storage_formats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.supported_input_storage_formats) for Model's supported input formats, and how instances should be expressed via any of them.

Fields

`instancesFormat` `string`

Required. The format in which instances are given, must be one of the [`Model's`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.model) [`supportedInputStorageFormats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.supported_input_storage_formats) .

`source` `Union type`

Required. The source of the input. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsSource` `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GcsSource)` )`

The Cloud Storage location for the input instances.

`bigquerySource` `object ( `[`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQuerySource)` )`

The BigQuery location of the input table. The schema of the table should be in the format described by the given context OpenAPI Schema, if one is provided. The table may contain additional columns that are not described by the schema, and they will be ignored.

`vertexMultimodalDatasetSource` `object ( `[`VertexMultimodalDatasetSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#VertexMultimodalDatasetSource)` )`

A Vertex Managed Dataset. Currently, only datasets of type Multimodal are supported.

End of mutually exclusive fields.

**JSON representation**

```
{
  "instancesFormat": string,

  // source
  "gcsSource": {
    object (GcsSource)
  },
  "bigquerySource": {
    object (BigQuerySource)
  },
  "vertexMultimodalDatasetSource": {
    object (VertexMultimodalDatasetSource)
  }
  // Union type
}
```

## VertexMultimodalDatasetSource

The Vertex Multimodal Dataset for the input content.

Fields

`datasetName` `string`

Required. The resource name of the Vertex Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

**JSON representation**

```
{
  "datasetName": string
}
```

## InstanceConfig

Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

Fields

`instanceType` `string`

The format of the instance that the Model accepts. Agent Platform will convert compatible [`batch prediction input instance formats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InputConfig.FIELDS.instances_format) to the specified format.

Supported values are:

- `object` : Each input is converted to JSON object format.

  - For `bigquery` , each row is converted to an object.
  - For `jsonl` , each line of the JSONL input must be an object.
  - Does not apply to `csv` , `file-list` , `tf-record` , or `tf-record-gzip` .

- `array` : Each input is converted to JSON array format.

  - For `bigquery` , each row is converted to an array. The order of columns is determined by the BigQuery column order, unless [`includedFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InstanceConfig.FIELDS.included_fields) is populated. [`includedFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InstanceConfig.FIELDS.included_fields) must be populated for specifying field orders.
  - For `jsonl` , if each line of the JSONL input is an object, [`includedFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InstanceConfig.FIELDS.included_fields) must be populated for specifying field orders.
  - Does not apply to `csv` , `file-list` , `tf-record` , or `tf-record-gzip` .

If not specified, Agent Platform converts the batch prediction input as follows:

- For `bigquery` and `csv` , the behavior is the same as `array` . The order of columns is the same as defined in the file or table, unless [`includedFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InstanceConfig.FIELDS.included_fields) is populated.
- For `jsonl` , the prediction instance format is determined by each line of the input.
- For `tf-record` / `tf-record-gzip` , each record will be converted to an object in the format of `{"b64": <value>}` , where `<value>` is the Base64-encoded string of the content of the record.
- For `file-list` , each file in the list will be converted to an object in the format of `{"b64": <value>}` , where `<value>` is the Base64-encoded string of the content of the file.

`keyField` `string`

The name of the field that is considered as a key.

The values identified by the key field is not included in the transformed instances that is sent to the Model. This is similar to specifying this name of the field in [`excludedFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InstanceConfig.FIELDS.excluded_fields) . In addition, the batch prediction output will not include the instances. Instead the output will only include the value of the key field, in a field named `key` in the output:

- For `jsonl` output format, the output will have a `key` field instead of the `instance` field.
- For `csv` / `bigquery` output format, the output will have have a `key` column instead of the instance feature columns.

The input must be JSONL with objects at each line, CSV, BigQuery or TfRecord.

`includedFields[]` `string`

Fields that will be included in the prediction instance that is sent to the Model.

If [`instanceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InstanceConfig.FIELDS.instance_type) is `array` , the order of field names in includedFields also determines the order of the values in the array.

When includedFields is populated, [`excludedFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InstanceConfig.FIELDS.excluded_fields) must be empty.

The input must be JSONL with objects at each line, BigQuery or TfRecord.

`excludedFields[]` `string`

Fields that will be excluded in the prediction instance that is sent to the Model.

Excluded will be attached to the batch prediction output if [`keyField`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InstanceConfig.FIELDS.key_field) is not specified.

When excludedFields is populated, [`includedFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#InstanceConfig.FIELDS.included_fields) must be empty.

The input must be JSONL with objects at each line, BigQuery or TfRecord.

**JSON representation**

```
{
  "instanceType": string,
  "keyField": string,
  "includedFields": [
    string
  ],
  "excludedFields": [
    string
  ]
}
```

## OutputConfig

Configures the output of [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob) . See [`Model.supported_output_storage_formats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.supported_output_storage_formats) for supported output formats, and how predictions are expressed via any of them.

Fields

`predictionsFormat` `string`

Required. The format in which Agent Platform gives the predictions, must be one of the [`Model's`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.model) [`supportedOutputStorageFormats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.supported_output_storage_formats) .

`destination` `Union type`

Required. The destination of the output. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsDestination` `object ( ``GcsDestination`` )`

The Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is `prediction-<model-display-name>-<job-create-time>` , where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601 format. Inside of it files `predictions_0001.<extension>` , `predictions_0002.<extension>` , ..., `predictions_N.<extension>` are created where `<extension>` depends on chosen [`predictionsFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#OutputConfig.FIELDS.predictions_format) , and N may equal 0001 and depends on the total number of successfully predicted instances. If the Model has both [`instance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata#FIELDS.instance_schema_uri) and [`prediction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata#FIELDS.parameters_schema_uri) schemata defined then each such file contains predictions as per the [`predictionsFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#OutputConfig.FIELDS.predictions_format) . If prediction for any instance failed (partially or completely), then an additional `errors_0001.<extension>` , `errors_0002.<extension>` ,..., `errors_N.<extension>` files are created (N depends on total number of failed predictions). These files contain the failed instances, as per their schema, followed by an additional `error` field which as value has [`google.rpc.Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status) containing only `code` and `message` fields.

`bigqueryDestination` `object ( `[`BigQueryDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQueryDestination)` )`

The BigQuery project or dataset location where the output is to be written to. If project is provided, a new dataset is created with name `prediction_<model-display-name>_<job-create-time>` where is made BigQuery-dataset-name compatible (for example, most special characters become underscores), and timestamp is in YYYY_MM_DDThh_mm_ss_sssZ "based on ISO-8601" format. In the dataset two tables will be created, `predictions` , and `errors` . If the Model has both [`instance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata#FIELDS.instance_schema_uri) and [`prediction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata#FIELDS.parameters_schema_uri) schemata defined then the tables have columns as follows: The `predictions` table contains instances for which the prediction succeeded, it has columns as per a concatenation of the Model's instance and prediction schemata. The `errors` table contains rows for which the prediction has failed, it has instance columns, as per the instance schema, followed by a single "errors" column, which as values has [`google.rpc.Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status) represented as a STRUCT, and containing only `code` and `message` .

`vertexMultimodalDatasetDestination` `object ( `[`VertexMultimodalDatasetDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#VertexMultimodalDatasetDestination)` )`

The details for a Vertex Multimodal Dataset that will be created for the output.

End of mutually exclusive fields.

**JSON representation**

```
{
  "predictionsFormat": string,

  // destination
  "gcsDestination": {
    object (GcsDestination)
  },
  "bigqueryDestination": {
    object (BigQueryDestination)
  },
  "vertexMultimodalDatasetDestination": {
    object (VertexMultimodalDatasetDestination)
  }
  // Union type
}
```

## VertexMultimodalDatasetDestination

The details for a Vertex Multimodal Dataset output.

Fields

`bigqueryDestination` `object ( `[`BigQueryDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQueryDestination)` )`

Optional. The destination of the underlying BigQuery table that will be created for the output Multimodal Dataset. If not specified, the BigQuery table will be created in a default BigQuery dataset.

`displayName` `string`

Optional. Display name of the output dataset.

**JSON representation**

```
{
  "bigqueryDestination": {
    object (BigQueryDestination)
  },
  "displayName": string
}
```

## ManualBatchTuningParameters

Manual batch tuning parameters.

Fields

`batchSize` `integer`

Immutable. The number of the records (e.g. instances) of the operation given in each batch to a machine replica. Machine type, and size of a single record should be considered when setting this parameter, higher value speeds up the batch operation's execution, but too high value will result in a whole batch not fitting in a machine's memory, and the whole operation will fail. The default value is 64.

**JSON representation**

```
{
  "batchSize": integer
}
```

## OutputInfo

Further describes this job's output. Supplements [`outputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.output_config) .

Fields

`bigqueryOutputTable` `string`

Output only. The name of the BigQuery table created, in `predictions_<timestamp>` format, into which the prediction output is written. Can be used by UI to generate the BigQuery output path, for example.

`output_location` `Union type`

The output location into which prediction output is written. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsOutputDirectory` `string`

Output only. The full path of the Cloud Storage directory created, into which the prediction output is written.

`bigqueryOutputDataset` `string`

Output only. The path of the BigQuery dataset created, in `bq://projectId.bqDatasetId` format, into which the prediction output is written.

`vertexMultimodalDatasetName` `string`

Output only. The resource name of the Vertex Managed Dataset created, into which the prediction output is written. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

End of mutually exclusive fields.

**JSON representation**

```
{
  "bigqueryOutputTable": string,

  // output_location
  "gcsOutputDirectory": string,
  "bigqueryOutputDataset": string,
  "vertexMultimodalDatasetName": string
  // Union type
}
```

## ResourcesConsumed

Statistics information about resource consumption.

Fields

`replicaHours` `number`

Output only. The number of replica hours used. Note that many replicas may run in parallel, and additionally any given work may be queued for some time. Therefore this value is not strictly related to wall time.

**JSON representation**

```
{
  "replicaHours": number
}
```

## CompletionStats

Success and error statistics of processing multiple entities (for example, DataItems or structured data rows) in batch.

Fields

`successfulCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The number of entities that had been processed successfully.

`failedCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The number of entities for which any error was encountered.

`incompleteCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. In cases when enough errors are encountered a job, pipeline, or operation may be failed as a whole. Below is the number of entities for which the processing had not been finished (either in successful or failed state). Set to -1 if the number is unknown (for example, the operation failed before the total entity number could be collected).

`successfulForecastPointCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The number of the successful forecast points that are generated by the forecasting model. This is ONLY used by the forecasting batch prediction.

**JSON representation**

```
{
  "successfulCount": string,
  "failedCount": string,
  "incompleteCount": string,
  "successfulForecastPointCount": string
}
```

## ModelMonitoringConfig

The model monitoring configuration used for Batch Prediction Job.

Fields

`objectiveConfigs[]` `object ( `[`ModelMonitoringObjectiveConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringObjectiveConfig)` )`

Model monitoring objective config.

`alertConfig` `object ( `[`ModelMonitoringAlertConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringAlertConfig)` )`

Model monitoring alert config.

`analysisInstanceSchemaUri` `string`

YAML schema file uri in Cloud Storage describing the format of a single instance that you want Tensorflow data Validation (TFDV) to analyze.

If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Agent Platform, this field must be set as all the fields in predict instance formatted as string.

`statsAnomaliesBaseDirectory` `object ( ``GcsDestination`` )`

A Google Cloud Storage location for batch prediction model monitoring to dump statistics and anomalies. If not provided, a folder will be created in customer project to hold statistics and anomalies.

**JSON representation**

```
{
  "objectiveConfigs": [
    {
      object (ModelMonitoringObjectiveConfig)
    }
  ],
  "alertConfig": {
    object (ModelMonitoringAlertConfig)
  },
  "analysisInstanceSchemaUri": string,
  "statsAnomaliesBaseDirectory": {
    object (GcsDestination)
  }
}
```

## ModelMonitoringStatsAnomalies

Statistics and anomalies generated by Model Monitoring.

Fields

`objective` `enum ( `[`ModelDeploymentMonitoringObjectiveType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#ModelDeploymentMonitoringObjectiveType)` )`

Model Monitoring Objective those stats and anomalies belonging to.

`deployedModelId` `string`

Deployed Model id.

`anomalyCount` `integer`

Number of anomalies within all stats.

`featureStats[]` `object ( `[`FeatureHistoricStatsAnomalies`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs#FeatureHistoricStatsAnomalies)` )`

A list of historical Stats and Anomalies generated for all Features.

**JSON representation**

```
{
  "objective": enum (ModelDeploymentMonitoringObjectiveType),
  "deployedModelId": string,
  "anomalyCount": integer,
  "featureStats": [
    {
      object (FeatureHistoricStatsAnomalies)
    }
  ]
}
```

## ModelDeploymentMonitoringObjectiveType

The Model Monitoring Objective types.

| Enums                                                    |                                                                                                                |
|----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| `MODEL_DEPLOYMENT_MONITORING_OBJECTIVE_TYPE_UNSPECIFIED` | Default value, should not be set.                                                                              |
| `RAW_FEATURE_SKEW`                                       | Raw feature values' stats to detect skew between Training-Prediction datasets.                                 |
| `RAW_FEATURE_DRIFT`                                      | Raw feature values' stats to detect drift between Serving-Prediction datasets.                                 |
| `FEATURE_ATTRIBUTION_SKEW`                               | feature attribution scores to detect skew between Training-Prediction datasets.                                |
| `FEATURE_ATTRIBUTION_DRIFT`                              | feature attribution scores to detect skew between Prediction datasets collected within different time windows. |

## FeatureHistoricStatsAnomalies

Historical Stats (and Anomalies) for a specific feature.

Fields

`featureDisplayName` `string`

Display name of the feature.

`threshold` `object ( `[`ThresholdConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ThresholdConfig)` )`

Threshold for anomaly detection.

`trainingStats` `object ( `[`FeatureStatsAnomaly`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureStatsAnomaly)` )`

Stats calculated for the Training Dataset.

`predictionStats[]` `object ( `[`FeatureStatsAnomaly`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureStatsAnomaly)` )`

A list of historical stats generated by different time window's Prediction Dataset.

**JSON representation**

```
{
  "featureDisplayName": string,
  "threshold": {
    object (ThresholdConfig)
  },
  "trainingStats": {
    object (FeatureStatsAnomaly)
  },
  "predictionStats": [
    {
      object (FeatureStatsAnomaly)
    }
  ]
}
```

| Methods                                                                                                                                         |                                          |
|-------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------|
| [`cancel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs/cancel) | Cancels a BatchPredictionJob.            |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs/create) | Creates a BatchPredictionJob.            |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs/delete) | Deletes a BatchPredictionJob.            |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs/get)       | Gets a BatchPredictionJob                |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs/list)     | Lists BatchPredictionJobs in a Location. |
