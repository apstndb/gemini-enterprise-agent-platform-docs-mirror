---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value
title: Value
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

`value` represents a dynamically typed value which can be either null, a number, a string, a boolean, a recursive struct value, or a list of values. A producer of value is expected to set one of these variants. Absence of any variant indicates an error.

Fields

`kind` `Union type`

The kind of value. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`nullValue` `null`

Represents a null value.

`numberValue` `number`

Represents a double value.

`stringValue` `string`

Represents a string value.

`boolValue` `boolean`

Represents a boolean value.

`structValue` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

Represents a structured value.

`listValue` `object ( `[`ListValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value#ListValue)` )`

Represents a repeated `value` .

`contentValue` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content)` )`

Represents rich content (text, image, etc.).

End of mutually exclusive fields.

**JSON representation**

```
{

  // kind
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean,
  "structValue": {
    object (Struct)
  },
  "listValue": {
    object (ListValue)
  },
  "contentValue": {
    object (Content)
  }
  // Union type
}
```

## ListValue

`ListValue` is a wrapper around a repeated field of values.

Fields

`values[]` `object ( `[`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value)` )`

Repeated field of dynamically typed values.

**JSON representation**

```
{
  "values": [
    {
      object (Value)
    }
  ]
}
```
