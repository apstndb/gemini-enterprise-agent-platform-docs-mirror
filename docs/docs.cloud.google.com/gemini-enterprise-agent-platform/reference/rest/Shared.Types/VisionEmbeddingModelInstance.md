---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelInstance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelInstance
title: VisionEmbeddingModelInstance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Input format for requesting embeddings from vision models. An embedding is a list of numbers that represents the semantic meaning of text, an image, or a video. Embeddings can be used for many applications, like searching for similar images or getting recommendations. Each instance must specify exactly one of `text` , `image` , or `video` field.

Fields

`image` `object ( `[`Image`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelInstance#Image)` )`

An image to generate embeddings for.

`text` `string`

Text to generate embeddings for.

`video` `object ( `[`Video`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelInstance#Video)` )`

A video to generate embeddings for.

**JSON representation**

```
{
  "image": {
    object (Image)
  },
  "text": string,
  "video": {
    object (Video)
  }
}
```

## Image

Represents an image input for embedding generation.

Fields

`mimeType` `string`

The MIME type of the image.

The supported MIME types are:

- `image/jpeg`
- `image/png`

`data` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`bytesBase64Encoded` `string`

Base64-encoded bytes of the image.

`gcsUri` `string`

A Cloud Storage URI pointing to the image file. Format: `gs://bucket/object`

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeType": string,

  // data
  "bytesBase64Encoded": string,
  "gcsUri": string
  // Union type
}
```

## Video

Represents a video input for embedding generation.

Fields

`videoSegmentConfig` `object ( `[`VideoSegmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelInstance#VideoSegmentConfig)` )`

Configuration for processing a video segment. If specified, embeddings are generated for the segment. If not specified, embeddings are generated for the entire video.

`data` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`bytesBase64Encoded` `string`

Base64-encoded bytes of the video.

`gcsUri` `string`

A Cloud Storage URI pointing to the video file. Format: `gs://bucket/object`

End of mutually exclusive fields.

**JSON representation**

```
{
  "videoSegmentConfig": {
    object (VideoSegmentConfig)
  },

  // data
  "bytesBase64Encoded": string,
  "gcsUri": string
  // Union type
}
```

## VideoSegmentConfig

Configuration for processing a segment of a video.

Fields

`startOffsetSec` `integer`

The start offset of the video segment in seconds.

`endOffsetSec` `integer`

The end offset of the video segment in seconds.

`intervalSec` `integer`

The interval of the video for which the embedding will be generated. The minimum value for `intervalSec` is 4. If the interval is less than 4, an `InvalidArgumentError` is returned. There are no limitations on the maximum value of the interval. However, if the interval is larger than `min(videoLength, 120s)` , it might affect the quality of the generated embeddings.

**JSON representation**

```
{
  "startOffsetSec": integer,
  "endOffsetSec": integer,
  "intervalSec": integer
}
```
