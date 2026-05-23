---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/update_prompt
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/update_prompt
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `update_prompt`

Updates an existing prompt's fields (display\_name, instructions, settings, or labels). This performs a patch; fields not specified remain unchanged. IMPORTANT: This parameter requires the numeric ID or UUID returned by the list tool, NOT the display name. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `update_prompt` MCP tool.

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
    &quot;name&quot;: &quot;update_prompt&quot;,
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

Request message for `DatasetService.UpdateDataset` .

### UpdateDatasetRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataset&quot;: {object (Dataset)},&quot;updateMask&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataset`

` object ( Dataset  ` )

Required. The Dataset which replaces the resource on the server.

`updateMask`

` string ( FieldMask  ` format)

Required. The update mask applies to the resource. For the `FieldMask` definition, see `  google.protobuf.FieldMask  ` . Updatable fields:

  - `display_name`
  - `description`
  - `labels`

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Dataset

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;metadataSchemaUri&quot;: string,&quot;metadata&quot;: value,&quot;dataItemCount&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;savedQueries&quot;: [{object (SavedQuery)}],&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;metadataArtifact&quot;: string,&quot;modelReference&quot;: string,&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. Identifier. The resource name of the Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

`displayName`

`string`

Required. The user-defined name of the Dataset. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description`

`string`

The description of the Dataset.

`metadataSchemaUri`

`string`

Required. Points to a YAML file stored on Google Cloud Storage describing additional information about the Dataset. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/metadata/.

`metadata`

` value ( Value  ` format)

Required. Additional information about the Dataset.

`dataItemCount`

`string ( int64 format)`

Output only. The number of DataItems in this Dataset. Only apply for non-structured Dataset.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Dataset was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Dataset was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag`

`string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize your Datasets.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Dataset:

  - "aiplatform.googleapis.com/dataset\_metadata\_schema": output only, its value is the `metadata_schema's` title.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`savedQueries[]`

` object ( SavedQuery  ` )

All SavedQueries belong to the Dataset will be returned in List/Get Dataset response. The annotation\_specs field will not be populated except for UI cases which will only use `annotation_spec_count` . In CreateDataset request, a SavedQuery is created together if this field is set, up to one SavedQuery can be set in CreateDatasetRequest. The SavedQuery should not contain any AnnotationSpec.

`encryptionSpec`

` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for a Dataset. If set, this Dataset and all sub-resources of this Dataset will be secured by this key.

`metadataArtifact`

`string`

Output only. The resource name of the Artifact that was created in MetadataStore when creating the Dataset. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}` .

`modelReference`

`string`

Optional. Reference to the public base model last used by the dataset. Only set for prompt datasets.

`satisfiesPzs`

`boolean`

Output only. Reserved for future use.

`satisfiesPzi`

`boolean`

Output only. Reserved for future use.

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

### SavedQuery

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
  &quot;metadata&quot;: value,
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;annotationFilter&quot;: string,
  &quot;problemType&quot;: string,
  &quot;annotationSpecCount&quot;: integer,
  &quot;etag&quot;: string,
  &quot;supportAutomlTraining&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. Resource name of the SavedQuery.

`displayName`

`string`

Required. The user-defined name of the SavedQuery. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`metadata`

` value ( Value  ` format)

Some additional information about the SavedQuery.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this SavedQuery was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when SavedQuery was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`annotationFilter`

`string`

Output only. Filters on the Annotations in the dataset.

`problemType`

`string`

Required. Problem type of the SavedQuery. Allowed values:

  - IMAGE\_CLASSIFICATION\_SINGLE\_LABEL
  - IMAGE\_CLASSIFICATION\_MULTI\_LABEL
  - IMAGE\_BOUNDING\_POLY
  - IMAGE\_BOUNDING\_BOX
  - TEXT\_CLASSIFICATION\_SINGLE\_LABEL
  - TEXT\_CLASSIFICATION\_MULTI\_LABEL
  - TEXT\_EXTRACTION
  - TEXT\_SENTIMENT
  - VIDEO\_CLASSIFICATION
  - VIDEO\_OBJECT\_TRACKING

