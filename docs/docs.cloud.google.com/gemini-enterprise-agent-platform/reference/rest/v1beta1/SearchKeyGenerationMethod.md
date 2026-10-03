---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SearchKeyGenerationMethod
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SearchKeyGenerationMethod
title: SearchKeyGenerationMethod
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Options for generating the search key from the conversation history.

Fields

`method` `Union type`

The method for generating the search key. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`lastEntry` `object ( `[`LastEntry`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SearchKeyGenerationMethod#LastEntry)` )`

Use only the last entry of the conversation history ( `contentsExample.contents` ) as the search key.

End of mutually exclusive fields.

**JSON representation**

```
{

  // method
  "lastEntry": {
    object (LastEntry)
  }
  // Union type
}
```

## LastEntry

This type has no fields.

Configuration for using only the last entry of the conversation history as the search key.
