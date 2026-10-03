---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `generate_content`

Generates content (text, image, etc.) based on a balanced prompt and given modality-specific configurations. Use this for Gemini model inference.

The following sample demonstrate how to use `curl` to invoke the `generate_content` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "generate_content",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for \[PredictionService.GenerateContent\].

### GenerateContentRequest

**JSON representation**

```
{
  "model": string,
  "contents": [
    {
      object (Content)
    }
  ],
  "cachedContent": string,
  "tools": [
    {
      object (Tool)
    }
  ],
  "toolConfig": {
    object (ToolConfig)
  },
  "labels": {
    string: string,
    ...
  },
  "safetySettings": [
    {
      object (SafetySetting)
    }
  ],
  "modelArmorConfig": {
    object (ModelArmorConfig)
  },
  "generationConfig": {
    object (GenerationConfig)
  },

  // Union field _system_instruction can be only one of the following:
  "systemInstruction": {
    object (Content)
  }
  // End of list of possible types for union field _system_instruction.
}
```

| Fields                                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `model`                                                                                     | `string` Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*` Tuned model endpoint format: `projects/{project}/locations/{location}/endpoints/{endpoint}`                                                                                                                                                                                                                                                         |
| `contents[]`                                                                                | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content)` )` Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request.                                                                                                                                                        |
| `cachedContent`                                                                             | `string` Optional. The name of the cached content used as context to serve the prediction. Note: only used in explicit caching, where users can have control over caching (e.g. what content to cache) and enjoy guaranteed cost savings. Format: `projects/{project}/locations/{location}/cachedContents/{cachedContent}`                                                                                                                                                                                                                     |
| `tools[]`                                                                                   | `object ( `[`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Tool)` )` Optional. A list of `Tools` the model may use to generate the next response. A `Tool` is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model.                                                                                                                                 |
| `toolConfig`                                                                                | `object ( `[`ToolConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.ToolConfig)` )` Optional. Tool config. This config is shared for all tools provided in the request.                                                                                                                                                                                                                                                                                            |
| `labels`                                                                                    | `map (key: string, value: string)` Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only. Label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `safetySettings[]`                                                                          | `object ( `[`SafetySetting`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.SafetySetting)` )` Optional. Per request settings for blocking unsafe content. Enforced on GenerateContentResponse.candidates.                                                                                                                                                                                                                                                              |
| `modelArmorConfig`                                                                          | `object ( `[`ModelArmorConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.ModelArmorConfig)` )` Optional. Settings for prompt and response sanitization using the Model Armor service. If supplied, safety_settings must not be supplied.                                                                                                                                                                                                                          |
| `generationConfig`                                                                          | `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GenerationConfig)` )` Optional. Generation config.                                                                                                                                                                                                                                                                                                                                     |
| Union field `_system_instruction` . `_system_instruction` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `systemInstruction`                                                                         | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content)` )` Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph.                                                                                                                                                                                                                   |

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

### ToolConfig

**JSON representation**

```
{
  "functionCallingConfig": {
    object (FunctionCallingConfig)
  },
  "retrievalConfig": {
    object (RetrievalConfig)
  }
}
```

| Fields                  |                                                                                                                                                                                                                          |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `functionCallingConfig` | `object ( `[`FunctionCallingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.FunctionCallingConfig)` )` Optional. Function calling config. |
| `retrievalConfig`       | `object ( `[`RetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.RetrievalConfig)` )` Optional. Retrieval config.                    |

### FunctionCallingConfig

**JSON representation**

```
{
  "mode": enum (Mode),
  "allowedFunctionNames": [
    string
  ],
  "streamFunctionCallArguments": boolean
}
```

| Fields                        |                                                                                                                                                                                                                                      |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mode`                        | `enum ( `[`Mode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.Mode_1)` )` Optional. Function calling mode.                                                 |
| `allowedFunctionNames[]`      | `string` Optional. Function names to call. Only set when the Mode is ANY. Function names should match `FunctionDeclaration.name` . With mode set to ANY, model will predict a function call from the set of function names provided. |
| `streamFunctionCallArguments` | `boolean` Optional. When set to true, arguments of a single function call will be streamed out in multiple parts/contents/responses. Partial parameter results will be returned in the `FunctionCall.partial_args` field.            |

### RetrievalConfig

**JSON representation**

```
{

  // Union field _lat_lng can be only one of the following:
  "latLng": {
    object (LatLng)
  }
  // End of list of possible types for union field _lat_lng.

  // Union field _language_code can be only one of the following:
  "languageCode": string
  // End of list of possible types for union field _language_code.
}
```

| Fields                                                                            |                                                                                                                                                                                   |
|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_lat_lng` . `_lat_lng` can be only one of the following:             |                                                                                                                                                                                   |
| `latLng`                                                                          | `object ( `[`LatLng`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.LatLng)` )` The location of the user. |
| Union field `_language_code` . `_language_code` can be only one of the following: |                                                                                                                                                                                   |
| `languageCode`                                                                    | `string` The language code of the user.                                                                                                                                           |

### LatLng

**JSON representation**

```
{
  "latitude": number,
  "longitude": number
}
```

| Fields      |                                                                                |
|-------------|--------------------------------------------------------------------------------|
| `latitude`  | `number` The latitude in degrees. It must be in the range \[-90.0, +90.0\].    |
| `longitude` | `number` The longitude in degrees. It must be in the range \[-180.0, +180.0\]. |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### SafetySetting

**JSON representation**

```
{
  "category": enum (HarmCategory),
  "threshold": enum (HarmBlockThreshold),
  "method": enum (HarmBlockMethod)
}
```

