---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoClassificationAnnotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoClassificationAnnotation
title: VideoClassificationAnnotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Annotation details specific to video classification.

Fields

`timeSegment` `object ( `[`TimeSegment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TimeSegment)` )`

This Annotation applies to the time period represented by the TimeSegment. If it's not set, the Annotation applies to the whole video.

`annotationSpecId` `string`

The resource id of the AnnotationSpec that this Annotation pertains to.

`displayName` `string`

The display name of the AnnotationSpec that this Annotation pertains to.

**JSON representation**

```
{
  "timeSegment": {
    object (TimeSegment)
  },
  "annotationSpecId": string,
  "displayName": string
}
```
