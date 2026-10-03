---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelResult
title: VisionEmbeddingModelResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The prediction result for a large vision model embedding request. An embedding is a vectorized representation of data such as image, text or video. The embeddings produced by this model can be used for tasks such as image retrieval, similarity comparison, and classification. The embedding vectors have 1024 dimensions.

Fields

`imageEmbedding` `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)`

The embedding generated from the input image. This field is populated if the prediction request contained an image.

`textEmbedding` `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)`

The embedding generated from the input text. This field is populated if the prediction request contained text.

`videoEmbeddings[]` `object ( `[`VideoEmbedding`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VisionEmbeddingModelResult#VideoEmbedding)` )`

The embeddings generated from the input video. This field is populated if the prediction request contained a video. The video is divided into 1-second segments, and an embedding is generated for each segment.

**JSON representation**

```
{
  "imageEmbedding": array,
  "textEmbedding": array,
  "videoEmbeddings": [
    {
      object (VideoEmbedding)
    }
  ]
}
```

## VideoEmbedding

Contains embedding data for a specific time segment of a video.

Fields

`startOffsetSec` `integer`

The start time of the video segment that this embedding represents, measured in seconds from the beginning of the video.

`endOffsetSec` `integer`

The end time of the video segment that this embedding represents, measured in seconds from the beginning of the video.

`embedding` `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)`

The 1024-dimension embedding vector for this video segment.

**JSON representation**

```
{
  "startOffsetSec": integer,
  "endOffsetSec": integer,
  "embedding": array
}
```
