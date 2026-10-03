---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeedbackContext
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeedbackContext
title: FeedbackContext
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Feedback context is a resource that represents additional information about the conversation where the feedback was given, such as the conversation history, system instructions, etc. If provided, feedback context allows to correlate the feedback with the conversation, even if the original session is deleted or not available.

Fields

`name` `string`

Identifier. The resource name. Assigned by the server on create.

Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/feedbackEntries/{feedbackEntry}/feedbackContext`

`contextEvents[]` `object ( `[`SessionEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SessionEvent)` )`

Optional. The session events from the originating session.

**JSON representation**

```
{
  "name": string,
  "contextEvents": [
    {
      object (SessionEvent)
    }
  ]
}
```
