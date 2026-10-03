---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models
title: 'REST Resource: projects.locations.models'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Model

A trained machine learning Model.

Fields

`name` `string`

Identifier. The resource name of the Model.

`versionId` `string`

Output only. Immutable. The version id of the model. A new version is committed when a new model version is uploaded or trained under an existing model id. It is an auto-incrementing decimal number in string representation.

`versionAliases[]` `string`

user provided version aliases so that a model version can be referenced via alias (i.e. `projects/{project}/locations/{location}/models/{modelId}@{version_alias}` instead of auto-generated version id (i.e. `projects/{project}/locations/{location}/models/{modelId}@{versionId})` . The format is \[a-z\]\[a-zA-Z0-9-\]{0,126}\[a-z0-9\] to distinguish from versionId. A default version alias will be created for the first version of the model, and there must be exactly one default version alias for a model.

`versionCreateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this version was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`versionUpdateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this version was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`displayName` `string`

Required. The display name of the Model. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

The description of the Model.

`versionDescription` `string`

The description of this version.

`defaultCheckpointId` `string`

The default checkpoint id of a model version.

`predictSchemata` `object ( `[`PredictSchemata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PredictSchemata)` )`

The schemata that describe formats of the Model's predictions and explanations as given and returned via [`PredictionService.Predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict#google.cloud.aiplatform.v1.PredictionService.Predict) and [`PredictionService.Explain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain#google.cloud.aiplatform.v1.PredictionService.Explain) .

`metadataSchemaUri` `string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Model, that is specific to it. Unset if the Model does not have any additional information. The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform, if no additional metadata is needed, this field is set to an empty string. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`metadata` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Immutable. An additional information about the Model; the schema of the metadata can be found in [`metadataSchema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.metadata_schema_uri) . Unset if the Model does not have any additional information.

`supportedExportFormats[]` `object ( `[`ExportFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ExportFormat)` )`

Output only. The formats in which this Model may be exported. If empty, this Model is not available for export.

`trainingPipeline` `string`

Output only. The resource name of the TrainingPipeline that uploaded this Model, if any.

`pipelineJob` `string`

Optional. This field is populated if the model is produced by a pipeline job.

`containerSpec` `object ( `[`ModelContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelContainerSpec)` )`

The specification of the container that is to be used when deploying this Model. The specification is ingested upon [`ModelService.UploadModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/upload#google.cloud.aiplatform.v1.ModelService.UploadModel) , and all binaries it contains are copied and stored internally by Agent Platform. Not required for AutoML Models.

`artifactUri` `string`

Immutable. The path to the directory containing the Model artifact and any of its supporting files. Not required for AutoML Models.

`supportedDeploymentResourcesTypes[]` `enum ( `[`DeploymentResourcesType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.DeploymentResourcesType)` )`

Output only. When this Model is deployed, its prediction resources are described by the `prediction_resources` field of the [`Endpoint.deployed_models`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint.FIELDS.deployed_models) object. Because not all Models support all resource configuration types, the configuration types this Model supports are listed here. If no configuration types are listed, the Model cannot be deployed to an [`Endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint) and does not support online predictions ( [`PredictionService.Predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict#google.cloud.aiplatform.v1.PredictionService.Predict) or [`PredictionService.Explain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain#google.cloud.aiplatform.v1.PredictionService.Explain) ). Such a Model can serve predictions by using a [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob) , if it has at least one entry each in [`supportedInputStorageFormats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.supported_input_storage_formats) and [`supportedOutputStorageFormats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.supported_output_storage_formats) .

`supportedInputStorageFormats[]` `string`

Output only. The formats this Model supports in [`BatchPredictionJob.input_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.input_config) . If [`PredictSchemata.instance_schema_uri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PredictSchemata#FIELDS.instance_schema_uri) exists, the instances should be given as per that schema.

The possible formats are:

- `jsonl` The JSON Lines format, where each instance is a single line. uses [`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#InputConfig.FIELDS.gcs_source) .

- `csv` The CSV format, where each instance is a single comma-separated line. The first line in the file is the header, containing comma-separated field names. uses [`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#InputConfig.FIELDS.gcs_source) .

- `tf-record` The TFRecord format, where each instance is a single record in tfrecord syntax. uses [`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#InputConfig.FIELDS.gcs_source) .

- `tf-record-gzip` Similar to `tf-record` , but the file is gzipped. uses [`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#InputConfig.FIELDS.gcs_source) .

- `bigquery` Each instance is a single row in BigQuery. uses [`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#InputConfig.FIELDS.bigquery_source) .

- `file-list` Each line of the file is the location of an instance to process, uses `gcsSource` field of the [`InputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#InputConfig) object.

If this Model doesn't support any of these formats it means it cannot be used with a [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob) . However, if it has [`supportedDeploymentResourcesTypes`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.supported_deployment_resources_types) , it could serve online predictions by using [`PredictionService.Predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict#google.cloud.aiplatform.v1.PredictionService.Predict) or [`PredictionService.Explain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain#google.cloud.aiplatform.v1.PredictionService.Explain) .

`supportedOutputStorageFormats[]` `string`

Output only. The formats this Model supports in [`BatchPredictionJob.output_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.output_config) . If both [`PredictSchemata.instance_schema_uri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PredictSchemata#FIELDS.instance_schema_uri) and [`PredictSchemata.prediction_schema_uri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PredictSchemata#FIELDS.prediction_schema_uri) exist, the predictions are returned together with their instances. In other words, the prediction has the original instance data first, followed by the actual prediction content (as per the schema).

The possible formats are:

- `jsonl` The JSON Lines format, where each prediction is a single line. uses [`GcsDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#OutputConfig.FIELDS.gcs_destination) .

- `csv` The CSV format, where each prediction is a single comma-separated line. The first line in the file is the header, containing comma-separated field names. uses [`GcsDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#OutputConfig.FIELDS.gcs_destination) .

- `bigquery` Each prediction is a single row in a BigQuery table, uses [`BigQueryDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#OutputConfig.FIELDS.bigquery_destination) .

If this Model doesn't support any of these formats it means it cannot be used with a [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob) . However, if it has [`supportedDeploymentResourcesTypes`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.FIELDS.supported_deployment_resources_types) , it could serve online predictions by using [`PredictionService.Predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict#google.cloud.aiplatform.v1.PredictionService.Predict) or [`PredictionService.Explain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain#google.cloud.aiplatform.v1.PredictionService.Explain) .

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Model was uploaded into Agent Platform.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Model was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`deployedModels[]` `object ( `[`DeployedModelRef`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.DeployedModelRef)` )`

Output only. The pointers to DeployedModels created from this Model. Note that Model could have been deployed to endpoints in different Locations.

`explanationSpec` `object ( `[`ExplanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExplanationSpec)` )`

The default explanation specification for this Model.

The Model can be used for [`requesting explanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain#google.cloud.aiplatform.v1.PredictionService.Explain) after being [`deployed`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel#google.cloud.aiplatform.v1.EndpointService.DeployModel) if it is populated. The Model can be used for [`batch explanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.generate_explanation) if it is populated.

All fields of the explanationSpec can be overridden by [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel.FIELDS.explanation_spec) of [`DeployModelRequest.deployed_model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel#body.request_body.FIELDS.deployed_model) , or [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.explanation_spec) of [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob) .

If the default explanation specification is not set for this Model, this Model can still be used for [`requesting explanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/explain#google.cloud.aiplatform.v1.PredictionService.Explain) by setting [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel.FIELDS.explanation_spec) of [`DeployModelRequest.deployed_model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/deployModel#body.request_body.FIELDS.deployed_model) and for [`batch explanation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.generate_explanation) by setting [`explanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.explanation_spec) of [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob) .

`etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your Models.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`dataStats` `object ( `[`DataStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.DataStats)` )`

Stats of data used for training or evaluating the Model.

Only populated when the Model is trained by a TrainingPipeline with [`data_input_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#TrainingPipeline.FIELDS.input_data_config) .

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec)` )`

Customer-managed encryption key spec for a Model. If set, this Model and all sub-resources of this Model will be secured by this key.

`modelSourceInfo` `object ( `[`ModelSourceInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelSourceInfo)` )`

Output only. Source of a model. It can either be automl training pipeline, custom training pipeline, BigQuery ML, or saved and tuned from Genie or Model Garden.

`originalModelInfo` `object ( `[`OriginalModelInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.OriginalModelInfo)` )`

Output only. If this Model is a copy of another Model, this contains info about the original.

`metadataArtifact` `string`

Output only. The resource name of the Artifact that was created in MetadataStore when creating the Model. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadataStore}/artifacts/{artifact}` .

`baseModelSource` `object ( `[`BaseModelSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.BaseModelSource)` )`

Optional. user input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

`checkpoints[]` `object ( `[`Checkpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.Checkpoint)` )`

Optional. Output only. The checkpoints of the model.

**JSON representation**

```
{
  "name": string,
  "versionId": string,
  "versionAliases": [
    string
  ],
  "versionCreateTime": string,
  "versionUpdateTime": string,
  "displayName": string,
  "description": string,
  "versionDescription": string,
  "defaultCheckpointId": string,
  "predictSchemata": {
    object (PredictSchemata)
  },
  "metadataSchemaUri": string,
  "metadata": value,
  "supportedExportFormats": [
    {
      object (ExportFormat)
    }
  ],
  "trainingPipeline": string,
  "pipelineJob": string,
  "containerSpec": {
    object (ModelContainerSpec)
  },
  "artifactUri": string,
  "supportedDeploymentResourcesTypes": [
    enum (DeploymentResourcesType)
  ],
  "supportedInputStorageFormats": [
    string
  ],
  "supportedOutputStorageFormats": [
    string
  ],
  "createTime": string,
  "updateTime": string,
  "deployedModels": [
    {
      object (DeployedModelRef)
    }
  ],
  "explanationSpec": {
    object (ExplanationSpec)
  },
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "dataStats": {
    object (DataStats)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "modelSourceInfo": {
    object (ModelSourceInfo)
  },
  "originalModelInfo": {
    object (OriginalModelInfo)
  },
  "metadataArtifact": string,
  "baseModelSource": {
    object (BaseModelSource)
  },
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean,
  "checkpoints": [
    {
      object (Checkpoint)
    }
  ]
}
```

### ExportFormat

Represents export format supported by the Model. All formats export to Google Cloud Storage.

Fields

`id` `string`

Output only. The id of the export format. The possible format IDs are:

- `tflite` Used for Android mobile devices.

- `edgetpu-tflite` Used for [Edge TPU](https://cloud.google.com/edge-tpu/) devices.

- `tf-saved-model` A tensorflow model in SavedModel format.

- `tf-js` A [TensorFlow.js](https://www.tensorflow.org/js) model that can be used in the browser and in Node.js using JavaScript.

- `core-ml` Used for iOS mobile devices.

- `custom-trained` A Model that was uploaded or trained by custom code.

- `genie` A tuned Model Garden model.

`exportableContents[]` `enum ( `[`ExportableContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ExportableContent)` )`

Output only. The content of this Model that may be exported.

**JSON representation**

```
{
  "id": string,
  "exportableContents": [
    enum (ExportableContent)
  ]
}
```

### ExportableContent

The Model content that can be exported.

| Enums                            |                                                                                                                                                                                                                                                                                                                                                            |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `EXPORTABLE_CONTENT_UNSPECIFIED` | Should not be used.                                                                                                                                                                                                                                                                                                                                        |
| `ARTIFACT`                       | Model artifact and any of its supported files. Will be exported to the location specified by the `artifactDestination` field of the [`ExportModelRequest.output_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/export#body.request_body.FIELDS.output_config) object.                 |
| `IMAGE`                          | The container image that is to be used when deploying this Model. Will be exported to the location specified by the `imageDestination` field of the [`ExportModelRequest.output_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/export#body.request_body.FIELDS.output_config) object. |

### DeploymentResourcesType

Identifies a type of Model's prediction resources.

| Enums                                   |                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `DEPLOYMENT_RESOURCES_TYPE_UNSPECIFIED` | Should not be used.                                                                                                                                                                                                                                                                                                                                                                                     |
| `DEDICATED_RESOURCES`                   | Resources that are dedicated to the [`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel) , and that need a higher degree of manual configuration.                                                                                                                                                             |
| `AUTOMATIC_RESOURCES`                   | Resources that to large degree are decided by Agent Platform, and require only a modest additional configuration.                                                                                                                                                                                                                                                                                       |
| `SHARED_RESOURCES`                      | Resources that can be shared by multiple [`DeployedModels`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel) . A pre-configured [`DeploymentResourcePool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.deploymentResourcePools#DeploymentResourcePool) is required. |

### DeployedModelRef

Points to a DeployedModel.

Fields

`endpoint` `string`

Immutable. A resource name of an Endpoint.

`deployedModelId` `string`

Immutable. An id of a DeployedModel in the above Endpoint.

`checkpointId` `string`

Immutable. The id of the Checkpoint deployed in the DeployedModel.

**JSON representation**

```
{
  "endpoint": string,
  "deployedModelId": string,
  "checkpointId": string
}
```

### DataStats

Stats of data used for train or evaluate the Model.

Fields

`trainingDataItemsCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of DataItems that were used for training this Model.

`validationDataItemsCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of DataItems that were used for validating this Model during training.

`testDataItemsCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of DataItems that were used for evaluating this Model. If the Model is evaluated multiple times, this will be the number of test DataItems used by the first evaluation. If the Model is not evaluated, the number is 0.

`trainingAnnotationsCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of Annotations that are used for training this Model.

`validationAnnotationsCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of Annotations that are used for validating this Model during training.

`testAnnotationsCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of Annotations that are used for evaluating this Model. If the Model is evaluated multiple times, this will be the number of test Annotations used by the first evaluation. If the Model is not evaluated, the number is 0.

**JSON representation**

```
{
  "trainingDataItemsCount": string,
  "validationDataItemsCount": string,
  "testDataItemsCount": string,
  "trainingAnnotationsCount": string,
  "validationAnnotationsCount": string,
  "testAnnotationsCount": string
}
```

### ModelSourceInfo

Detail description of the source information of the model.

Fields

`sourceType` `enum ( `[`ModelSourceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelSourceType)` )`

type of the model source.

`copy` `boolean`

If this Model is copy of another Model. If true then [`sourceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelSourceInfo.FIELDS.source_type) pertains to the original.

**JSON representation**

```
{
  "sourceType": enum (ModelSourceType),
  "copy": boolean
}
```

### ModelSourceType

Source of the model. Different from `objective` field, this `ModelSourceType` enum indicates the source from which the model was accessed or obtained, whereas the `objective` indicates the overall aim or function of this model.

| Enums                           |                                                              |
|---------------------------------|--------------------------------------------------------------|
| `MODEL_SOURCE_TYPE_UNSPECIFIED` | Should not be used.                                          |
| `AUTOML`                        | The Model is uploaded by automl training pipeline.           |
| `CUSTOM`                        | The Model is uploaded by user or custom training pipeline.   |
| `BQML`                          | The Model is registered and sync'ed from BigQuery ML.        |
| `MODEL_GARDEN`                  | The Model is saved or tuned from Model Garden.               |
| `GENIE`                         | The Model is saved or tuned from Genie.                      |
| `CUSTOM_TEXT_EMBEDDING`         | The Model is uploaded by text embedding finetuning pipeline. |
| `MARKETPLACE`                   | The Model is saved or tuned from Marketplace.                |

### OriginalModelInfo

Contains information about the original Model if this Model is a copy.

Fields

`model` `string`

Output only. The resource name of the Model this Model is a copy of, including the revision. Format: `projects/{project}/locations/{location}/models/{modelId}@{versionId}`

**JSON representation**

```
{
  "model": string
}
```

### BaseModelSource

user input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

Fields

`source` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`modelGardenSource` `object ( `[`ModelGardenSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.ModelGardenSource)` )`

Source information of Model Garden models.

`genieSource` `object ( `[`GenieSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.GenieSource)` )`

Information about the base model of Genie models.

End of mutually exclusive fields.

**JSON representation**

```
{

  // source
  "modelGardenSource": {
    object (ModelGardenSource)
  },
  "genieSource": {
    object (GenieSource)
  }
  // Union type
}
```

### ModelGardenSource

Contains information about the source of the models generated from Model Garden.

Fields

`publicModelName` `string`

Required. The model garden source model resource name.

`versionId` `string`

Optional. The model garden source model version id.

`skipHfModelCache` `boolean`

Optional. Whether to avoid pulling the model from the HF cache.

**JSON representation**

```
{
  "publicModelName": string,
  "versionId": string,
  "skipHfModelCache": boolean
}
```

### GenieSource

Contains information about the source of the models generated from Generative AI Studio.

Fields

`baseModelUri` `string`

Required. The public base model URI.

**JSON representation**

```
{
  "baseModelUri": string
}
```

### Checkpoint

Describes the machine learning model version checkpoint.

Fields

`checkpointId` `string`

The id of the checkpoint.

`epoch` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The epoch of the checkpoint.

`step` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The step of the checkpoint.

**JSON representation**

```
{
  "checkpointId": string,
  "epoch": string,
  "step": string
}
```

| Methods                                                                                                                                                           |                                                                              |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| [`copy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/copy)                                         | Copies an already existing Agent Platform Model into the specified Location. |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/delete)                                     | Deletes a Model.                                                             |
| [`deleteVersion`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/deleteVersion)                       | Deletes a Model version.                                                     |
| [`export`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/export)                                     | Exports a trained, exportable Model to a location specified by the user.     |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/get)                                           | Gets a Model.                                                                |
| [`getIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/getIamPolicy)                         | Gets the access control policy for a resource.                               |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/list)                                         | Lists Models in a Location.                                                  |
| [`listCheckpoints`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/listCheckpoints)                   | Lists checkpoints of the specified model version.                            |
| [`listVersions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/listVersions)                         | Lists versions of the specified model.                                       |
| [`mergeVersionAliases`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/mergeVersionAliases)           | Merges a set of aliases for a Model version.                                 |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/patch)                                       | Updates a Model.                                                             |
| [`setIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/setIamPolicy)                         | Sets the access control policy on the specified resource.                    |
| [`testIamPermissions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/testIamPermissions)             | Returns permissions that a caller has on the specified resource.             |
| [`updateExplanationDataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/updateExplanationDataset) | Incrementally update the dataset used for an examples model.                 |
| [`upload`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/upload)                                     | Uploads a Model artifact into Agent Platform.                                |
