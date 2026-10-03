---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/corroborate_content
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/corroborate_content
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `corroborate_content`

Evaluates the factuality of a piece of content (typically an LLM-generated response) against a set of facts from a RAG Engine Corpus, returning a per-claim citation score and supporting facts. Use this after a generation step when the user wants to verify groundedness, surface hallucinations, or attach citations to model output.

Differs from `retrieve_contexts` and `augment_prompt` : those happen *before* generation; `corroborate_content` happens *after* , on text the model already produced. Format: 'projects/{project_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

**Parameters** \* `parent` : The parent resource, of the form `projects/{project}/locations/{location}` . \* `content` : The input content to corroborate, in `Content` form. Only text is supported. \* `facts` : A list of facts to corroborate the content against. Typically obtained from a prior `retrieve_contexts` call. \* `parameters` : Optional per-request parameter overrides. \* `parameters.citation_threshold` : Only return claims whose citation score exceeds this threshold.

The following sample demonstrate how to use `curl` to invoke the `corroborate_content` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "corroborate_content",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for CorroborateContent.

### CorroborateContentRequest

**JSON representation**

```
{
  "parent": string,
  "facts": [
    {
      object (Fact)
    }
  ],
  "parameters": {
    object (Parameters)
  },

  // Union field _content can be only one of the following:
  "content": {
    object (Content)
  }
  // End of list of possible types for union field _content.
}
```

| Fields                                                                |                                                                                                                                                                                                                                                   |
|-----------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                                                              | `string` Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .                                            |
| `facts[]`                                                             | `object ( `[`Fact`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/augment_prompt#Output.Schema.Fact)` )` Optional. Facts used to generate the text can also be used to corroborate the text.            |
| `parameters`                                                          | `object ( `[`Parameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/corroborate_content#Input.Schema.Parameters)` )` Optional. Parameters that can be set to override default settings per request. |
| Union field `_content` . `_content` can be only one of the following: |                                                                                                                                                                                                                                                   |
| `content`                                                             | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Content)` )` Optional. Input content to corroborate, only text format is supported for now.         |

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

| Fields    |                                                                                                                                                                                                                                                                                                                              |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `role`    | `string` Optional. The producer of the content. Must be either 'user' or 'model'. If not set, the service will default to 'user'.                                                                                                                                                                                            |
| `parts[]` | `object ( `[`Part`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Part)` )` Required. A list of `Part` objects that make up a single message. Parts of a message can have different MIME types. A `Content` message must have at least one `Part` . |

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

| Fields                                                                |                                                                                                                                                                                                                                                                                                                             |
|-----------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `thought`                                                             | `boolean` Optional. Indicates whether the `part` represents the model's thought process or reasoning.                                                                                                                                                                                                                       |
| `thoughtSignature`                                                    | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. An opaque signature for the thought so it can be reused in subsequent requests. A base64-encoded string.                                                                                                                   |
| `mediaResolution`                                                     | `object ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.MediaResolution)` )` per part media resolution. Media resolution for the input media.                                                                                 |
| `audioTranscription`                                                  | `object ( `[`AudioTranscription`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AudioTranscription)` )` Optional. Audio (input or output) transcription. This is only set when this Part contains audio data.                                      |
| Union field `data` . `data` can be only one of the following:         |                                                                                                                                                                                                                                                                                                                             |
| `text`                                                                | `string` Optional. The text content of the part. When sent from the VSCode Gemini Code Assist extension, references to @mentioned items will be converted to markdown boldface text. For example `@my-repo` will be converted to and sent as `**my-repo**` by the IDE agent.                                                |
| `inlineData`                                                          | `object ( `[`Blob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Blob)` )` Optional. The inline data content of the part. This can be used to include images, audio, or video in a request.                                                       |
| `fileData`                                                            | `object ( `[`FileData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FileData)` )` Optional. The URI-based data of the part. This can be used to include files from Google Cloud Storage.                                                         |
| `functionCall`                                                        | `object ( `[`FunctionCall`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FunctionCall)` )` Optional. A predicted function call returned from the model. This contains the name of the function to call and the arguments to pass to the function. |
| `functionResponse`                                                    | `object ( `[`FunctionResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FunctionResponse)` )` Optional. The result of a function call. This is used to provide the model with the result of a function call that it predicted.               |
| `executableCode`                                                      | `object ( `[`ExecutableCode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ExecutableCode)` )` Optional. Code generated by the model that is intended to be executed.                                                                             |
| `codeExecutionResult`                                                 | `object ( `[`CodeExecutionResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.CodeExecutionResult)` )` Optional. The result of executing the `ExecutableCode` .                                                                                 |
| Union field `metadata` . `metadata` can be only one of the following: |                                                                                                                                                                                                                                                                                                                             |
| `videoMetadata`                                                       | `object ( `[`VideoMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.VideoMetadata)` )` Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data.                       |

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

