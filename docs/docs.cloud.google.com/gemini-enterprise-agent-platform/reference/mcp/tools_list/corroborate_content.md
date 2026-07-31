---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/corroborate_content
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/corroborate_content
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `corroborate_content`

Evaluates the factuality of a piece of content (typically an LLM-generated response) against a set of facts from a RAG Engine Corpus, returning a per-claim citation score and supporting facts. Use this after a generation step when the user wants to verify groundedness, surface hallucinations, or attach citations to model output.

Differs from `retrieve_contexts` and `augment_prompt` : those happen *before* generation; `corroborate_content` happens *after* , on text the model already produced. Format: 'projects/{project\_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

**Parameters** \* `parent` : The parent resource, of the form `projects/{project}/locations/{location}` . \* `content` : The input content to corroborate, in `Content` form. Only text is supported. \* `facts` : A list of facts to corroborate the content against. Typically obtained from a prior `retrieve_contexts` call. \* `parameters` : Optional per-request parameter overrides. \* `parameters.citation_threshold` : Only return claims whose citation score exceeds this threshold.

The following sample demonstrate how to use `curl` to invoke the `corroborate_content` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://aiplatform.googleapis.com/mcp/generate&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;corroborate_content&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for CorroborateContent.

### CorroborateContentRequest

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;facts&quot;: [{object (Fact)}],&quot;parameters&quot;: {object (Parameters)},// Union field _content can be only one of the following:&quot;content&quot;: {object (Content)}// End of list of possible types for union field _content.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .

`facts[]`

` object ( Fact  ` )

Optional. Facts used to generate the text can also be used to corroborate the text.

`parameters`

` object ( Parameters  ` )

Optional. Parameters that can be set to override default settings per request.

Union field `_content` .

`_content` can be only one of the following:

`content`

` object ( Content  ` )

Optional. Input content to corroborate, only text format is supported for now.

### Content

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;role&quot;: string,&quot;parts&quot;: [{object (Part)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`role`

`string`

Optional. The producer of the content. Must be either 'user' or 'model'.

If not set, the service will default to 'user'.

`parts[]`

` object ( Part  ` )

Required. A list of `Part` objects that make up a single message. Parts of a message can have different MIME types.

A `Content` message must have at least one `Part` .

### Part

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;thought&quot;: boolean,&quot;thoughtSignature&quot;: string,&quot;mediaResolution&quot;: {object (MediaResolution)},&quot;audioTranscription&quot;: {object (AudioTranscription)},// Union field data can be only one of the following:&quot;text&quot;: string,&quot;inlineData&quot;: {object (Blob)},&quot;fileData&quot;: {object (FileData)},&quot;functionCall&quot;: {object (FunctionCall)},&quot;functionResponse&quot;: {object (FunctionResponse)},&quot;executableCode&quot;: {object (ExecutableCode)},&quot;codeExecutionResult&quot;: {object (CodeExecutionResult)}// End of list of possible types for union field data.// Union field metadata can be only one of the following:&quot;videoMetadata&quot;: {object (VideoMetadata)}// End of list of possible types for union field metadata.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`thought`

`boolean`

Optional. Indicates whether the `part` represents the model's thought process or reasoning.

`thoughtSignature`

`string ( bytes format)`

Optional. An opaque signature for the thought so it can be reused in subsequent requests.

A base64-encoded string.

`mediaResolution`

` object ( MediaResolution  ` )

per part media resolution. Media resolution for the input media.

`audioTranscription`

` object ( AudioTranscription  ` )

Optional. Audio (input or output) transcription. This is only set when this Part contains audio data.

Union field `data` .

`data` can be only one of the following:

`text`

`string`

Optional. The text content of the part. When sent from the VSCode Gemini Code Assist extension, references to @mentioned items will be converted to markdown boldface text. For example `@my-repo` will be converted to and sent as `**my-repo**` by the IDE agent.

`inlineData`

` object ( Blob  ` )

Optional. The inline data content of the part. This can be used to include images, audio, or video in a request.

`fileData`

` object ( FileData  ` )

Optional. The URI-based data of the part. This can be used to include files from Google Cloud Storage.

`functionCall`

` object ( FunctionCall  ` )

Optional. A predicted function call returned from the model. This contains the name of the function to call and the arguments to pass to the function.

`functionResponse`

` object ( FunctionResponse  ` )

Optional. The result of a function call. This is used to provide the model with the result of a function call that it predicted.

`executableCode`

` object ( ExecutableCode  ` )

Optional. Code generated by the model that is intended to be executed.

`codeExecutionResult`

` object ( CodeExecutionResult  ` )

