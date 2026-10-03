---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_prompts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_prompts
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `list_prompts`

Lists all managed prompts in a location. Use this to browse existing prompts or map a user-friendly display_name to a technical resource name. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `list_prompts` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "list_prompts",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `DatasetService.ListDatasets` .

### ListDatasetsRequest

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
<p>Required. The name of the Dataset's parent resource. Format: <code>projects/{project}/locations/{location}</code></p></td>
</tr>
<tr class="even">
<td><code>filter</code></td>
<td><p><code>string</code></p>
<p>An expression for filtering the results of the request. For field names both snake_case and camelCase are supported.</p>
<ul>
<li><code>display_name</code> : supports = and !=</li>
<li><code>metadata_schema_uri</code> : supports = and !=</li>
<li><code>labels</code> supports general map functions that is:
<ul>
<li><code>labels.key=value</code> - key:value equality</li>
<li>`labels.key:* or labels:key - key existence</li>
<li>A key including a space must be quoted. <code>labels."a key"</code> .</li>
</ul></li>
</ul>
<p>Some examples:</p>
<ul>
<li><code>displayName="myDisplayName"</code></li>
<li><code>labels.myKey="myValue"</code></li>
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
<p>The standard list page token.</p></td>
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
</ul></td>
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

Response message for `DatasetService.ListDatasets` .

### ListDatasetsResponse

**JSON representation**

```
{
  "datasets": [
    {
      object (Dataset)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                                                                             |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `datasets[]`    | `object ( `[`Dataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_prompt#Input.Schema.Dataset)` )` A list of Datasets that matches the specified filter in the request. |
| `nextPageToken` | `string` The standard List next-page token.                                                                                                                                                                                 |

### Dataset

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "metadataSchemaUri": string,
  "metadata": value,
  "dataItemCount": string,
  "createTime": string,
  "updateTime": string,
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "savedQueries": [
    {
      object (SavedQuery)
    }
  ],
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "metadataArtifact": string,
  "modelReference": string,
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean
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
<p>Output only. Identifier. The resource name of the Dataset. Format: <code>projects/{project}/locations/{location}/datasets/{dataset}</code></p></td>
</tr>
<tr class="even">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>Required. The user-defined name of the Dataset. The name can be up to 128 characters long and can consist of any UTF-8 characters.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>The description of the Dataset.</p></td>
</tr>
<tr class="even">
<td><code>metadataSchemaUri</code></td>
<td><p><code>string</code></p>
<p>Required. Points to a YAML file stored on Google Cloud Storage describing additional information about the Dataset. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/metadata/.</p></td>
</tr>
<tr class="odd">
<td><code>metadata</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>Required. Additional information about the Dataset.</p></td>
</tr>
<tr class="even">
<td><code>dataItemCount</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. The number of DataItems in this Dataset. Only apply for non-structured Dataset.</p></td>
</tr>
<tr class="odd">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this Dataset was created.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>updateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this Dataset was last updated.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>etag</code></td>
<td><p><code>string</code></p>
<p>Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>The labels with user-defined metadata to organize your Datasets.</p>
<p>Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded).</p>
<p>See <a href="https://goo.gl/xmQnxf">https://goo.gl/xmQnxf</a> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Dataset:</p>
<ul>
<li>"aiplatform.googleapis.com/dataset_metadata_schema": output only, its value is the <code>metadata_schema's</code> title.</li>
</ul>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>savedQueries[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_prompt#Input.Schema.SavedQuery"><code>SavedQuery</code></a><code> )</code></p>
<p>All SavedQueries belong to the Dataset will be returned in List/Get Dataset response. The annotation_specs field will not be populated except for UI cases which will only use <code>annotation_spec_count</code> . In CreateDataset request, a SavedQuery is created together if this field is set, up to one SavedQuery can be set in CreateDatasetRequest. The SavedQuery should not contain any AnnotationSpec.</p></td>
</tr>
<tr class="even">
<td><code>encryptionSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Input.Schema.EncryptionSpec"><code>EncryptionSpec</code></a><code> )</code></p>
<p>Customer-managed encryption key spec for a Dataset. If set, this Dataset and all sub-resources of this Dataset will be secured by this key.</p></td>
</tr>
<tr class="odd">
<td><code>metadataArtifact</code></td>
<td><p><code>string</code></p>
<p>Output only. The resource name of the Artifact that was created in MetadataStore when creating the Dataset. The Artifact resource name pattern is <code>projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}</code> .</p></td>
</tr>
<tr class="even">
<td><code>modelReference</code></td>
<td><p><code>string</code></p>
<p>Optional. Reference to the public base model last used by the dataset. Only set for prompt datasets.</p></td>
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

### SavedQuery

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "metadata": value,
  "createTime": string,
  "updateTime": string,
  "annotationFilter": string,
  "problemType": string,
  "annotationSpecCount": integer,
  "etag": string,
  "supportAutomlTraining": boolean
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
<p>Output only. Resource name of the SavedQuery.</p></td>
</tr>
<tr class="even">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>Required. The user-defined name of the SavedQuery. The name can be up to 128 characters long and can consist of any UTF-8 characters.</p></td>
</tr>
<tr class="odd">
<td><code>metadata</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>Some additional information about the SavedQuery.</p></td>
</tr>
<tr class="even">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this SavedQuery was created.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>updateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when SavedQuery was last updated.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>annotationFilter</code></td>
<td><p><code>string</code></p>
<p>Output only. Filters on the Annotations in the dataset.</p></td>
</tr>
<tr class="odd">
<td><code>problemType</code></td>
<td><p><code>string</code></p>
<p>Required. Problem type of the SavedQuery. Allowed values:</p>
<ul>
<li>IMAGE_CLASSIFICATION_SINGLE_LABEL</li>
<li>IMAGE_CLASSIFICATION_MULTI_LABEL</li>
<li>IMAGE_BOUNDING_POLY</li>
<li>IMAGE_BOUNDING_BOX</li>
<li>TEXT_CLASSIFICATION_SINGLE_LABEL</li>
<li>TEXT_CLASSIFICATION_MULTI_LABEL</li>
<li>TEXT_EXTRACTION</li>
<li>TEXT_SENTIMENT</li>
<li>VIDEO_CLASSIFICATION</li>
<li>VIDEO_OBJECT_TRACKING</li>
</ul></td>
</tr>
<tr class="even">
<td><code>annotationSpecCount</code></td>
<td><p><code>integer</code></p>
<p>Output only. Number of AnnotationSpecs in the context of the SavedQuery.</p></td>
</tr>
<tr class="odd">
<td><code>etag</code></td>
<td><p><code>string</code></p>
<p>Used to perform a consistent read-modify-write update. If not set, a blind "overwrite" update happens.</p></td>
</tr>
<tr class="even">
<td><code>supportAutomlTraining</code></td>
<td><p><code>boolean</code></p>
<p>Output only. If the Annotations belonging to the SavedQuery can be used for AutoML training.</p></td>
</tr>
</tbody>
</table>

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

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
