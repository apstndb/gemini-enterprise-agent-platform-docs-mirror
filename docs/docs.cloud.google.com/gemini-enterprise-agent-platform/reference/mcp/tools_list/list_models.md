---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_models
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `list_models`

Lists available machine learning models in your project's Agent Platform Model Registry (not Model Garden). Use this to discover existing models and retrieve their numeric IDs for other tool calls. Format: 'projects/{project\_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'. Filter by 'display\_name', 'labels', or 'base\_model\_name'.

The following sample demonstrate how to use `curl` to invoke the `list_models` MCP tool.

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
    &quot;name&quot;: &quot;list_models&quot;,
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

Request message for `ModelService.ListModels` .

### ListModelsRequest

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
  &quot;parent&quot;: string,
  &quot;filter&quot;: string,
  &quot;pageSize&quot;: integer,
  &quot;pageToken&quot;: string,
  &quot;readMask&quot;: string,
  &quot;orderBy&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. The resource name of the Location to list the Models from. Format: `projects/{project}/locations/{location}`

`filter`

`string`

An expression for filtering the results of the request. For field names both snake\_case and camelCase are supported.

  - `model` supports = and \!=. `model` represents the Model ID, i.e. the last segment of the Model's `resource name` .
  - `display_name` supports = and \!=
  - `labels` supports general map functions that is:
      - `labels.key=value` - key:value equality
      - \`labels.key:\* or labels:key - key existence
      - A key including a space must be quoted. `labels."a key"` .
  - `base_model_name` only supports =

Some examples:

  - `model=1234`
  - `displayName="myDisplayName"`
  - `labels.myKey="myValue"`
  - `baseModelName="text-bison"`

`pageSize`

`integer`

The standard list page size.

`pageToken`

`string`

The standard list page token. Typically obtained via `ListModelsResponse.next_page_token` of the previous `ModelService.ListModels` call.

`readMask`

` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`orderBy`

`string`

A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields:

  - `display_name`
  - `create_time`
  - `update_time`

Example: `display_name, create_time desc` .

### FieldMask

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
  &quot;paths&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`paths[]`

`string`

The set of field mask paths.

## Output Schema

Response message for `ModelService.ListModels`

### ListModelsResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;models&quot;: [{object (Model)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`models[]`

` object ( Model  ` )

List of Models in the requested page.

`nextPageToken`

`string`

A token to retrieve next page of results. Pass to `ListModelsRequest.page_token` to obtain that page.

