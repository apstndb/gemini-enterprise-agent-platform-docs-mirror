---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores
title: 'REST Resource: projects.locations.metadataStores'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: MetadataStore

Instance of a metadata store. Contains a set of metadata that can be queried.

Fields

`name` `string`

Output only. The resource name of the MetadataStore instance.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this MetadataStore was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this MetadataStore was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec)` )`

Customer-managed encryption key spec for a metadata Store. If set, this metadata Store and all sub-resources of this metadata Store are secured using this key.

`description` `string`

description of the MetadataStore.

`state` `object ( `[`MetadataStoreState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores#MetadataStoreState)` )`

Output only. state information of the MetadataStore.

`dataplexConfig` `object ( `[`DataplexConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores#DataplexConfig)` )`

Optional. Dataplex integration settings.

**JSON representation**

```
{
  "name": string,
  "createTime": string,
  "updateTime": string,
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "description": string,
  "state": {
    object (MetadataStoreState)
  },
  "dataplexConfig": {
    object (DataplexConfig)
  }
}
```

## MetadataStoreState

Represents state information for a MetadataStore.

Fields

`diskUtilizationBytes` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The disk utilization of the MetadataStore in bytes.

**JSON representation**

```
{
  "diskUtilizationBytes": string
}
```

## DataplexConfig

Represents Dataplex integration settings.

Fields

`enabledPipelinesLineage` `boolean`

Optional. Whether or not data Lineage synchronization is enabled for Vertex Pipelines.

**JSON representation**

```
{
  "enabledPipelinesLineage": boolean
}
```

| Methods                                                                                                                               |                                                                                                   |
|---------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/create) | Initializes a MetadataStore, including allocation of resources.                                   |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/delete) | Deletes a single MetadataStore and all its child resources (Artifacts, Executions, and Contexts). |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/get)       | Retrieves a specific MetadataStore.                                                               |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores/list)     | Lists MetadataStores for a Location.                                                              |
