---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileMetadataConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileMetadataConfig
title: RagFileMetadataConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

metadata config for RagFile.

Fields

`metadata_schema_source` `Union type`

Specifies the metadata schema source. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsMetadataSchemaSource` `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GcsSource)` )`

Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - `gs://bucketName/my_directory/objectName/metadataSchema.json` - `gs://bucketName/my_directory` If the user provides a directory, the metadata schema will be read from the files that ends with "metadataSchema.json" in the directory.

`googleDriveMetadataSchemaSource` `object ( `[`GoogleDriveSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles#GoogleDriveSource)` )`

Google Drive location. Supports importing individual files as well as Google Drive folders. If the user provides a folder, the metadata schema will be read from the files that ends with "metadataSchema.json" in the directory.

`inlineMetadataSchemaSource` `string`

Inline metadata schema source. Must be a JSON string.

End of mutually exclusive fields.

`metadata_source` `Union type`

Specifies the metadata source. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsMetadataSource` `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GcsSource)` )`

Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - `gs://bucketName/my_directory/objectName/metadata.json` - `gs://bucketName/my_directory` If the user provides a directory, the metadata will be read from the files that ends with "metadata.json" in the directory.

`googleDriveMetadataSource` `object ( `[`GoogleDriveSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora.ragFiles#GoogleDriveSource)` )`

Google Drive location. Supports importing individual files as well as Google Drive folders. If the user provides a directory, the metadata will be read from the files that ends with "metadata.json" in the directory.

`inlineMetadataSource` `string`

Inline metadata source. Must be a JSON string.

End of mutually exclusive fields.

**JSON representation**

```
{

  // metadata_schema_source
  "gcsMetadataSchemaSource": {
    object (GcsSource)
  },
  "googleDriveMetadataSchemaSource": {
    object (GoogleDriveSource)
  },
  "inlineMetadataSchemaSource": string
  // Union type

  // metadata_source
  "gcsMetadataSource": {
    object (GcsSource)
  },
  "googleDriveMetadataSource": {
    object (GoogleDriveSource)
  },
  "inlineMetadataSource": string
  // Union type
}
```
