---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextClassificationPredictionInstance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextClassificationPredictionInstance
title: TextClassificationPredictionInstance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction input format for Text Classification.

Fields

`content` `string`

The text snippet to make the predictions on.

`mimeType` `string`

The MIME type of the text snippet. The supported MIME types are listed below. - text/plain

**JSON representation**

```
{
  "content": string,
  "mimeType": string
}
```
