---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageDataItem
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageDataItem
title: ImageDataItem
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Payload of Image DataItem.

Fields

`gcsUri` `string`

Required. Google Cloud Storage URI points to the original image in user's bucket. The image is up to 30MB in size.

`mimeType` `string`

Output only. The mime type of the content of the image. Only the images in below listed mime types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon

**JSON representation**

```
{
  "gcsUri": string,
  "mimeType": string
}
```
