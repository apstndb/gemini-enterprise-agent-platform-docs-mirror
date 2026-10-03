---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModalityTokenCount
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModalityTokenCount
title: ModalityTokenCount
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a breakdown of token usage by modality.

This message is used in \[CountTokensResponse\]\[google.cloud.aiplatform.master.CountTokensResponse\] and [`GenerateContentResponse.UsageMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#UsageMetadata) to provide a detailed view of how many tokens are used by each modality (e.g., text, image, video) in a request. This is particularly useful for multimodal models, allowing you to track and manage token consumption for billing and quota purposes.

Fields

`modality` `enum ( `[`Modality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModalityTokenCount#Modality)` )`

The modality that this token count applies to.

`tokenCount` `integer`

The number of tokens counted for this modality.

**JSON representation**

```
{
  "modality": enum (Modality),
  "tokenCount": integer
}
```

## Modality

The modality of a `Part` of a `Content` message. A modality is the type of media, such as an image or a video. It is used to categorize the content of a `Part` for token counting purposes.

| Enums                  |                                                             |
|------------------------|-------------------------------------------------------------|
| `MODALITY_UNSPECIFIED` | When a modality is not specified, it is treated as `TEXT` . |
| `TEXT`                 | The `Part` contains plain text.                             |
| `IMAGE`                | The `Part` contains an image.                               |
| `VIDEO`                | The `Part` contains a video.                                |
| `AUDIO`                | The `Part` contains audio.                                  |
| `DOCUMENT`             | The `Part` contains a document, such as a PDF.              |
