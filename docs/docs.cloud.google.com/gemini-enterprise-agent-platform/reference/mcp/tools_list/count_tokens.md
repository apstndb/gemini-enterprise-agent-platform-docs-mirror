---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/count_tokens
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/count_tokens
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `count_tokens`

Calculates the number of tokens in a given input without generating a response, helping you manage rate limits and estimate the cost of a request before sending it.

The following sample demonstrate how to use `curl` to invoke the `count_tokens` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "count_tokens",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `PredictionService.CountTokens` .

### CountTokensRequest

**JSON representation**

```
{
  "endpoint": string,
  "model": string,
  "instances": [
    value
  ],
  "contents": [
    {
      object (Content)
    }
  ],
  "tools": [
    {
      object (Tool)
    }
  ],

  // Union field _system_instruction can be only one of the following:
  "systemInstruction": {
    object (Content)
  }
  // End of list of possible types for union field _system_instruction.

  // Union field _generation_config can be only one of the following:
  "generationConfig": {
    object (GenerationConfig)
  }
  // End of list of possible types for union field _generation_config.
}
```

| Fields                                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `endpoint`                                                                                  | `string` Required. The name of the Endpoint requested to perform token counting. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`                                                                                                                                                                                                                                                        |
| `model`                                                                                     | `string` Optional. The name of the publisher model requested to serve the prediction. Format: `projects/{project}/locations/{location}/publishers/*/models/*`                                                                                                                                                                                                                                                  |
| `instances[]`                                                                               | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. The instances that are the input to token counting call. Schema is identical to the prediction schema of the underlying model.                                                                                                                                                                         |
| `contents[]`                                                                                | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content)` )` Optional. Input content.                                                                                                                                                                                                                           |
| `tools[]`                                                                                   | `object ( `[`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Tool)` )` Optional. A list of `Tools` the model may use to generate the next response. A `Tool` is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model. |
| Union field `_system_instruction` . `_system_instruction` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                |
| `systemInstruction`                                                                         | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content)` )` Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph.                                                                                   |
| Union field `_generation_config` . `_generation_config` can be only one of the following:   |                                                                                                                                                                                                                                                                                                                                                                                                                |
| `generationConfig`                                                                          | `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GenerationConfig)` )` Optional. Generation config that the model will use to generate the response.                                                                                                                                                    |

### Value

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean,
  "structValue": {
    object
  },
  "listValue": array
  // End of list of possible types for union field kind.
}
```

| Fields                                                                           |                                                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . The kind of value. `kind` can be only one of the following: |                                                                                                                                                                                                                                                |
| `nullValue`                                                                      | `null` Represents a JSON `null` .                                                                                                                                                                                                              |
| `numberValue`                                                                    | `number` Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type. |
| `stringValue`                                                                    | `string` Represents a JSON string.                                                                                                                                                                                                             |
| `boolValue`                                                                      | `boolean` Represents a JSON boolean ( `true` or `false` literal in JSON).                                                                                                                                                                      |
| `structValue`                                                                    | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Represents a JSON object.                                                                                                                     |
| `listValue`                                                                      | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` Represents a JSON array.                                                                                                                |

### Struct

**JSON representation**

```
{
  "fields": {
    string: value,
    ...
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                          |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map (key: string, value: value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format))` Unordered map of dynamically typed values. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### FieldsEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### ListValue

**JSON representation**

```
{
  "values": [
    value
  ]
}
```

| Fields     |                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Repeated field of dynamically typed values. |

### Content

**JSON representation**

```
{
  "role": string,
  "parts": [
    {
      object (Part)
    }
  ]
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                               |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `role`    | `string` Optional. The producer of the content. Must be either 'user' or 'model'. If not set, the service will default to 'user'.                                                                                                                                                                                             |
| `parts[]` | `object ( `[`Part`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Part)` )` Required. A list of `Part` objects that make up a single message. Parts of a message can have different MIME types. A `Content` message must have at least one `Part` . |

### Part

**JSON representation**

```
{
  "thought": boolean,
  "thoughtSignature": string,
  "mediaResolution": {
    object (MediaResolution)
  },
  "audioTranscription": {
    object (AudioTranscription)
  },

  // Union field data can be only one of the following:
  "text": string,
  "inlineData": {
    object (Blob)
  },
  "fileData": {
    object (FileData)
  },
  "functionCall": {
    object (FunctionCall)
  },
  "functionResponse": {
    object (FunctionResponse)
  },
  "executableCode": {
    object (ExecutableCode)
  },
  "codeExecutionResult": {
    object (CodeExecutionResult)
  }
  // End of list of possible types for union field data.

  // Union field metadata can be only one of the following:
  "videoMetadata": {
    object (VideoMetadata)
  }
  // End of list of possible types for union field metadata.
}
```

| Fields                                                                |                                                                                                                                                                                                                                                                                                                              |
|-----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `thought`                                                             | `boolean` Optional. Indicates whether the `part` represents the model's thought process or reasoning.                                                                                                                                                                                                                        |
| `thoughtSignature`                                                    | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. An opaque signature for the thought so it can be reused in subsequent requests. A base64-encoded string.                                                                                                                    |
| `mediaResolution`                                                     | `object ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MediaResolution)` )` per part media resolution. Media resolution for the input media.                                                                                 |
| `audioTranscription`                                                  | `object ( `[`AudioTranscription`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AudioTranscription)` )` Optional. Audio (input or output) transcription. This is only set when this Part contains audio data.                                      |
| Union field `data` . `data` can be only one of the following:         |                                                                                                                                                                                                                                                                                                                              |
| `text`                                                                | `string` Optional. The text content of the part. When sent from the VSCode Gemini Code Assist extension, references to @mentioned items will be converted to markdown boldface text. For example `@my-repo` will be converted to and sent as `**my-repo**` by the IDE agent.                                                 |
| `inlineData`                                                          | `object ( `[`Blob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Blob)` )` Optional. The inline data content of the part. This can be used to include images, audio, or video in a request.                                                       |
| `fileData`                                                            | `object ( `[`FileData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FileData)` )` Optional. The URI-based data of the part. This can be used to include files from Google Cloud Storage.                                                         |
| `functionCall`                                                        | `object ( `[`FunctionCall`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionCall)` )` Optional. A predicted function call returned from the model. This contains the name of the function to call and the arguments to pass to the function. |
| `functionResponse`                                                    | `object ( `[`FunctionResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionResponse)` )` Optional. The result of a function call. This is used to provide the model with the result of a function call that it predicted.               |
| `executableCode`                                                      | `object ( `[`ExecutableCode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ExecutableCode)` )` Optional. Code generated by the model that is intended to be executed.                                                                             |
| `codeExecutionResult`                                                 | `object ( `[`CodeExecutionResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CodeExecutionResult)` )` Optional. The result of executing the `ExecutableCode` .                                                                                 |
| Union field `metadata` . `metadata` can be only one of the following: |                                                                                                                                                                                                                                                                                                                              |
| `videoMetadata`                                                       | `object ( `[`VideoMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VideoMetadata)` )` Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data.                       |

### Blob

**JSON representation**

```
{
  "mimeType": string,
  "data": string,
  "displayName": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                     |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mimeType`    | `string` Required. The IANA standard MIME type of the source data.                                                                                                                                                                                                                                                  |
| `data`        | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Required. The raw bytes of the data. A base64-encoded string.                                                                                                                                                                |
| `displayName` | `string` Optional. The display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in `PromptMessage` for prompt management. It is used in the Gemini calls only when server-side tools ( `code_execution` , `google_search` , and `url_context` ) are enabled. |

### FileData

**JSON representation**

```
{
  "mimeType": string,
  "fileUri": string,
  "displayName": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                     |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mimeType`    | `string` Required. The IANA standard MIME type of the source data.                                                                                                                                                                                                                                                  |
| `fileUri`     | `string` Required. The URI of the file in Google Cloud Storage.                                                                                                                                                                                                                                                     |
| `displayName` | `string` Optional. The display name of the file. Used to provide a label or filename to distinguish files. This field is only returned in `PromptMessage` for prompt management. It is used in the Gemini calls only when server side tools ( `code_execution` , `google_search` , and `url_context` ) are enabled. |

### FunctionCall

**JSON representation**

```
{
  "id": string,
  "name": string,
  "args": {
    object
  },
  "partialArgs": [
    {
      object (PartialArg)
    }
  ],
  "willContinue": boolean
}
```

| Fields          |                                                                                                                                                                                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`            | `string` Optional. The unique id of the function call. If populated, the client to execute the `function_call` and return the response with the matching `id` .                                                                                                                                            |
| `name`          | `string` Optional. The name of the function to call. Matches `FunctionDeclaration.name` .                                                                                                                                                                                                                  |
| `args`          | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. The function parameters and values in JSON object format. See `FunctionDeclaration.parameters` for parameter details.                                                                           |
| `partialArgs[]` | `object ( `[`PartialArg`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PartialArg)` )` Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. |
| `willContinue`  | `boolean` Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow.                                                                                                                                                |

### PartialArg

**JSON representation**

```
{
  "jsonPath": string,
  "willContinue": boolean,

  // Union field delta can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean
  // End of list of possible types for union field delta.
}
```

| Fields                                                                                                   |                                                                                                                                                                   |
|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `jsonPath`                                                                                               | `string` Required. A JSON Path (RFC 9535) to the argument being streamed. <https://datatracker.ietf.org/doc/html/rfc9535> . e.g. "\$.foo.bar\[0\].data".          |
| `willContinue`                                                                                           | `boolean` Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow. |
| Union field `delta` . The delta of field value being streamed. `delta` can be only one of the following: |                                                                                                                                                                   |
| `nullValue`                                                                                              | `null` Optional. Represents a null value.                                                                                                                         |
| `numberValue`                                                                                            | `number` Optional. Represents a double value.                                                                                                                     |
| `stringValue`                                                                                            | `string` Optional. Represents a string value.                                                                                                                     |
| `boolValue`                                                                                              | `boolean` Optional. Represents a boolean value.                                                                                                                   |

### FunctionResponse

**JSON representation**

```
{
  "id": string,
  "name": string,
  "response": {
    object
  },
  "parts": [
    {
      object (FunctionResponsePart)
    }
  ]
}
```

| Fields     |                                                                                                                                                                                                                                                                                                                                                             |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`       | `string` Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id` .                                                                                                                                                                                                                |
| `name`     | `string` Required. The name of the function to call. Matches `FunctionDeclaration.name` and `FunctionCall.name` .                                                                                                                                                                                                                                           |
| `response` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Required. The function response in JSON object format. Use "output" key to specify function output and "error" key to specify error details (if any). If "output" and "error" keys are not specified, then whole "response" is treated as function output. |
| `parts[]`  | `object ( `[`FunctionResponsePart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionResponsePart)` )` Optional. Ordered `Parts` that constitute a function response. Parts may have different IANA MIME types.                                                              |

### FunctionResponsePart

**JSON representation**

```
{

  // Union field data can be only one of the following:
  "inlineData": {
    object (FunctionResponseBlob)
  },
  "fileData": {
    object (FunctionResponseFileData)
  }
  // End of list of possible types for union field data.
}
```

| Fields                                                                                                |                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `data` . The data of the function response part. `data` can be only one of the following: |                                                                                                                                                                                                               |
| `inlineData`                                                                                          | `object ( `[`FunctionResponseBlob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionResponseBlob)` )` Inline media bytes.     |
| `fileData`                                                                                            | `object ( `[`FunctionResponseFileData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionResponseFileData)` )` URI based data. |

### FunctionResponseBlob

**JSON representation**

```
{
  "mimeType": string,
  "data": string,
  "displayName": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                               |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mimeType`    | `string` Required. The IANA standard MIME type of the source data.                                                                                                                                                                                                                                                            |
| `data`        | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Required. Raw bytes. A base64-encoded string.                                                                                                                                                                                          |
| `displayName` | `string` Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. |

### FunctionResponseFileData

**JSON representation**

```
{
  "mimeType": string,
  "fileUri": string,
  "displayName": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                                         |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mimeType`    | `string` Required. The IANA standard MIME type of the source data.                                                                                                                                                                                                                                                                      |
| `fileUri`     | `string` Required. URI.                                                                                                                                                                                                                                                                                                                 |
| `displayName` | `string` Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. |

### ExecutableCode

**JSON representation**

```
{
  "language": enum (Language),
  "code": string,

  // Union field _id can be only one of the following:
  "id": string
  // End of list of possible types for union field _id.
}
```

| Fields                                                      |                                                                                                                                                                                                            |
|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `language`                                                  | `enum ( `[`Language`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Language)` )` Required. Programming language of the `code` . |
| `code`                                                      | `string` Required. The code to be executed.                                                                                                                                                                |
| Union field `_id` . `_id` can be only one of the following: |                                                                                                                                                                                                            |
| `id`                                                        | `string` Optional. Unique identifier of the `ExecutableCode` part. The server returns the `CodeExecutionResult` with the matching `id` .                                                                   |

### CodeExecutionResult

**JSON representation**

```
{
  "outcome": enum (Outcome),
  "output": string,

  // Union field _id can be only one of the following:
  "id": string
  // End of list of possible types for union field _id.
}
```

| Fields                                                      |                                                                                                                                                                                                    |
|-------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `outcome`                                                   | `enum ( `[`Outcome`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Outcome)` )` Required. Outcome of the code execution. |
| `output`                                                    | `string` Optional. Contains stdout when code execution is successful, stderr or other description otherwise.                                                                                       |
| Union field `_id` . `_id` can be only one of the following: |                                                                                                                                                                                                    |
| `id`                                                        | `string` Optional. The identifier of the `ExecutableCode` part this result is for. Only populated if the corresponding `ExecutableCode` has an id.                                                 |

### VideoMetadata

**JSON representation**

```
{
  "startOffset": string,
  "endOffset": string,
  "fps": number
}
```

| Fields        |                                                                                                                                                                                                                                                 |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startOffset` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. The start offset of the video. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
| `endOffset`   | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. The end offset of the video. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .   |
| `fps`         | `number` Optional. The frame rate of the video sent to the model. If not specified, the default value is 1.0. The valid range is (0.0, 24.0\].                                                                                                  |

### Duration

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years                                                                                    |
| `nanos`   | `integer` Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive. |

### MediaResolution

**JSON representation**

```
{

  // Union field value can be only one of the following:
  "level": enum (Level)
  // End of list of possible types for union field value.
}
```

| Fields                                                          |                                                                                                                                                                                                      |
|-----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `value` . `value` can be only one of the following: |                                                                                                                                                                                                      |
| `level`                                                         | `enum ( `[`Level`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Level)` )` The tokenization quality used for given media. |

### AudioTranscription

**JSON representation**

```
{
  "text": string,
  "speakerLabel": string,
  "words": [
    {
      object (WordInfo)
    }
  ]
}
```

| Fields         |                                                                                                                                                                                                                                                                    |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text`         | `string` Required. The transcription text of this audio segment.                                                                                                                                                                                                   |
| `speakerLabel` | `string` Optional. A label identifying the speaker of this audio segment (e.g. "spk_1", "spk_2"). Present when diarization is set.                                                                                                                                 |
| `words[]`      | `object ( `[`WordInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.WordInfo)` )` Optional. Detailed word-level transcriptions and timing details. Present when word_timestamp is set. |

### WordInfo

**JSON representation**

```
{
  "word": string,
  "startOffset": string,
  "endOffset": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `word`        | `string` Required. Transcript of the word.                                                                                                                                                                                                                                            |
| `startOffset` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. Start offset in time of the word relative to the start of the audio. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
| `endOffset`   | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. End offset in time of the word relative to the start of the audio. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .   |

### Tool

**JSON representation**

```
{
  "functionDeclarations": [
    {
      object (FunctionDeclaration)
    }
  ],
  "retrieval": {
    object (Retrieval)
  },
  "googleSearch": {
    object (GoogleSearch)
  },
  "googleSearchRetrieval": {
    object (GoogleSearchRetrieval)
  },
  "googleMaps": {
    object (GoogleMaps)
  },
  "enterpriseWebSearch": {
    object (EnterpriseWebSearch)
  },
  "parallelAiSearch": {
    object (ParallelAiSearch)
  },
  "codeExecution": {
    object (CodeExecution)
  },
  "urlContext": {
    object (UrlContext)
  },
  "computerUse": {
    object (ComputerUse)
  }
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>functionDeclarations[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionDeclaration"><code>FunctionDeclaration</code></a><code> )</code></p>
<p>Optional. Function tool type. One or more function declarations to be passed to the model along with the current user query. Model may decide to call a subset of these functions by populating <code>FunctionCall</code> in the response. User should provide a <code>FunctionResponse</code> for each function call in the next turn. Based on the function responses, Model will generate the final response back to the user. Maximum 512 function declarations can be provided.</p></td>
</tr>
<tr class="even">
<td><code>retrieval</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Retrieval"><code>Retrieval</code></a><code> )</code></p>
<p>Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation.</p></td>
</tr>
<tr class="odd">
<td><code>googleSearch</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GoogleSearch"><code>GoogleSearch</code></a><code> )</code></p>
<p>Optional. GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.</p></td>
</tr>
<tr class="even">
<td><code>googleSearchRetrieval </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GoogleSearchRetrieval"><code>GoogleSearchRetrieval</code></a><code> )</code></p>
<blockquote>
<p>Optional. The <code>google_search_retrieval</code> field is deprecated. Use <code>google_search</code> instead. This field is for use with Gemini 1.5 models; <code>google_search</code> is used for Gemini 2.0 and newer models.</p>
</blockquote>
<p>Optional. Specialized retrieval tool that is powered by Google Search.</p></td>
</tr>
<tr class="odd">
<td><code>googleMaps</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GoogleMaps"><code>GoogleMaps</code></a><code> )</code></p>
<p>Optional. GoogleMaps tool type. Tool to support Google Maps in Model.</p></td>
</tr>
<tr class="even">
<td><code>enterpriseWebSearch</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.EnterpriseWebSearch"><code>EnterpriseWebSearch</code></a><code> )</code></p>
<p>Optional. Tool to support searching public web data, powered by Agent Platform Search and Sec4 compliance.</p></td>
</tr>
<tr class="odd">
<td><code>parallelAiSearch</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ParallelAiSearch"><code>ParallelAiSearch</code></a><code> )</code></p>
<p>Optional. If specified, Agent Platform will use Parallel.ai to search for information to answer user queries. The search results will be grounded on Parallel.ai and presented to the model for response generation</p></td>
</tr>
<tr class="even">
<td><code>codeExecution</code></td>
<td><p><code>object ( </code><code>CodeExecution</code><code> )</code></p>
<p>Optional. CodeExecution tool type. Enables the model to execute code as part of generation.</p></td>
</tr>
<tr class="odd">
<td><code>urlContext</code></td>
<td><p><code>object ( </code><code>UrlContext</code><code> )</code></p>
<p>Optional. Tool to support URL context retrieval.</p></td>
</tr>
<tr class="even">
<td><code>computerUse</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ComputerUse"><code>ComputerUse</code></a><code> )</code></p>
<p>Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations.</p></td>
</tr>
</tbody>
</table>

### FunctionDeclaration

**JSON representation**

```
{
  "name": string,
  "description": string,
  "parameters": {
    object (Schema)
  },
  "parametersJsonSchema": value,
  "response": {
    object (Schema)
  },
  "responseJsonSchema": value
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots, colons and dashes, with a maximum length of 128.</p></td>
</tr>
<tr class="even">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>Optional. Description and purpose of the function. Model uses it to decide how and whether to call the function.</p></td>
</tr>
<tr class="odd">
<td><code>parameters</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema"><code>Schema</code></a><code> )</code></p>
<p>Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema Value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1</p></td>
</tr>
<tr class="even">
<td><code>parametersJsonSchema</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example:</p>
<pre data-fenced=""><code>{
  &quot;type&quot;: &quot;object&quot;,
  &quot;properties&quot;: {
    &quot;name&quot;: { &quot;type&quot;: &quot;string&quot; },
    &quot;age&quot;: { &quot;type&quot;: &quot;integer&quot; }
  },
  &quot;additionalProperties&quot;: false,
  &quot;required&quot;: [&quot;name&quot;, &quot;age&quot;],
  &quot;propertyOrdering&quot;: [&quot;name&quot;, &quot;age&quot;]
}</code></pre>
<p>This field is mutually exclusive with <code>parameters</code> .</p></td>
</tr>
<tr class="odd">
<td><code>response</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema"><code>Schema</code></a><code> )</code></p>
<p>Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function.</p></td>
</tr>
<tr class="even">
<td><code>responseJsonSchema</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function.</p>
<p>This field is mutually exclusive with <code>response</code> .</p></td>
</tr>
</tbody>
</table>

### Schema

**JSON representation**

```
{
  "type": enum (Type),
  "format": string,
  "title": string,
  "description": string,
  "nullable": boolean,
  "default": value,
  "items": {
    object (Schema)
  },
  "minItems": string,
  "maxItems": string,
  "enum": [
    string
  ],
  "properties": {
    string: {
      object (Schema)
    },
    ...
  },
  "propertyOrdering": [
    string
  ],
  "required": [
    string
  ],
  "minProperties": string,
  "maxProperties": string,
  "minimum": number,
  "maximum": number,
  "minLength": string,
  "maxLength": string,
  "pattern": string,
  "example": value,
  "anyOf": [
    {
      object (Schema)
    }
  ],
  "additionalProperties": value,
  "ref": string,
  "defs": {
    string: {
      object (Schema)
    },
    ...
  }
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`                 | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Type)` )` Optional. Data type of the schema field.                                                                                                                                                                                                                                                                                                                        |
| `format`               | `string` Optional. The format of the data. For `NUMBER` type, format can be `float` or `double` . For `INTEGER` type, format can be `int32` or `int64` . For `STRING` type, format can be `email` , `byte` , `date` , `date-time` , `password` , and other formats to further refine the data type.                                                                                                                                                                                                                 |
| `title`                | `string` Optional. Title for the schema.                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `description`          | `string` Optional. Describes the data. The model uses this field to understand the purpose of the schema and how to use it. It is a best practice to provide a clear and descriptive explanation for the schema and its properties here, rather than in the prompt.                                                                                                                                                                                                                                                 |
| `nullable`             | `boolean` Optional. Indicates if the value of this field can be null.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `default`              | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. Default value to use if the field is not specified.                                                                                                                                                                                                                                                                                                                                                         |
| `items`                | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` )` Optional. If type is `ARRAY` , `items` specifies the schema of elements in the array.                                                                                                                                                                                                                                                                     |
| `minItems`             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `ARRAY` , `min_items` specifies the minimum number of items in an array.                                                                                                                                                                                                                                                                                                                                |
| `maxItems`             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `ARRAY` , `max_items` specifies the maximum number of items in an array.                                                                                                                                                                                                                                                                                                                                |
| `enum[]`               | `string` Optional. Possible values of the field. This field can be used to restrict a value to a fixed set of values. To mark a field as an enum, set `format` to `enum` and provide the list of possible values in `enum` . For example: 1. To define directions: `{type:STRING, format:enum, enum:["EAST", "NORTH", "SOUTH", "WEST"]}` 2. To define apartment numbers: `{type:INTEGER, format:enum, enum:["101", "201", "301"]}`                                                                                  |
| `properties`           | `map (key: string, value: object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` ))` Optional. If type is `OBJECT` , `properties` is a map of property names to schema definitions for each property of the object. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                            |
| `propertyOrdering[]`   | `string` Optional. Order of properties displayed or used where order matters. This is not a standard field in OpenAPI specification, but can be used to control the order of properties.                                                                                                                                                                                                                                                                                                                            |
| `required[]`           | `string` Optional. If type is `OBJECT` , `required` lists the names of properties that must be present.                                                                                                                                                                                                                                                                                                                                                                                                             |
| `minProperties`        | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `OBJECT` , `min_properties` specifies the minimum number of properties that can be provided.                                                                                                                                                                                                                                                                                                            |
| `maxProperties`        | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `OBJECT` , `max_properties` specifies the maximum number of properties that can be provided.                                                                                                                                                                                                                                                                                                            |
| `minimum`              | `number` Optional. If type is `INTEGER` or `NUMBER` , `minimum` specifies the minimum allowed value.                                                                                                                                                                                                                                                                                                                                                                                                                |
| `maximum`              | `number` Optional. If type is `INTEGER` or `NUMBER` , `maximum` specifies the maximum allowed value.                                                                                                                                                                                                                                                                                                                                                                                                                |
| `minLength`            | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `STRING` , `min_length` specifies the minimum length of the string.                                                                                                                                                                                                                                                                                                                                     |
| `maxLength`            | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `STRING` , `max_length` specifies the maximum length of the string.                                                                                                                                                                                                                                                                                                                                     |
| `pattern`              | `string` Optional. If type is `STRING` , `pattern` specifies a regular expression that the string must match.                                                                                                                                                                                                                                                                                                                                                                                                       |
| `example`              | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. Example of an instance of this schema.                                                                                                                                                                                                                                                                                                                                                                      |
| `anyOf[]`              | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` )` Optional. The instance must be valid against any (one or more) of the subschemas listed in `any_of` .                                                                                                                                                                                                                                                     |
| `additionalProperties` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. If `type` is `OBJECT` , specifies how to handle properties not defined in `properties` . If it is a boolean `false` , no additional properties are allowed. If it is a schema, additional properties are allowed if they conform to the schema.                                                                                                                                                             |
| `ref`                  | `string` Optional. Allows referencing another schema definition to use in place of this schema. The value must be a valid reference to a schema in `defs` . For example, the following schema defines a reference to a schema node named "Pet": type: object properties: pet: ref: \#/defs/Pet defs: Pet: type: object properties: name: type: string The value of the "pet" property is a reference to the schema node named "Pet". See details in <https://json-schema.org/understanding-json-schema/structuring> |
| `defs`                 | `map (key: string, value: object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` ))` Optional. `defs` provides a map of schema definitions that can be reused by `ref` elsewhere in the schema. Only allowed at root level of the schema. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                      |

### PropertiesEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (Schema)
  }
}
```

| Fields  |                                                                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                  |
| `value` | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` )` |

### DefsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (Schema)
  }
}
```

| Fields  |                                                                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                  |
| `value` | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` )` |

### Retrieval

**JSON representation**

```
{
  "disableAttribution": boolean,

  // Union field source can be only one of the following:
  "vertexAiSearch": {
    object (VertexAISearch)
  },
  "vertexRagStore": {
    object (VertexRagStore)
  }
  // End of list of possible types for union field source.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>disableAttribution </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated. This option is no longer supported.</p></td>
</tr>
<tr class="even">
<td>Union field <code>source</code> . The source of the retrieval. <code>source</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>vertexAiSearch</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VertexAISearch"><code>VertexAISearch</code></a><code> )</code></p>
<p>Set to use data source powered by Agent Platform Search.</p></td>
</tr>
<tr class="even">
<td><code>vertexRagStore</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VertexRagStore"><code>VertexRagStore</code></a><code> )</code></p>
<p>Set to use data source powered by Vertex RAG store. User data is uploaded via the VertexRagDataService.</p></td>
</tr>
</tbody>
</table>

### VertexAISearch

**JSON representation**

```
{
  "datastore": string,
  "engine": string,
  "maxResults": integer,
  "filter": string,
  "dataStoreSpecs": [
    {
      object (DataStoreSpec)
    }
  ]
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                     |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `datastore`        | `string` Optional. Fully-qualified Agent Platform Search data store resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`                                                                                                                                                                                                                  |
| `engine`           | `string` Optional. Fully-qualified Agent Platform Search engine resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}`                                                                                                                                                                                                                            |
| `maxResults`       | `integer` Optional. Number of search results to return per query. The default value is 10. The maximumm allowed value is 10.                                                                                                                                                                                                                                                                        |
| `filter`           | `string` Optional. Filter strings to be passed to the search API.                                                                                                                                                                                                                                                                                                                                   |
| `dataStoreSpecs[]` | `object ( `[`DataStoreSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DataStoreSpec)` )` Specifications that define the specific DataStores to be searched, along with configurations for those data stores. This is only considered for Engines with multiple data stores. It should only be set if engine is used. |

### DataStoreSpec

**JSON representation**

```
{
  "dataStore": string,
  "filter": string
}
```

| Fields      |                                                                                                                                                                                                                                                 |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataStore` | `string` Full resource name of DataStore, such as Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`                                                                                             |
| `filter`    | `string` Optional. Filter specification to filter documents in the data store specified by data_store field. For more information on filtering, see [Filtering](https://cloud.google.com/generative-ai-app-builder/docs/filter-search-metadata) |

### VertexRagStore

**JSON representation**

```
{
  "ragCorpora": [
    string
  ],
  "ragResources": [
    {
      object (RagResource)
    }
  ],
  "ragRetrievalConfig": {
    object (RagRetrievalConfig)
  },
  "storeContext": boolean,

  // Union field _similarity_top_k can be only one of the following:
  "similarityTopK": integer
  // End of list of possible types for union field _similarity_top_k.

  // Union field _vector_distance_threshold can be only one of the following:
  "vectorDistanceThreshold": number
  // End of list of possible types for union field _vector_distance_threshold.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>ragCorpora[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated. Please use rag_resources instead.</p></td>
</tr>
<tr class="even">
<td><code>ragResources[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RagResource"><code>RagResource</code></a><code> )</code></p>
<p>Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.</p></td>
</tr>
<tr class="odd">
<td><code>ragRetrievalConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RagRetrievalConfig"><code>RagRetrievalConfig</code></a><code> )</code></p>
<p>Optional. The retrieval config for the Rag query.</p></td>
</tr>
<tr class="even">
<td><code>storeContext</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Currently only supported for Gemini Multimodal Live API.</p>
<p>In Gemini Multimodal Live API, if <code>store_context</code> bool is specified, Gemini will leverage it to automatically memorize the interactions between the client and Gemini, and retrieve context when needed to augment the response generation for users' ongoing and future interactions.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_similarity_top_k</code> .</p>
<p><code>_similarity_top_k</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>similarityTopK </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>integer</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Number of top k results to return from the selected corpora.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_vector_distance_threshold</code> .</p>
<p><code>_vector_distance_threshold</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>vectorDistanceThreshold </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>number</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Only return results with vector distance smaller than the threshold.</p></td>
</tr>
</tbody>
</table>

### RagResource

**JSON representation**

```
{
  "ragCorpus": string,
  "ragFileIds": [
    string
  ]
}
```

| Fields         |                                                                                                                        |
|----------------|------------------------------------------------------------------------------------------------------------------------|
| `ragCorpus`    | `string` Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}` |
| `ragFileIds[]` | `string` Optional. rag_file_id. The files should be in the same rag_corpus set in rag_corpus field.                    |

### RagRetrievalConfig

**JSON representation**

```
{
  "topK": integer,
  "hybridSearch": {
    object (HybridSearch)
  },
  "filter": {
    object (Filter)
  },
  "ranking": {
    object (Ranking)
  }
}
```

| Fields         |                                                                                                                                                                                                           |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `topK`         | `integer` Optional. The number of contexts to retrieve.                                                                                                                                                   |
| `hybridSearch` | `object ( `[`HybridSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.HybridSearch)` )` Optional. Config for Hybrid Search. |
| `filter`       | `object ( `[`Filter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Filter)` )` Optional. Config for filters.                   |
| `ranking`      | `object ( `[`Ranking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Ranking)` )` Optional. Config for ranking and reranking.   |

### HybridSearch

**JSON representation**

```
{

  // Union field _alpha can be only one of the following:
  "alpha": number
  // End of list of possible types for union field _alpha.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                         |
|-------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_alpha` . `_alpha` can be only one of the following: |                                                                                                                                                                                                                                                                                         |
| `alpha`                                                           | `number` Optional. Alpha value controls the weight between dense and sparse vector search results. The range is \[0, 1\], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally. |

### Filter

**JSON representation**

```
{
  "metadataFilter": string,

  // Union field vector_db_threshold can be only one of the following:
  "vectorDistanceThreshold": number,
  "vectorSimilarityThreshold": number
  // End of list of possible types for union field vector_db_threshold.
}
```

| Fields                                                                                                                                                                                         |                                                                                            |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| `metadataFilter`                                                                                                                                                                               | `string` Optional. String for metadata filtering.                                          |
| Union field `vector_db_threshold` . Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. `vector_db_threshold` can be only one of the following: |                                                                                            |
| `vectorDistanceThreshold`                                                                                                                                                                      | `number` Optional. Only returns contexts with vector distance smaller than the threshold.  |
| `vectorSimilarityThreshold`                                                                                                                                                                    | `number` Optional. Only returns contexts with vector similarity larger than the threshold. |

### Ranking

**JSON representation**

```
{

  // Union field ranking_config can be only one of the following:
  "rankService": {
    object (RankService)
  },
  "llmRanker": {
    object (LlmRanker)
  }
  // End of list of possible types for union field ranking_config.
}
```

| Fields                                                                                                                                                  |                                                                                                                                                                                                        |
|---------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `ranking_config` . Config options for ranking. Currently only Rank Service is supported. `ranking_config` can be only one of the following: |                                                                                                                                                                                                        |
| `rankService`                                                                                                                                           | `object ( `[`RankService`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RankService)` )` Optional. Config for Rank Service. |
| `llmRanker`                                                                                                                                             | `object ( `[`LlmRanker`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.LlmRanker)` )` Optional. Config for LlmRanker.        |

### RankService

**JSON representation**

```
{

  // Union field _model_name can be only one of the following:
  "modelName": string
  // End of list of possible types for union field _model_name.
}
```

| Fields                                                                      |                                                                                             |
|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| Union field `_model_name` . `_model_name` can be only one of the following: |                                                                                             |
| `modelName`                                                                 | `string` Optional. The model name of the rank service. Format: `semantic-ranker-512@latest` |

### LlmRanker

**JSON representation**

```
{

  // Union field _model_name can be only one of the following:
  "modelName": string
  // End of list of possible types for union field _model_name.
}
```

| Fields                                                                      |                                                                                                                                                                                |
|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_model_name` . `_model_name` can be only one of the following: |                                                                                                                                                                                |
| `modelName`                                                                 | `string` Optional. The model name used for ranking. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models) . |

### GoogleSearch

**JSON representation**

```
{
  "excludeDomains": [
    string
  ],

  // Union field _blocking_confidence can be only one of the following:
  "blockingConfidence": enum (PhishBlockThreshold)
  // End of list of possible types for union field _blocking_confidence.
}
```

| Fields                                                                                        |                                                                                                                                                                                                                                                                                            |
|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `excludeDomains[]`                                                                            | `string` Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: \["amazon.com", "facebook.com"\].                                                                                                                                   |
| Union field `_blocking_confidence` . `_blocking_confidence` can be only one of the following: |                                                                                                                                                                                                                                                                                            |
| `blockingConfidence`                                                                          | `enum ( `[`PhishBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PhishBlockThreshold)` )` Optional. Sites with confidence level chosen & above this value will be blocked from the search results. |

### GoogleSearchRetrieval

**JSON representation**

```
{
  "dynamicRetrievalConfig": {
    object (DynamicRetrievalConfig)
  }
}
```

| Fields                   |                                                                                                                                                                                                                                                               |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dynamicRetrievalConfig` | `object ( `[`DynamicRetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DynamicRetrievalConfig)` )` Specifies the dynamic retrieval configuration for the given source. |

### DynamicRetrievalConfig

**JSON representation**

```
{
  "mode": enum (Mode),

  // Union field _dynamic_threshold can be only one of the following:
  "dynamicThreshold": number
  // End of list of possible types for union field _dynamic_threshold.
}
```

| Fields                                                                                    |                                                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mode`                                                                                    | `enum ( `[`Mode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Mode)` )` The mode of the predictor to be used in dynamic retrieval. |
| Union field `_dynamic_threshold` . `_dynamic_threshold` can be only one of the following: |                                                                                                                                                                                                                |
| `dynamicThreshold`                                                                        | `number` Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used.                                                                                                  |

### GoogleMaps

**JSON representation**

```
{
  "enableWidget": boolean,
  "groundingTypes": {
    object (GroundingTypes)
  }
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>enableWidget </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: The Google Maps contextual widget behavior in Grounding with Google Maps is being deprecated; this field is planned for removal and no longer has any effect once removed.</p>
<p>If true, include the widget context token in the response.</p></td>
</tr>
<tr class="even">
<td><code>groundingTypes</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GroundingTypes"><code>GroundingTypes</code></a><code> )</code></p>
<p>Optional. Specifies the types of Google Maps grounding to enable. Defaults to <code>places</code> when unset.</p></td>
</tr>
</tbody>
</table>

### GroundingTypes

**JSON representation**

```
{
  "places": {
    object (Places)
  },
  "routing": {
    object (Routing)
  }
}
```

| Fields    |                                                                                                                                                         |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `places`  | `object ( ``Places`` )` Optional. Enables grounding with Google Maps Places. This is the default grounding type when no `GroundingTypes` are specified. |
| `routing` | `object ( ``Routing`` )` Optional. Enables grounding with Google Maps Routing APIs (ComputeRoutes and SearchAlongRoute).                                |

### EnterpriseWebSearch

**JSON representation**

```
{
  "excludeDomains": [
    string
  ],

  // Union field _blocking_confidence can be only one of the following:
  "blockingConfidence": enum (PhishBlockThreshold)
  // End of list of possible types for union field _blocking_confidence.
}
```

| Fields                                                                                        |                                                                                                                                                                                                                                                                                            |
|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `excludeDomains[]`                                                                            | `string` Optional. List of domains to be excluded from the search results. The default limit is 2000 domains.                                                                                                                                                                              |
| Union field `_blocking_confidence` . `_blocking_confidence` can be only one of the following: |                                                                                                                                                                                                                                                                                            |
| `blockingConfidence`                                                                          | `enum ( `[`PhishBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PhishBlockThreshold)` )` Optional. Sites with confidence level chosen & above this value will be blocked from the search results. |

### ParallelAiSearch

**JSON representation**

```
{
  "apiKey": string,
  "customConfigs": {
    object
  }
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `apiKey`        | `string` Optional. The API key for ParallelAiSearch. If an API key is not provided, the system will attempt to verify access by checking for an active Parallel.ai subscription through the Google Cloud Marketplace. See <https://docs.parallel.ai/search/search-quickstart> for more details.                                                                                                                                                                                                                                                                                                                                                                                       |
| `customConfigs` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. Custom configs for ParallelAiSearch. This field can be used to pass any parameter from the Parallel.ai Search API. See the Parallel.ai documentation for the full list of available parameters and their usage: <https://docs.parallel.ai/api-reference/search-beta/search> Currently only `source_policy` , `excerpts` , `max_results` , `mode` , `fetch_policy` can be set via this field. For example: { "source_policy": { "include_domains": \["google.com", "wikipedia.org"\], "exclude_domains": \["example.com"\] }, "fetch_policy": { "max_age_seconds": 3600 } } |

### ComputerUse

**JSON representation**

```
{
  "environment": enum (Environment),
  "excludedPredefinedFunctions": [
    string
  ]
}
```

| Fields                          |                                                                                                                                                                                                                                                                                                                                                                                                                     |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `environment`                   | `enum ( `[`Environment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Environment)` )` Required. The environment being operated.                                                                                                                                                                                                         |
| `excludedPredefinedFunctions[]` | `string` Optional. By default, [predefined functions](https://cloud.google.com/vertex-ai/generative-ai/docs/computer-use#supported-actions) are included in the final model call. Some of them can be explicitly excluded from being automatically included. This can serve two purposes: 1. Using a more restricted / different action space. 2. Improving the definitions / instructions of predefined functions. |

### GenerationConfig

**JSON representation**

```
{
  "stopSequences": [
    string
  ],
  "responseMimeType": string,
  "responseModalities": [
    enum (Modality)
  ],
  "thinkingConfig": {
    object (ThinkingConfig)
  },
  "modelConfig": {
    object (ModelConfig)
  },
  "responseFormat": [
    {
      object (ResponseFormat)
    }
  ],

  // Union field _temperature can be only one of the following:
  "temperature": number
  // End of list of possible types for union field _temperature.

  // Union field _top_p can be only one of the following:
  "topP": number
  // End of list of possible types for union field _top_p.

  // Union field _top_k can be only one of the following:
  "topK": number
  // End of list of possible types for union field _top_k.

  // Union field _candidate_count can be only one of the following:
  "candidateCount": integer
  // End of list of possible types for union field _candidate_count.

  // Union field _max_output_tokens can be only one of the following:
  "maxOutputTokens": integer
  // End of list of possible types for union field _max_output_tokens.

  // Union field _response_logprobs can be only one of the following:
  "responseLogprobs": boolean
  // End of list of possible types for union field _response_logprobs.

  // Union field _logprobs can be only one of the following:
  "logprobs": integer
  // End of list of possible types for union field _logprobs.

  // Union field _presence_penalty can be only one of the following:
  "presencePenalty": number
  // End of list of possible types for union field _presence_penalty.

  // Union field _frequency_penalty can be only one of the following:
  "frequencyPenalty": number
  // End of list of possible types for union field _frequency_penalty.

  // Union field _seed can be only one of the following:
  "seed": integer
  // End of list of possible types for union field _seed.

  // Union field _response_schema can be only one of the following:
  "responseSchema": {
    object (Schema)
  }
  // End of list of possible types for union field _response_schema.

  // Union field _response_json_schema can be only one of the following:
  "responseJsonSchema": value
  // End of list of possible types for union field _response_json_schema.

  // Union field _routing_config can be only one of the following:
  "routingConfig": {
    object (RoutingConfig)
  }
  // End of list of possible types for union field _routing_config.

  // Union field _audio_timestamp can be only one of the following:
  "audioTimestamp": boolean
  // End of list of possible types for union field _audio_timestamp.

  // Union field _media_resolution can be only one of the following:
  "mediaResolution": enum (MediaResolution)
  // End of list of possible types for union field _media_resolution.

  // Union field _speech_config can be only one of the following:
  "speechConfig": {
    object (SpeechConfig)
  }
  // End of list of possible types for union field _speech_config.

  // Union field _enable_affective_dialog can be only one of the following:
  "enableAffectiveDialog": boolean
  // End of list of possible types for union field _enable_affective_dialog.

  // Union field _image_config can be only one of the following:
  "imageConfig": {
    object (ImageConfig)
  }
  // End of list of possible types for union field _image_config.

  // Union field _audio_transcription_config can be only one of the following:
  "audioTranscriptionConfig": {
    object (AudioTranscriptionConfig)
  }
  // End of list of possible types for union field _audio_transcription_config.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>stopSequences[]</code></td>
<td><p><code>string</code></p>
<p>Optional. A list of character sequences that will stop the model from generating further tokens. If a stop sequence is generated, the output will end at that point. This is useful for controlling the length and structure of the output. For example, you can use ["\n", "###"] to stop generation at a new line or a specific marker.</p></td>
</tr>
<tr class="even">
<td><code>responseMimeType </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. The IANA standard MIME type of the response. The model will generate output that conforms to this MIME type. Supported values include 'text/plain' (default) and 'application/json'. The model needs to be prompted to output the appropriate response type, otherwise the behavior is undefined. Deprecated: Use <code>response_format</code> instead.</p></td>
</tr>
<tr class="odd">
<td><code>responseModalities[]</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Modality"><code>Modality</code></a><code> )</code></p>
<p>Optional. The modalities of the response. The model will generate a response that includes all the specified modalities. For example, if this is set to <code>[TEXT, IMAGE]</code> , the response will include both text and an image.</p></td>
</tr>
<tr class="even">
<td><code>thinkingConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ThinkingConfig"><code>ThinkingConfig</code></a><code> )</code></p>
<p>Optional. Configuration for thinking features. An error will be returned if this field is set for models that don't support thinking.</p></td>
</tr>
<tr class="odd">
<td><code>modelConfig </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ModelConfig"><code>ModelConfig</code></a><code> )</code></p>
<blockquote>
<p>Optional. The <code>model_config</code> field is deprecated and is not supported anymore. Use <code>routing_config</code> instead.</p>
</blockquote>
<p>Optional. Config for model selection.</p></td>
</tr>
<tr class="even">
<td><code>responseFormat[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ResponseFormat"><code>ResponseFormat</code></a><code> )</code></p>
<p>Optional. New response format field for the model to configure output formatting and delivery.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_temperature</code> .</p>
<p><code>_temperature</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>temperature</code></td>
<td><p><code>number</code></p>
<p>Optional. Controls the randomness of the output. A higher temperature results in more creative and diverse responses, while a lower temperature makes the output more predictable and focused. The valid range is (0.0, 2.0].</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_top_p</code> .</p>
<p><code>_top_p</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>topP</code></td>
<td><p><code>number</code></p>
<p>Optional. Specifies the nucleus sampling threshold. The model considers only the smallest set of tokens whose cumulative probability is at least <code>top_p</code> . This helps generate more diverse and less repetitive responses. For example, a <code>top_p</code> of 0.9 means the model considers tokens until the cumulative probability of the tokens to select from reaches 0.9. It's recommended to adjust either temperature or <code>top_p</code> , but not both.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_top_k</code> .</p>
<p><code>_top_k</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>topK</code></td>
<td><p><code>number</code></p>
<p>Optional. Specifies the top-k sampling threshold. The model considers only the top k most probable tokens for the next token. This can be useful for generating more coherent and less random text. For example, a <code>top_k</code> of 40 means the model will choose the next word from the 40 most likely words.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_candidate_count</code> .</p>
<p><code>_candidate_count</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>candidateCount</code></td>
<td><p><code>integer</code></p>
<p>Optional. The number of candidate responses to generate.</p>
<p>A higher <code>candidate_count</code> can provide more options to choose from, but it also consumes more resources. This can be useful for generating a variety of responses and selecting the best one.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_max_output_tokens</code> .</p>
<p><code>_max_output_tokens</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>maxOutputTokens</code></td>
<td><p><code>integer</code></p>
<p>Optional. The maximum number of tokens to generate in the response.</p>
<p>A token is approximately four characters. The default value varies by model. This parameter can be used to control the length of the generated text and prevent overly long responses.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_response_logprobs</code> .</p>
<p><code>_response_logprobs</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>responseLogprobs</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If set to true, the log probabilities of the output tokens are returned.</p>
<p>Log probabilities are the logarithm of the probability of a token appearing in the output. A higher log probability means the token is more likely to be generated. This can be useful for analyzing the model's confidence in its own output and for debugging.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_logprobs</code> .</p>
<p><code>_logprobs</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>logprobs</code></td>
<td><p><code>integer</code></p>
<p>Optional. The number of top log probabilities to return for each token.</p>
<p>This can be used to see which other tokens were considered likely candidates for a given position. A higher value will return more options, but it will also increase the size of the response.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_presence_penalty</code> .</p>
<p><code>_presence_penalty</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>presencePenalty</code></td>
<td><p><code>number</code></p>
<p>Optional. Penalizes tokens that have already appeared in the generated text. A positive value encourages the model to generate more diverse and less repetitive text. Valid values can range from [-2.0, 2.0].</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_frequency_penalty</code> .</p>
<p><code>_frequency_penalty</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>frequencyPenalty</code></td>
<td><p><code>number</code></p>
<p>Optional. Penalizes tokens based on their frequency in the generated text. A positive value helps to reduce the repetition of words and phrases. Valid values can range from [-2.0, 2.0].</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_seed</code> .</p>
<p><code>_seed</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>seed</code></td>
<td><p><code>integer</code></p>
<p>Optional. A seed for the random number generator.</p>
<p>By setting a seed, you can make the model's output mostly deterministic. For a given prompt and parameters (like temperature, top_p, etc.), the model will produce the same response every time. However, it's not a guaranteed absolute deterministic behavior. This is different from parameters like <code>temperature</code> , which control the <em>level</em> of randomness. <code>seed</code> ensures that the "random" choices the model makes are the same on every run, making it essential for testing and ensuring reproducible results.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_response_schema</code> .</p>
<p><code>_response_schema</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>responseSchema </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema"><code>Schema</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Lets you to specify a schema for the model's response, ensuring that the output conforms to a particular structure. This is useful for generating structured data such as JSON. The schema is a subset of the <a href="https://spec.openapis.org/oas/v3.0.3#schema">OpenAPI 3.0 schema object</a> object.</p>
<p>When this field is set, you must also set the <code>response_mime_type</code> to <code>application/json</code> . Deprecated: Use <code>response_format</code> instead.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_response_json_schema</code> .</p>
<p><code>_response_json_schema</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>responseJsonSchema </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. When this field is set, <code>response_schema</code> must be omitted and <code>response_mime_type</code> must be set to <code>application/json</code> . Deprecated: Use <code>response_format</code> instead.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_routing_config</code> .</p>
<p><code>_routing_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>routingConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RoutingConfig"><code>RoutingConfig</code></a><code> )</code></p>
<p>Optional. Routing configuration.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_audio_timestamp</code> .</p>
<p><code>_audio_timestamp</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>audioTimestamp</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If enabled, audio timestamps will be included in the request to the model. This can be useful for synchronizing audio with other modalities in the response.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_media_resolution</code> .</p>
<p><code>_media_resolution</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>mediaResolution</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MediaResolution_1"><code>MediaResolution</code></a><code> )</code></p>
<p>Optional. The token resolution at which input media content is sampled. This is used to control the trade-off between the quality of the response and the number of tokens used to represent the media. A higher resolution allows the model to perceive more detail, which can lead to a more nuanced response, but it will also use more tokens. This does not affect the image dimensions sent to the model.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_speech_config</code> .</p>
<p><code>_speech_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>speechConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SpeechConfig"><code>SpeechConfig</code></a><code> )</code></p>
<p>Optional. The speech generation config.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_enable_affective_dialog</code> .</p>
<p><code>_enable_affective_dialog</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>enableAffectiveDialog</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If enabled, the model will detect emotions and adapt its responses accordingly. For example, if the model detects that the user is frustrated, it may provide a more empathetic response.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_image_config</code> .</p>
<p><code>_image_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>imageConfig </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ImageConfig"><code>ImageConfig</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Config for image generation features. Deprecated: Use <code>response_format.image</code> instead.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_audio_transcription_config</code> .</p>
<p><code>_audio_transcription_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>audioTranscriptionConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AudioTranscriptionConfig"><code>AudioTranscriptionConfig</code></a><code> )</code></p>
<p>Optional. Config for audio transcription (speech recognition).</p></td>
</tr>
</tbody>
</table>

### RoutingConfig

**JSON representation**

```
{

  // Union field routing_config can be only one of the following:
  "autoMode": {
    object (AutoRoutingMode)
  },
  "manualMode": {
    object (ManualRoutingMode)
  }
  // End of list of possible types for union field routing_config.
}
```

| Fields                                                                                                              |                                                                                                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `routing_config` . The routing mode for the request. `routing_config` can be only one of the following: |                                                                                                                                                                                                                                                                    |
| `autoMode`                                                                                                          | `object ( `[`AutoRoutingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AutoRoutingMode)` )` In this mode, the model is selected automatically based on the content of the request. |
| `manualMode`                                                                                                        | `object ( `[`ManualRoutingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ManualRoutingMode)` )` In this mode, the model is specified manually.                                     |

### AutoRoutingMode

**JSON representation**

```
{

  // Union field _model_routing_preference can be only one of the following:
  "modelRoutingPreference": enum (ModelRoutingPreference)
  // End of list of possible types for union field _model_routing_preference.
}
```

| Fields                                                                                                  |                                                                                                                                                                                                                       |
|---------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_model_routing_preference` . `_model_routing_preference` can be only one of the following: |                                                                                                                                                                                                                       |
| `modelRoutingPreference`                                                                                | `enum ( `[`ModelRoutingPreference`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ModelRoutingPreference)` )` The model routing preference. |

### ManualRoutingMode

**JSON representation**

```
{

  // Union field _model_name can be only one of the following:
  "modelName": string
  // End of list of possible types for union field _model_name.
}
```

| Fields                                                                      |                                                                             |
|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| Union field `_model_name` . `_model_name` can be only one of the following: |                                                                             |
| `modelName`                                                                 | `string` The name of the model to use. Only public LLM models are accepted. |

### SpeechConfig

**JSON representation**

```
{
  "voiceConfig": {
    object (VoiceConfig)
  },
  "languageCode": string,
  "multiSpeakerVoiceConfig": {
    object (MultiSpeakerVoiceConfig)
  }
}
```

| Fields                    |                                                                                                                                                                                                                                                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `voiceConfig`             | `object ( `[`VoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VoiceConfig)` )` The configuration for the voice to use.                                                                                                      |
| `languageCode`            | `string` Optional. The language code (ISO 639-1) for the speech synthesis.                                                                                                                                                                                                                                       |
| `multiSpeakerVoiceConfig` | `object ( `[`MultiSpeakerVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MultiSpeakerVoiceConfig)` )` The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config` . |

### VoiceConfig

**JSON representation**

```
{

  // Union field voice_config can be only one of the following:
  "prebuiltVoiceConfig": {
    object (PrebuiltVoiceConfig)
  },
  "replicatedVoiceConfig": {
    object (ReplicatedVoiceConfig)
  }
  // End of list of possible types for union field voice_config.
}
```

| Fields                                                                                                                  |                                                                                                                                                                                                                                                                                                           |
|-------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `voice_config` . The configuration for the speaker to use. `voice_config` can be only one of the following: |                                                                                                                                                                                                                                                                                                           |
| `prebuiltVoiceConfig`                                                                                                   | `object ( `[`PrebuiltVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PrebuiltVoiceConfig)` )` The configuration for a prebuilt voice.                                                                               |
| `replicatedVoiceConfig`                                                                                                 | `object ( `[`ReplicatedVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ReplicatedVoiceConfig)` )` Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample. |

### PrebuiltVoiceConfig

**JSON representation**

```
{

  // Union field _voice_name can be only one of the following:
  "voiceName": string
  // End of list of possible types for union field _voice_name.
}
```

| Fields                                                                      |                                                 |
|-----------------------------------------------------------------------------|-------------------------------------------------|
| Union field `_voice_name` . `_voice_name` can be only one of the following: |                                                 |
| `voiceName`                                                                 | `string` The name of the prebuilt voice to use. |

### ReplicatedVoiceConfig

**JSON representation**

```
{
  "mimeType": string,
  "voiceSampleAudio": string
}
```

| Fields             |                                                                                                                                                                                                                                                |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mimeType`         | `string` Optional. The mimetype of the voice sample. The only currently supported value is `audio/wav` . This represents 16-bit signed little-endian wav data, with a 24kHz sampling rate. `mime_type` will default to `audio/wav` if not set. |
| `voiceSampleAudio` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. The sample of the custom voice. A base64-encoded string.                                                                                      |

### MultiSpeakerVoiceConfig

**JSON representation**

```
{
  "speakerVoiceConfigs": [
    {
      object (SpeakerVoiceConfig)
    }
  ]
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                 |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `speakerVoiceConfigs[]` | `object ( `[`SpeakerVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SpeakerVoiceConfig)` )` Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided. |

### SpeakerVoiceConfig

**JSON representation**

```
{
  "speaker": string,
  "voiceConfig": {
    object (VoiceConfig)
  }
}
```

| Fields        |                                                                                                                                                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `speaker`     | `string` Required. The name of the speaker. This should be the same as the speaker name used in the prompt.                                                                                                                    |
| `voiceConfig` | `object ( `[`VoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VoiceConfig)` )` Required. The configuration for the voice of this speaker. |

### ThinkingConfig

**JSON representation**

```
{

  // Union field _include_thoughts can be only one of the following:
  "includeThoughts": boolean
  // End of list of possible types for union field _include_thoughts.

  // Union field _thinking_budget can be only one of the following:
  "thinkingBudget": integer
  // End of list of possible types for union field _thinking_budget.

  // Union field _thinking_level can be only one of the following:
  "thinkingLevel": enum (ThinkingLevel)
  // End of list of possible types for union field _thinking_level.
}
```

| Fields                                                                                  |                                                                                                                                                                                                                                                                                                                            |
|-----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_include_thoughts` . `_include_thoughts` can be only one of the following: |                                                                                                                                                                                                                                                                                                                            |
| `includeThoughts`                                                                       | `boolean` Optional. If true, the model will include its thoughts in the response. "Thoughts" are the intermediate steps the model takes to arrive at the final response. They can provide insights into the model's reasoning process and help with debugging. If this is true, thoughts are returned only when available. |
| Union field `_thinking_budget` . `_thinking_budget` can be only one of the following:   |                                                                                                                                                                                                                                                                                                                            |
| `thinkingBudget`                                                                        | `integer` Optional. The token budget for the model's thinking process. The model will make a best effort to stay within this budget. This can be used to control the trade-off between response quality and latency.                                                                                                       |
| Union field `_thinking_level` . `_thinking_level` can be only one of the following:     |                                                                                                                                                                                                                                                                                                                            |
| `thinkingLevel`                                                                         | `enum ( `[`ThinkingLevel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ThinkingLevel)` )` Optional. The number of thoughts tokens that the model should generate.                                                                              |

### ModelConfig

**JSON representation**

```
{
  "featureSelectionPreference": enum (FeatureSelectionPreference)
}
```

| Fields                       |                                                                                                                                                                                                                                         |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `featureSelectionPreference` | `enum ( `[`FeatureSelectionPreference`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FeatureSelectionPreference)` )` Required. Feature selection preference. |

### ImageConfig

**JSON representation**

```
{

  // Union field _image_output_options can be only one of the following:
  "imageOutputOptions": {
    object (ImageOutputOptions)
  }
  // End of list of possible types for union field _image_output_options.

  // Union field _aspect_ratio can be only one of the following:
  "aspectRatio": string
  // End of list of possible types for union field _aspect_ratio.

  // Union field _person_generation can be only one of the following:
  "personGeneration": enum (PersonGeneration)
  // End of list of possible types for union field _person_generation.

  // Union field _image_size can be only one of the following:
  "imageSize": string
  // End of list of possible types for union field _image_size.
}
```

| Fields                                                                                          |                                                                                                                                                                                                                                           |
|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_image_output_options` . `_image_output_options` can be only one of the following: |                                                                                                                                                                                                                                           |
| `imageOutputOptions`                                                                            | `object ( `[`ImageOutputOptions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ImageOutputOptions)` )` Optional. The image output format for generated images. |
| Union field `_aspect_ratio` . `_aspect_ratio` can be only one of the following:                 |                                                                                                                                                                                                                                           |
| `aspectRatio`                                                                                   | `string` Optional. The desired aspect ratio for the generated images. The following aspect ratios are supported: "1:1" "2:3", "3:2" "3:4", "4:3" "4:5", "5:4" "9:16", "16:9" "21:9"                                                       |
| Union field `_person_generation` . `_person_generation` can be only one of the following:       |                                                                                                                                                                                                                                           |
| `personGeneration`                                                                              | `enum ( `[`PersonGeneration`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PersonGeneration)` )` Optional. Controls whether the model can generate people.     |
| Union field `_image_size` . `_image_size` can be only one of the following:                     |                                                                                                                                                                                                                                           |
| `imageSize`                                                                                     | `string` Optional. Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .                                                                            |

### ImageOutputOptions

**JSON representation**

```
{

  // Union field _mime_type can be only one of the following:
  "mimeType": string
  // End of list of possible types for union field _mime_type.

  // Union field _compression_quality can be only one of the following:
  "compressionQuality": integer
  // End of list of possible types for union field _compression_quality.
}
```

| Fields                                                                                        |                                                                         |
|-----------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_mime_type` . `_mime_type` can be only one of the following:                     |                                                                         |
| `mimeType`                                                                                    | `string` Optional. The image format that the output should be saved as. |
| Union field `_compression_quality` . `_compression_quality` can be only one of the following: |                                                                         |
| `compressionQuality`                                                                          | `integer` Optional. The compression quality of the output image.        |

### ResponseFormat

**JSON representation**

```
{

  // Union field format can be only one of the following:
  "text": {
    object (TextResponseFormat)
  },
  "audio": {
    object (AudioResponseFormat)
  },
  "image": {
    object (ImageResponseFormat)
  },
  "video": {
    object (VideoResponseFormat)
  }
  // End of list of possible types for union field format.
}
```

| Fields                                                                                              |                                                                                                                                                                                                          |
|-----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `format` . The format of the output content. `format` can be only one of the following: |                                                                                                                                                                                                          |
| `text`                                                                                              | `object ( `[`TextResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TextResponseFormat)` )` Text output format.    |
| `audio`                                                                                             | `object ( `[`AudioResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AudioResponseFormat)` )` Audio output format. |
| `image`                                                                                             | `object ( `[`ImageResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ImageResponseFormat)` )` Image output format. |
| `video`                                                                                             | `object ( `[`VideoResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VideoResponseFormat)` )` Video output format. |

### TextResponseFormat

**JSON representation**

```
{

  // Union field _mime_type can be only one of the following:
  "mimeType": enum (MimeType)
  // End of list of possible types for union field _mime_type.

  // Union field _schema can be only one of the following:
  "schema": value
  // End of list of possible types for union field _schema.
}
```

| Fields                                                                    |                                                                                                                                                                                                                    |
|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_mime_type` . `_mime_type` can be only one of the following: |                                                                                                                                                                                                                    |
| `mimeType`                                                                | `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MimeType)` )` Optional. The IANA standard MIME type of the response. |
| Union field `_schema` . `_schema` can be only one of the following:       |                                                                                                                                                                                                                    |
| `schema`                                                                  | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. The JSON schema that the output should conform to. Only applicable when mime_type is APPLICATION_JSON.     |

### AudioResponseFormat

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),

  // Union field _mime_type can be only one of the following:
  "mimeType": enum (MimeType)
  // End of list of possible types for union field _mime_type.

  // Union field _sample_rate can be only one of the following:
  "sampleRate": integer
  // End of list of possible types for union field _sample_rate.

  // Union field _bit_rate can be only one of the following:
  "bitRate": integer
  // End of list of possible types for union field _bit_rate.
}
```

| Fields                                                                        |                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `delivery`                                                                    | `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DeliveryMode)` )` Optional. Delivery mode for the generated content. |
| Union field `_mime_type` . `_mime_type` can be only one of the following:     |                                                                                                                                                                                                                        |
| `mimeType`                                                                    | `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MimeType_1)` )` Optional. The MIME type of the audio output.             |
| Union field `_sample_rate` . `_sample_rate` can be only one of the following: |                                                                                                                                                                                                                        |
| `sampleRate`                                                                  | `integer` Optional. Sample rate for the generated audio in Hertz.                                                                                                                                                      |
| Union field `_bit_rate` . `_bit_rate` can be only one of the following:       |                                                                                                                                                                                                                        |
| `bitRate`                                                                     | `integer` Optional. Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).                                                                                                             |

### ImageResponseFormat

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),

  // Union field _mime_type can be only one of the following:
  "mimeType": enum (MimeType)
  // End of list of possible types for union field _mime_type.

  // Union field _aspect_ratio can be only one of the following:
  "aspectRatio": enum (AspectRatio)
  // End of list of possible types for union field _aspect_ratio.

  // Union field _image_size can be only one of the following:
  "imageSize": enum (ImageSize)
  // End of list of possible types for union field _image_size.
}
```

| Fields                                                                          |                                                                                                                                                                                                                        |
|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `delivery`                                                                      | `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DeliveryMode)` )` Optional. Delivery mode for the generated content. |
| Union field `_mime_type` . `_mime_type` can be only one of the following:       |                                                                                                                                                                                                                        |
| `mimeType`                                                                      | `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MimeType_2)` )` Optional. The MIME type of the image output.             |
| Union field `_aspect_ratio` . `_aspect_ratio` can be only one of the following: |                                                                                                                                                                                                                        |
| `aspectRatio`                                                                   | `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AspectRatio)` )` Optional. The aspect ratio for the image output.     |
| Union field `_image_size` . `_image_size` can be only one of the following:     |                                                                                                                                                                                                                        |
| `imageSize`                                                                     | `enum ( `[`ImageSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ImageSize)` )` Optional. The size of the image output.                  |

### VideoResponseFormat

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),
  "gcsUri": string,
  "aspectRatio": enum (AspectRatio),

  // Union field _duration can be only one of the following:
  "duration": string
  // End of list of possible types for union field _duration.
}
```

| Fields                                                                  |                                                                                                                                                                                                                                                     |
|-------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `delivery`                                                              | `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DeliveryMode)` )` Optional. Delivery mode for the generated content.                              |
| `gcsUri`                                                                | `string` Optional. The Google Cloud Storage URI to store the video output. Required for Vertex if delivery is URI.                                                                                                                                  |
| `aspectRatio`                                                           | `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AspectRatio_1)` )` The aspect ratio for the video output.                                          |
| Union field `_duration` . `_duration` can be only one of the following: |                                                                                                                                                                                                                                                     |
| `duration`                                                              | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. The duration for the video output. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |

### AudioTranscriptionConfig

**JSON representation**

```
{
  "adaptationPhrases": [
    string
  ],
  "customVocabulary": [
    string
  ],
  "wordTimestamp": boolean,
  "diarization": boolean,

  // Union field language_config can be only one of the following:
  "languageAuto": {
    object (LanguageAuto)
  },
  "languageHints": {
    object (LanguageHints)
  }
  // End of list of possible types for union field language_config.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>adaptationPhrases[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. A list of phrases to bias the ASR model towards.</p></td>
</tr>
<tr class="even">
<td><code>customVocabulary[]</code></td>
<td><p><code>string</code></p>
<p>Optional. A list of custom vocabulary phrases to bias the speech recognition model toward recognizing specific terms.</p></td>
</tr>
<tr class="odd">
<td><code>wordTimestamp</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Configures word-level timestamp generation.</p></td>
</tr>
<tr class="even">
<td><code>diarization</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Configures speaker diarization.</p></td>
</tr>
<tr class="odd">
<td>Union field <code>language_config</code> . Required. Specifies how to handle the languages in the audio. <code>language_config</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>languageAuto</code></td>
<td><p><code>object ( </code><code>LanguageAuto</code><code> )</code></p>
<p>Optional. The model will detect the language automatically.</p></td>
</tr>
<tr class="odd">
<td><code>languageHints</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.LanguageHints"><code>LanguageHints</code></a><code> )</code></p>
<p>Optional. Specifies one or more languages in the audio.</p></td>
</tr>
</tbody>
</table>

### LanguageHints

**JSON representation**

```
{
  "languageCodes": [
    string
  ]
}
```

| Fields            |                                                                           |
|-------------------|---------------------------------------------------------------------------|
| `languageCodes[]` | `string` Required. BCP-47 language codes. At least one must be specified. |

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### Language

Supported programming languages for the generated code.

| Enums                  |                                                      |
|------------------------|------------------------------------------------------|
| `LANGUAGE_UNSPECIFIED` | Unspecified language. This value should not be used. |
| `PYTHON`               | Python \>= 3.10, with numpy and simpy available.     |

### Outcome

Enumeration of possible outcomes of the code execution.

| Enums                       |                                                                                                         |
|-----------------------------|---------------------------------------------------------------------------------------------------------|
| `OUTCOME_UNSPECIFIED`       | Unspecified status. This value should not be used.                                                      |
| `OUTCOME_OK`                | Code execution completed successfully. `output` contains the stdout, if any.                            |
| `OUTCOME_FAILED`            | Code execution failed. `output` contains the stderr and stdout, if any.                                 |
| `OUTCOME_DEADLINE_EXCEEDED` | Code execution ran for too long, and was cancelled. There may or may not be a partial `output` present. |

### Level

The media resolution level.

| Enums                          |                                                             |
|--------------------------------|-------------------------------------------------------------|
| `MEDIA_RESOLUTION_UNSPECIFIED` | Media resolution has not been set.                          |
| `MEDIA_RESOLUTION_LOW`         | Media resolution set to low.                                |
| `MEDIA_RESOLUTION_MEDIUM`      | Media resolution set to medium.                             |
| `MEDIA_RESOLUTION_HIGH`        | Media resolution set to high.                               |
| `MEDIA_RESOLUTION_ULTRA_HIGH`  | Media resolution set to ultra high. This is for image only. |

### Type

Type contains the list of OpenAPI data types as defined by <https://swagger.io/docs/specification/data-models/data-types/>

| Enums              |                                    |
|--------------------|------------------------------------|
| `TYPE_UNSPECIFIED` | Not specified, should not be used. |
| `STRING`           | OpenAPI string type                |
| `NUMBER`           | OpenAPI number type                |
| `INTEGER`          | OpenAPI integer type               |
| `BOOLEAN`          | OpenAPI boolean type               |
| `ARRAY`            | OpenAPI array type                 |
| `OBJECT`           | OpenAPI object type                |
| `NULL`             | Null type                          |

### PhishBlockThreshold

These are available confidence level user can set to block malicious urls with chosen confidence and above. For understanding different confidence of webrisk, please refer to <https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel>

| Enums                               |                                                          |
|-------------------------------------|----------------------------------------------------------|
| `PHISH_BLOCK_THRESHOLD_UNSPECIFIED` | Defaults to unspecified.                                 |
| `BLOCK_LOW_AND_ABOVE`               | Blocks Low and above confidence URL that is risky.       |
| `BLOCK_MEDIUM_AND_ABOVE`            | Blocks Medium and above confidence URL that is risky.    |
| `BLOCK_HIGH_AND_ABOVE`              | Blocks High and above confidence URL that is risky.      |
| `BLOCK_HIGHER_AND_ABOVE`            | Blocks Higher and above confidence URL that is risky.    |
| `BLOCK_VERY_HIGH_AND_ABOVE`         | Blocks Very high and above confidence URL that is risky. |
| `BLOCK_ONLY_EXTREMELY_HIGH`         | Blocks Extremely high confidence URL that is risky.      |

### Mode

The mode of the predictor to be used in dynamic retrieval.

| Enums              |                                                         |
|--------------------|---------------------------------------------------------|
| `MODE_UNSPECIFIED` | Always trigger retrieval.                               |
| `MODE_DYNAMIC`     | Run retrieval only when system decides it is necessary. |

### Environment

Represents the environment being operated, such as a web browser.

| Enums                     |                            |
|---------------------------|----------------------------|
| `ENVIRONMENT_UNSPECIFIED` | Defaults to browser.       |
| `ENVIRONMENT_BROWSER`     | Operates in a web browser. |

### ModelRoutingPreference

The model routing preference.

| Enums                |                                                                       |
|----------------------|-----------------------------------------------------------------------|
| `UNKNOWN`            | Unspecified model routing preference.                                 |
| `PRIORITIZE_QUALITY` | The model will be selected to prioritize the quality of the response. |
| `BALANCED`           | The model will be selected to balance quality and cost.               |
| `PRIORITIZE_COST`    | The model will be selected to prioritize the cost of the request.     |

### Modality

The modalities of the response.

| Enums                  |                                                  |
|------------------------|--------------------------------------------------|
| `MODALITY_UNSPECIFIED` | Unspecified modality. Will be processed as text. |
| `TEXT`                 | Text modality.                                   |
| `IMAGE`                | Image modality.                                  |
| `AUDIO`                | Audio modality.                                  |
| `VIDEO`                | Video modality.                                  |

### MediaResolution

Media resolution for the input media.

| Enums                          |                                                                  |
|--------------------------------|------------------------------------------------------------------|
| `MEDIA_RESOLUTION_UNSPECIFIED` | Media resolution has not been set.                               |
| `MEDIA_RESOLUTION_LOW`         | Media resolution set to low (64 tokens).                         |
| `MEDIA_RESOLUTION_MEDIUM`      | Media resolution set to medium (256 tokens).                     |
| `MEDIA_RESOLUTION_HIGH`        | Media resolution set to high (zoomed reframing with 256 tokens). |

### ThinkingLevel

The thinking level for the model.

| Enums                        |                             |
|------------------------------|-----------------------------|
| `THINKING_LEVEL_UNSPECIFIED` | Unspecified thinking level. |
| `LOW`                        | Low thinking level.         |
| `MEDIUM`                     | Medium thinking level.      |
| `HIGH`                       | High thinking level.        |
| `MINIMAL`                    | MINIMAL thinking level.     |

### FeatureSelectionPreference

Options for feature selection preference.

| Enums                                      |                                           |
|--------------------------------------------|-------------------------------------------|
| `FEATURE_SELECTION_PREFERENCE_UNSPECIFIED` | Unspecified feature selection preference. |
| `PRIORITIZE_QUALITY`                       | Prefer higher quality over lower cost.    |
| `BALANCED`                                 | Balanced feature selection preference.    |
| `PRIORITIZE_COST`                          | Prefer lower cost over higher quality.    |

### PersonGeneration

Enum for controlling the generation of people in images.

| Enums                           |                                                                                                  |
|---------------------------------|--------------------------------------------------------------------------------------------------|
| `PERSON_GENERATION_UNSPECIFIED` | The default behavior is unspecified. The model will decide whether to generate images of people. |
| `ALLOW_ALL`                     | Allows the model to generate images of people, including adults and children.                    |
| `ALLOW_ADULT`                   | Allows the model to generate images of adults, but not children.                                 |
| `ALLOW_NONE`                    | Prevents the model from generating images of people.                                             |

### MimeType

Supported MIME types for text output.

| Enums                   |                                      |
|-------------------------|--------------------------------------|
| `MIME_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `APPLICATION_JSON`      | JSON output format.                  |
| `TEXT_PLAIN`            | Plain text output format.            |

### MimeType

Supported MIME types for audio output.

| Enums                   |                                      |
|-------------------------|--------------------------------------|
| `MIME_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `AUDIO_MP3`             | MP3 audio format.                    |
| `AUDIO_OGG_OPUS`        | OGG Opus audio format.               |
| `AUDIO_L16`             | Raw PCM (L16) audio format.          |
| `AUDIO_WAV`             | WAV audio format.                    |
| `AUDIO_ALAW`            | A-law audio format.                  |
| `AUDIO_MULAW`           | Mu-law audio format.                 |

### DeliveryMode

The delivery mode for the output content.

| Enums                  |                                                      |
|------------------------|------------------------------------------------------|
| `DELIVERY_UNSPECIFIED` | Default value. This value is unused.                 |
| `INLINE`               | Generated bytes are returned inline in the response. |
| `URI`                  | Generated content is stored and a URI is returned.   |

### MimeType

Supported MIME types for image output.

| Enums                   |                                      |
|-------------------------|--------------------------------------|
| `MIME_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `IMAGE_JPEG`            | JPEG image format.                   |

### AspectRatio

Supported aspect ratios for image output.

| Enums                             |                                      |
|-----------------------------------|--------------------------------------|
| `ASPECT_RATIO_UNSPECIFIED`        | Default value. This value is unused. |
| `ASPECT_RATIO_ONE_BY_ONE`         | 1:1 aspect ratio.                    |
| `ASPECT_RATIO_TWO_BY_THREE`       | 2:3 aspect ratio.                    |
| `ASPECT_RATIO_THREE_BY_TWO`       | 3:2 aspect ratio.                    |
| `ASPECT_RATIO_THREE_BY_FOUR`      | 3:4 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_THREE`      | 4:3 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_FIVE`       | 4:5 aspect ratio.                    |
| `ASPECT_RATIO_FIVE_BY_FOUR`       | 5:4 aspect ratio.                    |
| `ASPECT_RATIO_NINE_BY_SIXTEEN`    | 9:16 aspect ratio.                   |
| `ASPECT_RATIO_SIXTEEN_BY_NINE`    | 16:9 aspect ratio.                   |
| `ASPECT_RATIO_TWENTY_ONE_BY_NINE` | 21:9 aspect ratio.                   |
| `ASPECT_RATIO_ONE_BY_EIGHT`       | 1:8 aspect ratio.                    |
| `ASPECT_RATIO_EIGHT_BY_ONE`       | 8:1 aspect ratio.                    |
| `ASPECT_RATIO_ONE_BY_FOUR`        | 1:4 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_ONE`        | 4:1 aspect ratio.                    |

### ImageSize

Supported image sizes for image output.

| Enums                    |                                      |
|--------------------------|--------------------------------------|
| `IMAGE_SIZE_UNSPECIFIED` | Default value. This value is unused. |
| `IMAGE_SIZE_FIVE_TWELVE` | 512px image size.                    |
| `IMAGE_SIZE_ONE_K`       | 1K image size.                       |
| `IMAGE_SIZE_TWO_K`       | 2K image size.                       |
| `IMAGE_SIZE_FOUR_K`      | 4K image size.                       |

### AspectRatio

Supported aspect ratios for video output.

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `ASPECT_RATIO_UNSPECIFIED`     | Default value. This value is unused. |
| `ASPECT_RATIO_SIXTEEN_BY_NINE` | 16:9 aspect ratio.                   |
| `ASPECT_RATIO_NINE_BY_SIXTEEN` | 9:16 aspect ratio.                   |

## Output Schema

Response message for `PredictionService.CountTokens` .

### CountTokensResponse

**JSON representation**

```
{
  "totalTokens": integer,
  "totalBillableCharacters": integer,
  "promptTokensDetails": [
    {
      object (ModalityTokenCount)
    }
  ]
}
```

| Fields                    |                                                                                                                                                                                                                                                            |
|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `totalTokens`             | `integer` The total number of tokens counted across all instances from the request.                                                                                                                                                                        |
| `totalBillableCharacters` | `integer` The total number of billable characters counted across all instances from the request.                                                                                                                                                           |
| `promptTokensDetails[]`   | `object ( `[`ModalityTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.ModalityTokenCount)` )` Output only. List of modalities that were processed in the request input. |

### ModalityTokenCount

**JSON representation**

```
{
  "modality": enum (Modality),
  "tokenCount": integer
}
```

| Fields       |                                                                                                                                                                                                           |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `modality`   | `enum ( `[`Modality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.Modality)` )` The modality that this token count applies to. |
| `tokenCount` | `integer` The number of tokens counted for this modality.                                                                                                                                                 |

### Modality

The modality of a `Part` of a `Content` message. A modality is the type of media, such as an image or a video. It is used to categorize the content of a `Part` for token counting purposes.

| Enums                  |                                                             |
|------------------------|-------------------------------------------------------------|
| `MODALITY_UNSPECIFIED` | When a modality is not specified, it is treated as `TEXT` . |
| `TEXT`                 | The `Part` contains plain text.                             |
| `IMAGE`                | The `Part` contains an image.                               |
| `VIDEO`                | The `Part` contains a video.                                |
| `AUDIO`                | The `Part` contains audio.                                  |
| `DOCUMENT`             | The `Part` contains a document, such as a PDF.              |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
