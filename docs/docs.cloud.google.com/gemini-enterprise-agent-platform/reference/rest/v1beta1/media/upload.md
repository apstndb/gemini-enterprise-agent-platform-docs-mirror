---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/media/upload
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/media/upload
title: 'Method: media.upload'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : media.upload

Upload a file into a RagCorpus.

### Endpoint

  - Upload URI, for media upload requests:  

post `https: / /{service-endpoint} /upload /v1beta1 /{parent} /ragFiles:upload`

  - Metadata URI, for metadata-only requests:  

post `https: / /{service-endpoint} /v1beta1 /{parent} /ragFiles:upload`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the RagCorpus resource into which to upload the file. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

### Request body

The request body contains data with the following structure:

Fields

`ragFile` ` object ( RagFile  ` )

Required. The RagFile to upload.

`uploadRagFileConfig` ` object ( UploadRagFileConfig  ` )

Required. The config for the RagFiles to be uploaded into the RagCorpus. `  VertexRagDataService.UploadRagFile  ` .

### Response body

Response message for `  VertexRagDataService.UploadRagFile  ` .

If successful, the response body contains data with the following structure:

Fields

`result` `Union type`

The result of the upload. `result` can be only one of the following:

`ragFile` ` object ( RagFile  ` )

The RagFile that had been uploaded into the RagCorpus.

`error` ` object ( Status  ` )

The error that occurred while processing the RagFile.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// result&quot;ragFile&quot;: {object (RagFile)},&quot;error&quot;: {object (Status)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## UploadRagFileConfig

Config for uploading RagFile.

Fields

` ragFileChunkingConfig (deprecated)  ` ` object ( RagFileChunkingConfig  ` )

> This item is deprecated\!

Specifies the size and overlap of chunks after uploading RagFile.

`ragFileTransformationConfig` ` object ( RagFileTransformationConfig  ` )

Specifies the transformation config for RagFiles.

` ragFileMetadataConfig (deprecated)  ` ` object ( RagFileMetadataConfig  ` )

> This item is deprecated\!

Optional. Specifies the metadata config for RagFiles. Including paths for metadata schema and metadata. Alteratively, inline metadata schema and metadata can be provided. Deprecated: Not in use.

`ragFileParsingConfig` ` object ( RagFileParsingConfig  ` )

Optional. Specifies the parsing config for RagFiles. RAG will use the default parser if this field is not set.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragFileChunkingConfig&quot;: {object (RagFileChunkingConfig)},&quot;ragFileTransformationConfig&quot;: {object (RagFileTransformationConfig)},&quot;ragFileMetadataConfig&quot;: {object (RagFileMetadataConfig)},&quot;ragFileParsingConfig&quot;: {object (RagFileParsingConfig)}}</code></pre></td>
</tr>
</tbody>
</table>
