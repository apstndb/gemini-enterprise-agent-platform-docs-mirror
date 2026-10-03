---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextSentimentAnnotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextSentimentAnnotation
title: TextSentimentAnnotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Annotation details specific to text sentiment.

Fields

`sentiment` `integer`

The sentiment score for text.

`sentimentMax` `integer`

The sentiment max score for text.

`annotationSpecId` `string`

The resource id of the AnnotationSpec that this Annotation pertains to.

`displayName` `string`

The display name of the AnnotationSpec that this Annotation pertains to.

**JSON representation**

```
{
  "sentiment": integer,
  "sentimentMax": integer,
  "annotationSpecId": string,
  "displayName": string
}
```