### Model

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;versionId&quot;: string,&quot;versionAliases&quot;: [string],&quot;versionCreateTime&quot;: string,&quot;versionUpdateTime&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;versionDescription&quot;: string,&quot;defaultCheckpointId&quot;: string,&quot;predictSchemata&quot;: {object (PredictSchemata)},&quot;metadataSchemaUri&quot;: string,&quot;metadata&quot;: value,&quot;supportedExportFormats&quot;: [{object (ExportFormat)}],&quot;trainingPipeline&quot;: string,&quot;pipelineJob&quot;: string,&quot;containerSpec&quot;: {object (ModelContainerSpec)},&quot;artifactUri&quot;: string,&quot;supportedDeploymentResourcesTypes&quot;: [enum (DeploymentResourcesType)],&quot;supportedInputStorageFormats&quot;: [string],&quot;supportedOutputStorageFormats&quot;: [string],&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;deployedModels&quot;: [{object (DeployedModelRef)}],&quot;explanationSpec&quot;: {object (ExplanationSpec)},&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;dataStats&quot;: {object (DataStats)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;modelSourceInfo&quot;: {object (ModelSourceInfo)},&quot;originalModelInfo&quot;: {object (OriginalModelInfo)},&quot;metadataArtifact&quot;: string,&quot;baseModelSource&quot;: {object (BaseModelSource)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean,&quot;checkpoints&quot;: [{object (Checkpoint)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Identifier. The resource name of the Model.

`versionId`

`string`

Output only. Immutable. The version ID of the model. A new version is committed when a new model version is uploaded or trained under an existing model id. It is an auto-incrementing decimal number in string representation.

`versionAliases[]`

`string`

User provided version aliases so that a model version can be referenced via alias (i.e. `projects/{project}/locations/{location}/models/{model_id}@{version_alias}` instead of auto-generated version id (i.e. `projects/{project}/locations/{location}/models/{model_id}@{version_id})` . The format is \[a-z\]\[a-zA-Z0-9-\]{0,126}\[a-z0-9\] to distinguish from version\_id. A default version alias will be created for the first version of the model, and there must be exactly one default version alias for a model.

`versionCreateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this version was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`versionUpdateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this version was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`displayName`

`string`

Required. The display name of the Model. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description`

`string`

The description of the Model.

`versionDescription`

`string`

The description of this version.

`defaultCheckpointId`

`string`

The default checkpoint id of a model version.

`predictSchemata`

` object ( PredictSchemata  ` )

The schemata that describe formats of the Model's predictions and explanations as given and returned via `PredictionService.Predict` and `PredictionService.Explain` .

`metadataSchemaUri`

`string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Model, that is specific to it. Unset if the Model does not have any additional information. The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform, if no additional metadata is needed, this field is set to an empty string. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`metadata`

` value ( Value  ` format)

Immutable. An additional information about the Model; the schema of the metadata can be found in `metadata_schema` . Unset if the Model does not have any additional information.

`supportedExportFormats[]`

` object ( ExportFormat  ` )

Output only. The formats in which this Model may be exported. If empty, this Model is not available for export.

`trainingPipeline`

`string`

Output only. The resource name of the TrainingPipeline that uploaded this Model, if any.

`pipelineJob`

`string`

Optional. This field is populated if the model is produced by a pipeline job.

`containerSpec`

` object ( ModelContainerSpec  ` )

Input only. The specification of the container that is to be used when deploying this Model. The specification is ingested upon `ModelService.UploadModel` , and all binaries it contains are copied and stored internally by Agent Platform. Not required for AutoML Models.

`artifactUri`

`string`

Immutable. The path to the directory containing the Model artifact and any of its supporting files. Not required for AutoML Models.

`supportedDeploymentResourcesTypes[]`

`enum ( DeploymentResourcesType` )

Output only. When this Model is deployed, its prediction resources are described by the `prediction_resources` field of the `Endpoint.deployed_models` object. Because not all Models support all resource configuration types, the configuration types this Model supports are listed here. If no configuration types are listed, the Model cannot be deployed to an `Endpoint` and does not support online predictions ( `PredictionService.Predict` or `PredictionService.Explain` ). Such a Model can serve predictions by using a `BatchPredictionJob` , if it has at least one entry each in `supported_input_storage_formats` and `supported_output_storage_formats` .

`supportedInputStorageFormats[]`

`string`

Output only. The formats this Model supports in `BatchPredictionJob.input_config` . If `PredictSchemata.instance_schema_uri` exists, the instances should be given as per that schema.

The possible formats are:

  - `jsonl` The JSON Lines format, where each instance is a single line. Uses `GcsSource` .

  - `csv` The CSV format, where each instance is a single comma-separated line. The first line in the file is the header, containing comma-separated field names. Uses `GcsSource` .

  - `tf-record` The TFRecord format, where each instance is a single record in tfrecord syntax. Uses `GcsSource` .

  - `tf-record-gzip` Similar to `tf-record` , but the file is gzipped. Uses `GcsSource` .

  - `bigquery` Each instance is a single row in BigQuery. Uses `BigQuerySource` .

  - `file-list` Each line of the file is the location of an instance to process, uses `gcs_source` field of the `InputConfig` object.

If this Model doesn't support any of these formats it means it cannot be used with a `BatchPredictionJob` . However, if it has `supported_deployment_resources_types` , it could serve online predictions by using `PredictionService.Predict` or `PredictionService.Explain` .

`supportedOutputStorageFormats[]`

`string`

Output only. The formats this Model supports in `BatchPredictionJob.output_config` . If both `PredictSchemata.instance_schema_uri` and `PredictSchemata.prediction_schema_uri` exist, the predictions are returned together with their instances. In other words, the prediction has the original instance data first, followed by the actual prediction content (as per the schema).

The possible formats are:

  - `jsonl` The JSON Lines format, where each prediction is a single line. Uses `GcsDestination` .

  - `csv` The CSV format, where each prediction is a single comma-separated line. The first line in the file is the header, containing comma-separated field names. Uses `GcsDestination` .

  - `bigquery` Each prediction is a single row in a BigQuery table, uses `BigQueryDestination` .

If this Model doesn't support any of these formats it means it cannot be used with a `BatchPredictionJob` . However, if it has `supported_deployment_resources_types` , it could serve online predictions by using `PredictionService.Predict` or `PredictionService.Explain` .

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Model was uploaded into Agent Platform.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Model was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`deployedModels[]`

` object ( DeployedModelRef  ` )

Output only. The pointers to DeployedModels created from this Model. Note that Model could have been deployed to Endpoints in different Locations.

`explanationSpec`

` object ( ExplanationSpec  ` )

The default explanation specification for this Model.

The Model can be used for `requesting explanation` after being `deployed` if it is populated. The Model can be used for `batch explanation` if it is populated.

All fields of the explanation\_spec can be overridden by `explanation_spec` of `DeployModelRequest.deployed_model` , or `explanation_spec` of `BatchPredictionJob` .

If the default explanation specification is not set for this Model, this Model can still be used for `requesting explanation` by setting `explanation_spec` of `DeployModelRequest.deployed_model` and for `batch explanation` by setting `explanation_spec` of `BatchPredictionJob` .

`etag`

`string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize your Models.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`dataStats`

` object ( DataStats  ` )

Stats of data used for training or evaluating the Model.

Only populated when the Model is trained by a TrainingPipeline with `data_input_config` .

`encryptionSpec`

` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for a Model. If set, this Model and all sub-resources of this Model will be secured by this key.

`modelSourceInfo`

` object ( ModelSourceInfo  ` )

Output only. Source of a model. It can either be automl training pipeline, custom training pipeline, BigQuery ML, or saved and tuned from Genie or Model Garden.

`originalModelInfo`

` object ( OriginalModelInfo  ` )

Output only. If this Model is a copy of another Model, this contains info about the original.

`metadataArtifact`

`string`

