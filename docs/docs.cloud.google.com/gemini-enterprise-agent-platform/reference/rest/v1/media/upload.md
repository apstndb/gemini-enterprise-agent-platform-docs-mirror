---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/media/upload
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/media/upload
title: 'Method: media.upload'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : media.upload

Upload a file into a RagCorpus.

### Endpoint

- Upload URI, for media upload requests:  

post `https: / /{service-endpoint} /upload /v1 /{parent} /ragFiles:upload`

- Metadata URI, for metadata-only requests:  

post `https: / /{service-endpoint} /v1 /{parent} /ragFiles:upload`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the RagCorpus resource into which to upload the file. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

### Request body

The request body contains data with the following structure:

Fields

`ragFile` `object ( `[`RagFile`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles#RagFile)` )`

Required. The RagFile to upload.

`uploadRagFileConfig` `object ( `[`UploadRagFileConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/media/upload#UploadRagFileConfig)` )`

Required. The config for the RagFiles to be uploaded into the RagCorpus. [`VertexRagDataService.UploadRagFile`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/media/upload#google.cloud.aiplatform.v1.VertexRagDataService.UploadRagFile) .

### Response body

Response message for [`VertexRagDataService.UploadRagFile`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/media/upload#google.cloud.aiplatform.v1.VertexRagDataService.UploadRagFile) .

If successful, the response body contains data with the following structure:

Fields

`result` `Union type`

The result of the upload. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`ragFile` `object ( `[`RagFile`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora.ragFiles#RagFile)` )`

The RagFile that had been uploaded into the RagCorpus.

`error` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

The error that occurred while processing the RagFile.

End of mutually exclusive fields.

**JSON representation**

```
{

  // result
  "ragFile": {
    object (RagFile)
  },
  "error": {
    object (Status)
  }
  // Union type
}
```

## UploadRagFileConfig

Config for uploading RagFile.

Fields

`ragFileTransformationConfig` `object ( `[`RagFileTransformationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagFileTransformationConfig)` )`

Specifies the transformation config for RagFiles.

**JSON representation**

```
{
  "ragFileTransformationConfig": {
    object (RagFileTransformationConfig)
  }
}
```