| Fields      |                                                                                                                                                                                                                                                                                                          |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `category`  | `enum ( `[`HarmCategory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.HarmCategory)` )` Required. The harm category to be blocked.                                                                                             |
| `threshold` | `enum ( `[`HarmBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.HarmBlockThreshold)` )` Required. The threshold for blocking content. If the harm probability exceeds this threshold, the content will be blocked. |
| `method`    | `enum ( `[`HarmBlockMethod`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.HarmBlockMethod)` )` Optional. The method for blocking content. If not specified, the default behavior is to use the probability score.               |

### ModelArmorConfig

**JSON representation**

```
{
  "promptTemplateName": string,
  "responseTemplateName": string
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `promptTemplateName`   | `string` Optional. The resource name of the Model Armor template to use for prompt screening. A Model Armor template is a set of customized filters and thresholds that define how Model Armor screens content. If specified, Model Armor will use this template to check the user's prompt for safety and security risks before it is sent to the model. The name must be in the format `projects/{project}/locations/{location}/templates/{template}` .         |
| `responseTemplateName` | `string` Optional. The resource name of the Model Armor template to use for response screening. A Model Armor template is a set of customized filters and thresholds that define how Model Armor screens content. If specified, Model Armor will use this template to check the model's response for safety and security risks before it is returned to the user. The name must be in the format `projects/{project}/locations/{location}/templates/{template}` . |

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

### Mode

Function calling mode.

| Enums              |                                                                                                                                                                                                                                                                                                          |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `MODE_UNSPECIFIED` | Unspecified function calling mode. This value should not be used.                                                                                                                                                                                                                                        |
| `AUTO`             | Default model behavior, model decides to predict either function calls or natural language response.                                                                                                                                                                                                     |
| `ANY`              | Model is constrained to always predicting function calls only. If "allowed_function_names" are set, the predicted function calls will be limited to any one of "allowed_function_names", else the predicted function calls will be any one of the provided "function_declarations".                      |
| `NONE`             | Model will not predict any function calls. Model behavior is same as when not passing any function declarations.                                                                                                                                                                                         |
| `VALIDATED`        | Model is constrained to predict either function calls or natural language response. If "allowed_function_names" are set, the predicted function calls will be limited to any one of "allowed_function_names", else the predicted function calls will be any one of the provided "function_declarations". |

### HarmCategory

Harm categories that can be detected in user input and model responses.

| Enums                                   |                                                                                                             |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------|
| `HARM_CATEGORY_UNSPECIFIED`             | Default value. This value is unused.                                                                        |
| `HARM_CATEGORY_HATE_SPEECH`             | Content that promotes violence or incites hatred against individuals or groups based on certain attributes. |
| `HARM_CATEGORY_DANGEROUS_CONTENT`       | Content that promotes, facilitates, or enables dangerous activities.                                        |
| `HARM_CATEGORY_HARASSMENT`              | Abusive, threatening, or content intended to bully, torment, or ridicule.                                   |
| `HARM_CATEGORY_SEXUALLY_EXPLICIT`       | Content that contains sexually explicit material.                                                           |
| `HARM_CATEGORY_CIVIC_INTEGRITY`         | Deprecated: Election filter is not longer supported. The harm category is civic integrity.                  |
| `HARM_CATEGORY_IMAGE_HATE`              | Images that contain hate speech.                                                                            |
| `HARM_CATEGORY_IMAGE_DANGEROUS_CONTENT` | Images that contain dangerous content.                                                                      |
| `HARM_CATEGORY_IMAGE_HARASSMENT`        | Images that contain harassment.                                                                             |
| `HARM_CATEGORY_IMAGE_SEXUALLY_EXPLICIT` | Images that contain sexually explicit content.                                                              |
| `HARM_CATEGORY_JAILBREAK`               | Prompts designed to bypass safety filters.                                                                  |

### HarmBlockThreshold

Thresholds for blocking content based on harm probability.

| Enums                              |                                                               |
|------------------------------------|---------------------------------------------------------------|
| `HARM_BLOCK_THRESHOLD_UNSPECIFIED` | The harm block threshold is unspecified.                      |
| `BLOCK_LOW_AND_ABOVE`              | Block content with a low harm probability or higher.          |
| `BLOCK_MEDIUM_AND_ABOVE`           | Block content with a medium harm probability or higher.       |
| `BLOCK_ONLY_HIGH`                  | Block content with a high harm probability.                   |
| `BLOCK_NONE`                       | Do not block any content, regardless of its harm probability. |
| `OFF`                              | Turn off the safety filter entirely.                          |

### HarmBlockMethod

The method for blocking content.

| Enums                           |                                                                  |
|---------------------------------|------------------------------------------------------------------|
| `HARM_BLOCK_METHOD_UNSPECIFIED` | The harm block method is unspecified.                            |
| `SEVERITY`                      | The harm block method uses both probability and severity scores. |
| `PROBABILITY`                   | The harm block method uses the probability score.                |

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

Response message for \[PredictionService.GenerateContent\].

### GenerateContentResponse

**JSON representation**

```
{
  "candidates": [
    {
      object (Candidate)
    }
  ],
  "modelVersion": string,
  "createTime": string,
  "responseId": string,
  "promptFeedback": {
    object (PromptFeedback)
  },
  "usageMetadata": {
    object (UsageMetadata)
  }
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `candidates[]`   | `object ( `[`Candidate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.Candidate)` )` Output only. Generated candidates.                                                                                                                                                                                                                                    |
| `modelVersion`   | `string` Output only. The model version used to generate the response.                                                                                                                                                                                                                                                                                                                                                               |
| `createTime`     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when the request is made to the server. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `responseId`     | `string` Output only. response_id is used to identify each response. It is the encoding of the event_id.                                                                                                                                                                                                                                                                                                                             |
| `promptFeedback` | `object ( `[`PromptFeedback`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.PromptFeedback)` )` Output only. Content filter results for a prompt sent in the request. Note: Sent only in the first stream chunk. Only happens when no candidates were generated due to content violations.                                                                  |
| `usageMetadata`  | `object ( `[`UsageMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.UsageMetadata)` )` Usage metadata about the response(s).                                                                                                                                                                                                                         |

### Candidate

**JSON representation**

```
{
  "index": integer,
  "content": {
    object (Content)
  },
  "avgLogprobs": number,
  "logprobsResult": {
    object (LogprobsResult)
  },
  "finishReason": enum (FinishReason),
  "safetyRatings": [
    {
      object (SafetyRating)
    }
  ],
  "citationMetadata": {
    object (CitationMetadata)
  },
  "groundingMetadata": {
    object (GroundingMetadata)
  },
  "urlContextMetadata": {
    object (UrlContextMetadata)
  },

  // Union field _finish_message can be only one of the following:
  "finishMessage": string
  // End of list of possible types for union field _finish_message.
}
```

| Fields                                                                              |                                                                                                                                                                                                                                                                                                                                                                             |
|-------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `index`                                                                             | `integer` Output only. The 0-based index of this candidate in the list of generated responses. This is useful for distinguishing between multiple candidates when `candidate_count` \> 1.                                                                                                                                                                                   |
| `content`                                                                           | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content)` )` Output only. The content of the candidate.                                                                                                                                                                      |
| `avgLogprobs`                                                                       | `number` Output only. The average log probability of the tokens in this candidate. This is a length-normalized score that can be used to compare the quality of candidates of different lengths. A higher average log probability suggests a more confident and coherent response.                                                                                          |
| `logprobsResult`                                                                    | `object ( `[`LogprobsResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.LogprobsResult)` )` Output only. The detailed log probability information for the tokens in this candidate. This is useful for debugging, understanding model uncertainty, and identifying potential "hallucinations". |
| `finishReason`                                                                      | `enum ( `[`FinishReason`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.FinishReason)` )` Output only. The reason why the model stopped generating tokens. If empty, the model has not stopped generating.                                                                                         |
| `safetyRatings[]`                                                                   | `object ( `[`SafetyRating`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.SafetyRating)` )` Output only. A list of ratings for the safety of a response candidate. There is at most one rating per category.                                                                                       |
| `citationMetadata`                                                                  | `object ( `[`CitationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.CitationMetadata)` )` Output only. A collection of citations that apply to the generated content.                                                                                                                    |
| `groundingMetadata`                                                                 | `object ( `[`GroundingMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.GroundingMetadata)` )` Output only. Metadata returned when grounding is enabled. It contains the sources used to ground the generated content.                                                                      |
| `urlContextMetadata`                                                                | `object ( `[`UrlContextMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.UrlContextMetadata)` )` Output only. Metadata returned when the model uses the `url_context` tool to get information from a user-provided URL.                                                                     |
| Union field `_finish_message` . `_finish_message` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                             |
| `finishMessage`                                                                     | `string` Output only. Describes the reason the model stopped generating tokens in more detail. This field is returned only when `finish_reason` is set.                                                                                                                                                                                                                     |

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

