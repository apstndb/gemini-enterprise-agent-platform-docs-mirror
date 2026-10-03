---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextDataItem
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextDataItem
title: TextDataItem
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Payload of Text DataItem.

Fields

`gcsUri` `string`

Output only. Google Cloud Storage URI points to a copy of the original text in the Vertex-managed bucket in the user's project. The text file is up to 10MB in size.

**JSON representation**

```
{
  "gcsUri": string
}
```
