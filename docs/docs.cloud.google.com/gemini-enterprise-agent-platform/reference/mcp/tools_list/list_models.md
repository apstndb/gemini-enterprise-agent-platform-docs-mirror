---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_models
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `list_models`

Lists available machine learning models in your project's Agent Platform Model Registry (not Model Garden). Use this to discover existing models and retrieve their numeric IDs for other tool calls. Format: 'projects/{project_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'. Filter by 'display_name', 'labels', or 'base_model_name'.

The following sample demonstrate how to use `curl` to invoke the `list_models` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "list_models",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `ModelService.ListModels` .

### ListModelsRequest

**JSON representation**

```
{
  "parent": string,
  "filter": string,
  "pageSize": integer,
  "pageToken": string,
  "readMask": string,
  "orderBy": string
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
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. The resource name of the Location to list the Models from. Format: <code>projects/{project}/locations/{location}</code></p></td>
</tr>
<tr class="even">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>An expression for filtering the results of the request. For field names both snake_case and camelCase are supported.</p>
<ul>
<li><code>model</code> supports = and !=. <code>model</code> represents the Model ID, i.e. the last segment of the Model's <code>resource name</code> .</li>
<li><code>display_name</code> supports = and !=</li>
<li><code>labels</code> supports general map functions that is:
<ul>
<li><code>labels.key=value</code> - key:value equality</li>
<li>`labels.key:* or labels:key - key existence</li>
<li>A key including a space must be quoted. <code>labels."a key"</code> .</li>
</ul></li>
<li><code>base_model_name</code> only supports =</li>
</ul>
<p>Some examples:</p>
<ul>
<li><code>model=1234</code></li>
<li><code>displayName="myDisplayName"</code></li>
<li><code>labels.myKey="myValue"</code></li>
<li><code>baseModelName="text-bison"</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>pageSize</code></td>
<td><p><code>integer</code></p>
<p>The standard list page size.</p></td>
</tr>
<tr class="even">
<td><code>pageToken</code></td>
<td><p><code>string</code></p>
<p>The standard list page token. Typically obtained via <code>ListModelsResponse.next_page_token</code> of the previous <code>ModelService.ListModels</code> call.</p></td>
</tr>
<tr class="odd">
<td><code>readMask</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a><code> format)</code></p>
<p>Mask specifying which fields to read.</p>
<p>This is a comma-separated list of fully qualified names of fields. Example: <code>"user.displayName,photo"</code> .</p></td>
</tr>
<tr class="even">
<td><code>orderBy</code></td>
<td><p><code>string</code></p>
<p>A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields:</p>
<ul>
<li><code>display_name</code></li>
<li><code>create_time</code></li>
<li><code>update_time</code></li>
</ul>
<p>Example: <code>display_name, create_time desc</code> .</p></td>
</tr>
</tbody>
</table>

### FieldMask

**JSON representation**

```
{
  "paths": [
    string
  ]
}
```

| Fields    |                                       |
|-----------|---------------------------------------|
| `paths[]` | `string` The set of field mask paths. |

## Output Schema

Response message for `ModelService.ListModels`

### ListModelsResponse

**JSON representation**

```
{
  "models": [
    {
      object (Model)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                                         |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `models[]`      | `object ( `[`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Model)` )` List of Models in the requested page. |
| `nextPageToken` | `string` A token to retrieve next page of results. Pass to `ListModelsRequest.page_token` to obtain that page.                                                                          |

