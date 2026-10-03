---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes
title: 'REST Resource: projects.locations.indexes'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Index

A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search.

Fields

`name` `string`

Output only. The resource name of the Index.

`displayName` `string`

Required. The display name of the Index. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

The description of the Index.

`metadataSchemaUri` `string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Index, that is specific to it. Unset if the Index does not have any additional information. The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`metadata` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

An additional information about the Index; the schema of the metadata can be found in [`metadataSchema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes#Index.FIELDS.metadata_schema_uri) .

`deployedIndexes[]` `object ( `[`DeployedIndexRef`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes#DeployedIndexRef)` )`

Output only. The pointers to DeployedIndexes created from this Index. An Index can be only deleted if all its DeployedIndexes had been undeployed first.

`etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your Indexes.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Index was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Index was most recently updated. This also includes any update to the contents of the Index. Note that Operations working on this Index may have their [`Operations.metadata.generic_metadata.update_time`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenericOperationMetadata#FIELDS.update_time) a little after the value of this timestamp, yet that does not mean their results are not already reflected in the Index. result of any successfully completed Operation on the Index is reflected in it.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`indexStats` `object ( `[`IndexStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes#IndexStats)` )`

Output only. Stats of the index resource.

`indexUpdateMethod` `enum ( `[`IndexUpdateMethod`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes#IndexUpdateMethod)` )`

Immutable. The update method to use with this Index. If not set, BATCH_UPDATE will be used by default.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec)` )`

Immutable. Customer-managed encryption key spec for an Index. If set, this Index and all sub-resources of this Index will be secured by this key.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "metadataSchemaUri": string,
  "metadata": value,
  "deployedIndexes": [
    {
      object (DeployedIndexRef)
    }
  ],
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "indexStats": {
    object (IndexStats)
  },
  "indexUpdateMethod": enum (IndexUpdateMethod),
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean
}
```

## DeployedIndexRef

Points to a DeployedIndex.

Fields

`indexEndpoint` `string`

Immutable. A resource name of the IndexEndpoint.

`deployedIndexId` `string`

Immutable. The id of the DeployedIndex in the above IndexEndpoint.

`displayName` `string`

Output only. The display name of the DeployedIndex.

**JSON representation**

```
{
  "indexEndpoint": string,
  "deployedIndexId": string,
  "displayName": string
}
```

## IndexStats

Stats of the Index.

Fields

`vectorsCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The number of dense vectors in the Index.

`sparseVectorsCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The number of sparse vectors in the Index.

`shardsCount` `integer`

Output only. The number of shards in the Index.

**JSON representation**

```
{
  "vectorsCount": string,
  "sparseVectorsCount": string,
  "shardsCount": integer
}
```

## IndexUpdateMethod

The update method of an Index.

| Enums                             |                                                                                                                                                                                 |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `INDEX_UPDATE_METHOD_UNSPECIFIED` | Should not be used.                                                                                                                                                             |
| `BATCH_UPDATE`                    | BatchUpdate: user can call indexes.patch with files on Cloud Storage of Datapoints to update.                                                                                   |
| `STREAM_UPDATE`                   | StreamUpdate: user can call indexes.upsertDatapoints/DeleteDatapoints to update the Index and the updates will be applied in corresponding DeployedIndexes in nearly real-time. |

| Methods                                                                                                                                            |                                      |
|----------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/create)                     | Creates an Index.                    |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/delete)                     | Deletes an Index.                    |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/get)                           | Gets an Index.                       |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/list)                         | Lists Indexes in a Location.         |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/patch)                       | Updates an Index.                    |
| [`removeDatapoints`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/removeDatapoints) | Remove Datapoints from an Index.     |
| [`upsertDatapoints`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.indexes/upsertDatapoints) | Add/update Datapoints into an Index. |