### LogprobsResult

**JSON representation**

```
{
  "topCandidates": [
    {
      object (TopCandidates)
    }
  ],
  "chosenCandidates": [
    {
      object (Candidate)
    }
  ]
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                         |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `topCandidates[]`    | `object ( `[`TopCandidates`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.TopCandidates)` )` A list of the top candidate tokens at each decoding step. The length of this list is equal to the total number of decoding steps.                                                                |
| `chosenCandidates[]` | `object ( `[`Candidate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.Candidate_1)` )` A list of the chosen candidate tokens at each decoding step. The length of this list is equal to the total number of decoding steps. Note that the chosen candidate might not be in `top_candidates` . |

### TopCandidates

**JSON representation**

```
{
  "candidates": [
    {
      object (Candidate)
    }
  ]
}
```

| Fields         |                                                                                                                                                                                                                                               |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `candidates[]` | `object ( `[`Candidate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.Candidate_1)` )` The list of candidate tokens, sorted by log probability in descending order. |

### Candidate

**JSON representation**

```
{

  // Union field _token can be only one of the following:
  "token": string
  // End of list of possible types for union field _token.

  // Union field _token_id can be only one of the following:
  "tokenId": integer
  // End of list of possible types for union field _token_id.

  // Union field _log_probability can be only one of the following:
  "logProbability": number
  // End of list of possible types for union field _log_probability.
}
```

| Fields                                                                                |                                                                                                                                                                                                                                                                                               |
|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_token` . `_token` can be only one of the following:                     |                                                                                                                                                                                                                                                                                               |
| `token`                                                                               | `string` The token's string representation.                                                                                                                                                                                                                                                   |
| Union field `_token_id` . `_token_id` can be only one of the following:               |                                                                                                                                                                                                                                                                                               |
| `tokenId`                                                                             | `integer` The token's numerical ID. While the `token` field provides the string representation of the token, the `token_id` is the numerical representation that the model uses internally. This can be useful for developers who want to build custom logic based on the model's vocabulary. |
| Union field `_log_probability` . `_log_probability` can be only one of the following: |                                                                                                                                                                                                                                                                                               |
| `logProbability`                                                                      | `number` The log probability of this token. A higher value indicates that the model was more confident in this token. The log probability can be used to assess the relative likelihood of different tokens and to identify when the model is uncertain.                                      |

### SafetyRating

**JSON representation**

