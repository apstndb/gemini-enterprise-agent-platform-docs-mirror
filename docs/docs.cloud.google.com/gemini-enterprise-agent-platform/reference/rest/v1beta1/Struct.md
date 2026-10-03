---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct
title: Struct
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

`Struct` represents a structured data value, consisting of fields which map to dynamically typed values.

Fields

`fields[]` `object ( `[`Field`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct#Field)` )`

Dynamically typed fields. List instead of map because LLMs are sensitive to ordering, and we want to give users full control.

**JSON representation**

```
{
  "fields": [
    {
      object (Field)
    }
  ]
}
```

## Field

Represents a single field in a struct.

Fields

`name` `string`

`value` `object ( `[`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value)` )`

**JSON representation**

```
{
  "name": string,
  "value": {
    object (Value)
  }
}
```