Output only. The resource name of the Artifact that was created in MetadataStore when creating the Model. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}` .

`baseModelSource`

` object ( BaseModelSource  ` )

Optional. User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

`satisfiesPzs`

`boolean`

Output only. Reserved for future use.

`satisfiesPzi`

`boolean`

Output only. Reserved for future use.

`checkpoints[]`

` object ( Checkpoint  ` )

Optional. Output only. The checkpoints of the model.

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

### PredictSchemata

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
  &quot;instanceSchemaUri&quot;: string,
  &quot;parametersSchemaUri&quot;: string,
  &quot;predictionSchemaUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`instanceSchemaUri`

`string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in `PredictRequest.instances` , `ExplainRequest.instances` and `BatchPredictionJob.input_config` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`parametersSchemaUri`

`string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via `PredictRequest.parameters` , `ExplainRequest.parameters` and `BatchPredictionJob.model_parameters` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform, if no parameters are supported, then it is set to an empty string. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`predictionSchemaUri`

`string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via `PredictResponse.predictions` , `ExplainResponse.explanations` , and `BatchPredictionJob.output_config` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

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

### ExportFormat

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;exportableContents&quot;: [enum (ExportableContent)]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`id`

`string`

Output only. The ID of the export format. The possible format IDs are:

  - `tflite` Used for Android mobile devices.

  - `edgetpu-tflite` Used for [Edge TPU](https://cloud.google.com/edge-tpu/) devices.

  - `tf-saved-model` A tensorflow model in SavedModel format.

  - `tf-js` A [TensorFlow.js](https://www.tensorflow.org/js) model that can be used in the browser and in Node.js using JavaScript.

  - `core-ml` Used for iOS mobile devices.

  - `custom-trained` A Model that was uploaded or trained by custom code.

  - `genie` A tuned Model Garden model.

`exportableContents[]`

`enum ( ExportableContent` )

Output only. The content of this Model that may be exported.

### ModelContainerSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;imageUri&quot;: string,&quot;command&quot;: [string],&quot;args&quot;: [string],&quot;env&quot;: [{object (EnvVar)}],&quot;ports&quot;: [{object (Port)}],&quot;predictRoute&quot;: string,&quot;healthRoute&quot;: string,&quot;invokeRoutePrefix&quot;: string,&quot;grpcPorts&quot;: [{object (Port)}],&quot;deploymentTimeout&quot;: string,&quot;sharedMemorySizeMb&quot;: string,&quot;startupProbe&quot;: {object (Probe)},&quot;healthProbe&quot;: {object (Probe)},&quot;livenessProbe&quot;: {object (Probe)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`imageUri`

`string`

Required. Immutable. URI of the Docker image to be used as the custom container for serving predictions. This URI must identify an image in Artifact Registry. Learn more about the [container publishing requirements](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#publishing) , including permissions requirements for the Agent Platform Service Agent.

The container image is ingested upon `ModelService.UploadModel` , stored internally, and this original path is afterwards not used.

To learn about the requirements for the Docker image itself, see [Custom container requirements](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements) .

You can use the URI to one of Agent Platform's [pre-built container images for prediction](https://cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) in this field.

`command[]`

`string`

Immutable. Specifies the command that runs when the container starts. This overrides the container's [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) . Specify this field as an array of executable and arguments, similar to a Docker `ENTRYPOINT` 's "exec" form, not its "shell" form.

If you do not specify this field, then the container's `ENTRYPOINT` runs, in conjunction with the `args` field or the container's [`CMD`](https://docs.docker.com/engine/reference/builder/#cmd) , if either exists. If this field is not specified and the container does not have an `ENTRYPOINT` , then refer to the Docker documentation about [how `CMD` and `ENTRYPOINT` interact](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact) .

If you specify this field, then you can also specify the `args` field to provide additional arguments for this command. However, if you specify this field, then the container's `CMD` is ignored. See the [Kubernetes documentation about how the `command` and `args` fields interact with a container's `ENTRYPOINT` and `CMD`](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/#notes) .

In this field, you can reference [environment variables set by Agent Platform](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) and environment variables set in the `env` field. You cannot reference environment variables set in the Docker image. In order for environment variables to be expanded, reference them by using the following syntax:

`$( VARIABLE_NAME )`

Note that this differs from Bash variable expansion, which does not use parentheses. If a variable cannot be resolved, the reference in the input string is used unchanged. To avoid variable expansion, you can escape this syntax with `$$` ; for example:

`$$( VARIABLE_NAME )`

This field corresponds to the `command` field of the Kubernetes Containers [v1 core API](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core) .

`args[]`

`string`

Immutable. Specifies arguments for the command that runs when the container starts. This overrides the container's [`CMD`](https://docs.docker.com/engine/reference/builder/#cmd) . Specify this field as an array of executable and arguments, similar to a Docker `CMD` 's "default parameters" form.

If you don't specify this field but do specify the `command` field, then the command from the `command` field runs without any additional arguments. See the [Kubernetes documentation about how the `command` and `args` fields interact with a container's `ENTRYPOINT` and `CMD`](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/#notes) .

If you don't specify this field and don't specify the `command` field, then the container's [`ENTRYPOINT`](https://docs.docker.com/engine/reference/builder/#cmd) and `CMD` determine what runs based on their default behavior. See the Docker documentation about [how `CMD` and `ENTRYPOINT` interact](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact) .

In this field, you can reference [environment variables set by Agent Platform](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) and environment variables set in the `env` field. You cannot reference environment variables set in the Docker image. In order for environment variables to be expanded, reference them by using the following syntax:

`$( VARIABLE_NAME )`

Note that this differs from Bash variable expansion, which does not use parentheses. If a variable cannot be resolved, the reference in the input string is used unchanged. To avoid variable expansion, you can escape this syntax with `$$` ; for example:

`$$( VARIABLE_NAME )`

This field corresponds to the `args` field of the Kubernetes Containers [v1 core API](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core) .

`env[]`

` object ( EnvVar  ` )

Immutable. List of environment variables to set in the container. After the container starts running, code running in the container can read these environment variables.

Additionally, the `command` and `args` fields can reference these variables. Later entries in this list can also reference earlier entries. For example, the following example sets the variable `VAR_2` to have the value `foo bar` :

```json
[
  {
    "name": "VAR_1",
    "value": "foo"
  },
  {
    "name": "VAR_2",
    "value": "$(VAR_1) bar"
  }
]
```

If you switch the order of the variables in the example, then the expansion does not occur.

This field corresponds to the `env` field of the Kubernetes Containers [v1 core API](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core) .

`ports[]`

` object ( Port  ` )

Immutable. List of ports to expose from the container. Agent Platform sends any prediction requests that it receives to the first port on this list. Agent Platform also sends [liveness and health checks](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#liveness) to this port.

If you do not specify this field, it defaults to following value:

```json
[
  {
    "containerPort": 8080
  }
]
```

Agent Platform does not use ports other than the first one listed. This field corresponds to the `ports` field of the Kubernetes Containers [v1 core API](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core) .

`predictRoute`

`string`

Immutable. HTTP path on the container to send prediction requests to. Agent Platform forwards requests sent using `projects.locations.endpoints.predict` to this path on the container's IP address and port. Agent Platform then returns the container's response in the API response.

For example, if you set this field to `/foo` , then when Agent Platform receives a prediction request, it forwards the request body in a POST request to the `/foo` path on the port of your container specified by the first value of this `ModelContainerSpec` 's `ports` field.

If you don't specify this field, it defaults to the following value when you `deploy this Model to an Endpoint` :

`/v1/endpoints/ ENDPOINT /deployedModels/ DEPLOYED_MODEL :predict`

The placeholders in this value are replaced as follows:

  - ENDPOINT : The last segment (following `endpoints/` )of the Endpoint.name\]\[\] field of the Endpoint where this Model has been deployed. (Agent Platform makes this value available to your container code as the [`AIP_ENDPOINT_ID` environment variable](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) .)

  - DEPLOYED\_MODEL : `DeployedModel.id` of the `DeployedModel` . (Agent Platform makes this value available to your container code as the [`AIP_DEPLOYED_MODEL_ID` environment variable](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) .)

`healthRoute`

`string`

Immutable. HTTP path on the container to send health checks to. Agent Platform intermittently sends GET requests to this path on the container's IP address and port to check that the container is healthy. Read more about [health checks](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#health) .

For example, if you set this field to `/bar` , then Agent Platform intermittently sends a GET request to the `/bar` path on the port of your container specified by the first value of this `ModelContainerSpec` 's `ports` field.

If you don't specify this field, it defaults to the following value when you `deploy this Model to an Endpoint` :

`/v1/endpoints/ ENDPOINT /deployedModels/ DEPLOYED_MODEL :predict`

The placeholders in this value are replaced as follows:

  - ENDPOINT : The last segment (following `endpoints/` )of the Endpoint.name\]\[\] field of the Endpoint where this Model has been deployed. (Agent Platform makes this value available to your container code as the [`AIP_ENDPOINT_ID` environment variable](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) .)

  - DEPLOYED\_MODEL : `DeployedModel.id` of the `DeployedModel` . (Agent Platform makes this value available to your container code as the [`AIP_DEPLOYED_MODEL_ID` environment variable](https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables) .)

`invokeRoutePrefix`

`string`

Immutable. Invoke route prefix for the custom container. "/\*" is the only supported value right now. By setting this field, any non-root route on this model will be accessible with invoke http call eg: "/invoke/foo/bar", however the \[PredictionService.Invoke\] RPC is not supported yet.

Only one of `predict_route` or `invoke_route_prefix` can be set, and we default to using `predict_route` if this field is not set. If this field is set, the Model can only be deployed to dedicated endpoint.

`grpcPorts[]`

` object ( Port  ` )

Immutable. List of ports to expose from the container. Agent Platform sends gRPC prediction requests that it receives to the first port on this list. Agent Platform also sends liveness and health checks to this port.

If you do not specify this field, gRPC requests to the container will be disabled.

Agent Platform does not use ports other than the first one listed. This field corresponds to the `ports` field of the Kubernetes Containers v1 core API.

`deploymentTimeout`

` string ( Duration  ` format)