```
{
  "category": enum (HarmCategory),
  "probability": enum (HarmProbability),
  "probabilityScore": number,
  "severity": enum (HarmSeverity),
  "severityScore": number,
  "blocked": boolean,
  "overwrittenThreshold": enum (HarmBlockThreshold)
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `category`             | `enum ( `[`HarmCategory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.HarmCategory)` )` Output only. The harm category of this rating.                                                                                                                                                                                            |
| `probability`          | `enum ( `[`HarmProbability`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.HarmProbability)` )` Output only. The probability of harm for this category.                                                                                                                                                                            |
| `probabilityScore`     | `number` Output only. The probability score of harm for this category.                                                                                                                                                                                                                                                                                                                                      |
| `severity`             | `enum ( `[`HarmSeverity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.HarmSeverity)` )` Output only. The severity of harm for this category.                                                                                                                                                                                     |
| `severityScore`        | `number` Output only. The severity score of harm for this category.                                                                                                                                                                                                                                                                                                                                         |
| `blocked`              | `boolean` Output only. Indicates whether the content was blocked because of this rating.                                                                                                                                                                                                                                                                                                                    |
| `overwrittenThreshold` | `enum ( `[`HarmBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Input.Schema.HarmBlockThreshold)` )` Output only. The overwritten threshold for the safety category of Gemini 2.0 image out. If minors are detected in the output image, the threshold of each safety category will be overwritten if user sets a lower threshold. |

### CitationMetadata

**JSON representation**

```
{
  "citations": [
    {
      object (Citation)
    }
  ]
}
```

| Fields        |                                                                                                                                                                                                                |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `citations[]` | `object ( `[`Citation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.Citation)` )` Output only. A list of citations for the content. |

### Citation

**JSON representation**

```
{
  "startIndex": integer,
  "endIndex": integer,
  "uri": string,
  "title": string,
  "license": string,
  "publicationDate": {
    object (Date)
  }
}
```

| Fields            |                                                                                                                                                                                                                       |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startIndex`      | `integer` Output only. The start index of the citation in the content.                                                                                                                                                |
| `endIndex`        | `integer` Output only. The end index of the citation in the content.                                                                                                                                                  |
| `uri`             | `string` Output only. The URI of the source of the citation.                                                                                                                                                          |
| `title`           | `string` Output only. The title of the source of the citation.                                                                                                                                                        |
| `license`         | `string` Output only. The license of the source of the citation.                                                                                                                                                      |
| `publicationDate` | `object ( `[`Date`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.Date)` )` Output only. The publication date of the source of the citation. |

### Date

**JSON representation**

```
{
  "year": integer,
  "month": integer,
  "day": integer
}
```

| Fields  |                                                                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `year`  | `integer` Year of the date. Must be from 1 to 9999, or 0 to specify a date without a year.                                                                             |
| `month` | `integer` Month of a year. Must be from 1 to 12, or 0 to specify a year without a month and day.                                                                       |
| `day`   | `integer` Day of a month. Must be from 1 to 31 and valid for the year and month, or 0 to specify a year by itself or a year and month where the day isn't significant. |

### GroundingMetadata

**JSON representation**

```
{
  "webSearchQueries": [
    string
  ],
  "imageSearchQueries": [
    string
  ],
  "retrievalQueries": [
    string
  ],
  "groundingChunks": [
    {
      object (GroundingChunk)
    }
  ],
  "groundingSupports": [
    {
      object (GroundingSupport)
    }
  ],
  "sourceFlaggingUris": [
    {
      object (SourceFlaggingUri)
    }
  ],

  // Union field _search_entry_point can be only one of the following:
  "searchEntryPoint": {
    object (SearchEntryPoint)
  }
  // End of list of possible types for union field _search_entry_point.

  // Union field _retrieval_metadata can be only one of the following:
  "retrievalMetadata": {
    object (RetrievalMetadata)
  }
  // End of list of possible types for union field _retrieval_metadata.

  // Union field _google_maps_widget_context_token can be only one of the
  // following:
  "googleMapsWidgetContextToken": string
  // End of list of possible types for union field
  // _google_maps_widget_context_token.
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
<td><code>webSearchQueries[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The web search queries that were used to generate the content. This field is populated only when the grounding source is Google Search.</p></td>
</tr>
<tr class="even">
<td><code>imageSearchQueries[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The image search queries that were used to generate the content. This field is populated only when the grounding source is Google Search with the Image Search search_type enabled.</p></td>
</tr>
<tr class="odd">
<td><code>retrievalQueries[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The queries that were executed by the retrieval tools. This field is populated only when the grounding source is a retrieval tool, such as Agent Platform Search.</p></td>
</tr>
<tr class="even">
<td><code>groundingChunks[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.GroundingChunk"><code>GroundingChunk</code></a><code> )</code></p>
<p>A list of supporting references retrieved from the grounding source. This field is populated when the grounding source is Google Search, Agent Platform Search, or Google Maps.</p></td>
</tr>
<tr class="odd">
<td><code>groundingSupports[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.GroundingSupport"><code>GroundingSupport</code></a><code> )</code></p>
<p>Optional. A list of grounding supports that connect the generated content to the grounding chunks. This field is populated when the grounding source is Google Search or Agent Platform Search.</p></td>
</tr>
<tr class="even">
<td><code>sourceFlaggingUris[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.SourceFlaggingUri"><code>SourceFlaggingUri</code></a><code> )</code></p>
<p>Optional. Output only. A list of URIs that can be used to flag a place or review for inappropriate content. This field is populated only when the grounding source is Google Maps.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_search_entry_point</code> .</p>
<p><code>_search_entry_point</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>searchEntryPoint</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.SearchEntryPoint"><code>SearchEntryPoint</code></a><code> )</code></p>
<p>Optional. A web search entry point that can be used to display search results. This field is populated only when the grounding source is Google Search.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_retrieval_metadata</code> .</p>
<p><code>_retrieval_metadata</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>retrievalMetadata</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.RetrievalMetadata"><code>RetrievalMetadata</code></a><code> )</code></p>
<p>Optional. Output only. Metadata related to the retrieval grounding source.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_google_maps_widget_context_token</code> .</p>
<p><code>_google_maps_widget_context_token</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>googleMapsWidgetContextToken </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Output only. Deprecated: The Google Maps contextual widget behavior in Grounding with Google Maps is being deprecated; this field is planned for removal and will no longer be populated once removed.</p>
<p>A token that can be used to render a Google Maps widget with the contextual data. This field is populated only when the grounding source is Google Maps.</p></td>
</tr>
</tbody>
</table>

### SearchEntryPoint

**JSON representation**

```
{
  "renderedContent": string,
  "sdkBlob": string
}
```

| Fields            |                                                                                                                                                                                                                                                                                              |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `renderedContent` | `string` Optional. An HTML snippet that can be embedded in a web page or an application's webview. This snippet displays a search result, including the title, URL, and a brief description of the search result.                                                                            |
| `sdkBlob`         | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. A base64-encoded JSON object that contains a list of search queries and their corresponding search URLs. This information can be used to build a custom search UI. A base64-encoded string. |

### GroundingChunk

**JSON representation**

```
{

  // Union field chunk_type can be only one of the following:
  "web": {
    object (Web)
  },
  "retrievedContext": {
    object (RetrievedContext)
  },
  "maps": {
    object (Maps)
  }
  // End of list of possible types for union field chunk_type.
}
```

| Fields                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `chunk_type` . The source of the grounding chunk, which can be from Google Search, Agent Platform Search, or Google Maps. `chunk_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                |
| `web`                                                                                                                                                                                | `object ( `[`Web`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.Web)` )` A grounding chunk from a web page, typically from Google Search. See the `Web` message for details.                                                                         |
| `retrievedContext`                                                                                                                                                                   | `object ( `[`RetrievedContext`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.RetrievedContext)` )` A grounding chunk from a data source retrieved by a retrieval tool, such as Agent Platform Search. See the `RetrievedContext` message for details |
| `maps`                                                                                                                                                                               | `object ( `[`Maps`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.Maps)` )` A grounding chunk from Google Maps. See the `Maps` message for details.                                                                                                   |

