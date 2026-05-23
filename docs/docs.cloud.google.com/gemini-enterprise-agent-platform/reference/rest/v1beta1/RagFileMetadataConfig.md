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

Specifies the metadata schema source. `metadata_schema_source` can be only one of the following:

`gcsMetadataSchemaSource` ` object ( GcsSource  ` )

Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - `gs://bucketName/my_directory/objectName/metadataSchema.json` - `gs://bucketName/my_directory` If the user provides a directory, the metadata schema will be read from the files that ends with "metadataSchema.json" in the directory.

`googleDriveMetadataSchemaSource` ` object ( GoogleDriveSource  ` )

Google Drive location. Supports importing individual files as well as Google Drive folders. If the user provides a folder, the metadata schema will be read from the files that ends with "metadataSchema.json" in the directory.

`inlineMetadataSchemaSource` `string`

Inline metadata schema source. Must be a JSON string.

`metadata_source` `Union type`

Specifies the metadata source. `metadata_source` can be only one of the following:

`gcsMetadataSource` ` object ( GcsSource  ` )

Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - `gs://bucketName/my_directory/objectName/metadata.json` - `gs://bucketName/my_directory` If the user provides a directory, the metadata will be read from the files that ends with "metadata.json" in the directory.

`googleDriveMetadataSource` ` object ( GoogleDriveSource  ` )

Google Drive location. Supports importing individual files as well as Google Drive folders. If the user provides a directory, the metadata will be read from the files that ends with "metadata.json" in the directory.

`inlineMetadataSource` `string`

Inline metadata source. Must be a JSON string.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// metadata_schema_source&quot;gcsMetadataSchemaSource&quot;: {object (GcsSource)},&quot;googleDriveMetadataSchemaSource&quot;: {object (GoogleDriveSource)},&quot;inlineMetadataSchemaSource&quot;: string// Union type// metadata_source&quot;gcsMetadataSource&quot;: {object (GcsSource)},&quot;googleDriveMetadataSource&quot;: {object (GoogleDriveSource)},&quot;inlineMetadataSource&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>
