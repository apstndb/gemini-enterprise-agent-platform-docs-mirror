---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PredictionResult
title: PredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a line of JSONL in the batch prediction output file.

Fields

`prediction` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

The prediction result. value is used here instead of Any so that JsonFormat does not append an extra "@type" field when we convert the proto to JSON and so we can represent array of objects. Do not set error if this is set.

`error` `object ( `[`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PredictionResult#Error)` )`

The error result. Do not set prediction if this is set.

`input` `Union type`

Some identifier from the input so that the prediction can be mapped back to the input instance. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`instance` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

user's input instance. Struct is used here instead of Any so that JsonFormat does not append an extra "@type" field when we convert the proto to JSON.

`key` `string`

Optional user-provided key from the input instance.

End of mutually exclusive fields.

**JSON representation**

```
{
  "prediction": value,
  "error": {
    object (Error)
  },

  // input
  "instance": {
    object
  },
  "key": string
  // Union type
}
```

## Error

Fields

`status` `enum ( `[`Code`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Code)` )`

Error status. This will be serialized into the enum name e.g. "NOT_FOUND".

`message` `string`

Error message with additional details.

**JSON representation**

```
{
  "status": enum (Code),
  "message": string
}
```
