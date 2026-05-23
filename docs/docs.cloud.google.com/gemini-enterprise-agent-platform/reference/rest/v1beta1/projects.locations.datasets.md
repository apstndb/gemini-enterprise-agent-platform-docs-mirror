---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets
title: 'REST Resource: projects.locations.datasets'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Dataset

A collection of DataItems and Annotations on them.

Fields

`name` `string`

Output only. Identifier. The resource name of the Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

`displayName` `string`

Required. The user-defined name of the Dataset. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

The description of the Dataset.

`metadataSchemaUri` `string`

Required. Points to a YAML file stored on Google Cloud Storage describing additional information about the Dataset. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/metadata/.

`metadata` ` value ( Value  ` format)

Required. Additional information about the Dataset.

`dataItemCount` `string ( int64 format)`

Output only. The number of DataItems in this Dataset. Only apply for non-structured Dataset.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Dataset was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Dataset was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your Datasets.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Dataset (System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each Dataset:

  - "aiplatform.googleapis.com/dataset\_metadata\_schema": output only, its value is the `  metadataSchema's  ` title.

`savedQueries[]` ` object ( SavedQuery  ` )

All SavedQueries belong to the Dataset will be returned in List/Get Dataset response. The annotationSpecs field will not be populated except for UI cases which will only use `  annotationSpecCount  ` . In datasets.create request, a SavedQuery is created together if this field is set, up to one SavedQuery can be set in CreateDatasetRequest. The SavedQuery should not contain any AnnotationSpec.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for a Dataset. If set, this Dataset and all sub-resources of this Dataset will be secured by this key.

`metadataArtifact` `string`

Output only. The resource name of the Artifact that was created in MetadataStore when creating the Dataset. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadataStore}/artifacts/{artifact}` .

`modelReference` `string`

Optional. Reference to the public base model last used by the dataset. Only set for prompt datasets.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;metadataSchemaUri&quot;: string,&quot;metadata&quot;: value,&quot;dataItemCount&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;savedQueries&quot;: [{object (SavedQuery)}],&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;metadataArtifact&quot;: string,&quot;modelReference&quot;: string,&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## SavedQuery

A SavedQuery is a view of the dataset. It references a subset of annotations by problem type and filters.

Fields

`name` `string`

Output only. Resource name of the SavedQuery.

`displayName` `string`

Required. The user-defined name of the SavedQuery. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`metadata` ` value ( Value  ` format)

Some additional information about the SavedQuery.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this SavedQuery was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when SavedQuery was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`annotationFilter` `string`

Output only. Filters on the Annotations in the dataset.

`problemType` `string`

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

`annotationSpecCount` `integer`

Output only. Number of AnnotationSpecs in the context of the SavedQuery.

`etag` `string`

Used to perform a consistent read-modify-write update. If not set, a blind "overwrite" update happens.

`supportAutomlTraining` `boolean`

Output only. If the Annotations belonging to the SavedQuery can be used for AutoML training.

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

## Methods

### `            assemble           `

Assembles each row of a multimodal dataset and writes the result into a BigQuery table.

### `            assess           `

Assesses the state or validity of the dataset with respect to a given use case.

### `            create           `

Creates a Dataset.

### `            delete           `

Deletes a Dataset.

### `            export           `

Exports data from a Dataset.

### `            get           `

Gets a Dataset.

### `            import           `

Imports data into a Dataset.

### `            list           `

Lists Datasets in a Location.

### `            patch           `

Updates a Dataset.

### `            searchDataItems           `

Searches DataItems in a Dataset.