### Web

**JSON representation**

```
{

  // Union field _uri can be only one of the following:
  "uri": string
  // End of list of possible types for union field _uri.

  // Union field _title can be only one of the following:
  "title": string
  // End of list of possible types for union field _title.

  // Union field _domain can be only one of the following:
  "domain": string
  // End of list of possible types for union field _domain.
}
```

| Fields                                                              |                                                                                                                     |
|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| Union field `_uri` . `_uri` can be only one of the following:       |                                                                                                                     |
| `uri`                                                               | `string` The URI of the web page that contains the evidence.                                                        |
| Union field `_title` . `_title` can be only one of the following:   |                                                                                                                     |
| `title`                                                             | `string` The title of the web page that contains the evidence.                                                      |
| Union field `_domain` . `_domain` can be only one of the following: |                                                                                                                     |
| `domain`                                                            | `string` The domain of the web page that contains the evidence. This can be used to filter out low-quality sources. |

### RetrievedContext

**JSON representation**

```
{

  // Union field context_details can be only one of the following:
  "ragChunk": {
    object (RagChunk)
  }
  // End of list of possible types for union field context_details.

  // Union field _uri can be only one of the following:
  "uri": string
  // End of list of possible types for union field _uri.

  // Union field _title can be only one of the following:
  "title": string
  // End of list of possible types for union field _title.

  // Union field _text can be only one of the following:
  "text": string
  // End of list of possible types for union field _text.

  // Union field _document_name can be only one of the following:
  "documentName": string
  // End of list of possible types for union field _document_name.
}
```

| Fields                                                                                                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                     |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `context_details` . Provides tool-specific details about the retrieved context. This allows for different types of retrieval tools to return their own specific metadata. `context_details` can be only one of the following: |                                                                                                                                                                                                                                                                                                                     |
| `ragChunk`                                                                                                                                                                                                                                | `object ( `[`RagChunk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.RagChunk)` )` Additional context for a Retrieval-Augmented Generation (RAG) retrieval result. This is populated only when the RAG retrieval tool is used.            |
| Union field `_uri` . `_uri` can be only one of the following:                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                     |
| `uri`                                                                                                                                                                                                                                     | `string` The URI of the retrieved data source.                                                                                                                                                                                                                                                                      |
| Union field `_title` . `_title` can be only one of the following:                                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                     |
| `title`                                                                                                                                                                                                                                   | `string` The title of the retrieved data source.                                                                                                                                                                                                                                                                    |
| Union field `_text` . `_text` can be only one of the following:                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                     |
| `text`                                                                                                                                                                                                                                    | `string` The content of the retrieved data source.                                                                                                                                                                                                                                                                  |
| Union field `_document_name` . `_document_name` can be only one of the following:                                                                                                                                                         |                                                                                                                                                                                                                                                                                                                     |
| `documentName`                                                                                                                                                                                                                            | `string` Output only. The full resource name of the referenced Agent Platform Search document. This is used to identify the specific document that was retrieved. The format is `projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/branches/{branch}/documents/{document}` . |

### RagChunk

**JSON representation**

```
{
  "text": string,
  "fileId": string,
  "chunkId": string,

  // Union field _page_span can be only one of the following:
  "pageSpan": {
    object (PageSpan)
  }
  // End of list of possible types for union field _page_span.
}
```

| Fields                                                                    |                                                                                                                                                                                                                                        |
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text`                                                                    | `string` The content of the chunk.                                                                                                                                                                                                     |
| `fileId`                                                                  | `string` The ID of the file that the chunk belongs to.                                                                                                                                                                                 |
| `chunkId`                                                                 | `string` The ID of the chunk.                                                                                                                                                                                                          |
| Union field `_page_span` . `_page_span` can be only one of the following: |                                                                                                                                                                                                                                        |
| `pageSpan`                                                                | `object ( `[`PageSpan`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.PageSpan)` )` If populated, represents where the chunk starts and ends in the document. |

### PageSpan

**JSON representation**

```
{
  "firstPage": integer,
  "lastPage": integer
}
```