Optional. The result of executing the `ExecutableCode` .

Union field `metadata` .

`metadata` can be only one of the following:

`videoMetadata`

` object ( VideoMetadata  ` )

Optional. Video metadata. The metadata should only be specified while the video data is presented in inline\_data or file\_data.

### Blob

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;mimeType&quot;: string,
  &quot;data&quot;: string,
  &quot;displayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mimeType`

`string`

Required. The IANA standard MIME type of the source data.

`data`

`string ( bytes format)`

Required. The raw bytes of the data.

A base64-encoded string.

`displayName`

`string`

Optional. The display name of the blob. Used to provide a label or filename to distinguish blobs.

This field is only returned in `PromptMessage` for prompt management. It is used in the Gemini calls only when server-side tools ( `code_execution` , `google_search` , and `url_context` ) are enabled.

### FileData

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;mimeType&quot;: string,
  &quot;fileUri&quot;: string,
  &quot;displayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mimeType`

`string`

Required. The IANA standard MIME type of the source data.

`fileUri`

`string`

Required. The URI of the file in Google Cloud Storage.

`displayName`

`string`

Optional. The display name of the file. Used to provide a label or filename to distinguish files.

This field is only returned in `PromptMessage` for prompt management. It is used in the Gemini calls only when server side tools ( `code_execution` , `google_search` , and `url_context` ) are enabled.

### FunctionCall

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;name&quot;: string,&quot;args&quot;: {object},&quot;partialArgs&quot;: [{object (PartialArg)}],&quot;willContinue&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`id`

`string`

Optional. The unique id of the function call. If populated, the client to execute the `function_call` and return the response with the matching `id` .

`name`

`string`

Optional. The name of the function to call. Matches `FunctionDeclaration.name` .

`args`

` object ( Struct  ` format)

Optional. The function parameters and values in JSON object format. See `FunctionDeclaration.parameters` for parameter details.

`partialArgs[]`

` object ( PartialArg  ` )

Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally.

`willContinue`

`boolean`

Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow.

### Struct

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;fields&quot;: {
    string: value,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fields`

` map (key: string, value: value ( Value  ` format))

Unordered map of dynamically typed values.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### FieldsEntry

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` value ( Value  ` format)

### Value

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field kind can be only one of the following:&quot;nullValue&quot;: null,&quot;numberValue&quot;: number,&quot;stringValue&quot;: string,&quot;boolValue&quot;: boolean,&quot;structValue&quot;: {object},&quot;listValue&quot;: array// End of list of possible types for union field kind.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `kind` . The kind of value. `kind` can be only one of the following:

`nullValue`

`null`

Represents a JSON `null` .

`numberValue`

`number`

Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type.

`stringValue`

`string`

Represents a JSON string.

`boolValue`

`boolean`

Represents a JSON boolean ( `true` or `false` literal in JSON).

`structValue`

` object ( Struct  ` format)

Represents a JSON object.

`listValue`

` array ( ListValue  ` format)

Represents a JSON array.

### ListValue

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;values&quot;: [
    value
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`values[]`

` value ( Value  ` format)

Repeated field of dynamically typed values.

### PartialArg

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;jsonPath&quot;: string,&quot;willContinue&quot;: boolean,// Union field delta can be only one of the following:&quot;nullValue&quot;: null,&quot;numberValue&quot;: number,&quot;stringValue&quot;: string,&quot;boolValue&quot;: boolean// End of list of possible types for union field delta.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`jsonPath`

`string`

Required. A JSON Path (RFC 9535) to the argument being streamed. <https://datatracker.ietf.org/doc/html/rfc9535> . e.g. "$.foo.bar\[0\].data".

`willContinue`

`boolean`

Optional. Whether this is not the last part of the same json\_path. If true, another PartialArg message for the current json\_path is expected to follow.

Union field `delta` . The delta of field value being streamed. `delta` can be only one of the following:

`nullValue`

`null`

Optional. Represents a null value.

`numberValue`

`number`

Optional. Represents a double value.

`stringValue`

`string`

Optional. Represents a string value.

`boolValue`

`boolean`

Optional. Represents a boolean value.

### FunctionResponse

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;name&quot;: string,&quot;response&quot;: {object},&quot;parts&quot;: [{object (FunctionResponsePart)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`id`

`string`

Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id` .

`name`

`string`

Required. The name of the function to call. Matches `FunctionDeclaration.name` and `FunctionCall.name` .

`response`

` object ( Struct  ` format)

Required. The function response in JSON object format. Use "output" key to specify function output and "error" key to specify error details (if any). If "output" and "error" keys are not specified, then whole "response" is treated as function output.

`parts[]`

` object ( FunctionResponsePart  ` )

Optional. Ordered `Parts` that constitute a function response. Parts may have different IANA MIME types.

### FunctionResponsePart

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field data can be only one of the following:&quot;inlineData&quot;: {object (FunctionResponseBlob)},&quot;fileData&quot;: {object (FunctionResponseFileData)}// End of list of possible types for union field data.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `data` . The data of the function response part. `data` can be only one of the following:

`inlineData`

` object ( FunctionResponseBlob  ` )

Inline media bytes.

`fileData`

` object ( FunctionResponseFileData  ` )

URI based data.

### FunctionResponseBlob

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;mimeType&quot;: string,
  &quot;data&quot;: string,
  &quot;displayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mimeType`

`string`

Required. The IANA standard MIME type of the source data.

`data`

`string ( bytes format)`

Required. Raw bytes.

A base64-encoded string.

`displayName`

`string`

Optional. Display name of the blob.

Used to provide a label or filename to distinguish blobs.

This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code\_execution, google\_search, and url\_context) are enabled.

### FunctionResponseFileData

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;mimeType&quot;: string,
  &quot;fileUri&quot;: string,
  &quot;displayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mimeType`

`string`

Required. The IANA standard MIME type of the source data.

`fileUri`

`string`

Required. URI.

`displayName`

`string`

Optional. Display name of the file data.

Used to provide a label or filename to distinguish file datas.

This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code\_execution, google\_search, and url\_context) are enabled.

### ExecutableCode

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;language&quot;: enum (Language),&quot;code&quot;: string,// Union field _id can be only one of the following:&quot;id&quot;: string// End of list of possible types for union field _id.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`language`

` enum ( Language  ` )

Required. Programming language of the `code` .

`code`

`string`

Required. The code to be executed.

Union field `_id` .

`_id` can be only one of the following:

`id`

`string`

Optional. Unique identifier of the `ExecutableCode` part. The server returns the `CodeExecutionResult` with the matching `id` .

### CodeExecutionResult

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outcome&quot;: enum (Outcome),&quot;output&quot;: string,// Union field _id can be only one of the following:&quot;id&quot;: string// End of list of possible types for union field _id.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outcome`

` enum ( Outcome  ` )

