---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AnnotationSpecColor
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AnnotationSpecColor
title: AnnotationSpecColor
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

An entry of mapping between color and AnnotationSpec. The mapping is used in segmentation mask.

Fields

`color` `object ( `[`Color`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Color)` )`

The color of the AnnotationSpec in a segmentation mask.

`displayName` `string`

The display name of the AnnotationSpec represented by the color in the segmentation mask.

`id` `string`

The id of the AnnotationSpec represented by the color in the segmentation mask.

**JSON representation**

```
{
  "color": {
    object (Color)
  },
  "displayName": string,
  "id": string
}
```
