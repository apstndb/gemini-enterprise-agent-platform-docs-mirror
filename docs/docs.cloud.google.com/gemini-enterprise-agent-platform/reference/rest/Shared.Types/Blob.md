---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Blob
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Blob
title: Blob
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A content blob.

A `blob` contains data of a specific media type. It is used to represent images, audio, and video.

Fields

`mimeType` `string`

Required. The IANA standard MIME type of the source data.

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

Required. The raw bytes of the data.

A base64-encoded string.

`displayName` `string`

Optional. The display name of the blob. Used to provide a label or filename to distinguish blobs.

This field is only returned in `PromptMessage` for prompt management. It is used in the Gemini calls only when server-side tools ( `codeExecution` , `googleSearch` , and `urlContext` ) are enabled.

**JSON representation**

```
{
  "mimeType": string,
  "data": string,
  "displayName": string
}
```