| Fields          |                                                                                                                                                                                                                                                                                                           |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`            | `string` Optional. The unique id of the function call. If populated, the client to execute the `function_call` and return the response with the matching `id` .                                                                                                                                           |
| `name`          | `string` Optional. The name of the function to call. Matches `FunctionDeclaration.name` .                                                                                                                                                                                                                 |
| `args`          | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. The function parameters and values in JSON object format. See `FunctionDeclaration.parameters` for parameter details.                                                                          |
| `partialArgs[]` | `object ( `[`PartialArg`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PartialArg)` )` Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. |
| `willContinue`  | `boolean` Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow.                                                                                                                                               |

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
| `parts[]`  | `object ( `[`FunctionResponsePart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FunctionResponsePart)` )` Optional. Ordered `Parts` that constitute a function response. Parts may have different IANA MIME types.                                                               |

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

| Fields                                                                                                |                                                                                                                                                                                                              |
|-------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `data` . The data of the function response part. `data` can be only one of the following: |                                                                                                                                                                                                              |
| `inlineData`                                                                                          | `object ( `[`FunctionResponseBlob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FunctionResponseBlob)` )` Inline media bytes.     |
| `fileData`                                                                                            | `object ( `[`FunctionResponseFileData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FunctionResponseFileData)` )` URI based data. |

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

| Fields                                                      |                                                                                                                                                                                                           |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `language`                                                  | `enum ( `[`Language`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Language)` )` Required. Programming language of the `code` . |
| `code`                                                      | `string` Required. The code to be executed.                                                                                                                                                               |
| Union field `_id` . `_id` can be only one of the following: |                                                                                                                                                                                                           |
| `id`                                                        | `string` Optional. Unique identifier of the `ExecutableCode` part. The server returns the `CodeExecutionResult` with the matching `id` .                                                                  |

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

| Fields                                                      |                                                                                                                                                                                                   |
|-------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `outcome`                                                   | `enum ( `[`Outcome`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Outcome)` )` Required. Outcome of the code execution. |
| `output`                                                    | `string` Optional. Contains stdout when code execution is successful, stderr or other description otherwise.                                                                                      |
| Union field `_id` . `_id` can be only one of the following: |                                                                                                                                                                                                   |
| `id`                                                        | `string` Optional. The identifier of the `ExecutableCode` part this result is for. Only populated if the corresponding `ExecutableCode` has an id.                                                |

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

| Fields                                                          |                                                                                                                                                                                                     |
|-----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `value` . `value` can be only one of the following: |                                                                                                                                                                                                     |
| `level`                                                         | `enum ( `[`Level`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Level)` )` The tokenization quality used for given media. |

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

| Fields         |                                                                                                                                                                                                                                                                   |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text`         | `string` Required. The transcription text of this audio segment.                                                                                                                                                                                                  |
| `speakerLabel` | `string` Optional. A label identifying the speaker of this audio segment (e.g. "spk_1", "spk_2"). Present when diarization is set.                                                                                                                                |
| `words[]`      | `object ( `[`WordInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.WordInfo)` )` Optional. Detailed word-level transcriptions and timing details. Present when word_timestamp is set. |

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

### Fact

**JSON representation**