Immutable. Deployment timeout. Limit for deployment timeout is 2 hours.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`sharedMemorySizeMb`

`string ( int64 format)`

Immutable. The amount of the VM memory to reserve as the shared memory for the model in megabytes.

`startupProbe`

` object ( Probe  ` )

Immutable. Specification for Kubernetes startup probe.

`healthProbe`

` object ( Probe  ` )

Immutable. Specification for Kubernetes readiness probe.

`livenessProbe`

` object ( Probe  ` )

Immutable. Specification for Kubernetes liveness probe.

### EnvVar

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
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. Name of the environment variable. Must be a valid C identifier.

`value`

`string`

Required. Variables that reference a $(VAR\_NAME) are expanded using the previous defined environment variables in the container and any service environment variables. If a variable cannot be resolved, the reference in the input string will be unchanged. The $(VAR\_NAME) syntax can be escaped with a double $$, ie: $$(VAR\_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not.

### Port

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
  &quot;containerPort&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`containerPort`

`integer`

The number of the port to expose on the pod's IP address. Must be a valid port number, between 1 and 65535 inclusive.

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

### Probe

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;periodSeconds&quot;: integer,&quot;timeoutSeconds&quot;: integer,&quot;failureThreshold&quot;: integer,&quot;successThreshold&quot;: integer,&quot;initialDelaySeconds&quot;: integer,// Union field probe_type can be only one of the following:&quot;exec&quot;: {object (ExecAction)},&quot;httpGet&quot;: {object (HttpGetAction)},&quot;grpc&quot;: {object (GrpcAction)},&quot;tcpSocket&quot;: {object (TcpSocketAction)}// End of list of possible types for union field probe_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`periodSeconds`

`integer`

How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1. Must be less than timeout\_seconds.

Maps to Kubernetes probe argument 'periodSeconds'.

`timeoutSeconds`

`integer`

Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1. Must be greater or equal to period\_seconds.

Maps to Kubernetes probe argument 'timeoutSeconds'.

`failureThreshold`

`integer`

Number of consecutive failures before the probe is considered failed. Defaults to 3. Minimum value is 1.

Maps to Kubernetes probe argument 'failureThreshold'.

`successThreshold`

`integer`

Number of consecutive successes before the probe is considered successful. Defaults to 1. Minimum value is 1.

Maps to Kubernetes probe argument 'successThreshold'.

`initialDelaySeconds`

`integer`

Number of seconds to wait before starting the probe. Defaults to 0. Minimum value is 0.

Maps to Kubernetes probe argument 'initialDelaySeconds'.

Union field `probe_type` .

`probe_type` can be only one of the following:

`exec`

` object ( ExecAction  ` )

