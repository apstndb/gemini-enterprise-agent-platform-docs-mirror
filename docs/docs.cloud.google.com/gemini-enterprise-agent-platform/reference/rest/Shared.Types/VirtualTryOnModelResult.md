---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelResult
title: VirtualTryOnModelResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents the output of a Virtual Try-On prediction.

Fields

`images[]` `object ( `[`Image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VirtualTryOnModelResult#Image)` )`

A list of generated images. The number of images returned is equal to the `sampleCount` parameter provided in the request.

**JSON representation**

```
{
  "images": [
    {
      object (Image)
    }
  ]
}
```

## Image

Contains a generated image or information about why the image was filtered out.

Fields

`mimeType` `string`

The MIME type of the generated image.

Supported values are: \* `image/png` \* `image/jpeg`

`data` `Union type`

The generated image data or filtering reason. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`bytesBase64Encoded` `string`

The generated image encoded as a base64 encoded bytes string.

`gcsUri` `string`

The Google Cloud Storage URI where the generated image is stored.

`raiFilteredReason` `string`

The reason why the generated image was filtered out by Responsible AI checks. If this field is present, no image is returned.

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeType": string,

  // data
  "bytesBase64Encoded": string,
  "gcsUri": string,
  "raiFilteredReason": string
  // Union type
}
```
