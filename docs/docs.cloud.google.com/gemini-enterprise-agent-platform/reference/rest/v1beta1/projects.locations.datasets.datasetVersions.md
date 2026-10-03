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

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this DatasetVersion was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this DatasetVersion was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`bigQueryDatasetName` `string`

Output only. name of the associated BigQuery dataset.

`displayName` `string`

The user-defined name of the DatasetVersion. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`metadata` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Required. Output only. Additional information about the DatasetVersion.

`modelReference` `string`

Output only. Reference to the public base model last used by the dataset version. Only set for prompt dataset versions.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

**JSON representation**

```
{
  "name": string,
  "createTime": string,
  "updateTime": string,
  "etag": string,
  "bigQueryDatasetName": string,
  "displayName": string,
  "metadata": value,
  "modelReference": string,
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean
}
```

| Methods                                                                                                                                                |                                     |
|--------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.datasetVersions/create)   | Create a version from a Dataset.    |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.datasetVersions/delete)   | Deletes a Dataset version.          |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.datasetVersions/get)         | Gets a Dataset version.             |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.datasetVersions/list)       | Lists DatasetVersions in a Dataset. |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.datasetVersions/patch)     | Updates a DatasetVersion.           |
| [`restore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.datasetVersions/restore) | Restores a dataset version.         |