```
{

  // Union field _query can be only one of the following:
  "query": string
  // End of list of possible types for union field _query.

  // Union field _title can be only one of the following:
  "title": string
  // End of list of possible types for union field _title.

  // Union field _uri can be only one of the following:
  "uri": string
  // End of list of possible types for union field _uri.

  // Union field _summary can be only one of the following:
  "summary": string
  // End of list of possible types for union field _summary.

  // Union field _vector_distance can be only one of the following:
  "vectorDistance": number
  // End of list of possible types for union field _vector_distance.

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _chunk can be only one of the following:
  "chunk": {
    object (RagChunk)
  }
  // End of list of possible types for union field _chunk.
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
<td><p>Union field <code>_query</code> .</p>
<p><code>_query</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>query</code></td>
<td><p><code>string</code></p>
<p>Query that is used to retrieve this fact.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_title</code> .</p>
<p><code>_title</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>title</code></td>
<td><p><code>string</code></p>
<p>If present, it refers to the title of this fact.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_uri</code> .</p>
<p><code>_uri</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>uri</code></td>
<td><p><code>string</code></p>
<p>If present, this uri links to the source of the fact.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_summary</code> .</p>
<p><code>_summary</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>summary</code></td>
<td><p><code>string</code></p>
<p>If present, the summary/snippet of the fact.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_vector_distance</code> .</p>
<p><code>_vector_distance</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>vectorDistance </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>number</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>If present, the distance between the query vector and this fact vector.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_score</code> .</p>
<p><code>_score</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>score</code></td>
<td><p><code>number</code></p>
<p>If present, according to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the fact and its range depends on the metric type.</p>
<p>For example, if the metric type is COSINE_DISTANCE, it represents the distance between the query and the fact. The larger the distance, the less relevant the fact is to the query. The range is [0, 2], while 0 means the most relevant and 2 means the least relevant.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_chunk</code> .</p>
<p><code>_chunk</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>chunk</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Output.Schema.RagChunk"><code>RagChunk</code></a><code> )</code></p>
<p>If present, chunk properties.</p></td>
</tr>
</tbody>
</table>

### RagChunk

**JSON representation**

```
{
  "text": string,

  // Union field _page_span can be only one of the following:
  "pageSpan": {
    object (PageSpan)
  }
  // End of list of possible types for union field _page_span.
}
```

| Fields                                                                    |                                                                                                                                                                                                                                         |
|---------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text`                                                                    | `string` The content of the chunk.                                                                                                                                                                                                      |
| Union field `_page_span` . `_page_span` can be only one of the following: |                                                                                                                                                                                                                                         |
| `pageSpan`                                                                | `object ( `[`PageSpan`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Output.Schema.PageSpan)` )` If populated, represents where the chunk starts and ends in the document. |

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

### Parameters

**JSON representation**

```
{
  "citationThreshold": number
}
```

| Fields              |                                                                                      |
|---------------------|--------------------------------------------------------------------------------------|
| `citationThreshold` | `number` Optional. Only return claims with citation score larger than the threshold. |

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

## Output Schema

Response message for CorroborateContent.

### CorroborateContentResponse

**JSON representation**

```
{
  "claims": [
    {
      object (Claim)
    }
  ],

  // Union field _corroboration_score can be only one of the following:
  "corroborationScore": number
  // End of list of possible types for union field _corroboration_score.
}
```

| Fields                                                                                        |                                                                                                                                                                                                                                               |
|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `claims[]`                                                                                    | `object ( `[`Claim`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/corroborate_content#Output.Schema.Claim)` )` Claims that are extracted from the input content and facts that support the claims. |
| Union field `_corroboration_score` . `_corroboration_score` can be only one of the following: |                                                                                                                                                                                                                                               |
| `corroborationScore`                                                                          | `number` Confidence score of corroborating content. Value is \[0,1\] with 1 is the most confidence.                                                                                                                                           |

### Claim

**JSON representation**

```
{
  "factIndexes": [
    integer
  ],

  // Union field _start_index can be only one of the following:
  "startIndex": integer
  // End of list of possible types for union field _start_index.

  // Union field _end_index can be only one of the following:
  "endIndex": integer
  // End of list of possible types for union field _end_index.

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                                        |                                                                       |
|-------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| `factIndexes[]`                                                               | `integer` Indexes of the facts supporting this claim.                 |
| Union field `_start_index` . `_start_index` can be only one of the following: |                                                                       |
| `startIndex`                                                                  | `integer` Index in the input text where the claim starts (inclusive). |
| Union field `_end_index` . `_end_index` can be only one of the following:     |                                                                       |
| `endIndex`                                                                    | `integer` Index in the input text where the claim ends (exclusive).   |
| Union field `_score` . `_score` can be only one of the following:             |                                                                       |
| `score`                                                                       | `number` Confidence score of this corroboration.                      |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