Required. Outcome of the code execution.

`output`

`string`

Optional. Contains stdout when code execution is successful, stderr or other description otherwise.

Union field `_id` .

`_id` can be only one of the following:

`id`

`string`

Optional. The identifier of the `ExecutableCode` part this result is for. Only populated if the corresponding `ExecutableCode` has an id.

### VideoMetadata

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;startOffset&quot;: string,
  &quot;endOffset&quot;: string,
  &quot;fps&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`startOffset`

` string ( Duration  ` format)

Optional. The start offset of the video.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`endOffset`

` string ( Duration  ` format)

Optional. The end offset of the video.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`fps`

`number`

Optional. The frame rate of the video sent to the model. If not specified, the default value is 1.0. The valid range is (0.0, 24.0\].

### Duration

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years

`nanos`

`integer`

Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive.

### MediaResolution

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field value can be only one of the following:&quot;level&quot;: enum (Level)// End of list of possible types for union field value.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `value` .

`value` can be only one of the following:

`level`

` enum ( Level  ` )

The tokenization quality used for given media.

### AudioTranscription

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;text&quot;: string,&quot;speakerLabel&quot;: string,&quot;words&quot;: [{object (WordInfo)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`text`

`string`

Required. The transcription text of this audio segment.

`speakerLabel`

`string`

Optional. A label identifying the speaker of this audio segment (e.g. "spk\_1", "spk\_2"). Present when diarization is set.

`words[]`

` object ( WordInfo  ` )

Optional. Detailed word-level transcriptions and timing details. Present when word\_timestamp is set.

### WordInfo

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;word&quot;: string,
  &quot;startOffset&quot;: string,
  &quot;endOffset&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`word`

`string`

Required. Transcript of the word.

`startOffset`

` string ( Duration  ` format)

Optional. Start offset in time of the word relative to the start of the audio.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`endOffset`

` string ( Duration  ` format)

Optional. End offset in time of the word relative to the start of the audio.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### Fact

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _query can be only one of the following:&quot;query&quot;: string// End of list of possible types for union field _query.// Union field _title can be only one of the following:&quot;title&quot;: string// End of list of possible types for union field _title.// Union field _uri can be only one of the following:&quot;uri&quot;: string// End of list of possible types for union field _uri.// Union field _summary can be only one of the following:&quot;summary&quot;: string// End of list of possible types for union field _summary.// Union field _vector_distance can be only one of the following:&quot;vectorDistance&quot;: number// End of list of possible types for union field _vector_distance.// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _chunk can be only one of the following:&quot;chunk&quot;: {object (RagChunk)}// End of list of possible types for union field _chunk.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_query` .