| Fields      |                                                                          |
|-------------|--------------------------------------------------------------------------|
| `firstPage` | `integer` Page where chunk starts in the document. Inclusive. 1-indexed. |
| `lastPage`  | `integer` Page where chunk ends in the document. Inclusive. 1-indexed.   |

### Maps

**JSON representation**

```
{
  "placeAnswerSources": {
    object (PlaceAnswerSources)
  },

  // Union field _uri can be only one of the following:
  "uri": string
  // End of list of possible types for union field _uri.

  // Union field _title can be only one of the following:
  "title": string
  // End of list of possible types for union field _title.

  // Union field _text can be only one of the following:
  "text": string
  // End of list of possible types for union field _text.

  // Union field _place_id can be only one of the following:
  "placeId": string
  // End of list of possible types for union field _place_id.
}
```

| Fields                                                                  |                                                                                                                                                                                                                                                                                                                                                            |
|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `placeAnswerSources`                                                    | `object ( `[`PlaceAnswerSources`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.PlaceAnswerSources)` )` The sources that were used to generate the place answer. This includes review snippets and photos that were used to generate the answer, as well as URIs to flag content. |
| Union field `_uri` . `_uri` can be only one of the following:           |                                                                                                                                                                                                                                                                                                                                                            |
| `uri`                                                                   | `string` The URI of the place.                                                                                                                                                                                                                                                                                                                             |
| Union field `_title` . `_title` can be only one of the following:       |                                                                                                                                                                                                                                                                                                                                                            |
| `title`                                                                 | `string` The title of the place.                                                                                                                                                                                                                                                                                                                           |
| Union field `_text` . `_text` can be only one of the following:         |                                                                                                                                                                                                                                                                                                                                                            |
| `text`                                                                  | `string` The text of the place answer.                                                                                                                                                                                                                                                                                                                     |
| Union field `_place_id` . `_place_id` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                            |
| `placeId`                                                               | `string` This Place's resource name, in `places/{place_id}` format. This can be used to look up the place in the Google Maps API.                                                                                                                                                                                                                          |

### PlaceAnswerSources

**JSON representation**

```
{
  "reviewSnippets": [
    {
      object (ReviewSnippet)
    }
  ]
}
```

| Fields             |                                                                                                                                                                                                                                   |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reviewSnippets[]` | `object ( `[`ReviewSnippet`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.ReviewSnippet)` )` Snippets of reviews that were used to generate the answer. |

### ReviewSnippet

**JSON representation**

```
{
  "reviewId": string,
  "googleMapsUri": string,
  "title": string
}
```

| Fields          |                                                         |
|-----------------|---------------------------------------------------------|
| `reviewId`      | `string` The ID of the review that is being referenced. |
| `googleMapsUri` | `string` A link to show the review on Google Maps.      |
| `title`         | `string` The title of the review.                       |

### GroundingSupport

**JSON representation**

```
{
  "groundingChunkIndices": [
    integer
  ],
  "confidenceScores": [
    number
  ],
  "renderedParts": [
    integer
  ],

  // Union field _segment can be only one of the following:
  "segment": {
    object (Segment)
  }
  // End of list of possible types for union field _segment.
}
```

| Fields                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-----------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `groundingChunkIndices[]`                                             | `integer` A list of indices into the `grounding_chunks` field of the `GroundingMetadata` message. These indices specify which grounding chunks support the claim made in the content segment. For example, if this field has the values `[1, 3]` , it means that `grounding_chunks[1]` and `grounding_chunks[3]` are the sources for the claim in the content segment.                                              |
| `confidenceScores[]`                                                  | `number` The confidence scores for the support references. This list is parallel to the `grounding_chunk_indices` list. A score is a value between 0.0 and 1.0, with a higher score indicating a higher confidence that the reference supports the claim. For Gemini 2.0 and before, this list has the same size as `grounding_chunk_indices` . For Gemini 2.5 and later, this list is empty and should be ignored. |
| `renderedParts[]`                                                     | `integer` Indices into the `rendered_parts` field of the `GroundingMetadata` message. These indices specify which rendered parts are associated with this support message.                                                                                                                                                                                                                                          |
| Union field `_segment` . `_segment` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `segment`                                                             | `object ( `[`Segment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.Segment)` )` The content segment that this support message applies to.                                                                                                                                                                                                |

### Segment

**JSON representation**

```
{
  "partIndex": integer,
  "startIndex": integer,
  "endIndex": integer,
  "text": string
}
```

| Fields       |                                                                                                                                                                                                                                   |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `partIndex`  | `integer` Output only. The index of the `Part` object that this segment belongs to. This is useful for associating the segment with a specific part of the content.                                                               |
| `startIndex` | `integer` Output only. The start index of the segment in the `Part` , measured in bytes. This marks the beginning of the segment and is inclusive, meaning the byte at this index is the first byte of the segment.               |
| `endIndex`   | `integer` Output only. The end index of the segment in the `Part` , measured in bytes. This marks the end of the segment and is exclusive, meaning the segment includes content up to, but not including, the byte at this index. |
| `text`       | `string` Output only. The text of the segment.                                                                                                                                                                                    |

### RetrievalMetadata

**JSON representation**

```
{
  "googleSearchDynamicRetrievalScore": number
}
```

| Fields                              |                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `googleSearchDynamicRetrievalScore` | `number` Optional. A score indicating how likely it is that a Google Search query could help answer the prompt. The score is in the range of `[0, 1]` . A score of 1 means the model is confident that a search will be helpful, and 0 means it is not. This score is populated only when Google Search grounding and dynamic retrieval are enabled. The score is used to determine whether to trigger a search. |

### SourceFlaggingUri

**JSON representation**

```
{
  "sourceId": string,
  "flagContentUri": string
}
```

| Fields           |                                                        |
|------------------|--------------------------------------------------------|
| `sourceId`       | `string` The ID of the place or review.                |
| `flagContentUri` | `string` The URI that can be used to flag the content. |