ExecAction probes the health of a container by executing a command.

`httpGet`

` object ( HttpGetAction  ` )

HttpGetAction probes the health of a container by sending an HTTP GET request.

`grpc`

` object ( GrpcAction  ` )

GrpcAction probes the health of a container by sending a gRPC request.

`tcpSocket`

` object ( TcpSocketAction  ` )

TcpSocketAction probes the health of a container by opening a TCP socket connection.

### ExecAction

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
  &quot;command&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`command[]`

`string`

Command is the command line to execute inside the container, the working directory for the command is root ('/') in the container's filesystem. The command is simply exec'd, it is not run inside a shell, so traditional shell instructions ('|', etc) won't work. To use a shell, you need to explicitly call out to that shell. Exit status of 0 is treated as live/healthy and non-zero is unhealthy.

### HttpGetAction

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;path&quot;: string,&quot;port&quot;: integer,&quot;host&quot;: string,&quot;scheme&quot;: string,&quot;httpHeaders&quot;: [{object (HttpHeader)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`path`

`string`

Path to access on the HTTP server.

`port`

`integer`

Number of the port to access on the container. Number must be in the range 1 to 65535.

`host`

`string`

Host name to connect to, defaults to the model serving container's IP. You probably want to set "Host" in httpHeaders instead.

`scheme`

`string`

Scheme to use for connecting to the host. Defaults to HTTP. Acceptable values are "HTTP" or "HTTPS".

`httpHeaders[]`

` object ( HttpHeader  ` )

Custom headers to set in the request. HTTP allows repeated headers.

### HttpHeader

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
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

The header field name. This will be canonicalized upon output, so case-variant names will be understood as the same header.

`value`

`string`

The header field value

### GrpcAction

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
  &quot;port&quot;: integer,
  &quot;service&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`port`

`integer`

Port number of the gRPC service. Number must be in the range 1 to 65535.

`service`

`string`

Service is the name of the service to place in the gRPC HealthCheckRequest. See <https://github.com/grpc/grpc/blob/master/doc/health-checking.md> .

If this is not specified, the default behavior is defined by gRPC.

### TcpSocketAction

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
  &quot;port&quot;: integer,
  &quot;host&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`port`

`integer`

Number of the port to access on the container. Number must be in the range 1 to 65535.

`host`

`string`

Optional: Host name to connect to, defaults to the model serving container's IP.

### DeployedModelRef

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
  &quot;endpoint&quot;: string,
  &quot;deployedModelId&quot;: string,
  &quot;checkpointId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`endpoint`

`string`

Immutable. A resource name of an Endpoint.

`deployedModelId`

`string`

Immutable. An ID of a DeployedModel in the above Endpoint.

`checkpointId`

`string`

Immutable. The ID of the Checkpoint deployed in the DeployedModel.

### ExplanationSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parameters&quot;: {object (ExplanationParameters)},&quot;metadata&quot;: {object (ExplanationMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parameters`

` object ( ExplanationParameters  ` )

Required. Parameters that configure explaining of the Model's predictions.

`metadata`

` object ( ExplanationMetadata  ` )

Optional. Metadata describing the Model's input and output for explanation.

### ExplanationParameters

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;topK&quot;: integer,&quot;outputIndices&quot;: array,// Union field method can be only one of the following:&quot;sampledShapleyAttribution&quot;: {object (SampledShapleyAttribution)},&quot;integratedGradientsAttribution&quot;: {object (IntegratedGradientsAttribution)},&quot;xraiAttribution&quot;: {object (XraiAttribution)},&quot;examples&quot;: {object (Examples)}// End of list of possible types for union field method.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`topK`

`integer`

If populated, returns attributions for top K indices of outputs (defaults to 1). Only applies to Models that predicts more than one outputs (e,g, multi-class Models). When set to -1, returns explanations for all outputs.

`outputIndices`

` array ( ListValue  ` format)

If populated, only returns attributions that have `output_index` contained in output\_indices. It must be an ndarray of integers, with the same shape of the output it's explaining.

If not populated, returns attributions for `top_k` indices of outputs. If neither top\_k nor output\_indices is populated, returns the argmax index of the outputs.

Only applicable to Models that predict multiple outputs (e,g, multi-class Models that predict multiple classes).

Union field `method` .

`method` can be only one of the following:

`sampledShapleyAttribution`

` object ( SampledShapleyAttribution  ` )

An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features. Refer to this paper for model details: <https://arxiv.org/abs/1306.4265> .

`integratedGradientsAttribution`

` object ( IntegratedGradientsAttribution  ` )

An attribution method that computes Aumann-Shapley values taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1703.01365>

`xraiAttribution`

` object ( XraiAttribution  ` )

An attribution method that redistributes Integrated Gradients attribution to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1906.02825>

XRAI currently performs better on natural images, like a picture of a house or an animal. If the images are taken in artificial environments, like a lab or manufacturing line, or from diagnostic equipment, like x-rays or quality-control cameras, use Integrated Gradients instead.

`examples`

` object ( Examples  ` )

