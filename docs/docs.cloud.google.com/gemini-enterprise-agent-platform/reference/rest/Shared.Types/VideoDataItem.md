---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoDataItem
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoDataItem
title: VideoDataItem
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Payload of Video DataItem.

Fields

`gcsUri` `string`

Required. Google Cloud Storage URI points to the original video in user's bucket. The video is up to 50 GB in size and up to 3 hour in duration.

`mimeType` `string`

Output only. The mime type of the content of the video. Only the videos in below listed mime types are supported. Supported mimeType: - video/mp4 - video/avi - video/quicktime

**JSON representation**

```
{
  "gcsUri": string,
  "mimeType": string
}
```