### UrlContextMetadata

**JSON representation**

```
{
  "urlMetadata": [
    {
      object (UrlMetadata)
    }
  ]
}
```

| Fields          |                                                                                                                                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `urlMetadata[]` | `object ( `[`UrlMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.UrlMetadata)` )` Output only. A list of URL metadata, with one entry for each URL retrieved by the tool. |

### UrlMetadata

**JSON representation**

```
{
  "retrievedUrl": string,
  "urlRetrievalStatus": enum (UrlRetrievalStatus)
}
```

| Fields               |                                                                                                                                                                                                                 |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `retrievedUrl`       | `string` The URL retrieved by the tool.                                                                                                                                                                         |
| `urlRetrievalStatus` | `enum ( `[`UrlRetrievalStatus`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.UrlRetrievalStatus)` )` The status of the URL retrieval. |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### PromptFeedback

**JSON representation**

```
{
  "blockReason": enum (BlockedReason),
  "safetyRatings": [
    {
      object (SafetyRating)
    }
  ],
  "blockReasonMessage": string
}
```

| Fields               |                                                                                                                                                                                                                                                              |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `blockReason`        | `enum ( `[`BlockedReason`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.BlockedReason)` )` Output only. The reason why the prompt was blocked.                                     |
| `safetyRatings[]`    | `object ( `[`SafetyRating`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.SafetyRating)` )` Output only. A list of safety ratings for the prompt. There is one rating per category. |
| `blockReasonMessage` | `string` Output only. A readable message that explains the reason why the prompt was blocked.                                                                                                                                                                |

### UsageMetadata

**JSON representation**

```
{
  "promptTokenCount": integer,
  "candidatesTokenCount": integer,
  "totalTokenCount": integer,
  "toolUsePromptTokenCount": integer,
  "thoughtsTokenCount": integer,
  "cachedContentTokenCount": integer,
  "promptTokensDetails": [
    {
      object (ModalityTokenCount)
    }
  ],
  "cacheTokensDetails": [
    {
      object (ModalityTokenCount)
    }
  ],
  "candidatesTokensDetails": [
    {
      object (ModalityTokenCount)
    }
  ],
  "toolUsePromptTokensDetails": [
    {
      object (ModalityTokenCount)
    }
  ],
  "trafficType": enum (TrafficType)
}
```

| Fields                         |                                                                                                                                                                                                                                                                                                                                        |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `promptTokenCount`             | `integer` The total number of tokens in the prompt. This includes any text, images, or other media provided in the request. When `cached_content` is set, this also includes the number of tokens in the cached content.                                                                                                               |
| `candidatesTokenCount`         | `integer` The total number of tokens in the generated candidates.                                                                                                                                                                                                                                                                      |
| `totalTokenCount`              | `integer` The total number of tokens for the entire request. This is the sum of `prompt_token_count` , `candidates_token_count` , `tool_use_prompt_token_count` , and `thoughts_token_count` .                                                                                                                                         |
| `toolUsePromptTokenCount`      | `integer` Output only. The number of tokens in the results from tool executions, which are provided back to the model as input, if applicable.                                                                                                                                                                                         |
| `thoughtsTokenCount`           | `integer` Output only. The number of tokens that were part of the model's generated "thoughts" output, if applicable.                                                                                                                                                                                                                  |
| `cachedContentTokenCount`      | `integer` Output only. The number of tokens in the cached content that was used for this request.                                                                                                                                                                                                                                      |
| `promptTokensDetails[]`        | `object ( `[`ModalityTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.ModalityTokenCount)` )` Output only. A detailed breakdown of the token count for each modality in the prompt.                                                                 |
| `cacheTokensDetails[]`         | `object ( `[`ModalityTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.ModalityTokenCount)` )` Output only. A detailed breakdown of the token count for each modality in the cached content.                                                         |
| `candidatesTokensDetails[]`    | `object ( `[`ModalityTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.ModalityTokenCount)` )` Output only. A detailed breakdown of the token count for each modality in the generated candidates.                                                   |
| `toolUsePromptTokensDetails[]` | `object ( `[`ModalityTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.ModalityTokenCount)` )` Output only. A detailed breakdown by modality of the token counts from the results of tool executions, which are provided back to the model as input. |
| `trafficType`                  | `enum ( `[`TrafficType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.TrafficType)` )` Output only. The traffic type for this request.                                                                                                                       |

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

### FinishReason

The reason why the model stopped generating tokens. If this field is empty, the model has not stopped generating.

| Enums                       |                                                                                                                                                                                                  |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `FINISH_REASON_UNSPECIFIED` | The finish reason is unspecified.                                                                                                                                                                |
| `STOP`                      | The model reached a natural stopping point or a configured stop sequence.                                                                                                                        |
| `MAX_TOKENS`                | The model generated the maximum number of tokens allowed by the `max_output_tokens` parameter.                                                                                                   |
| `SAFETY`                    | The model stopped generating because the content potentially violates safety policies. NOTE: When streaming, the `content` field is empty if content filters block the output.                   |
| `RECITATION`                | The model stopped generating because the content may be a recitation from a source.                                                                                                              |
| `OTHER`                     | The model stopped generating for a reason not otherwise specified.                                                                                                                               |
| `BLOCKLIST`                 | The model stopped generating because the content contains a term from a configured blocklist.                                                                                                    |
| `PROHIBITED_CONTENT`        | The model stopped generating because the content may be prohibited.                                                                                                                              |
| `SPII`                      | The model stopped generating because the content may contain sensitive personally identifiable information (SPII).                                                                               |
| `MALFORMED_FUNCTION_CALL`   | The model generated a function call that is syntactically invalid and can't be parsed.                                                                                                           |
| `MODEL_ARMOR`               | The model response was blocked by Model Armor.                                                                                                                                                   |
| `IMAGE_SAFETY`              | The generated image potentially violates safety policies.                                                                                                                                        |
| `IMAGE_PROHIBITED_CONTENT`  | The generated image may contain prohibited content.                                                                                                                                              |
| `IMAGE_RECITATION`          | The generated image may be a recitation from a source.                                                                                                                                           |
| `IMAGE_OTHER`               | The image generation stopped for a reason not otherwise specified.                                                                                                                               |
| `UNEXPECTED_TOOL_CALL`      | The model generated a function call that is semantically invalid. This can happen, for example, if function calling is not enabled or the generated function is not in the function declaration. |
| `NO_IMAGE`                  | The model was expected to generate an image, but didn't.                                                                                                                                         |

