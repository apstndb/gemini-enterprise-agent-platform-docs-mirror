---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InstanceData
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InstanceData
title: InstanceData
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Instance data used to populate placeholders in a metric prompt template.

Fields

`data` `Union type`

Supported formats for instance data. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` `string`

Text data.

`contents` `object ( `[`Contents`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InstanceData#Contents)` )`

List of Gemini content data.

End of mutually exclusive fields.

**JSON representation**

```
{

  // data
  "text": string,
  "contents": {
    object (Contents)
  }
  // Union type
}
```

## Contents

List of standard Content messages from Gemini API.

Fields

`contents[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content)` )`

Optional. Repeated contents.

**JSON representation**

```
{
  "contents": [
    {
      object (Content)
    }
  ]
}
```
