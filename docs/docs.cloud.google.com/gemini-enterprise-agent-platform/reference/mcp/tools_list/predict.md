---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/predict
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/predict
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `predict`

Perform online predictions for a wide range of machine learning models. Use this to get real-time inference results from your deployed models on Agent Platform.

The following sample demonstrate how to use `curl` to invoke the `predict` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "predict",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `PredictionService.Predict` .

### PredictRequest

**JSON representation**

```
{
  "endpoint": string,
  "instances": [
    value
  ],
  "parameters": value,
  "labels": {
    string: string,
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
<td><code>endpoint</code></td>
<td><p><code>string</code></p>
<p>Required. The resource name of the publisher model or endpoint requested to serve the prediction. For Google models like Embedding or Veo, use the publisher model format. For tuned models or other models deployed to an Agent Platform endpoint, use the endpoint format.</p>
<ul>
<li>Publisher model format: <code>projects/{project}/locations/{location}/publishers/google/models/{model}</code></li>
<li>Endpoint format: <code>projects/{project}/locations/{location}/endpoints/{endpoint}</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>instances[]</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behavior is as documented by that Model. The schema of each instance depends on the type of request.</p>
<ul>
<li>For a generative AI request to a Text Embedding model, see <code>TextEmbeddingPredictionInstance</code></li>
<li>For a generative AI request to a Multimodal Embedding model, see <code>VisionEmbeddingModelInstance</code></li>
<li>For a video generation request to a Veo model, see <code>VideoGenerationModelInstance</code></li>
<li>For a traditional machine learning request to a deployed custom model, the schema of any single instance is defined by the model's <code>instanceSchemaUri</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>parameters</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>The parameters that govern the prediction. The schema of the parameters depends on the type of request.</p>
<ul>
<li>For a generative AI request to a Text Embedding model, see <code>TextEmbeddingPredictionParams</code></li>
<li>For a generative AI request to a Multimodal Embedding model, see <code>VisionEmbeddingModelParams</code></li>
<li>For a video generation request to a Veo model, see <code>VideoGenerationModelParams</code></li>
<li>For a traditional machine learning request to a deployed custom model, the schema of the parameters is defined by the model's <code>parametersSchemaUri</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Optional. The user labels for Imagen billing usage only. Only Imagen supports labels. For other use cases, it will be ignored.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
</tbody>
</table>

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

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

## Output Schema

Response message for `PredictionService.Predict` .

### PredictResponse

**JSON representation**

```
{
  "predictions": [
    value
  ],
  "deployedModelId": string,
  "model": string,
  "modelVersionId": string,
  "modelDisplayName": string,
  "metadata": value
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
<td><code>predictions[]</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>The predictions that are the output of the predictions call. The schema of each prediction depends on the type of request.</p>
<ul>
<li>For a generative AI request to a Text Embedding model, see <code>TextEmbeddingPredictionResult</code></li>
<li>For a generative AI request to a Multimodal Embedding model, see <code>VisionEmbeddingModelResult</code></li>
<li>For a video generation request to a Veo model, see <code>VideoGenerationModelResult</code></li>
<li>For a traditional machine learning request to a deployed custom model, the schema of each prediction is defined by the model's <code>predictionSchemaUri</code> .</li>
</ul></td>
</tr>
<tr class="even">
<td><code>deployedModelId</code></td>
<td><p><code>string</code></p>
<p>ID of the Endpoint's DeployedModel that served this prediction.</p></td>
</tr>
<tr class="odd">
<td><code>model</code></td>
<td><p><code>string</code></p>
<p>Output only. The resource name of the Model which is deployed as the DeployedModel that this prediction hits.</p></td>
</tr>
<tr class="even">
<td><code>modelVersionId</code></td>
<td><p><code>string</code></p>
<p>Output only. The version ID of the Model which is deployed as the DeployedModel that this prediction hits.</p></td>
</tr>
<tr class="odd">
<td><code>modelDisplayName</code></td>
<td><p><code>string</code></p>
<p>Output only. The <code>display name</code> of the Model which is deployed as the DeployedModel that this prediction hits.</p></td>
</tr>
<tr class="even">
<td><code>metadata</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>Output only. Request-level metadata returned by the model. The metadata type will be dependent upon the model implementation.</p></td>
</tr>
</tbody>
</table>

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

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ✅
