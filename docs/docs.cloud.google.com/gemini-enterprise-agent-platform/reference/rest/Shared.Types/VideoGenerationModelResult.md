---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoGenerationModelResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoGenerationModelResult
title: VideoGenerationModelResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction result from a video generation model. When you request a prediction from a video generation model, the model generates videos based on your input and returns URIs to these videos in Google Cloud Storage.

Fields

`gcsUris[]` `string`

A list of Google Cloud Storage URIs for generated videos. For each input instance in your prediction request, the model may generate one or more videos. This field provides the Google Cloud Storage URIs for each of these videos.

**JSON representation**

```
{
  "gcsUris": [
    string
  ]
}
```
