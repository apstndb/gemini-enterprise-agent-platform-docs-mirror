---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GcsSource
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GcsSource
title: GcsSource
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The Google Cloud Storage location for the input content.

Fields

`uris[]` `string`

Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see <https://cloud.google.com/storage/docs/wildcards> .

**JSON representation**

```
{
  "uris": [
    string
  ]
}
```
