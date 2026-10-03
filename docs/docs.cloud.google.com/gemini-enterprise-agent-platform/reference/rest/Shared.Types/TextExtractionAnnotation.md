---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionAnnotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionAnnotation
title: TextExtractionAnnotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Annotation details specific to text extraction.

Fields

`textSegment` `object ( `[`TextSegment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionAnnotation#TextSegment)` )`

The segment of the text content.

`annotationSpecId` `string`

The resource id of the AnnotationSpec that this Annotation pertains to.

`displayName` `string`

The display name of the AnnotationSpec that this Annotation pertains to.

**JSON representation**

```
{
  "textSegment": {
    object (TextSegment)
  },
  "annotationSpecId": string,
  "displayName": string
}
```

## TextSegment

The text segment inside of DataItem.

Fields

`startOffset` `string`

Zero-based character index of the first character of the text segment (counting characters from the beginning of the text).

`endOffset` `string`

Zero-based character index of the first character past the end of the text segment (counting character from the beginning of the text). The character at the endOffset is NOT included in the text segment.

`content` `string`

The text content in the segment for output only.

**JSON representation**

```
{
  "startOffset": string,
  "endOffset": string,
  "content": string
}
```