### Model

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Identifier. The resource name of the Model.</p></td>
</tr>
<tr class="even">
<td><code>versionId</code></td>
<td><p><code>string</code></p>
<p>Output only. Immutable. The version ID of the model. A new version is committed when a new model version is uploaded or trained under an existing model id. It is an auto-incrementing decimal number in string representation.</p></td>
</tr>
<tr class="odd">
<td><code>versionAliases[]</code></td>
<td><p><code>string</code></p>
<p>User provided version aliases so that a model version can be referenced via alias (i.e. <code>projects/{project}/locations/{location}/models/{model_id}@{version_alias}</code> instead of auto-generated version id (i.e. <code>projects/{project}/locations/{location}/models/{model_id}@{version_id})</code> . The format is [a-z][a-zA-Z0-9-]{0,126}[a-z0-9] to distinguish from version_id. A default version alias will be created for the first version of the model, and there must be exactly one default version alias for a model.</p></td>
</tr>
<tr class="even">
<td><code>versionCreateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this version was created.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>versionUpdateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this version was most recently updated.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>Required. The display name of the Model. The name can be up to 128 characters long and can consist of any UTF-8 characters.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>The description of the Model.</p></td>
</tr>
<tr class="even">
<td><code>versionDescription</code></td>
<td><p><code>string</code></p>
<p>The description of this version.</p></td>
</tr>
<tr class="odd">
<td><code>defaultCheckpointId</code></td>
<td><p><code>string</code></p>
<p>The default checkpoint id of a model version.</p></td>
</tr>
<tr class="even">
<td><code>predictSchemata</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.PredictSchemata"><code>PredictSchemata</code></a><code> )</code></p>
<p>The schemata that describe formats of the Model's predictions and explanations as given and returned via <code>PredictionService.Predict</code> and <code>PredictionService.Explain</code> .</p></td>
</tr>
<tr class="odd">
<td><code>metadataSchemaUri</code></td>
<td><p><code>string</code></p>
<p>Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Model, that is specific to it. Unset if the Model does not have any additional information. The schema is defined as an OpenAPI 3.0.2 <a href="https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject">Schema Object</a> . AutoML Models always have this field populated by Agent Platform, if no additional metadata is needed, this field is set to an empty string. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.</p></td>
</tr>
<tr class="even">
<td><code>metadata</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>Immutable. An additional information about the Model; the schema of the metadata can be found in <code>metadata_schema</code> . Unset if the Model does not have any additional information.</p></td>
</tr>
<tr class="odd">
<td><code>supportedExportFormats[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ExportFormat"><code>ExportFormat</code></a><code> )</code></p>
<p>Output only. The formats in which this Model may be exported. If empty, this Model is not available for export.</p></td>
</tr>
<tr class="even">
<td><code>trainingPipeline</code></td>
<td><p><code>string</code></p>
<p>Output only. The resource name of the TrainingPipeline that uploaded this Model, if any.</p></td>
</tr>
<tr class="odd">
<td><code>pipelineJob</code></td>
<td><p><code>string</code></p>
<p>Optional. This field is populated if the model is produced by a pipeline job.</p></td>
</tr>
<tr class="even">
<td><code>containerSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ModelContainerSpec"><code>ModelContainerSpec</code></a><code> )</code></p>
<p>The specification of the container that is to be used when deploying this Model. The specification is ingested upon <code>ModelService.UploadModel</code> , and all binaries it contains are copied and stored internally by Agent Platform. Not required for AutoML Models.</p></td>
</tr>
<tr class="odd">
<td><code>artifactUri</code></td>
<td><p><code>string</code></p>
<p>Immutable. The path to the directory containing the Model artifact and any of its supporting files. Not required for AutoML Models.</p></td>
</tr>
<tr class="even">
<td><code>supportedDeploymentResourcesTypes[]</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.DeploymentResourcesType"><code>DeploymentResourcesType</code></a><code> )</code></p>
<p>Output only. When this Model is deployed, its prediction resources are described by the <code>prediction_resources</code> field of the <code>Endpoint.deployed_models</code> object. Because not all Models support all resource configuration types, the configuration types this Model supports are listed here. If no configuration types are listed, the Model cannot be deployed to an <code>Endpoint</code> and does not support online predictions ( <code>PredictionService.Predict</code> or <code>PredictionService.Explain</code> ). Such a Model can serve predictions by using a <code>BatchPredictionJob</code> , if it has at least one entry each in <code>supported_input_storage_formats</code> and <code>supported_output_storage_formats</code> .</p></td>
</tr>
<tr class="odd">
<td><code>supportedInputStorageFormats[]</code></td>
<td><p><code>string</code></p>
<p>Output only. The formats this Model supports in <code>BatchPredictionJob.input_config</code> . If <code>PredictSchemata.instance_schema_uri</code> exists, the instances should be given as per that schema.</p>
<p>The possible formats are:</p>
<ul>
<li><p><code>jsonl</code> The JSON Lines format, where each instance is a single line. Uses <code>GcsSource</code> .</p></li>
<li><p><code>csv</code> The CSV format, where each instance is a single comma-separated line. The first line in the file is the header, containing comma-separated field names. Uses <code>GcsSource</code> .</p></li>
<li><p><code>tf-record</code> The TFRecord format, where each instance is a single record in tfrecord syntax. Uses <code>GcsSource</code> .</p></li>
<li><p><code>tf-record-gzip</code> Similar to <code>tf-record</code> , but the file is gzipped. Uses <code>GcsSource</code> .</p></li>
<li><p><code>bigquery</code> Each instance is a single row in BigQuery. Uses <code>BigQuerySource</code> .</p></li>
<li><p><code>file-list</code> Each line of the file is the location of an instance to process, uses <code>gcs_source</code> field of the <code>InputConfig</code> object.</p></li>
</ul>
<p>If this Model doesn't support any of these formats it means it cannot be used with a <code>BatchPredictionJob</code> . However, if it has <code>supported_deployment_resources_types</code> , it could serve online predictions by using <code>PredictionService.Predict</code> or <code>PredictionService.Explain</code> .</p></td>
</tr>
<tr class="even">
<td><code>supportedOutputStorageFormats[]</code></td>
<td><p><code>string</code></p>
<p>Output only. The formats this Model supports in <code>BatchPredictionJob.output_config</code> . If both <code>PredictSchemata.instance_schema_uri</code> and <code>PredictSchemata.prediction_schema_uri</code> exist, the predictions are returned together with their instances. In other words, the prediction has the original instance data first, followed by the actual prediction content (as per the schema).</p>
<p>The possible formats are:</p>
<ul>
<li><p><code>jsonl</code> The JSON Lines format, where each prediction is a single line. Uses <code>GcsDestination</code> .</p></li>
<li><p><code>csv</code> The CSV format, where each prediction is a single comma-separated line. The first line in the file is the header, containing comma-separated field names. Uses <code>GcsDestination</code> .</p></li>
<li><p><code>bigquery</code> Each prediction is a single row in a BigQuery table, uses <code>BigQueryDestination</code> .</p></li>
</ul>
<p>If this Model doesn't support any of these formats it means it cannot be used with a <code>BatchPredictionJob</code> . However, if it has <code>supported_deployment_resources_types</code> , it could serve online predictions by using <code>PredictionService.Predict</code> or <code>PredictionService.Explain</code> .</p></td>
</tr>
<tr class="odd">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this Model was uploaded into Agent Platform.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>updateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this Model was most recently updated.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>deployedModels[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.DeployedModelRef"><code>DeployedModelRef</code></a><code> )</code></p>
<p>Output only. The pointers to DeployedModels created from this Model. Note that Model could have been deployed to Endpoints in different Locations.</p></td>
</tr>
<tr class="even">
<td><code>explanationSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ExplanationSpec"><code>ExplanationSpec</code></a><code> )</code></p>
<p>The default explanation specification for this Model.</p>
<p>The Model can be used for <code>requesting explanation</code> after being <code>deployed</code> if it is populated. The Model can be used for <code>batch explanation</code> if it is populated.</p>
<p>All fields of the explanation_spec can be overridden by <code>explanation_spec</code> of <code>DeployModelRequest.deployed_model</code> , or <code>explanation_spec</code> of <code>BatchPredictionJob</code> .</p>
<p>If the default explanation specification is not set for this Model, this Model can still be used for <code>requesting explanation</code> by setting <code>explanation_spec</code> of <code>DeployModelRequest.deployed_model</code> and for <code>batch explanation</code> by setting <code>explanation_spec</code> of <code>BatchPredictionJob</code> .</p></td>
</tr>
<tr class="odd">
<td><code>etag</code></td>
<td><p><code>string</code></p>
<p>Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>The labels with user-defined metadata to organize your Models.</p>
<p>Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.</p>
<p>See <a href="https://goo.gl/xmQnxf">https://goo.gl/xmQnxf</a> for more information and examples of labels.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>dataStats</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.DataStats"><code>DataStats</code></a><code> )</code></p>
<p>Stats of data used for training or evaluating the Model.</p>
<p>Only populated when the Model is trained by a TrainingPipeline with <code>data_input_config</code> .</p></td>
</tr>
<tr class="even">
<td><code>encryptionSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec"><code>EncryptionSpec</code></a><code> )</code></p>
<p>Customer-managed encryption key spec for a Model. If set, this Model and all sub-resources of this Model will be secured by this key.</p></td>
</tr>
<tr class="odd">
<td><code>modelSourceInfo</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ModelSourceInfo"><code>ModelSourceInfo</code></a><code> )</code></p>
<p>Output only. Source of a model. It can either be automl training pipeline, custom training pipeline, BigQuery ML, or saved and tuned from Genie or Model Garden.</p></td>
</tr>
<tr class="even">
<td><code>originalModelInfo</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.OriginalModelInfo"><code>OriginalModelInfo</code></a><code> )</code></p>
<p>Output only. If this Model is a copy of another Model, this contains info about the original.</p></td>
</tr>
<tr class="odd">
<td><code>metadataArtifact</code></td>
<td><p><code>string</code></p>
<p>Output only. The resource name of the Artifact that was created in MetadataStore when creating the Model. The Artifact resource name pattern is <code>projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}</code> .</p></td>
</tr>
<tr class="even">
<td><code>baseModelSource</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.BaseModelSource"><code>BaseModelSource</code></a><code> )</code></p>
<p>Optional. User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.</p></td>
</tr>
<tr class="odd">
<td><code>satisfiesPzs</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Reserved for future use.</p></td>
</tr>
<tr class="even">
<td><code>satisfiesPzi</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Reserved for future use.</p></td>
</tr>
<tr class="odd">
<td><code>checkpoints[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Checkpoint"><code>Checkpoint</code></a><code> )</code></p>
<p>Optional. Output only. The checkpoints of the model.</p></td>
</tr>
</tbody>
</table>

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

### PredictSchemata

**JSON representation**

```
{
  "instanceSchemaUri": string,
  "parametersSchemaUri": string,
  "predictionSchemaUri": string
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `instanceSchemaUri`   | `string` Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in `PredictRequest.instances` , `ExplainRequest.instances` and `BatchPredictionJob.input_config` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.                                                                        |
| `parametersSchemaUri` | `string` Immutable. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via `PredictRequest.parameters` , `ExplainRequest.parameters` and `BatchPredictionJob.model_parameters` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform, if no parameters are supported, then it is set to an empty string. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access. |
| `predictionSchemaUri` | `string` Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via `PredictResponse.predictions` , `ExplainResponse.explanations` , and `BatchPredictionJob.output_config` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.                                |

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

### ExportFormat

**JSON representation**

```
{
  "id": string,
  "exportableContents": [
    enum (ExportableContent)
  ]
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
<td><code>id</code></td>
<td><p><code>string</code></p>
<p>Output only. The ID of the export format. The possible format IDs are:</p>
<ul>
<li><p><code>tflite</code> Used for Android mobile devices.</p></li>
<li><p><code>edgetpu-tflite</code> Used for <a href="https://cloud.google.com/edge-tpu/">Edge TPU</a> devices.</p></li>
<li><p><code>tf-saved-model</code> A tensorflow model in SavedModel format.</p></li>
<li><p><code>tf-js</code> A <a href="https://www.tensorflow.org/js">TensorFlow.js</a> model that can be used in the browser and in Node.js using JavaScript.</p></li>
<li><p><code>core-ml</code> Used for iOS mobile devices.</p></li>
<li><p><code>custom-trained</code> A Model that was uploaded or trained by custom code.</p></li>
<li><p><code>genie</code> A tuned Model Garden model.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><code>exportableContents[]</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ExportableContent"><code>ExportableContent</code></a><code> )</code></p>
<p>Output only. The content of this Model that may be exported.</p></td>
</tr>
</tbody>
</table>

### ModelContainerSpec

**JSON representation**

```
{
  "imageUri": string,
  "command": [
    string
  ],
  "args": [
    string
  ],
  "env": [
    {
      object (EnvVar)
    }
  ],
  "ports": [
    {
      object (Port)
    }
  ],
  "predictRoute": string,
  "healthRoute": string,
  "invokeRoutePrefix": string,
  "grpcPorts": [
    {
      object (Port)
    }
  ],
  "deploymentTimeout": string,
  "sharedMemorySizeMb": string,
  "startupProbe": {
    object (Probe)
  },
  "healthProbe": {
    object (Probe)
  },
  "livenessProbe": {
    object (Probe)
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
<td><code>imageUri</code></td>
<td><p><code>string</code></p>
<p>Required. Immutable. URI of the Docker image to be used as the custom container for serving predictions. This URI must identify an image in Artifact Registry. Learn more about the <a href="https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#publishing">container publishing requirements</a> , including permissions requirements for the Agent Platform Service Agent.</p>
<p>The container image is ingested upon <code>ModelService.UploadModel</code> , stored internally, and this original path is afterwards not used.</p>
<p>To learn about the requirements for the Docker image itself, see <a href="https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#">Custom container requirements</a> .</p>
<p>You can use the URI to one of Agent Platform's <a href="https://cloud.google.com/vertex-ai/docs/predictions/pre-built-containers">pre-built container images for prediction</a> in this field.</p></td>
</tr>
<tr class="even">
<td><code>command[]</code></td>
<td><p><code>string</code></p>
<p>Immutable. Specifies the command that runs when the container starts. This overrides the container's <a href="https://docs.docker.com/engine/reference/builder/#entrypoint">ENTRYPOINT</a> . Specify this field as an array of executable and arguments, similar to a Docker <code>ENTRYPOINT</code> 's "exec" form, not its "shell" form.</p>
<p>If you do not specify this field, then the container's <code>ENTRYPOINT</code> runs, in conjunction with the <code>args</code> field or the container's <a href="https://docs.docker.com/engine/reference/builder/#cmd"><code>CMD</code></a> , if either exists. If this field is not specified and the container does not have an <code>ENTRYPOINT</code> , then refer to the Docker documentation about <a href="https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact">how <code>CMD</code> and <code>ENTRYPOINT</code> interact</a> .</p>
<p>If you specify this field, then you can also specify the <code>args</code> field to provide additional arguments for this command. However, if you specify this field, then the container's <code>CMD</code> is ignored. See the <a href="https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/#notes">Kubernetes documentation about how the <code>command</code> and <code>args</code> fields interact with a container's <code>ENTRYPOINT</code> and <code>CMD</code></a> .</p>
<p>In this field, you can reference <a href="https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables">environment variables set by Agent Platform</a> and environment variables set in the <code>env</code> field. You cannot reference environment variables set in the Docker image. In order for environment variables to be expanded, reference them by using the following syntax:</p>
<p><code>$( </code><var translate="no"> VARIABLE_NAME </var><code> )</code></p>
<p>Note that this differs from Bash variable expansion, which does not use parentheses. If a variable cannot be resolved, the reference in the input string is used unchanged. To avoid variable expansion, you can escape this syntax with <code>$$</code> ; for example:</p>
<p><code>$$( </code><var translate="no"> VARIABLE_NAME </var><code> )</code></p>
<p>This field corresponds to the <code>command</code> field of the Kubernetes Containers <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core">v1 core API</a> .</p></td>
</tr>
<tr class="odd">
<td><code>args[]</code></td>
<td><p><code>string</code></p>
<p>Immutable. Specifies arguments for the command that runs when the container starts. This overrides the container's <a href="https://docs.docker.com/engine/reference/builder/#cmd"><code>CMD</code></a> . Specify this field as an array of executable and arguments, similar to a Docker <code>CMD</code> 's "default parameters" form.</p>
<p>If you don't specify this field but do specify the <code>command</code> field, then the command from the <code>command</code> field runs without any additional arguments. See the <a href="https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/#notes">Kubernetes documentation about how the <code>command</code> and <code>args</code> fields interact with a container's <code>ENTRYPOINT</code> and <code>CMD</code></a> .</p>
<p>If you don't specify this field and don't specify the <code>command</code> field, then the container's <a href="https://docs.docker.com/engine/reference/builder/#cmd"><code>ENTRYPOINT</code></a> and <code>CMD</code> determine what runs based on their default behavior. See the Docker documentation about <a href="https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact">how <code>CMD</code> and <code>ENTRYPOINT</code> interact</a> .</p>
<p>In this field, you can reference <a href="https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables">environment variables set by Agent Platform</a> and environment variables set in the <code>env</code> field. You cannot reference environment variables set in the Docker image. In order for environment variables to be expanded, reference them by using the following syntax:</p>
<p><code>$( </code><var translate="no"> VARIABLE_NAME </var><code> )</code></p>
<p>Note that this differs from Bash variable expansion, which does not use parentheses. If a variable cannot be resolved, the reference in the input string is used unchanged. To avoid variable expansion, you can escape this syntax with <code>$$</code> ; for example:</p>
<p><code>$$( </code><var translate="no"> VARIABLE_NAME </var><code> )</code></p>
<p>This field corresponds to the <code>args</code> field of the Kubernetes Containers <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core">v1 core API</a> .</p></td>
</tr>
<tr class="even">
<td><code>env[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EnvVar"><code>EnvVar</code></a><code> )</code></p>
<p>Immutable. List of environment variables to set in the container. After the container starts running, code running in the container can read these environment variables.</p>
<p>Additionally, the <code>command</code> and <code>args</code> fields can reference these variables. Later entries in this list can also reference earlier entries. For example, the following example sets the variable <code>VAR_2</code> to have the value <code>foo bar</code> :</p>
<pre class="json"><code>[
  {
    &quot;name&quot;: &quot;VAR_1&quot;,
    &quot;value&quot;: &quot;foo&quot;
  },
  {
    &quot;name&quot;: &quot;VAR_2&quot;,
    &quot;value&quot;: &quot;$(VAR_1) bar&quot;
  }
]</code></pre>
<p>If you switch the order of the variables in the example, then the expansion does not occur.</p>
<p>This field corresponds to the <code>env</code> field of the Kubernetes Containers <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core">v1 core API</a> .</p></td>
</tr>
<tr class="odd">
<td><code>ports[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Port"><code>Port</code></a><code> )</code></p>
<p>Immutable. List of ports to expose from the container. Agent Platform sends any prediction requests that it receives to the first port on this list. Agent Platform also sends <a href="https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#liveness">liveness and health checks</a> to this port.</p>
<p>If you do not specify this field, it defaults to following value:</p>
<pre class="json"><code>[
  {
    &quot;containerPort&quot;: 8080
  }
]</code></pre>
<p>Agent Platform does not use ports other than the first one listed. This field corresponds to the <code>ports</code> field of the Kubernetes Containers <a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#container-v1-core">v1 core API</a> .</p></td>
</tr>
<tr class="even">
<td><code>predictRoute</code></td>
<td><p><code>string</code></p>
<p>Immutable. HTTP path on the container to send prediction requests to. Agent Platform forwards requests sent using <code>projects.locations.endpoints.predict</code> to this path on the container's IP address and port. Agent Platform then returns the container's response in the API response.</p>
<p>For example, if you set this field to <code>/foo</code> , then when Agent Platform receives a prediction request, it forwards the request body in a POST request to the <code>/foo</code> path on the port of your container specified by the first value of this <code>ModelContainerSpec</code> 's <code>ports</code> field.</p>
<p>If you don't specify this field, it defaults to the following value when you <code>deploy this Model to an Endpoint</code> :</p>
<p><code>/v1/endpoints/ </code><var translate="no"> ENDPOINT </var><code> /deployedModels/ </code><var translate="no"> DEPLOYED_MODEL </var><code> :predict</code></p>
<p>The placeholders in this value are replaced as follows:</p>
<ul>
<li><p><var translate="no"> ENDPOINT </var> : The last segment (following <code>endpoints/</code> )of the Endpoint.name][] field of the Endpoint where this Model has been deployed. (Agent Platform makes this value available to your container code as the <a href="https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables"><code>AIP_ENDPOINT_ID</code> environment variable</a> .)</p></li>
<li><p><var translate="no"> DEPLOYED_MODEL </var> : <code>DeployedModel.id</code> of the <code>DeployedModel</code> . (Agent Platform makes this value available to your container code as the <a href="https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables"><code>AIP_DEPLOYED_MODEL_ID</code> environment variable</a> .)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>healthRoute</code></td>
<td><p><code>string</code></p>
<p>Immutable. HTTP path on the container to send health checks to. Agent Platform intermittently sends GET requests to this path on the container's IP address and port to check that the container is healthy. Read more about <a href="https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#health">health checks</a> .</p>
<p>For example, if you set this field to <code>/bar</code> , then Agent Platform intermittently sends a GET request to the <code>/bar</code> path on the port of your container specified by the first value of this <code>ModelContainerSpec</code> 's <code>ports</code> field.</p>
<p>If you don't specify this field, it defaults to the following value when you <code>deploy this Model to an Endpoint</code> :</p>
<p><code>/v1/endpoints/ </code><var translate="no"> ENDPOINT </var><code> /deployedModels/ </code><var translate="no"> DEPLOYED_MODEL </var><code> :predict</code></p>
<p>The placeholders in this value are replaced as follows:</p>
<ul>
<li><p><var translate="no"> ENDPOINT </var> : The last segment (following <code>endpoints/</code> )of the Endpoint.name][] field of the Endpoint where this Model has been deployed. (Agent Platform makes this value available to your container code as the <a href="https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables"><code>AIP_ENDPOINT_ID</code> environment variable</a> .)</p></li>
<li><p><var translate="no"> DEPLOYED_MODEL </var> : <code>DeployedModel.id</code> of the <code>DeployedModel</code> . (Agent Platform makes this value available to your container code as the <a href="https://cloud.google.com/vertex-ai/docs/predictions/custom-container-requirements#aip-variables"><code>AIP_DEPLOYED_MODEL_ID</code> environment variable</a> .)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><code>invokeRoutePrefix</code></td>
<td><p><code>string</code></p>
<p>Immutable. Invoke route prefix for the custom container. "/*" is the only supported value right now. By setting this field, any non-root route on this model will be accessible with invoke http call eg: "/invoke/foo/bar", however the [PredictionService.Invoke] RPC is not supported yet.</p>
<p>Only one of <code>predict_route</code> or <code>invoke_route_prefix</code> can be set, and we default to using <code>predict_route</code> if this field is not set. If this field is set, the Model can only be deployed to dedicated endpoint.</p></td>
</tr>
<tr class="odd">
<td><code>grpcPorts[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Port"><code>Port</code></a><code> )</code></p>
<p>Immutable. List of ports to expose from the container. Agent Platform sends gRPC prediction requests that it receives to the first port on this list. Agent Platform also sends liveness and health checks to this port.</p>
<p>If you do not specify this field, gRPC requests to the container will be disabled.</p>
<p>Agent Platform does not use ports other than the first one listed. This field corresponds to the <code>ports</code> field of the Kubernetes Containers v1 core API.</p></td>
</tr>
<tr class="even">
<td><code>deploymentTimeout</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#duration"><code>Duration</code></a><code> format)</code></p>
<p>Immutable. Deployment timeout. Limit for deployment timeout is 2 hours.</p>
<p>A duration in seconds with up to nine fractional digits, ending with ' <code>s</code> '. Example: <code>"3.5s"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>sharedMemorySizeMb</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Immutable. The amount of the VM memory to reserve as the shared memory for the model in megabytes.</p></td>
</tr>
<tr class="even">
<td><code>startupProbe</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Probe"><code>Probe</code></a><code> )</code></p>
<p>Immutable. Specification for Kubernetes startup probe.</p></td>
</tr>
<tr class="odd">
<td><code>healthProbe</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Probe"><code>Probe</code></a><code> )</code></p>
<p>Immutable. Specification for Kubernetes readiness probe.</p></td>
</tr>
<tr class="even">
<td><code>livenessProbe</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Probe"><code>Probe</code></a><code> )</code></p>
<p>Immutable. Specification for Kubernetes liveness probe.</p></td>
</tr>
</tbody>
</table>

### EnvVar

**JSON representation**

```
{
  "name": string,
  "value": string
}
```

| Fields  |                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`  | `string` Required. Name of the environment variable. Must be a valid C identifier.                                                                                                                                                                                                                                                                                                                                                                  |
| `value` | `string` Required. Variables that reference a \$(VAR_NAME) are expanded using the previous defined environment variables in the container and any service environment variables. If a variable cannot be resolved, the reference in the input string will be unchanged. The \$(VAR_NAME) syntax can be escaped with a double \$\$, ie: \$\$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |

### Port

**JSON representation**

```
{
  "containerPort": integer
}
```

| Fields          |                                                                                                                                 |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------|
| `containerPort` | `integer` The number of the port to expose on the pod's IP address. Must be a valid port number, between 1 and 65535 inclusive. |

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

### Probe

**JSON representation**

```
{
  "periodSeconds": integer,
  "timeoutSeconds": integer,
  "failureThreshold": integer,
  "successThreshold": integer,
  "initialDelaySeconds": integer,

  // Union field probe_type can be only one of the following:
  "exec": {
    object (ExecAction)
  },
  "httpGet": {
    object (HttpGetAction)
  },
  "grpc": {
    object (GrpcAction)
  },
  "tcpSocket": {
    object (TcpSocketAction)
  }
  // End of list of possible types for union field probe_type.
}
```

| Fields                                                                    |                                                                                                                                                                                                                                                            |
|---------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `periodSeconds`                                                           | `integer` How often (in seconds) to perform the probe. Default to 10 seconds. Minimum value is 1. Must be less than timeout_seconds. Maps to Kubernetes probe argument 'periodSeconds'.                                                                    |
| `timeoutSeconds`                                                          | `integer` Number of seconds after which the probe times out. Defaults to 1 second. Minimum value is 1. Must be greater or equal to period_seconds. Maps to Kubernetes probe argument 'timeoutSeconds'.                                                     |
| `failureThreshold`                                                        | `integer` Number of consecutive failures before the probe is considered failed. Defaults to 3. Minimum value is 1. Maps to Kubernetes probe argument 'failureThreshold'.                                                                                   |
| `successThreshold`                                                        | `integer` Number of consecutive successes before the probe is considered successful. Defaults to 1. Minimum value is 1. Maps to Kubernetes probe argument 'successThreshold'.                                                                              |
| `initialDelaySeconds`                                                     | `integer` Number of seconds to wait before starting the probe. Defaults to 0. Minimum value is 0. Maps to Kubernetes probe argument 'initialDelaySeconds'.                                                                                                 |
| Union field `probe_type` . `probe_type` can be only one of the following: |                                                                                                                                                                                                                                                            |
| `exec`                                                                    | `object ( `[`ExecAction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ExecAction)` )` ExecAction probes the health of a container by executing a command.                            |
| `httpGet`                                                                 | `object ( `[`HttpGetAction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.HttpGetAction)` )` HttpGetAction probes the health of a container by sending an HTTP GET request.           |
| `grpc`                                                                    | `object ( `[`GrpcAction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.GrpcAction)` )` GrpcAction probes the health of a container by sending a gRPC request.                         |
| `tcpSocket`                                                               | `object ( `[`TcpSocketAction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.TcpSocketAction)` )` TcpSocketAction probes the health of a container by opening a TCP socket connection. |

### ExecAction

**JSON representation**

```
{
  "command": [
    string
  ]
}
```

| Fields      |                                                                                                                                                                                                                                                                                                                                                                                                                      |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `command[]` | `string` Command is the command line to execute inside the container, the working directory for the command is root ('/') in the container's filesystem. The command is simply exec'd, it is not run inside a shell, so traditional shell instructions ('\|', etc) won't work. To use a shell, you need to explicitly call out to that shell. Exit status of 0 is treated as live/healthy and non-zero is unhealthy. |

### HttpGetAction

**JSON representation**

```
{
  "path": string,
  "port": integer,
  "host": string,
  "scheme": string,
  "httpHeaders": [
    {
      object (HttpHeader)
    }
  ]
}
```

| Fields          |                                                                                                                                                                                                                                 |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `path`          | `string` Path to access on the HTTP server.                                                                                                                                                                                     |
| `port`          | `integer` Number of the port to access on the container. Number must be in the range 1 to 65535.                                                                                                                                |
| `host`          | `string` Host name to connect to, defaults to the model serving container's IP. You probably want to set "Host" in httpHeaders instead.                                                                                         |
| `scheme`        | `string` Scheme to use for connecting to the host. Defaults to HTTP. Acceptable values are "HTTP" or "HTTPS".                                                                                                                   |
| `httpHeaders[]` | `object ( `[`HttpHeader`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.HttpHeader)` )` Custom headers to set in the request. HTTP allows repeated headers. |

### HttpHeader

**JSON representation**

```
{
  "name": string,
  "value": string
}
```

| Fields  |                                                                                                                                      |
|---------|--------------------------------------------------------------------------------------------------------------------------------------|
| `name`  | `string` The header field name. This will be canonicalized upon output, so case-variant names will be understood as the same header. |
| `value` | `string` The header field value                                                                                                      |

### GrpcAction

**JSON representation**

```
{
  "port": integer,
  "service": string
}
```

| Fields    |                                                                                                                                                                                                                                 |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `port`    | `integer` Port number of the gRPC service. Number must be in the range 1 to 65535.                                                                                                                                              |
| `service` | `string` Service is the name of the service to place in the gRPC HealthCheckRequest. See <https://github.com/grpc/grpc/blob/master/doc/health-checking.md> . If this is not specified, the default behavior is defined by gRPC. |

### TcpSocketAction

**JSON representation**

```
{
  "port": integer,
  "host": string
}
```

| Fields |                                                                                                  |
|--------|--------------------------------------------------------------------------------------------------|
| `port` | `integer` Number of the port to access on the container. Number must be in the range 1 to 65535. |
| `host` | `string` Optional: Host name to connect to, defaults to the model serving container's IP.        |

### DeployedModelRef

**JSON representation**

```
{
  "endpoint": string,
  "deployedModelId": string,
  "checkpointId": string
}
```

| Fields            |                                                                             |
|-------------------|-----------------------------------------------------------------------------|
| `endpoint`        | `string` Immutable. A resource name of an Endpoint.                         |
| `deployedModelId` | `string` Immutable. An ID of a DeployedModel in the above Endpoint.         |
| `checkpointId`    | `string` Immutable. The ID of the Checkpoint deployed in the DeployedModel. |

### ExplanationSpec

**JSON representation**

```
{
  "parameters": {
    object (ExplanationParameters)
  },
  "metadata": {
    object (ExplanationMetadata)
  }
}
```

| Fields       |                                                                                                                                                                                                                                                              |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parameters` | `object ( `[`ExplanationParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ExplanationParameters)` )` Required. Parameters that configure explaining of the Model's predictions. |
| `metadata`   | `object ( `[`ExplanationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ExplanationMetadata)` )` Optional. Metadata describing the Model's input and output for explanation.    |

### ExplanationParameters

**JSON representation**

```
{
  "topK": integer,
  "outputIndices": array,

  // Union field method can be only one of the following:
  "sampledShapleyAttribution": {
    object (SampledShapleyAttribution)
  },
  "integratedGradientsAttribution": {
    object (IntegratedGradientsAttribution)
  },
  "xraiAttribution": {
    object (XraiAttribution)
  },
  "examples": {
    object (Examples)
  }
  // End of list of possible types for union field method.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `topK`                                                            | `integer` If populated, returns attributions for top K indices of outputs (defaults to 1). Only applies to Models that predicts more than one outputs (e,g, multi-class Models). When set to -1, returns explanations for all outputs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `outputIndices`                                                   | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` If populated, only returns attributions that have `output_index` contained in output_indices. It must be an ndarray of integers, with the same shape of the output it's explaining. If not populated, returns attributions for `top_k` indices of outputs. If neither top_k nor output_indices is populated, returns the argmax index of the outputs. Only applicable to Models that predict multiple outputs (e,g, multi-class Models that predict multiple classes).                                                                                                                          |
| Union field `method` . `method` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `sampledShapleyAttribution`                                       | `object ( `[`SampledShapleyAttribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.SampledShapleyAttribution)` )` An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features. Refer to this paper for model details: <https://arxiv.org/abs/1306.4265> .                                                                                                                                                                                                           |
| `integratedGradientsAttribution`                                  | `object ( `[`IntegratedGradientsAttribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.IntegratedGradientsAttribution)` )` An attribution method that computes Aumann-Shapley values taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1703.01365>                                                                                                                                                                                                                                                                                                 |
| `xraiAttribution`                                                 | `object ( `[`XraiAttribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.XraiAttribution)` )` An attribution method that redistributes Integrated Gradients attribution to segmented regions, taking advantage of the model's fully differentiable structure. Refer to this paper for more details: <https://arxiv.org/abs/1906.02825> XRAI currently performs better on natural images, like a picture of a house or an animal. If the images are taken in artificial environments, like a lab or manufacturing line, or from diagnostic equipment, like x-rays or quality-control cameras, use Integrated Gradients instead. |
| `examples`                                                        | `object ( `[`Examples`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Examples)` )` Example-based explanations that returns the nearest neighbors from the provided dataset.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

### SampledShapleyAttribution

**JSON representation**

```
{
  "pathCount": integer
}
```

| Fields      |                                                                                                                                                               |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pathCount` | `integer` Required. The number of feature permutations to consider when approximating the Shapley values. Valid range of its value is \[1, 50\], inclusively. |

### IntegratedGradientsAttribution

**JSON representation**

```
{
  "stepCount": integer,
  "smoothGradConfig": {
    object (SmoothGradConfig)
  },
  "blurBaselineConfig": {
    object (BlurBaselineConfig)
  }
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stepCount`          | `integer` Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is within the desired error range. Valid range of its value is \[1, 100\], inclusively.                                                                                                                                                                                                                                 |
| `smoothGradConfig`   | `object ( `[`SmoothGradConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.SmoothGradConfig)` )` Config for SmoothGrad approximation of gradients. When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf> |
| `blurBaselineConfig` | `object ( `[`BlurBaselineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.BlurBaselineConfig)` )` Config for IG with blur baseline. When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>                                |

### SmoothGradConfig

**JSON representation**

```
{
  "noisySampleCount": integer,

  // Union field GradientNoiseSigma can be only one of the following:
  "noiseSigma": number,
  "featureNoiseSigma": {
    object (FeatureNoiseSigma)
  }
  // End of list of possible types for union field GradientNoiseSigma.
}
```

| Fields                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `noisySampleCount`                                                                                                                                                                                                                         | `integer` The number of gradient samples to use for approximation. The higher this number, the more accurate the gradient is, but the runtime complexity increases by this factor as well. Valid range of its value is \[1, 50\]. Defaults to 3.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `GradientNoiseSigma` . Represents the standard deviation of the gaussian kernel that will be used to add noise to the interpolated inputs prior to computing gradients. `GradientNoiseSigma` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `noiseSigma`                                                                                                                                                                                                                               | `number` This is a single float value and will be used to add noise to all the features. Use this field when all features are normalized to have the same distribution: scale to range \[0, 1\], \[-1, 1\] or z-scoring, where features are normalized to have 0-mean and 1-variance. Learn more about [normalization](https://developers.google.com/machine-learning/data-prep/transform/normalization) . For best results the recommended value is about 10% - 20% of the standard deviation of the input feature. Refer to section 3.2 of the SmoothGrad paper: <https://arxiv.org/pdf/1706.03825.pdf> . Defaults to 0.1. If the distribution is different per feature, set `feature_noise_sigma` instead for each feature. |
| `featureNoiseSigma`                                                                                                                                                                                                                        | `object ( `[`FeatureNoiseSigma`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.FeatureNoiseSigma)` )` This is similar to `noise_sigma` , but provides additional flexibility. A separate noise sigma can be provided for each feature, which is useful if their distributions are different. No noise is added to features that are not set. If this field is unset, `noise_sigma` will be used for all features.                                                                                                                                                                                                                                          |

### FeatureNoiseSigma

**JSON representation**

```
{
  "noiseSigma": [
    {
      object (NoiseSigmaForFeature)
    }
  ]
}
```

| Fields         |                                                                                                                                                                                                                                                          |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `noiseSigma[]` | `object ( `[`NoiseSigmaForFeature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.NoiseSigmaForFeature)` )` Noise sigma per feature. No noise is added to features that are not set. |

### NoiseSigmaForFeature

**JSON representation**

```
{
  "name": string,
  "sigma": number
}
```

| Fields  |                                                                                                                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`  | `string` The name of the input feature for which noise sigma is provided. The features are defined in `explanation metadata inputs` .                                                                                                               |
| `sigma` | `number` This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to `noise_sigma` but represents the noise added to the current feature. Defaults to 0.1. |

### BlurBaselineConfig

**JSON representation**

```
{
  "maxBlurSigma": number
}
```

| Fields         |                                                                                                                                                                                                                                             |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `maxBlurSigma` | `number` The standard deviation of the blur kernel for the blurred baseline. The same blurring parameter is used for both the height and the width dimension. If not set, the method defaults to the zero (i.e. black for images) baseline. |

### XraiAttribution

**JSON representation**

```
{
  "stepCount": integer,
  "smoothGradConfig": {
    object (SmoothGradConfig)
  },
  "blurBaselineConfig": {
    object (BlurBaselineConfig)
  }
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stepCount`          | `integer` Required. The number of steps for approximating the path integral. A good value to start is 50 and gradually increase until the sum to diff property is met within the desired error range. Valid range of its value is \[1, 100\], inclusively.                                                                                                                                                                                                                             |
| `smoothGradConfig`   | `object ( `[`SmoothGradConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.SmoothGradConfig)` )` Config for SmoothGrad approximation of gradients. When enabled, the gradients are approximated by averaging the gradients from noisy samples in the vicinity of the inputs. Adding noise can help improve the computed gradients. Refer to this paper for more details: <https://arxiv.org/pdf/1706.03825.pdf> |
| `blurBaselineConfig` | `object ( `[`BlurBaselineConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.BlurBaselineConfig)` )` Config for XRAI with blur baseline. When enabled, a linear path from the maximally blurred image to the input image is created. Using a blurred baseline instead of zero (black image) is motivated by the BlurIG approach explained here: <https://arxiv.org/abs/2004.03383>                              |

### Examples

**JSON representation**

```
{
  "neighborCount": integer,

  // Union field source can be only one of the following:
  "exampleGcsSource": {
    object (ExampleGcsSource)
  }
  // End of list of possible types for union field source.

  // Union field config can be only one of the following:
  "nearestNeighborSearchConfig": value,
  "presets": {
    object (Presets)
  }
  // End of list of possible types for union field config.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                                                                                                       |
|-------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `neighborCount`                                                   | `integer` The number of neighbors to return when querying for examples.                                                                                                                                                                                                                                                                                               |
| Union field `source` . `source` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                       |
| `exampleGcsSource`                                                | `object ( `[`ExampleGcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ExampleGcsSource)` )` The Cloud Storage input instances.                                                                                                                                                            |
| Union field `config` . `config` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                       |
| `nearestNeighborSearchConfig`                                     | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` The full configuration for the generated index, the semantics are the same as `metadata` and should match [NearestNeighborSearchConfig](https://cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations-example-based#nearest-neighbor-search-config) . |
| `presets`                                                         | `object ( `[`Presets`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Presets)` )` Simplified preset configuration, which automatically sets configuration values based on the desired query speed-precision trade-off and modality.                                                               |

### ExampleGcsSource

**JSON representation**

```
{
  "dataFormat": enum (DataFormat),
  "gcsSource": {
    object (GcsSource)
  }
}
```

| Fields       |                                                                                                                                                                                                                                                                                          |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataFormat` | `enum ( `[`DataFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.DataFormat)` )` The format in which instances are given, if not specified, assume it's JSONL format. Currently only JSONL format is supported. |
| `gcsSource`  | `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.GcsSource)` )` The Cloud Storage location for the input instances.                                                                            |

### GcsSource

**JSON representation**

```
{
  "uris": [
    string
  ]
}
```

| Fields   |                                                                                                                                                                                         |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uris[]` | `string` Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see <https://cloud.google.com/storage/docs/wildcards> . |

### Presets

**JSON representation**

```
{
  "modality": enum (Modality),

  // Union field _query can be only one of the following:
  "query": enum (Query)
  // End of list of possible types for union field _query.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `modality`                                                        | `enum ( `[`Modality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Modality)` )` The modality of the uploaded model, which automatically configures the distance measurement and feature normalization for the underlying example index and queries. If your model does not precisely fit one of these types, it is okay to choose the closest type. |
| Union field `_query` . `_query` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `query`                                                           | `enum ( `[`Query`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Query)` )` Preset option controlling parameters for speed-precision trade-off when querying for examples. If omitted, defaults to `PRECISE` .                                                                                                                                        |

### ExplanationMetadata

**JSON representation**

```
{
  "inputs": {
    string: {
      object (InputMetadata)
    },
    ...
  },
  "outputs": {
    string: {
      object (OutputMetadata)
    },
    ...
  },
  "featureAttributionsSchemaUri": string,
  "latentSpaceSource": string
}
```

| Fields                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `inputs`                       | `map (key: string, value: object ( `[`InputMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.InputMetadata)` ))` Required. Map from feature names to feature input metadata. Keys are the name of the features. Values are the specification of the feature. An empty InputMetadata is valid. It describes a text feature which has the name specified as the key in `ExplanationMetadata.inputs` . The baseline of the empty feature is chosen by Agent Platform. For Agent Platform-provided Tensorflow images, the key can be any friendly name of the feature. Once specified, `featureAttributions` are keyed by this key (if not grouped with another feature). For custom images, the key must match with the key in `instance` . An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `outputs`                      | `map (key: string, value: object ( `[`OutputMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.OutputMetadata)` ))` Required. Map from output names to output metadata. For Agent Platform-provided Tensorflow images, keys can be any user defined string that consists of any UTF-8 characters. For custom images, keys are the name of the output field in the prediction to be explained. Currently only one key is allowed. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                                                                                                          |
| `featureAttributionsSchemaUri` | `string` Points to a YAML file stored on Google Cloud Storage describing the format of the `feature attributions` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML tabular Models always have this field populated by Agent Platform. Note: The URI given on output may be different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.                                                                                                                                                                                                                                                                                                                                                                                                    |
| `latentSpaceSource`            | `string` Name of the source to generate embeddings for example based explanations.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### InputsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (InputMetadata)
  }
}
```

| Fields  |                                                                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                          |
| `value` | `object ( `[`InputMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.InputMetadata)` )` |

### InputMetadata

**JSON representation**

```
{
  "inputBaselines": [
    value
  ],
  "inputTensorName": string,
  "encoding": enum (Encoding),
  "modality": string,
  "featureValueDomain": {
    object (FeatureValueDomain)
  },
  "indicesTensorName": string,
  "denseShapeTensorName": string,
  "indexFeatureMapping": [
    string
  ],
  "encodedTensorName": string,
  "encodedBaselines": [
    value
  ],
  "visualization": {
    object (Visualization)
  },
  "groupName": string
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `inputBaselines[]`      | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Baseline inputs for this feature. If no baseline is specified, Agent Platform chooses the baseline for this feature. If multiple baselines are specified, Agent Platform returns the average attributions across them in `Attribution.feature_attributions` . For Agent Platform-provided Tensorflow images (both 1.x and 2.x), the shape of each baseline must match the shape of the input tensor. If a scalar is provided, we broadcast to the same shape as the input tensor. For custom images, the element of the baselines must be in the same format as the feature's input in the `instance` \[\]. The schema of any single instance may be specified via Endpoint's DeployedModels' `Model's` `PredictSchemata's` `instance_schema_uri` . |
| `inputTensorName`       | `string` Name of the input tensor for this feature. Required and is only applicable to Agent Platform-provided images for Tensorflow.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `encoding`              | `enum ( `[`Encoding`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Encoding)` )` Defines how the feature is encoded into the input tensor. Defaults to IDENTITY.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `modality`              | `string` Modality of the feature. Valid values are: numeric, image. Defaults to numeric.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `featureValueDomain`    | `object ( `[`FeatureValueDomain`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.FeatureValueDomain)` )` The domain details of the input feature value. Like min/max, original mean or standard deviation if normalized.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `indicesTensorName`     | `string` Specifies the index of the values of the input tensor. Required when the input tensor is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `denseShapeTensorName`  | `string` Specifies the shape of the values of the input if the input is a sparse representation. Refer to Tensorflow documentation for more details: <https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor> .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `indexFeatureMapping[]` | `string` A list of feature names for each index in the input tensor. Required when the input `InputMetadata.encoding` is BAG_OF_FEATURES, BAG_OF_FEATURES_SPARSE, INDICATOR.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `encodedTensorName`     | `string` Encoded tensor is a transformation of the input tensor. Must be provided if choosing `Integrated Gradients attribution` or `XRAI attribution` and the input tensor is not differentiable. An encoded tensor is generated if the input tensor is encoded by a lookup table.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `encodedBaselines[]`    | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` A list of baselines for the encoded tensor. The shape of each baseline should match the shape of the encoded tensor. If a scalar is provided, Agent Platform broadcasts to the same shape as the encoded tensor.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `visualization`         | `object ( `[`Visualization`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Visualization)` )` Visualization configurations for image explanation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `groupName`             | `string` Name of the group that the input belongs to. Features with the same group name will be treated as one feature when computing attributions. Features grouped together can have different shapes in value. If provided, there will be one single attribution generated in `Attribution.feature_attributions` , keyed by the group name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

### FeatureValueDomain

**JSON representation**

```
{
  "minValue": number,
  "maxValue": number,
  "originalMean": number,
  "originalStddev": number
}
```

| Fields           |                                                                                                                                                                               |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `minValue`       | `number` The minimum permissible value for this feature.                                                                                                                      |
| `maxValue`       | `number` The maximum permissible value for this feature.                                                                                                                      |
| `originalMean`   | `number` If this input feature has been normalized to a mean value of 0, the original_mean specifies the mean value of the domain prior to normalization.                     |
| `originalStddev` | `number` If this input feature has been normalized to a standard deviation of 1.0, the original_stddev specifies the standard deviation of the domain prior to normalization. |

### Visualization

**JSON representation**

```
{
  "type": enum (Type),
  "polarity": enum (Polarity),
  "colorMap": enum (ColorMap),
  "clipPercentUpperbound": number,
  "clipPercentLowerbound": number,
  "overlayType": enum (OverlayType)
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`                  | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Type)` )` Type of the image visualization. Only applicable to `Integrated Gradients attribution` . OUTLINES shows regions of attribution, while PIXELS shows per-pixel attribution. Defaults to OUTLINES.                                                                                                                                   |
| `polarity`              | `enum ( `[`Polarity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Polarity)` )` Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.                                                                                                                                                                                                                     |
| `colorMap`              | `enum ( `[`ColorMap`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ColorMap)` )` The color scheme used for the highlighted areas. Defaults to PINK_GREEN for `Integrated Gradients attribution` , which shows positive attributions in green and negative in pink. Defaults to VIRIDIS for `XRAI attribution` , which highlights the most influential regions in yellow and the least influential in blue. |
| `clipPercentUpperbound` | `number` Excludes attributions above the specified percentile from the highlighted areas. Using the clip_percent_upperbound and clip_percent_lowerbound together can be useful for filtering out noise and making it easier to see areas of strong attribution. Defaults to 99.9.                                                                                                                                                                                               |
| `clipPercentLowerbound` | `number` Excludes attributions below the specified percentile, from the highlighted areas. Defaults to 62.                                                                                                                                                                                                                                                                                                                                                                      |
| `overlayType`           | `enum ( `[`OverlayType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.OverlayType)` )` How the original image is displayed in the visualization. Adjusting the overlay can help increase visual clarity if the original image makes it difficult to view the visualization. Defaults to NONE.                                                                                                              |

### OutputsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (OutputMetadata)
  }
}
```

| Fields  |                                                                                                                                                                     |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                            |
| `value` | `object ( `[`OutputMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.OutputMetadata)` )` |

### OutputMetadata

**JSON representation**

```
{
  "outputTensorName": string,

  // Union field display_name_mapping can be only one of the following:
  "indexDisplayNameMapping": value,
  "displayNameMappingKey": string
  // End of list of possible types for union field display_name_mapping.
}
```

| Fields                                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `outputTensorName`                                                                                                                                                                                                                                                                  | `string` Name of the output tensor. Required and is only applicable to Agent Platform provided images for Tensorflow.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Union field `display_name_mapping` . Defines how to map `Attribution.output_index` to `Attribution.output_display_name` . If neither of the fields are specified, `Attribution.output_display_name` will not be populated. `display_name_mapping` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `indexDisplayNameMapping`                                                                                                                                                                                                                                                           | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Static mapping between the index and display name. Use this if the outputs are a deterministic n-dimensional array, e.g. a list of scores of all the classes in a pre-defined order for a multi-classification Model. It's not feasible if the outputs are non-deterministic, e.g. the Model produces top-k classes or sort the outputs by their values. The shape of the value must be an n-dimensional array of strings. The number of dimensions must match that of the outputs to be explained. The `Attribution.output_display_name` is populated by locating in the mapping with `Attribution.output_index` . |
| `displayNameMappingKey`                                                                                                                                                                                                                                                             | `string` Specify a field name in the prediction to look for the display name. Use this if the prediction contains the display names for the outputs. The display names in the prediction must have the same shape of the outputs, so that it can be located by `Attribution.output_index` for a specific output.                                                                                                                                                                                                                                                                                                                                                                                                  |

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

### DataStats

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

| Fields                       |                                                                                                                                                                                                                                                                                                                           |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `trainingDataItemsCount`     | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of DataItems that were used for training this Model.                                                                                                                                                                        |
| `validationDataItemsCount`   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of DataItems that were used for validating this Model during training.                                                                                                                                                      |
| `testDataItemsCount`         | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of DataItems that were used for evaluating this Model. If the Model is evaluated multiple times, this will be the number of test DataItems used by the first evaluation. If the Model is not evaluated, the number is 0.    |
| `trainingAnnotationsCount`   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of Annotations that are used for training this Model.                                                                                                                                                                       |
| `validationAnnotationsCount` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of Annotations that are used for validating this Model during training.                                                                                                                                                     |
| `testAnnotationsCount`       | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of Annotations that are used for evaluating this Model. If the Model is evaluated multiple times, this will be the number of test Annotations used by the first evaluation. If the Model is not evaluated, the number is 0. |

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

### ModelSourceInfo

**JSON representation**

```
{
  "sourceType": enum (ModelSourceType),
  "copy": boolean
}
```

| Fields       |                                                                                                                                                                                               |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `sourceType` | `enum ( `[`ModelSourceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ModelSourceType)` )` Type of the model source. |
| `copy`       | `boolean` If this Model is copy of another Model. If true then `source_type` pertains to the original.                                                                                        |

### OriginalModelInfo

**JSON representation**

```
{
  "model": string
}
```

| Fields  |                                                                                                                                                                                        |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `model` | `string` Output only. The resource name of the Model this Model is a copy of, including the revision. Format: `projects/{project}/locations/{location}/models/{model_id}@{version_id}` |

### BaseModelSource

**JSON representation**

```
{

  // Union field source can be only one of the following:
  "modelGardenSource": {
    object (ModelGardenSource)
  },
  "genieSource": {
    object (GenieSource)
  }
  // End of list of possible types for union field source.
}
```

| Fields                                                            |                                                                                                                                                                                                                      |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `source` . `source` can be only one of the following: |                                                                                                                                                                                                                      |
| `modelGardenSource`                                               | `object ( `[`ModelGardenSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.ModelGardenSource)` )` Source information of Model Garden models. |
| `genieSource`                                                     | `object ( `[`GenieSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.GenieSource)` )` Information about the base model of Genie models.      |

### ModelGardenSource

**JSON representation**

```
{
  "publicModelName": string,
  "versionId": string,
  "skipHfModelCache": boolean
}
```

| Fields             |                                                                           |
|--------------------|---------------------------------------------------------------------------|
| `publicModelName`  | `string` Required. The model garden source model resource name.           |
| `versionId`        | `string` Optional. The model garden source model version ID.              |
| `skipHfModelCache` | `boolean` Optional. Whether to avoid pulling the model from the HF cache. |

### GenieSource

**JSON representation**

```
{
  "baseModelUri": string
}
```

| Fields         |                                               |
|----------------|-----------------------------------------------|
| `baseModelUri` | `string` Required. The public base model URI. |

### Checkpoint

**JSON representation**

```
{
  "checkpointId": string,
  "epoch": string,
  "step": string
}
```

| Fields         |                                                                                                                     |
|----------------|---------------------------------------------------------------------------------------------------------------------|
| `checkpointId` | `string` The ID of the checkpoint.                                                                                  |
| `epoch`        | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The epoch of the checkpoint. |
| `step`         | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The step of the checkpoint.  |

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### ExportableContent

The Model content that can be exported.

| Enums                            |                                                                                                                                                                                                |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `EXPORTABLE_CONTENT_UNSPECIFIED` | Should not be used.                                                                                                                                                                            |
| `ARTIFACT`                       | Model artifact and any of its supported files. Will be exported to the location specified by the `artifactDestination` field of the `ExportModelRequest.output_config` object.                 |
| `IMAGE`                          | The container image that is to be used when deploying this Model. Will be exported to the location specified by the `imageDestination` field of the `ExportModelRequest.output_config` object. |

### DeploymentResourcesType

Identifies a type of Model's prediction resources.

| Enums                                   |                                                                                                                    |
|-----------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| `DEPLOYMENT_RESOURCES_TYPE_UNSPECIFIED` | Should not be used.                                                                                                |
| `DEDICATED_RESOURCES`                   | Resources that are dedicated to the `DeployedModel` , and that need a higher degree of manual configuration.       |
| `AUTOMATIC_RESOURCES`                   | Resources that to large degree are decided by Agent Platform, and require only a modest additional configuration.  |
| `SHARED_RESOURCES`                      | Resources that can be shared by multiple `DeployedModels` . A pre-configured `DeploymentResourcePool` is required. |

### DataFormat

The format of the input example instances.

| Enums                     |                                      |
|---------------------------|--------------------------------------|
| `DATA_FORMAT_UNSPECIFIED` | Format unspecified, used when unset. |
| `JSONL`                   | Examples are stored in JSONL files.  |

### Query

Preset option controlling parameters for query speed-precision trade-off

| Enums     |                                                                |
|-----------|----------------------------------------------------------------|
| `PRECISE` | More precise neighbors as a trade-off against slower response. |
| `FAST`    | Faster response as a trade-off against less precise neighbors. |

### Modality

Preset option controlling parameters for different modalities

| Enums                  |                                                                   |
|------------------------|-------------------------------------------------------------------|
| `MODALITY_UNSPECIFIED` | Should not be set. Added as a recommended best practice for enums |
| `IMAGE`                | IMAGE modality                                                    |
| `TEXT`                 | TEXT modality                                                     |
| `TABULAR`              | TABULAR modality                                                  |

### Encoding

Defines how a feature is encoded. Defaults to IDENTITY.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>ENCODING_UNSPECIFIED</code></td>
<td>Default value. This is the same as IDENTITY.</td>
</tr>
<tr class="even">
<td><code>IDENTITY</code></td>
<td>The tensor represents one feature.</td>
</tr>
<tr class="odd">
<td><code>BAG_OF_FEATURES</code></td>
<td><p>The tensor represents a bag of features where each index maps to a feature. <code>InputMetadata.index_feature_mapping</code> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [27, 6.0, 150]
index_feature_mapping = [&quot;age&quot;, &quot;height&quot;, &quot;weight&quot;]</code></pre></td>
</tr>
<tr class="even">
<td><code>BAG_OF_FEATURES_SPARSE</code></td>
<td><p>The tensor represents a bag of features where each index maps to a feature. Zero values in the tensor indicates feature being non-existent. <code>InputMetadata.index_feature_mapping</code> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [2, 0, 5, 0, 1]
index_feature_mapping = [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;, &quot;e&quot;]</code></pre></td>
</tr>
<tr class="odd">
<td><code>INDICATOR</code></td>
<td><p>The tensor is a list of binaries representing whether a feature exists or not (1 indicates existence). <code>InputMetadata.index_feature_mapping</code> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [1, 0, 1, 0, 1]
index_feature_mapping = [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;, &quot;e&quot;]</code></pre></td>
</tr>
<tr class="even">
<td><code>COMBINED_EMBEDDING</code></td>
<td><p>The tensor is encoded into a 1-dimensional array represented by an encoded tensor. <code>InputMetadata.encoded_tensor_name</code> must be provided for this encoding. For example:</p>
<pre data-fenced=""><code>input = [&quot;This&quot;, &quot;is&quot;, &quot;a&quot;, &quot;test&quot;, &quot;.&quot;]
encoded = [0.1, 0.2, 0.3, 0.4, 0.5]</code></pre></td>
</tr>
<tr class="odd">
<td><code>CONCAT_EMBEDDING</code></td>
<td><p>Select this encoding when the input tensor is encoded into a 2-dimensional array represented by an encoded tensor. <code>InputMetadata.encoded_tensor_name</code> must be provided for this encoding. The first dimension of the encoded tensor's shape is the same as the input tensor's shape. For example:</p>
<pre data-fenced=""><code>input = [&quot;This&quot;, &quot;is&quot;, &quot;a&quot;, &quot;test&quot;, &quot;.&quot;]
encoded = [[0.1, 0.2, 0.3, 0.4, 0.5],
           [0.2, 0.1, 0.4, 0.3, 0.5],
           [0.5, 0.1, 0.3, 0.5, 0.4],
           [0.5, 0.3, 0.1, 0.2, 0.4],
           [0.4, 0.3, 0.2, 0.5, 0.1]]</code></pre></td>
</tr>
</tbody>
</table>

### Type

Type of the image visualization. Only applicable to `Integrated Gradients attribution` .

| Enums              |                                                                                 |
|--------------------|---------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED` | Should not be used.                                                             |
| `PIXELS`           | Shows which pixel contributed to the image prediction.                          |
| `OUTLINES`         | Shows which region contributed to the image prediction by outlining the region. |

### Polarity

Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.

| Enums                  |                                                                                                      |
|------------------------|------------------------------------------------------------------------------------------------------|
| `POLARITY_UNSPECIFIED` | Default value. This is the same as POSITIVE.                                                         |
| `POSITIVE`             | Highlights the pixels/outlines that were most influential to the model's prediction.                 |
| `NEGATIVE`             | Setting polarity to negative highlights areas that does not lead to the models's current prediction. |
| `BOTH`                 | Shows both positive and negative attributions.                                                       |

### ColorMap

The color scheme used for highlighting areas.

| Enums                   |                                                                                                                                                                                            |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `COLOR_MAP_UNSPECIFIED` | Should not be used.                                                                                                                                                                        |
| `PINK_GREEN`            | Positive: green. Negative: pink.                                                                                                                                                           |
| `VIRIDIS`               | Viridis color map: A perceptually uniform color mapping which is easier to see by those with colorblindness and progresses from yellow to green to blue. Positive: yellow. Negative: blue. |
| `RED`                   | Positive: red. Negative: red.                                                                                                                                                              |
| `GREEN`                 | Positive: green. Negative: green.                                                                                                                                                          |
| `RED_GREEN`             | Positive: green. Negative: red.                                                                                                                                                            |
| `PINK_WHITE_GREEN`      | PiYG palette.                                                                                                                                                                              |

### OverlayType

How the original image is displayed in the visualization.

| Enums                      |                                                                                                               |
|----------------------------|---------------------------------------------------------------------------------------------------------------|
| `OVERLAY_TYPE_UNSPECIFIED` | Default value. This is the same as NONE.                                                                      |
| `NONE`                     | No overlay.                                                                                                   |
| `ORIGINAL`                 | The attributions are shown on top of the original image.                                                      |
| `GRAYSCALE`                | The attributions are shown on top of grayscaled version of the original image.                                |
| `MASK_BLACK`               | The attributions are used as a mask to reveal predictive parts of the image and hide the un-predictive parts. |

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

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