`annotationSpecCount`

`integer`

Output only. Number of AnnotationSpecs in the context of the SavedQuery.

`etag`

`string`

Used to perform a consistent read-modify-write update. If not set, a blind "overwrite" update happens.

`supportAutomlTraining`

`boolean`

Output only. If the Annotations belonging to the SavedQuery can be used for AutoML training.

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

A collection of DataItems and Annotations on them.

### Dataset

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;metadataSchemaUri&quot;: string,&quot;metadata&quot;: value,&quot;dataItemCount&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;savedQueries&quot;: [{object (SavedQuery)}],&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;metadataArtifact&quot;: string,&quot;modelReference&quot;: string,&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. Identifier. The resource name of the Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

`displayName`

`string`

Required. The user-defined name of the Dataset. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description`

`string`

The description of the Dataset.

`metadataSchemaUri`

`string`

Required. Points to a YAML file stored on Google Cloud Storage describing additional information about the Dataset. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/metadata/.

`metadata`

` value ( Value  ` format)

Required. Additional information about the Dataset.

`dataItemCount`

`string ( int64 format)`

Output only. The number of DataItems in this Dataset. Only apply for non-structured Dataset.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Dataset was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this Dataset was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag`

`string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize your Datasets.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Dataset:

  - "aiplatform.googleapis.com/dataset\_metadata\_schema": output only, its value is the `metadata_schema's` title.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`savedQueries[]`

` object ( SavedQuery  ` )

All SavedQueries belong to the Dataset will be returned in List/Get Dataset response. The annotation\_specs field will not be populated except for UI cases which will only use `annotation_spec_count` . In CreateDataset request, a SavedQuery is created together if this field is set, up to one SavedQuery can be set in CreateDatasetRequest. The SavedQuery should not contain any AnnotationSpec.

`encryptionSpec`

` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for a Dataset. If set, this Dataset and all sub-resources of this Dataset will be secured by this key.

`metadataArtifact`

`string`

Output only. The resource name of the Artifact that was created in MetadataStore when creating the Dataset. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}` .

`modelReference`

`string`

Optional. Reference to the public base model last used by the dataset. Only set for prompt datasets.

`satisfiesPzs`

`boolean`

Output only. Reserved for future use.

`satisfiesPzi`

`boolean`

Output only. Reserved for future use.

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

### SavedQuery

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
  &quot;metadata&quot;: value,
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;annotationFilter&quot;: string,
  &quot;problemType&quot;: string,
  &quot;annotationSpecCount&quot;: integer,
  &quot;etag&quot;: string,
  &quot;supportAutomlTraining&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. Resource name of the SavedQuery.

`displayName`

`string`

Required. The user-defined name of the SavedQuery. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`metadata`

` value ( Value  ` format)

Some additional information about the SavedQuery.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this SavedQuery was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when SavedQuery was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`annotationFilter`

`string`

Output only. Filters on the Annotations in the dataset.

`problemType`

`string`

Required. Problem type of the SavedQuery. Allowed values:

  - IMAGE\_CLASSIFICATION\_SINGLE\_LABEL
  - IMAGE\_CLASSIFICATION\_MULTI\_LABEL
  - IMAGE\_BOUNDING\_POLY
  - IMAGE\_BOUNDING\_BOX
  - TEXT\_CLASSIFICATION\_SINGLE\_LABEL
  - TEXT\_CLASSIFICATION\_MULTI\_LABEL
  - TEXT\_EXTRACTION
  - TEXT\_SENTIMENT
  - VIDEO\_CLASSIFICATION
  - VIDEO\_OBJECT\_TRACKING

`annotationSpecCount`

`integer`

Output only. Number of AnnotationSpecs in the context of the SavedQuery.

`etag`

`string`

Used to perform a consistent read-modify-write update. If not set, a blind "overwrite" update happens.

`supportAutomlTraining`

`boolean`

Output only. If the Annotations belonging to the SavedQuery can be used for AutoML training.

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

### Tool Annotations

Destructive Hint: ✅ | Idempotent Hint: ✅ | Read Only Hint: ❌ | Open World Hint: ❌
