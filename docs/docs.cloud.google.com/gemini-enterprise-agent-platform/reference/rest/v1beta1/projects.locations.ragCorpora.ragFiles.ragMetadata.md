---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata
title: 'REST Resource: projects.locations.ragCorpora.ragFiles.ragMetadata'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: RagMetadata

metadata for RagFile provided by users.

Fields

`name` `string`

Identifier. Resource name of the RagMetadata. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}/ragFiles/{ragFile}/ragMetadata/{ragMetadata}`

`userSpecifiedMetadata` `object ( `[`UserSpecifiedMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata#UserSpecifiedMetadata)` )`

user provided metadata.

**JSON representation**

```
{
  "name": string,
  "userSpecifiedMetadata": {
    object (UserSpecifiedMetadata)
  }
}
```

## UserSpecifiedMetadata

metadata provided by users.

Fields

`key` `string`

Required. Key of the metadata. The key must be set with type by CreateRagDataSchema.

`value` `object ( `[`MetadataValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata#MetadataValue)` )`

value of the metadata. The value must be able to convert to the type according to the data schema.

**JSON representation**

```
{
  "key": string,
  "value": {
    object (MetadataValue)
  }
}
```

## MetadataValue

value of metadata, including all types available in data schema.

Fields

`value` `Union type`

The value of the metadata. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`intValue` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

value of int type metadata.

`floatValue` `number`

value of float type metadata.

`strValue` `string`

value of string type metadata.

`datetimeValue` `string`

value of date time type metadata.

`boolValue` `boolean`

value of boolean type metadata.

`listValue` `object ( `[`MetadataList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata#MetadataList)` )`

value of list type metadata.

End of mutually exclusive fields.

**JSON representation**

```
{

  // value
  "intValue": string,
  "floatValue": number,
  "strValue": string,
  "datetimeValue": string,
  "boolValue": boolean,
  "listValue": {
    object (MetadataList)
  }
  // Union type
}
```

## MetadataList

List representation in metadata.

Fields

`values[]` `object ( `[`MetadataValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata#MetadataValue)` )`

The values of `LIST` data type metadata.

**JSON representation**

```
{
  "values": [
    {
      object (MetadataValue)
    }
  ]
}
```

| Methods                                                                                                                                                               |                                        |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------|
| [`batchCreate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/batchCreate) | Batch Create one or more RagMetadatas  |
| [`batchDelete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/batchDelete) | Batch Deletes one or more RagMetadata. |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/create)           | Creates a RagMetadata.                 |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/delete)           | Deletes a RagMetadata.                 |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/get)                 | Gets a RagMetadata.                    |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/list)               | Lists RagMetadata in a RagFile.        |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles.ragMetadata/patch)             | Updates a RagMetadata.                 |