`_query` can be only one of the following:

`query`

`string`

Query that is used to retrieve this fact.

Union field `_title` .

`_title` can be only one of the following:

`title`

`string`

If present, it refers to the title of this fact.

Union field `_uri` .

`_uri` can be only one of the following:

`uri`

`string`

If present, this uri links to the source of the fact.

Union field `_summary` .

`_summary` can be only one of the following:

`summary`

`string`

If present, the summary/snippet of the fact.

Union field `_vector_distance` .

`_vector_distance` can be only one of the following:

` vectorDistance (deprecated)  `

`number`

> This item is deprecated\!

If present, the distance between the query vector and this fact vector.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

If present, according to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the fact and its range depends on the metric type.

For example, if the metric type is COSINE\_DISTANCE, it represents the distance between the query and the fact. The larger the distance, the less relevant the fact is to the query. The range is \[0, 2\], while 0 means the most relevant and 2 means the least relevant.

Union field `_chunk` .

`_chunk` can be only one of the following:

`chunk`

` object ( RagChunk  ` )

If present, chunk properties.

### RagChunk

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;text&quot;: string,// Union field _page_span can be only one of the following:&quot;pageSpan&quot;: {object (PageSpan)}// End of list of possible types for union field _page_span.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`text`

`string`

The content of the chunk.

Union field `_page_span` .

`_page_span` can be only one of the following:

`pageSpan`

` object ( PageSpan  ` )

If populated, represents where the chunk starts and ends in the document.

### PageSpan

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;firstPage&quot;: integer,
  &quot;lastPage&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`firstPage`

`integer`

Page where chunk starts in the document. Inclusive. 1-indexed.

`lastPage`

`integer`

Page where chunk ends in the document. Inclusive. 1-indexed.

### Parameters

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;citationThreshold&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`citationThreshold`

`number`

Optional. Only return claims with citation score larger than the threshold.

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

Enums

`NULL_VALUE`

Null value.

### Language

Supported programming languages for the generated code.

Enums

`LANGUAGE_UNSPECIFIED`

Unspecified language. This value should not be used.

`PYTHON`

Python \>= 3.10, with numpy and simpy available.

### Outcome

Enumeration of possible outcomes of the code execution.

Enums

`OUTCOME_UNSPECIFIED`

Unspecified status. This value should not be used.

`OUTCOME_OK`

Code execution completed successfully. `output` contains the stdout, if any.

`OUTCOME_FAILED`

Code execution failed. `output` contains the stderr and stdout, if any.

`OUTCOME_DEADLINE_EXCEEDED`

Code execution ran for too long, and was cancelled. There may or may not be a partial `output` present.

### Level

The media resolution level.

Enums

`MEDIA_RESOLUTION_UNSPECIFIED`

Media resolution has not been set.

`MEDIA_RESOLUTION_LOW`

Media resolution set to low.

`MEDIA_RESOLUTION_MEDIUM`

Media resolution set to medium.

`MEDIA_RESOLUTION_HIGH`

Media resolution set to high.

`MEDIA_RESOLUTION_ULTRA_HIGH`

Media resolution set to ultra high. This is for image only.

## Output Schema

Response message for CorroborateContent.

### CorroborateContentResponse

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;claims&quot;: [{object (Claim)}],// Union field _corroboration_score can be only one of the following:&quot;corroborationScore&quot;: number// End of list of possible types for union field _corroboration_score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`claims[]`

` object ( Claim  ` )

Claims that are extracted from the input content and facts that support the claims.

Union field `_corroboration_score` .

`_corroboration_score` can be only one of the following:

`corroborationScore`

`number`

Confidence score of corroborating content. Value is \[0,1\] with 1 is the most confidence.

### Claim

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;factIndexes&quot;: [integer],// Union field _start_index can be only one of the following:&quot;startIndex&quot;: integer// End of list of possible types for union field _start_index.// Union field _end_index can be only one of the following:&quot;endIndex&quot;: integer// End of list of possible types for union field _end_index.// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`factIndexes[]`

`integer`

Indexes of the facts supporting this claim.

Union field `_start_index` .

`_start_index` can be only one of the following:

`startIndex`

`integer`

Index in the input text where the claim starts (inclusive).

Union field `_end_index` .

`_end_index` can be only one of the following:

`endIndex`

`integer`

Index in the input text where the claim ends (exclusive).

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Confidence score of this corroboration.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
