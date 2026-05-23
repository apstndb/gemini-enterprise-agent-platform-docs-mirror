---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.datasetVersions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.datasetVersions
title: 'REST Resource: projects.locations.datasets.datasetVersions'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: DatasetVersion

Describes the dataset version.

Fields

`name` `string`

Output only. Identifier. The resource name of the DatasetVersion. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{datasetVersion}`

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this DatasetVersion was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this DatasetVersion was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`bigQueryDatasetName` `string`

Output only. name of the associated BigQuery dataset.

`displayName` `string`

The user-defined name of the DatasetVersion. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`metadata` ` value ( Value  ` format)

Required. Output only. Additional information about the DatasetVersion.

`modelReference` `string`

Output only. Reference to the public base model last used by the dataset version. Only set for prompt dataset versions.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;etag&quot;: string,
  &quot;bigQueryDatasetName&quot;: string,
  &quot;displayName&quot;: string,
  &quot;metadata&quot;: value,
  &quot;modelReference&quot;: string,
  &quot;satisfiesPzs&quot;: boolean,
  &quot;satisfiesPzi&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Create a version from a Dataset.

### `            delete           `

Deletes a Dataset version.

### `            get           `

Gets a Dataset version.

### `            list           `

Lists DatasetVersions in a Dataset.

### `            patch           `

Updates a DatasetVersion.

### `            restore           `

Restores a dataset version.