Example-based explanations that returns the nearest neighbors from the provided dataset.

### SampledShapleyAttribution

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
  &quot;pathCount&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`pathCount`

`integer`

Required. The number of feature permutations to consider when approximating the Shapley values.

Valid range of its value is \[1, 50\], inclusively.

### IntegratedGradientsAttribution

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stepCount&quot;: integer,&quot;smoothGradConfig&quot;: {object (SmoothGradConfig)},&quot;blurBaselineConfig&quot;: {object (BlurBaselineConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stepCount`

`integer`

Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is within the desired error range.

Valid range of its value is \[1, 100\], inclusively.

`smoothGradConfig`

` object ( SmoothGradConfig  ` )

Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf>

`blurBaselineConfig`

` object ( BlurBaselineConfig  ` )

Config for IG with blur baseline.

When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>

### SmoothGradConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;noisySampleCount&quot;: integer,// Union field GradientNoiseSigma can be only one of the following:&quot;noiseSigma&quot;: number,&quot;featureNoiseSigma&quot;: {object (FeatureNoiseSigma)}// End of list of possible types for union field GradientNoiseSigma.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`noisySampleCount`

`integer`

The number of gradient samples to use for approximation. The higher this number, the more accurate the gradient is, but the runtime complexity increases by this factor as well. Valid range of its value is \[1, 50\]. Defaults to 3.

Union field `GradientNoiseSigma` . Represents the standard deviation of the gaussian kernel that will be used to add noise to the interpolated inputs prior to computing gradients. `GradientNoiseSigma` can be only one of the following:

`noiseSigma`

`number`

This is a single float value and will be used to add noise to all the features. Use this field when all features are normalized to have the same distribution: scale to range \[0, 1\], \[-1, 1\] or z-scoring, where features are normalized to have 0-mean and 1-variance. Learn more about [normalization](https://developers.google.com/machine-learning/data-prep/transform/normalization) .

For best results the recommended value is about 10% - 20% of the standard deviation of the input feature. Refer to section 3.2 of the SmoothGrad paper: <https://arxiv.org/pdf/1706.03825.pdf> . Defaults to 0.1.

If the distribution is different per feature, set `feature_noise_sigma` instead for each feature.

`featureNoiseSigma`

` object ( FeatureNoiseSigma  ` )

This is similar to `noise_sigma` , but provides additional flexibility. A separate noise sigma can be provided for each feature, which is useful if their distributions are different. No noise is added to features that are not set. If this field is unset, `noise_sigma` will be used for all features.

### FeatureNoiseSigma

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;noiseSigma&quot;: [{object (NoiseSigmaForFeature)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`noiseSigma[]`

` object ( NoiseSigmaForFeature  ` )

Noise sigma per feature. No noise is added to features that are not set.

### NoiseSigmaForFeature

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
  &quot;sigma&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

The name of the input feature for which noise sigma is provided. The features are defined in `explanation metadata inputs` .

`sigma`

`number`

This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to `noise_sigma` but represents the noise added to the current feature. Defaults to 0.1.

### BlurBaselineConfig

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
  &quot;maxBlurSigma&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`maxBlurSigma`

`number`

The standard deviation of the blur kernel for the blurred baseline. The same blurring parameter is used for both the height and the width dimension. If not set, the method defaults to the zero (i.e. black for images) baseline.

### XraiAttribution

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stepCount&quot;: integer,&quot;smoothGradConfig&quot;: {object (SmoothGradConfig)},&quot;blurBaselineConfig&quot;: {object (BlurBaselineConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stepCount`

`integer`

Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is met within the desired error range.

Valid range of its value is \[1, 100\], inclusively.

`smoothGradConfig`

` object ( SmoothGradConfig  ` )

Config for SmoothGrad approximation of gradients.

When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf>

`blurBaselineConfig`

` object ( BlurBaselineConfig  ` )

Config for XRAI with blur baseline.

When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>

### Examples

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;neighborCount&quot;: integer,// Union field source can be only one of the following:&quot;exampleGcsSource&quot;: {object (ExampleGcsSource)}// End of list of possible types for union field source.// Union field config can be only one of the following:&quot;nearestNeighborSearchConfig&quot;: value,&quot;presets&quot;: {object (Presets)}// End of list of possible types for union field config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`neighborCount`

`integer`

The number of neighbors to return when querying for examples.

Union field `source` .

`source` can be only one of the following:

`exampleGcsSource`

` object ( ExampleGcsSource  ` )

The Cloud Storage input instances.

Union field `config` .

`config` can be only one of the following:

`nearestNeighborSearchConfig`

` value ( Value  ` format)

The full configuration for the generated index, the semantics are the same as `metadata` and should match [NearestNeighborSearchConfig](https://cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations-example-based#nearest-neighbor-search-config) .

`presets`

` object ( Presets  ` )

Simplified preset configuration, which automatically sets configuration values based on the desired query speed-precision trade-off and modality.

### ExampleGcsSource

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataFormat&quot;: enum (DataFormat),&quot;gcsSource&quot;: {object (GcsSource)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataFormat`

`enum ( DataFormat` )

The format in which instances are given, if not specified, assume it's JSONL format. Currently only JSONL format is supported.

`gcsSource`

` object ( GcsSource  ` )

The Cloud Storage location for the input instances.

### GcsSource

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
  &quot;uris&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`uris[]`

`string`

Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see <https://cloud.google.com/storage/docs/wildcards> .

### Presets

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modality&quot;: enum (Modality),// Union field _query can be only one of the following:&quot;query&quot;: enum (Query)// End of list of possible types for union field _query.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`modality`

`enum ( Modality` )

The modality of the uploaded model, which automatically configures the distance measurement and feature normalization for the underlying example index and queries. If your model does not precisely fit one of these types, it is okay to choose the closest type.

Union field `_query` .

`_query` can be only one of the following:

`query`

`enum ( Query` )

Preset option controlling parameters for speed-precision trade-off when querying for examples. If omitted, defaults to `PRECISE` .

### ExplanationMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputs&quot;: {string: {object (InputMetadata)},...},&quot;outputs&quot;: {string: {object (OutputMetadata)},...},&quot;featureAttributionsSchemaUri&quot;: string,&quot;latentSpaceSource&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`inputs`

` map (key: string, value: object ( InputMetadata  ` ))

Required. Map from feature names to feature input metadata. Keys are the name of the features. Values are the specification of the feature.

An empty InputMetadata is valid. It describes a text feature which has the name specified as the key in `ExplanationMetadata.inputs` . The baseline of the empty feature is chosen by Agent Platform.

For Agent Platform-provided Tensorflow images, the key can be any friendly name of the feature. Once specified, `featureAttributions` are keyed by this key (if not grouped with another feature).

For custom images, the key must match with the key in `instance` .

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`outputs`

` map (key: string, value: object ( OutputMetadata  ` ))

Required. Map from output names to output metadata.

For Agent Platform-provided Tensorflow images, keys can be any user defined string that consists of any UTF-8 characters.

For custom images, keys are the name of the output field in the prediction to be explained.

Currently only one key is allowed.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`featureAttributionsSchemaUri`

`string`

Points to a YAML file stored on Google Cloud Storage describing the format of the `feature attributions` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML tabular Models always have this field populated by Agent Platform. Note: The URI given on output may be different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`latentSpaceSource`

`string`

Name of the source to generate embeddings for example based explanations.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (InputMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( InputMetadata  ` )

### InputMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputBaselines&quot;: [value],&quot;inputTensorName&quot;: string,&quot;encoding&quot;: enum (Encoding),&quot;modality&quot;: string,&quot;featureValueDomain&quot;: {object (FeatureValueDomain)},&quot;indicesTensorName&quot;: string,&quot;denseShapeTensorName&quot;: string,&quot;indexFeatureMapping&quot;: [string],&quot;encodedTensorName&quot;: string,&quot;encodedBaselines&quot;: [value],&quot;visualization&quot;: {object (Visualization)},&quot;groupName&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`inputBaselines[]`

` value ( Value  ` format)

Baseline inputs for this feature.

If no baseline is specified, Agent Platform chooses the baseline for this feature. If multiple baselines are specified, Agent Platform returns the average attributions across them in `Attribution.feature_attributions` .

For Agent Platform-provided Tensorflow images (both 1.x and 2.x), the shape of each baseline must match the shape of the input tensor. If a scalar is provided, we broadcast to the same shape as the input tensor.

For custom images, the element of the baselines must be in the same format as the feature's input in the `instance` \[\]. The schema of any single instance may be specified via Endpoint's DeployedModels' `Model's` `PredictSchemata's` `instance_schema_uri` .

`inputTensorName`

`string`

Name of the input tensor for this feature. Required and is only applicable to Agent Platform-provided images for Tensorflow.

`encoding`

`enum ( Encoding` )

Defines how the feature is encoded into the input tensor. Defaults to IDENTITY.

`modality`

`string`

Modality of the feature. Valid values are: numeric, image. Defaults to numeric.

`featureValueDomain`

` object ( FeatureValueDomain  ` )

The domain details of the input feature value. Like min/max, original mean or standard deviation if normalized.

`indicesTensorName`

`string`

Specifies the index of the values of the input tensor. Required when the input tensor is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .

`denseShapeTensorName`

`string`

Specifies the shape of the values of the input if the input is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .

`indexFeatureMapping[]`

`string`

A list of feature names for each index in the input tensor. Required when the input `InputMetadata.encoding` is BAG\_OF\_FEATURES, BAG\_OF\_FEATURES\_SPARSE, INDICATOR.

`encodedTensorName`

`string`

Encoded tensor is a transformation of the input tensor. Must be provided if choosing `Integrated Gradients attribution` or `XRAI attribution` and the input tensor is not differentiable.

An encoded tensor is generated if the input tensor is encoded by a lookup table.

`encodedBaselines[]`

` value ( Value  ` format)

A list of baselines for the encoded tensor.

The shape of each baseline should match the shape of the encoded tensor. If a scalar is provided, Agent Platform broadcasts to the same shape as the encoded tensor.

`visualization`

` object ( Visualization  ` )

Visualization configurations for image explanation.

`groupName`

`string`

Name of the group that the input belongs to. Features with the same group name will be treated as one feature when computing attributions. Features grouped together can have different shapes in value. If provided, there will be one single attribution generated in `Attribution.feature_attributions` , keyed by the group name.

### FeatureValueDomain

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
  &quot;minValue&quot;: number,
  &quot;maxValue&quot;: number,
  &quot;originalMean&quot;: number,
  &quot;originalStddev&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`minValue`

`number`

The minimum permissible value for this feature.

`maxValue`

`number`

The maximum permissible value for this feature.

`originalMean`

`number`

If this input feature has been normalized to a mean value of 0, the original\_mean specifies the mean value of the domain prior to normalization.

`originalStddev`

`number`

If this input feature has been normalized to a standard deviation of 1.0, the original\_stddev specifies the standard deviation of the domain prior to normalization.

### Visualization

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (Type),&quot;polarity&quot;: enum (Polarity),&quot;colorMap&quot;: enum (ColorMap),&quot;clipPercentUpperbound&quot;: number,&quot;clipPercentLowerbound&quot;: number,&quot;overlayType&quot;: enum (OverlayType)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

`enum ( Type` )

Type of the image visualization. Only applicable to `Integrated Gradients attribution` . OUTLINES shows regions of attribution, while PIXELS shows per-pixel attribution. Defaults to OUTLINES.

`polarity`

`enum ( Polarity` )

Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.

`colorMap`

`enum ( ColorMap` )

The color scheme used for the highlighted areas.

Defaults to PINK\_GREEN for `Integrated Gradients attribution` , which shows positive attributions in green and negative in pink.

Defaults to VIRIDIS for `XRAI attribution` , which highlights the most influential regions in yellow and the least influential in blue.

`clipPercentUpperbound`

`number`

Excludes attributions above the specified percentile from the highlighted areas. Using the clip\_percent\_upperbound and clip\_percent\_lowerbound together can be useful for filtering out noise and making it easier to see areas of strong attribution. Defaults to 99.9.

`clipPercentLowerbound`

`number`

Excludes attributions below the specified percentile, from the highlighted areas. Defaults to 62.

`overlayType`

`enum ( OverlayType` )

How the original image is displayed in the visualization. Adjusting the overlay can help increase visual clarity if the original image makes it difficult to view the visualization. Defaults to NONE.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (OutputMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( OutputMetadata  ` )

### OutputMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outputTensorName&quot;: string,// Union field display_name_mapping can be only one of the following:&quot;indexDisplayNameMapping&quot;: value,&quot;displayNameMappingKey&quot;: string// End of list of possible types for union field display_name_mapping.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outputTensorName`

`string`

Name of the output tensor. Required and is only applicable to Agent Platform provided images for Tensorflow.

Union field `display_name_mapping` . Defines how to map `Attribution.output_index` to `Attribution.output_display_name` .

If neither of the fields are specified, `Attribution.output_display_name` will not be populated. `display_name_mapping` can be only one of the following:

`indexDisplayNameMapping`

` value ( Value  ` format)

Static mapping between the index and display name.

Use this if the outputs are a deterministic n-dimensional array, e.g. a list of scores of all the classes in a pre-defined order for a multi-classification Model. It's not feasible if the outputs are non-deterministic, e.g. the Model produces top-k classes or sort the outputs by their values.

The shape of the value must be an n-dimensional array of strings. The number of dimensions must match that of the outputs to be explained. The `Attribution.output_display_name` is populated by locating in the mapping with `Attribution.output_index` .

`displayNameMappingKey`

`string`

Specify a field name in the prediction to look for the display name.

Use this if the prediction contains the display names for the outputs.

The display names in the prediction must have the same shape of the outputs, so that it can be located by `Attribution.output_index` for a specific output.

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

### DataStats

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
  &quot;trainingDataItemsCount&quot;: string,
  &quot;validationDataItemsCount&quot;: string,
  &quot;testDataItemsCount&quot;: string,
  &quot;trainingAnnotationsCount&quot;: string,
  &quot;validationAnnotationsCount&quot;: string,
  &quot;testAnnotationsCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`trainingDataItemsCount`

`string ( int64 format)`

Number of DataItems that were used for training this Model.

`validationDataItemsCount`

`string ( int64 format)`

Number of DataItems that were used for validating this Model during training.

`testDataItemsCount`

`string ( int64 format)`

Number of DataItems that were used for evaluating this Model. If the Model is evaluated multiple times, this will be the number of test DataItems used by the first evaluation. If the Model is not evaluated, the number is 0.

`trainingAnnotationsCount`

`string ( int64 format)`

Number of Annotations that are used for training this Model.

`validationAnnotationsCount`

`string ( int64 format)`

Number of Annotations that are used for validating this Model during training.

`testAnnotationsCount`

`string ( int64 format)`

Number of Annotations that are used for evaluating this Model. If the Model is evaluated multiple times, this will be the number of test Annotations used by the first evaluation. If the Model is not evaluated, the number is 0.

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

### ModelSourceInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceType&quot;: enum (ModelSourceType),&quot;copy&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`sourceType`

`enum ( ModelSourceType` )

Type of the model source.

`copy`

`boolean`

If this Model is copy of another Model. If true then `source_type` pertains to the original.

### OriginalModelInfo

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
  &quot;model&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`model`

`string`

Output only. The resource name of the Model this Model is a copy of, including the revision. Format: `projects/{project}/locations/{location}/models/{model_id}@{version_id}`

### BaseModelSource

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field source can be only one of the following:&quot;modelGardenSource&quot;: {object (ModelGardenSource)},&quot;genieSource&quot;: {object (GenieSource)}// End of list of possible types for union field source.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `source` .

`source` can be only one of the following:

`modelGardenSource`

` object ( ModelGardenSource  ` )

Source information of Model Garden models.

`genieSource`

` object ( GenieSource  ` )

Information about the base model of Genie models.

### ModelGardenSource

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
  &quot;publicModelName&quot;: string,
  &quot;versionId&quot;: string,
  &quot;skipHfModelCache&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`publicModelName`

`string`

Required. The model garden source model resource name.

`versionId`

`string`

Optional. The model garden source model version ID.

`skipHfModelCache`

`boolean`

Optional. Whether to avoid pulling the model from the HF cache.

### GenieSource

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
  &quot;baseModelUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`baseModelUri`

`string`

Required. The public base model URI.

### Checkpoint

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
  &quot;checkpointId&quot;: string,
  &quot;epoch&quot;: string,
  &quot;step&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`checkpointId`

`string`

The ID of the checkpoint.

`epoch`

`string ( int64 format)`

The epoch of the checkpoint.

`step`

`string ( int64 format)`

The step of the checkpoint.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
