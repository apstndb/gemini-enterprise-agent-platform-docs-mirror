---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookIdleShutdownConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookIdleShutdownConfig
title: NotebookIdleShutdownConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The idle shutdown configuration of NotebookRuntimeTemplate, which contains the idleTimeout as required field.

Fields

`idleTimeout` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Required. Duration is accurate to the second. In Notebook, Idle Timeout is accurate to minute so the range of idleTimeout (second) is: 10 \* 60 \~ 1440 \* 60.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`idleShutdownDisabled` `boolean`

Whether Idle Shutdown is disabled in this NotebookRuntimeTemplate.

**JSON representation**

```
{
  "idleTimeout": string,
  "idleShutdownDisabled": boolean
}
```