### HarmCategory

Harm categories that can be detected in user input and model responses.

| Enums                                   |                                                                                                             |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------|
| `HARM_CATEGORY_UNSPECIFIED`             | Default value. This value is unused.                                                                        |
| `HARM_CATEGORY_HATE_SPEECH`             | Content that promotes violence or incites hatred against individuals or groups based on certain attributes. |
| `HARM_CATEGORY_DANGEROUS_CONTENT`       | Content that promotes, facilitates, or enables dangerous activities.                                        |
| `HARM_CATEGORY_HARASSMENT`              | Abusive, threatening, or content intended to bully, torment, or ridicule.                                   |
| `HARM_CATEGORY_SEXUALLY_EXPLICIT`       | Content that contains sexually explicit material.                                                           |
| `HARM_CATEGORY_CIVIC_INTEGRITY`         | Deprecated: Election filter is not longer supported. The harm category is civic integrity.                  |
| `HARM_CATEGORY_IMAGE_HATE`              | Images that contain hate speech.                                                                            |
| `HARM_CATEGORY_IMAGE_DANGEROUS_CONTENT` | Images that contain dangerous content.                                                                      |
| `HARM_CATEGORY_IMAGE_HARASSMENT`        | Images that contain harassment.                                                                             |
| `HARM_CATEGORY_IMAGE_SEXUALLY_EXPLICIT` | Images that contain sexually explicit content.                                                              |
| `HARM_CATEGORY_JAILBREAK`               | Prompts designed to bypass safety filters.                                                                  |

### HarmProbability

The probability of harm for a given category.

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `HARM_PROBABILITY_UNSPECIFIED` | The harm probability is unspecified. |
| `NEGLIGIBLE`                   | The harm probability is negligible.  |
| `LOW`                          | The harm probability is low.         |
| `MEDIUM`                       | The harm probability is medium.      |
| `HIGH`                         | The harm probability is high.        |

### HarmSeverity

The severity of harm for a given category.

| Enums                       |                                   |
|-----------------------------|-----------------------------------|
| `HARM_SEVERITY_UNSPECIFIED` | The harm severity is unspecified. |
| `HARM_SEVERITY_NEGLIGIBLE`  | The harm severity is negligible.  |
| `HARM_SEVERITY_LOW`         | The harm severity is low.         |
| `HARM_SEVERITY_MEDIUM`      | The harm severity is medium.      |
| `HARM_SEVERITY_HIGH`        | The harm severity is high.        |

### HarmBlockThreshold

Thresholds for blocking content based on harm probability.

| Enums                              |                                                               |
|------------------------------------|---------------------------------------------------------------|
| `HARM_BLOCK_THRESHOLD_UNSPECIFIED` | The harm block threshold is unspecified.                      |
| `BLOCK_LOW_AND_ABOVE`              | Block content with a low harm probability or higher.          |
| `BLOCK_MEDIUM_AND_ABOVE`           | Block content with a medium harm probability or higher.       |
| `BLOCK_ONLY_HIGH`                  | Block content with a high harm probability.                   |
| `BLOCK_NONE`                       | Do not block any content, regardless of its harm probability. |
| `OFF`                              | Turn off the safety filter entirely.                          |

### UrlRetrievalStatus

The status of a URL retrieval.

| Enums                              |                                      |
|------------------------------------|--------------------------------------|
| `URL_RETRIEVAL_STATUS_UNSPECIFIED` | Default value. This value is unused. |
| `URL_RETRIEVAL_STATUS_SUCCESS`     | The URL was retrieved successfully.  |
| `URL_RETRIEVAL_STATUS_ERROR`       | The URL retrieval failed.            |

### BlockedReason

The reason why the prompt was blocked.

| Enums                        |                                                                                                                                              |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| `BLOCKED_REASON_UNSPECIFIED` | The blocked reason is unspecified.                                                                                                           |
| `SAFETY`                     | The prompt was blocked for safety reasons.                                                                                                   |
| `OTHER`                      | The prompt was blocked for other reasons. For example, it may be due to the prompt's language, or because it contains other harmful content. |
| `BLOCKLIST`                  | The prompt was blocked because it contains a term from the terminology blocklist.                                                            |
| `PROHIBITED_CONTENT`         | The prompt was blocked because it contains prohibited content.                                                                               |
| `MODEL_ARMOR`                | The prompt was blocked by Model Armor.                                                                                                       |
| `IMAGE_SAFETY`               | The prompt was blocked because it contains content that is unsafe for image generation.                                                      |
| `JAILBREAK`                  | The prompt was blocked as a jailbreak attempt.                                                                                               |

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

### TrafficType

The type of traffic that this request was processed with, indicating which quota is consumed.

| Enums                      |                                                      |
|----------------------------|------------------------------------------------------|
| `TRAFFIC_TYPE_UNSPECIFIED` | Unspecified request traffic type.                    |
| `ON_DEMAND`                | The request was processed using Pay-As-You-Go quota. |
| `ON_DEMAND_PRIORITY`       | Type for Priority Pay-As-You-Go traffic.             |
| `ON_DEMAND_FLEX`           | Type for Flex traffic.                               |
| `PROVISIONED_THROUGHPUT`   | Type for Provisioned Throughput traffic.             |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ✅
