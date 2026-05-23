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
    &quot;name&quot;: &quot;generate_content&quot;,
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

Request message for \[PredictionService.GenerateContent\].

### GenerateContentRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;model&quot;: string,&quot;contents&quot;: [{object (Content)}],&quot;cachedContent&quot;: string,&quot;tools&quot;: [{object (Tool)}],&quot;toolConfig&quot;: {object (ToolConfig)},&quot;labels&quot;: {string: string,...},&quot;safetySettings&quot;: [{object (SafetySetting)}],&quot;modelArmorConfig&quot;: {object (ModelArmorConfig)},&quot;generationConfig&quot;: {object (GenerationConfig)},// Union field _system_instruction can be only one of the following:&quot;systemInstruction&quot;: {object (Content)}// End of list of possible types for union field _system_instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`model`

`string`

Required. The fully qualified name of the publisher model or tuned model endpoint to use.

Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`

Tuned model endpoint format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

`contents[]`

` object ( Content  ` )

Required. The content of the current conversation with the model.

For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request.

`cachedContent`

`string`

Optional. The name of the cached content used as context to serve the prediction. Note: only used in explicit caching, where users can have control over caching (e.g. what content to cache) and enjoy guaranteed cost savings. Format: `projects/{project}/locations/{location}/cachedContents/{cachedContent}`

`tools[]`

` object ( Tool  ` )

Optional. A list of `Tools` the model may use to generate the next response.

A `Tool` is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model.

`toolConfig`

` object ( ToolConfig  ` )

Optional. Tool config. This config is shared for all tools provided in the request.

`labels`

`map (key: string, value: string)`

Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only.

Label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`safetySettings[]`

` object ( SafetySetting  ` )

Optional. Per request settings for blocking unsafe content. Enforced on GenerateContentResponse.candidates.

`modelArmorConfig`

` object ( ModelArmorConfig  ` )

Optional. Settings for prompt and response sanitization using the Model Armor service. If supplied, safety\_settings must not be supplied.

`generationConfig`

` object ( GenerationConfig  ` )

Optional. Generation config.

Union field `_system_instruction` .

`_system_instruction` can be only one of the following:

`systemInstruction`

` object ( Content  ` )

Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;thought&quot;: boolean,&quot;thoughtSignature&quot;: string,&quot;mediaResolution&quot;: {object (MediaResolution)},// Union field data can be only one of the following:&quot;text&quot;: string,&quot;inlineData&quot;: {object (Blob)},&quot;fileData&quot;: {object (FileData)},&quot;functionCall&quot;: {object (FunctionCall)},&quot;functionResponse&quot;: {object (FunctionResponse)},&quot;executableCode&quot;: {object (ExecutableCode)},&quot;codeExecutionResult&quot;: {object (CodeExecutionResult)}// End of list of possible types for union field data.// Union field metadata can be only one of the following:&quot;videoMetadata&quot;: {object (VideoMetadata)}// End of list of possible types for union field metadata.}</code></pre></td>
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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;language&quot;: enum (Language),&quot;code&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`language`

`enum ( Language` )

Required. Programming language of the `code` .

`code`

`string`

Required. The code to be executed.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outcome&quot;: enum (Outcome),&quot;output&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outcome`

`enum ( Outcome` )

Required. Outcome of the code execution.

`output`

`string`

Optional. Contains stdout when code execution is successful, stderr or other description otherwise.

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

`enum ( Level` )

The tokenization quality used for given media.

### Tool

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;functionDeclarations&quot;: [{object (FunctionDeclaration)}],&quot;retrieval&quot;: {object (Retrieval)},&quot;googleSearch&quot;: {object (GoogleSearch)},&quot;googleSearchRetrieval&quot;: {object (GoogleSearchRetrieval)},&quot;googleMaps&quot;: {object (GoogleMaps)},&quot;enterpriseWebSearch&quot;: {object (EnterpriseWebSearch)},&quot;codeExecution&quot;: {object (CodeExecution)},&quot;urlContext&quot;: {object (UrlContext)},&quot;computerUse&quot;: {object (ComputerUse)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`functionDeclarations[]`

` object ( FunctionDeclaration  ` )

Optional. Function tool type. One or more function declarations to be passed to the model along with the current user query. Model may decide to call a subset of these functions by populating `FunctionCall` in the response. User should provide a `FunctionResponse` for each function call in the next turn. Based on the function responses, Model will generate the final response back to the user. Maximum 512 function declarations can be provided.

`retrieval`

` object ( Retrieval  ` )

Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation.

`googleSearch`

` object ( GoogleSearch  ` )

Optional. GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

` googleSearchRetrieval (deprecated)  `

` object ( GoogleSearchRetrieval  ` )

> Optional. The `google_search_retrieval` field is deprecated. Use `google_search` instead. This field is for use with Gemini 1.5 models; `google_search` is used for Gemini 2.0 and newer models.

Optional. Specialized retrieval tool that is powered by Google Search.

`googleMaps`

` object ( GoogleMaps  ` )

Optional. GoogleMaps tool type. Tool to support Google Maps in Model.

`enterpriseWebSearch`

` object ( EnterpriseWebSearch  ` )

Optional. Tool to support searching public web data, powered by Agent Platform Search and Sec4 compliance.

`codeExecution`

`object ( CodeExecution` )

Optional. CodeExecution tool type. Enables the model to execute code as part of generation.

`urlContext`

`object ( UrlContext` )

Optional. Tool to support URL context retrieval.

`computerUse`

` object ( ComputerUse  ` )

Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations.

### FunctionDeclaration

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;description&quot;: string,&quot;parameters&quot;: {object (Schema)},&quot;parametersJsonSchema&quot;: value,&quot;response&quot;: {object (Schema)},&quot;responseJsonSchema&quot;: value}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots, colons and dashes, with a maximum length of 128.

`description`

`string`

Optional. Description and purpose of the function. Model uses it to decide how and whether to call the function.

`parameters`

` object ( Schema  ` )

Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema Value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1

`parametersJsonSchema`

` value ( Value  ` format)

Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example:

    {
      "type": "object",
      "properties": {
        "name": { "type": "string" },
        "age": { "type": "integer" }
      },
      "additionalProperties": false,
      "required": ["name", "age"],
      "propertyOrdering": ["name", "age"]
    }

This field is mutually exclusive with `parameters` .

`response`

` object ( Schema  ` )

Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function.

`responseJsonSchema`

` value ( Value  ` format)

Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function.

This field is mutually exclusive with `response` .

### Schema

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (Type),&quot;format&quot;: string,&quot;title&quot;: string,&quot;description&quot;: string,&quot;nullable&quot;: boolean,&quot;default&quot;: value,&quot;items&quot;: {object (Schema)},&quot;minItems&quot;: string,&quot;maxItems&quot;: string,&quot;enum&quot;: [string],&quot;properties&quot;: {string: {object (Schema)},...},&quot;propertyOrdering&quot;: [string],&quot;required&quot;: [string],&quot;minProperties&quot;: string,&quot;maxProperties&quot;: string,&quot;minimum&quot;: number,&quot;maximum&quot;: number,&quot;minLength&quot;: string,&quot;maxLength&quot;: string,&quot;pattern&quot;: string,&quot;example&quot;: value,&quot;anyOf&quot;: [{object (Schema)}],&quot;additionalProperties&quot;: value,&quot;ref&quot;: string,&quot;defs&quot;: {string: {object (Schema)},...}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

`enum ( Type` )

Optional. Data type of the schema field.

`format`

`string`

Optional. The format of the data. For `NUMBER` type, format can be `float` or `double` . For `INTEGER` type, format can be `int32` or `int64` . For `STRING` type, format can be `email` , `byte` , `date` , `date-time` , `password` , and other formats to further refine the data type.

`title`

`string`

Optional. Title for the schema.

`description`

`string`

Optional. Describes the data. The model uses this field to understand the purpose of the schema and how to use it. It is a best practice to provide a clear and descriptive explanation for the schema and its properties here, rather than in the prompt.

`nullable`

`boolean`

Optional. Indicates if the value of this field can be null.

`default`

` value ( Value  ` format)

Optional. Default value to use if the field is not specified.

`items`

` object ( Schema  ` )

Optional. If type is `ARRAY` , `items` specifies the schema of elements in the array.

`minItems`

`string ( int64 format)`

Optional. If type is `ARRAY` , `min_items` specifies the minimum number of items in an array.

`maxItems`

`string ( int64 format)`

Optional. If type is `ARRAY` , `max_items` specifies the maximum number of items in an array.

`enum[]`

`string`

Optional. Possible values of the field. This field can be used to restrict a value to a fixed set of values. To mark a field as an enum, set `format` to `enum` and provide the list of possible values in `enum` . For example: 1. To define directions: `{type:STRING, format:enum, enum:["EAST", "NORTH", "SOUTH", "WEST"]}` 2. To define apartment numbers: `{type:INTEGER, format:enum, enum:["101", "201", "301"]}`

`properties`

` map (key: string, value: object ( Schema  ` ))

Optional. If type is `OBJECT` , `properties` is a map of property names to schema definitions for each property of the object.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`propertyOrdering[]`

`string`

Optional. Order of properties displayed or used where order matters. This is not a standard field in OpenAPI specification, but can be used to control the order of properties.

`required[]`

`string`

Optional. If type is `OBJECT` , `required` lists the names of properties that must be present.

`minProperties`

`string ( int64 format)`

Optional. If type is `OBJECT` , `min_properties` specifies the minimum number of properties that can be provided.

`maxProperties`

`string ( int64 format)`

Optional. If type is `OBJECT` , `max_properties` specifies the maximum number of properties that can be provided.

`minimum`

`number`

Optional. If type is `INTEGER` or `NUMBER` , `minimum` specifies the minimum allowed value.

`maximum`

`number`

Optional. If type is `INTEGER` or `NUMBER` , `maximum` specifies the maximum allowed value.

`minLength`

`string ( int64 format)`

Optional. If type is `STRING` , `min_length` specifies the minimum length of the string.

`maxLength`

`string ( int64 format)`

Optional. If type is `STRING` , `max_length` specifies the maximum length of the string.

`pattern`

`string`

Optional. If type is `STRING` , `pattern` specifies a regular expression that the string must match.

`example`

` value ( Value  ` format)

Optional. Example of an instance of this schema.

`anyOf[]`

` object ( Schema  ` )

Optional. The instance must be valid against any (one or more) of the subschemas listed in `any_of` .

`additionalProperties`

` value ( Value  ` format)

Optional. If `type` is `OBJECT` , specifies how to handle properties not defined in `properties` . If it is a boolean `false` , no additional properties are allowed. If it is a schema, additional properties are allowed if they conform to the schema.

`ref`

`string`

Optional. Allows referencing another schema definition to use in place of this schema. The value must be a valid reference to a schema in `defs` .

For example, the following schema defines a reference to a schema node named "Pet":

type: object properties: pet: ref: \#/defs/Pet defs: Pet: type: object properties: name: type: string

The value of the "pet" property is a reference to the schema node named "Pet". See details in <https://json-schema.org/understanding-json-schema/structuring>

`defs`

` map (key: string, value: object ( Schema  ` ))

Optional. `defs` provides a map of schema definitions that can be reused by `ref` elsewhere in the schema. Only allowed at root level of the schema.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### PropertiesEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (Schema)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( Schema  ` )

### DefsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (Schema)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( Schema  ` )

### Retrieval

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;disableAttribution&quot;: boolean,// Union field source can be only one of the following:&quot;vertexAiSearch&quot;: {object (VertexAISearch)},&quot;vertexRagStore&quot;: {object (VertexRagStore)}// End of list of possible types for union field source.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` disableAttribution (deprecated)  `

`boolean`

> This item is deprecated\!

Optional. Deprecated. This option is no longer supported.

Union field `source` . The source of the retrieval. `source` can be only one of the following:

`vertexAiSearch`

` object ( VertexAISearch  ` )

Set to use data source powered by Agent Platform Search.

`vertexRagStore`

` object ( VertexRagStore  ` )

Set to use data source powered by Vertex RAG store. User data is uploaded via the VertexRagDataService.

### VertexAISearch

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;datastore&quot;: string,&quot;engine&quot;: string,&quot;maxResults&quot;: integer,&quot;filter&quot;: string,&quot;dataStoreSpecs&quot;: [{object (DataStoreSpec)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`datastore`

`string`

Optional. Fully-qualified Agent Platform Search data store resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`

`engine`

`string`

Optional. Fully-qualified Agent Platform Search engine resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}`

`maxResults`

`integer`

Optional. Number of search results to return per query. The default value is 10. The maximumm allowed value is 10.

`filter`

`string`

Optional. Filter strings to be passed to the search API.

`dataStoreSpecs[]`

` object ( DataStoreSpec  ` )

Specifications that define the specific DataStores to be searched, along with configurations for those data stores. This is only considered for Engines with multiple data stores. It should only be set if engine is used.

### DataStoreSpec

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
  &quot;dataStore&quot;: string,
  &quot;filter&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataStore`

`string`

Full resource name of DataStore, such as Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`

`filter`

`string`

Optional. Filter specification to filter documents in the data store specified by data\_store field. For more information on filtering, see [Filtering](https://cloud.google.com/generative-ai-app-builder/docs/filter-search-metadata)

### VertexRagStore

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragCorpora&quot;: [string],&quot;ragResources&quot;: [{object (RagResource)}],&quot;ragRetrievalConfig&quot;: {object (RagRetrievalConfig)},&quot;storeContext&quot;: boolean,// Union field _similarity_top_k can be only one of the following:&quot;similarityTopK&quot;: integer// End of list of possible types for union field _similarity_top_k.// Union field _vector_distance_threshold can be only one of the following:&quot;vectorDistanceThreshold&quot;: number// End of list of possible types for union field _vector_distance_threshold.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` ragCorpora[] (deprecated)  `

`string`

> This item is deprecated\!

Optional. Deprecated. Please use rag\_resources instead.

`ragResources[]`

` object ( RagResource  ` )

Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.

`ragRetrievalConfig`

` object ( RagRetrievalConfig  ` )

Optional. The retrieval config for the Rag query.

`storeContext`

`boolean`

Optional. Currently only supported for Gemini Multimodal Live API.

In Gemini Multimodal Live API, if `store_context` bool is specified, Gemini will leverage it to automatically memorize the interactions between the client and Gemini, and retrieve context when needed to augment the response generation for users' ongoing and future interactions.

Union field `_similarity_top_k` .

`_similarity_top_k` can be only one of the following:

` similarityTopK (deprecated)  `

`integer`

> This item is deprecated\!

Optional. Number of top k results to return from the selected corpora.

Union field `_vector_distance_threshold` .

`_vector_distance_threshold` can be only one of the following:

` vectorDistanceThreshold (deprecated)  `

`number`

> This item is deprecated\!

Optional. Only return results with vector distance smaller than the threshold.

### RagResource

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
  &quot;ragCorpus&quot;: string,
  &quot;ragFileIds&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`ragCorpus`

`string`

Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`

`ragFileIds[]`

`string`

Optional. rag\_file\_id. The files should be in the same rag\_corpus set in rag\_corpus field.

### RagRetrievalConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;topK&quot;: integer,&quot;hybridSearch&quot;: {object (HybridSearch)},&quot;filter&quot;: {object (Filter)},&quot;ranking&quot;: {object (Ranking)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`topK`

`integer`

Optional. The number of contexts to retrieve.

`hybridSearch`

` object ( HybridSearch  ` )

Optional. Config for Hybrid Search.

`filter`

` object ( Filter  ` )

Optional. Config for filters.

`ranking`

` object ( Ranking  ` )

Optional. Config for ranking and reranking.

### HybridSearch

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _alpha can be only one of the following:&quot;alpha&quot;: number// End of list of possible types for union field _alpha.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_alpha` .

`_alpha` can be only one of the following:

`alpha`

`number`

Optional. Alpha value controls the weight between dense and sparse vector search results. The range is \[0, 1\], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally.

### Filter

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metadataFilter&quot;: string,// Union field vector_db_threshold can be only one of the following:&quot;vectorDistanceThreshold&quot;: number,&quot;vectorSimilarityThreshold&quot;: number// End of list of possible types for union field vector_db_threshold.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`metadataFilter`

`string`

Optional. String for metadata filtering.

Union field `vector_db_threshold` . Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. `vector_db_threshold` can be only one of the following:

`vectorDistanceThreshold`

`number`

Optional. Only returns contexts with vector distance smaller than the threshold.

`vectorSimilarityThreshold`

`number`

Optional. Only returns contexts with vector similarity larger than the threshold.

### Ranking

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field ranking_config can be only one of the following:&quot;rankService&quot;: {object (RankService)},&quot;llmRanker&quot;: {object (LlmRanker)}// End of list of possible types for union field ranking_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `ranking_config` . Config options for ranking. Currently only Rank Service is supported. `ranking_config` can be only one of the following:

`rankService`

` object ( RankService  ` )

Optional. Config for Rank Service.

`llmRanker`

` object ( LlmRanker  ` )

Optional. Config for LlmRanker.

### RankService

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _model_name can be only one of the following:&quot;modelName&quot;: string// End of list of possible types for union field _model_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_model_name` .

`_model_name` can be only one of the following:

`modelName`

`string`

Optional. The model name of the rank service. Format: `semantic-ranker-512@latest`

### LlmRanker

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _model_name can be only one of the following:&quot;modelName&quot;: string// End of list of possible types for union field _model_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_model_name` .

`_model_name` can be only one of the following:

`modelName`

`string`

Optional. The model name used for ranking. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models) .

### GoogleSearch

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;excludeDomains&quot;: [string],// Union field _blocking_confidence can be only one of the following:&quot;blockingConfidence&quot;: enum (PhishBlockThreshold)// End of list of possible types for union field _blocking_confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`excludeDomains[]`

`string`

Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: \["amazon.com", "facebook.com"\].

Union field `_blocking_confidence` .

`_blocking_confidence` can be only one of the following:

`blockingConfidence`

`enum ( PhishBlockThreshold` )

Optional. Sites with confidence level chosen & above this value will be blocked from the search results.

### GoogleSearchRetrieval

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dynamicRetrievalConfig&quot;: {object (DynamicRetrievalConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dynamicRetrievalConfig`

` object ( DynamicRetrievalConfig  ` )

Specifies the dynamic retrieval configuration for the given source.

### DynamicRetrievalConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mode&quot;: enum (Mode),// Union field _dynamic_threshold can be only one of the following:&quot;dynamicThreshold&quot;: number// End of list of possible types for union field _dynamic_threshold.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mode`

`enum ( Mode` )

The mode of the predictor to be used in dynamic retrieval.

Union field `_dynamic_threshold` .

`_dynamic_threshold` can be only one of the following:

`dynamicThreshold`

`number`

Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used.

### GoogleMaps

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
  &quot;enableWidget&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enableWidget`

`boolean`

Optional. If true, include the widget context token in the response.

### EnterpriseWebSearch

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;excludeDomains&quot;: [string],// Union field _blocking_confidence can be only one of the following:&quot;blockingConfidence&quot;: enum (PhishBlockThreshold)// End of list of possible types for union field _blocking_confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`excludeDomains[]`

`string`

Optional. List of domains to be excluded from the search results. The default limit is 2000 domains.

Union field `_blocking_confidence` .

`_blocking_confidence` can be only one of the following:

`blockingConfidence`

`enum ( PhishBlockThreshold` )

Optional. Sites with confidence level chosen & above this value will be blocked from the search results.

### ComputerUse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;environment&quot;: enum (Environment),&quot;excludedPredefinedFunctions&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`environment`

`enum ( Environment` )

Required. The environment being operated.

`excludedPredefinedFunctions[]`

`string`

Optional. By default, [predefined functions](https://cloud.google.com/vertex-ai/generative-ai/docs/computer-use#supported-actions) are included in the final model call. Some of them can be explicitly excluded from being automatically included. This can serve two purposes: 1. Using a more restricted / different action space. 2. Improving the definitions / instructions of predefined functions.

### ToolConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;functionCallingConfig&quot;: {object (FunctionCallingConfig)},&quot;retrievalConfig&quot;: {object (RetrievalConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`functionCallingConfig`

` object ( FunctionCallingConfig  ` )

Optional. Function calling config.

`retrievalConfig`

` object ( RetrievalConfig  ` )

Optional. Retrieval config.

### FunctionCallingConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mode&quot;: enum (Mode),&quot;allowedFunctionNames&quot;: [string],&quot;streamFunctionCallArguments&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mode`

`enum ( Mode` )

Optional. Function calling mode.

`allowedFunctionNames[]`

`string`

Optional. Function names to call. Only set when the Mode is ANY. Function names should match `FunctionDeclaration.name` . With mode set to ANY, model will predict a function call from the set of function names provided.

`streamFunctionCallArguments`

`boolean`

Optional. When set to true, arguments of a single function call will be streamed out in multiple parts/contents/responses. Partial parameter results will be returned in the `FunctionCall.partial_args` field.

### RetrievalConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _lat_lng can be only one of the following:&quot;latLng&quot;: {object (LatLng)}// End of list of possible types for union field _lat_lng.// Union field _language_code can be only one of the following:&quot;languageCode&quot;: string// End of list of possible types for union field _language_code.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_lat_lng` .

`_lat_lng` can be only one of the following:

`latLng`

` object ( LatLng  ` )

The location of the user.

Union field `_language_code` .

`_language_code` can be only one of the following:

`languageCode`

`string`

The language code of the user.

### LatLng

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
  &quot;latitude&quot;: number,
  &quot;longitude&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`latitude`

`number`

The latitude in degrees. It must be in the range \[-90.0, +90.0\].

`longitude`

`number`

The longitude in degrees. It must be in the range \[-180.0, +180.0\].

### LabelsEntry

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
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### SafetySetting

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;category&quot;: enum (HarmCategory),&quot;threshold&quot;: enum (HarmBlockThreshold),&quot;method&quot;: enum (HarmBlockMethod)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`category`

`enum ( HarmCategory` )

Required. The harm category to be blocked.

`threshold`

`enum ( HarmBlockThreshold` )

Required. The threshold for blocking content. If the harm probability exceeds this threshold, the content will be blocked.

`method`

`enum ( HarmBlockMethod` )

Optional. The method for blocking content. If not specified, the default behavior is to use the probability score.

### ModelArmorConfig

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
  &quot;promptTemplateName&quot;: string,
  &quot;responseTemplateName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`promptTemplateName`

`string`

Optional. The resource name of the Model Armor template to use for prompt screening.

A Model Armor template is a set of customized filters and thresholds that define how Model Armor screens content. If specified, Model Armor will use this template to check the user's prompt for safety and security risks before it is sent to the model.

The name must be in the format `projects/{project}/locations/{location}/templates/{template}` .

`responseTemplateName`

`string`

Optional. The resource name of the Model Armor template to use for response screening.

A Model Armor template is a set of customized filters and thresholds that define how Model Armor screens content. If specified, Model Armor will use this template to check the model's response for safety and security risks before it is returned to the user.

The name must be in the format `projects/{project}/locations/{location}/templates/{template}` .

### GenerationConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stopSequences&quot;: [string],&quot;responseMimeType&quot;: string,&quot;responseModalities&quot;: [enum (Modality)],&quot;thinkingConfig&quot;: {object (ThinkingConfig)},&quot;modelConfig&quot;: {object (ModelConfig)},// Union field _temperature can be only one of the following:&quot;temperature&quot;: number// End of list of possible types for union field _temperature.// Union field _top_p can be only one of the following:&quot;topP&quot;: number// End of list of possible types for union field _top_p.// Union field _top_k can be only one of the following:&quot;topK&quot;: number// End of list of possible types for union field _top_k.// Union field _candidate_count can be only one of the following:&quot;candidateCount&quot;: integer// End of list of possible types for union field _candidate_count.// Union field _max_output_tokens can be only one of the following:&quot;maxOutputTokens&quot;: integer// End of list of possible types for union field _max_output_tokens.// Union field _response_logprobs can be only one of the following:&quot;responseLogprobs&quot;: boolean// End of list of possible types for union field _response_logprobs.// Union field _logprobs can be only one of the following:&quot;logprobs&quot;: integer// End of list of possible types for union field _logprobs.// Union field _presence_penalty can be only one of the following:&quot;presencePenalty&quot;: number// End of list of possible types for union field _presence_penalty.// Union field _frequency_penalty can be only one of the following:&quot;frequencyPenalty&quot;: number// End of list of possible types for union field _frequency_penalty.// Union field _seed can be only one of the following:&quot;seed&quot;: integer// End of list of possible types for union field _seed.// Union field _response_schema can be only one of the following:&quot;responseSchema&quot;: {object (Schema)}// End of list of possible types for union field _response_schema.// Union field _response_json_schema can be only one of the following:&quot;responseJsonSchema&quot;: value// End of list of possible types for union field _response_json_schema.// Union field _routing_config can be only one of the following:&quot;routingConfig&quot;: {object (RoutingConfig)}// End of list of possible types for union field _routing_config.// Union field _audio_timestamp can be only one of the following:&quot;audioTimestamp&quot;: boolean// End of list of possible types for union field _audio_timestamp.// Union field _media_resolution can be only one of the following:&quot;mediaResolution&quot;: enum (MediaResolution)// End of list of possible types for union field _media_resolution.// Union field _speech_config can be only one of the following:&quot;speechConfig&quot;: {object (SpeechConfig)}// End of list of possible types for union field _speech_config.// Union field _enable_affective_dialog can be only one of the following:&quot;enableAffectiveDialog&quot;: boolean// End of list of possible types for union field _enable_affective_dialog.// Union field _image_config can be only one of the following:&quot;imageConfig&quot;: {object (ImageConfig)}// End of list of possible types for union field _image_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stopSequences[]`

`string`

Optional. A list of character sequences that will stop the model from generating further tokens. If a stop sequence is generated, the output will end at that point. This is useful for controlling the length and structure of the output. For example, you can use \["\\n", "\#\#\#"\] to stop generation at a new line or a specific marker.

`responseMimeType`

`string`

Optional. The IANA standard MIME type of the response. The model will generate output that conforms to this MIME type. Supported values include 'text/plain' (default) and 'application/json'. The model needs to be prompted to output the appropriate response type, otherwise the behavior is undefined.

`responseModalities[]`

`enum ( Modality` )

Optional. The modalities of the response. The model will generate a response that includes all the specified modalities. For example, if this is set to `[TEXT, IMAGE]` , the response will include both text and an image.

`thinkingConfig`

` object ( ThinkingConfig  ` )

Optional. Configuration for thinking features. An error will be returned if this field is set for models that don't support thinking.

` modelConfig (deprecated)  `

` object ( ModelConfig  ` )

> Optional. The `model_config` field is deprecated and is not supported anymore. Use `routing_config` instead.

Optional. Config for model selection.

Union field `_temperature` .

`_temperature` can be only one of the following:

`temperature`

`number`

Optional. Controls the randomness of the output. A higher temperature results in more creative and diverse responses, while a lower temperature makes the output more predictable and focused. The valid range is (0.0, 2.0\].

Union field `_top_p` .

`_top_p` can be only one of the following:

`topP`

`number`

Optional. Specifies the nucleus sampling threshold. The model considers only the smallest set of tokens whose cumulative probability is at least `top_p` . This helps generate more diverse and less repetitive responses. For example, a `top_p` of 0.9 means the model considers tokens until the cumulative probability of the tokens to select from reaches 0.9. It's recommended to adjust either temperature or `top_p` , but not both.

Union field `_top_k` .

`_top_k` can be only one of the following:

`topK`

`number`

Optional. Specifies the top-k sampling threshold. The model considers only the top k most probable tokens for the next token. This can be useful for generating more coherent and less random text. For example, a `top_k` of 40 means the model will choose the next word from the 40 most likely words.

Union field `_candidate_count` .

`_candidate_count` can be only one of the following:

`candidateCount`

`integer`

Optional. The number of candidate responses to generate.

A higher `candidate_count` can provide more options to choose from, but it also consumes more resources. This can be useful for generating a variety of responses and selecting the best one.

Union field `_max_output_tokens` .

`_max_output_tokens` can be only one of the following:

`maxOutputTokens`

`integer`

Optional. The maximum number of tokens to generate in the response.

A token is approximately four characters. The default value varies by model. This parameter can be used to control the length of the generated text and prevent overly long responses.

Union field `_response_logprobs` .

`_response_logprobs` can be only one of the following:

`responseLogprobs`

`boolean`

Optional. If set to true, the log probabilities of the output tokens are returned.

Log probabilities are the logarithm of the probability of a token appearing in the output. A higher log probability means the token is more likely to be generated. This can be useful for analyzing the model's confidence in its own output and for debugging.

Union field `_logprobs` .

`_logprobs` can be only one of the following:

`logprobs`

`integer`

Optional. The number of top log probabilities to return for each token.

This can be used to see which other tokens were considered likely candidates for a given position. A higher value will return more options, but it will also increase the size of the response.

Union field `_presence_penalty` .

`_presence_penalty` can be only one of the following:

`presencePenalty`

`number`

Optional. Penalizes tokens that have already appeared in the generated text. A positive value encourages the model to generate more diverse and less repetitive text. Valid values can range from \[-2.0, 2.0\].

Union field `_frequency_penalty` .

`_frequency_penalty` can be only one of the following:

`frequencyPenalty`

`number`

Optional. Penalizes tokens based on their frequency in the generated text. A positive value helps to reduce the repetition of words and phrases. Valid values can range from \[-2.0, 2.0\].

Union field `_seed` .

`_seed` can be only one of the following:

`seed`

`integer`

Optional. A seed for the random number generator.

By setting a seed, you can make the model's output mostly deterministic. For a given prompt and parameters (like temperature, top\_p, etc.), the model will produce the same response every time. However, it's not a guaranteed absolute deterministic behavior. This is different from parameters like `temperature` , which control the *level* of randomness. `seed` ensures that the "random" choices the model makes are the same on every run, making it essential for testing and ensuring reproducible results.

Union field `_response_schema` .

`_response_schema` can be only one of the following:

`responseSchema`

` object ( Schema  ` )

Optional. Lets you to specify a schema for the model's response, ensuring that the output conforms to a particular structure. This is useful for generating structured data such as JSON. The schema is a subset of the [OpenAPI 3.0 schema object](https://spec.openapis.org/oas/v3.0.3#schema) object.

When this field is set, you must also set the `response_mime_type` to `application/json` .

Union field `_response_json_schema` .

`_response_json_schema` can be only one of the following:

`responseJsonSchema`

` value ( Value  ` format)

Optional. When this field is set, `response_schema` must be omitted and `response_mime_type` must be set to `application/json` .

Union field `_routing_config` .

`_routing_config` can be only one of the following:

`routingConfig`

` object ( RoutingConfig  ` )

Optional. Routing configuration.

Union field `_audio_timestamp` .

`_audio_timestamp` can be only one of the following:

`audioTimestamp`

`boolean`

Optional. If enabled, audio timestamps will be included in the request to the model. This can be useful for synchronizing audio with other modalities in the response.

Union field `_media_resolution` .

`_media_resolution` can be only one of the following:

`mediaResolution`

`enum ( MediaResolution` )

Optional. The token resolution at which input media content is sampled. This is used to control the trade-off between the quality of the response and the number of tokens used to represent the media. A higher resolution allows the model to perceive more detail, which can lead to a more nuanced response, but it will also use more tokens. This does not affect the image dimensions sent to the model.

Union field `_speech_config` .

`_speech_config` can be only one of the following:

`speechConfig`

` object ( SpeechConfig  ` )

Optional. The speech generation config.

Union field `_enable_affective_dialog` .

`_enable_affective_dialog` can be only one of the following:

`enableAffectiveDialog`

`boolean`

Optional. If enabled, the model will detect emotions and adapt its responses accordingly. For example, if the model detects that the user is frustrated, it may provide a more empathetic response.

Union field `_image_config` .

`_image_config` can be only one of the following:

`imageConfig`

` object ( ImageConfig  ` )

Optional. Config for image generation features.

### RoutingConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field routing_config can be only one of the following:&quot;autoMode&quot;: {object (AutoRoutingMode)},&quot;manualMode&quot;: {object (ManualRoutingMode)}// End of list of possible types for union field routing_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `routing_config` . The routing mode for the request. `routing_config` can be only one of the following:

`autoMode`

` object ( AutoRoutingMode  ` )

In this mode, the model is selected automatically based on the content of the request.

`manualMode`

` object ( ManualRoutingMode  ` )

In this mode, the model is specified manually.

### AutoRoutingMode

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _model_routing_preference can be only one of the following:&quot;modelRoutingPreference&quot;: enum (ModelRoutingPreference)// End of list of possible types for union field _model_routing_preference.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_model_routing_preference` .

`_model_routing_preference` can be only one of the following:

`modelRoutingPreference`

`enum ( ModelRoutingPreference` )

The model routing preference.

### ManualRoutingMode

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _model_name can be only one of the following:&quot;modelName&quot;: string// End of list of possible types for union field _model_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_model_name` .

`_model_name` can be only one of the following:

`modelName`

`string`

The name of the model to use. Only public LLM models are accepted.

### SpeechConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;voiceConfig&quot;: {object (VoiceConfig)},&quot;languageCode&quot;: string,&quot;multiSpeakerVoiceConfig&quot;: {object (MultiSpeakerVoiceConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`voiceConfig`

` object ( VoiceConfig  ` )

The configuration for the voice to use.

`languageCode`

`string`

Optional. The language code (ISO 639-1) for the speech synthesis.

`multiSpeakerVoiceConfig`

` object ( MultiSpeakerVoiceConfig  ` )

The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config` .

### VoiceConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field voice_config can be only one of the following:&quot;prebuiltVoiceConfig&quot;: {object (PrebuiltVoiceConfig)},&quot;replicatedVoiceConfig&quot;: {object (ReplicatedVoiceConfig)}// End of list of possible types for union field voice_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `voice_config` . The configuration for the speaker to use. `voice_config` can be only one of the following:

`prebuiltVoiceConfig`

` object ( PrebuiltVoiceConfig  ` )

The configuration for a prebuilt voice.

`replicatedVoiceConfig`

` object ( ReplicatedVoiceConfig  ` )

Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample.

### PrebuiltVoiceConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _voice_name can be only one of the following:&quot;voiceName&quot;: string// End of list of possible types for union field _voice_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_voice_name` .

`_voice_name` can be only one of the following:

`voiceName`

`string`

The name of the prebuilt voice to use.

### ReplicatedVoiceConfig

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
  &quot;voiceSampleAudio&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mimeType`

`string`

Optional. The mimetype of the voice sample. The only currently supported value is `audio/wav` . This represents 16-bit signed little-endian wav data, with a 24kHz sampling rate. `mime_type` will default to `audio/wav` if not set.

`voiceSampleAudio`

`string ( bytes format)`

Optional. The sample of the custom voice.

A base64-encoded string.

### MultiSpeakerVoiceConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;speakerVoiceConfigs&quot;: [{object (SpeakerVoiceConfig)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`speakerVoiceConfigs[]`

` object ( SpeakerVoiceConfig  ` )

Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided.

### SpeakerVoiceConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;speaker&quot;: string,&quot;voiceConfig&quot;: {object (VoiceConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`speaker`

`string`

Required. The name of the speaker. This should be the same as the speaker name used in the prompt.

`voiceConfig`

` object ( VoiceConfig  ` )

Required. The configuration for the voice of this speaker.

### ThinkingConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _include_thoughts can be only one of the following:&quot;includeThoughts&quot;: boolean// End of list of possible types for union field _include_thoughts.// Union field _thinking_budget can be only one of the following:&quot;thinkingBudget&quot;: integer// End of list of possible types for union field _thinking_budget.// Union field _thinking_level can be only one of the following:&quot;thinkingLevel&quot;: enum (ThinkingLevel)// End of list of possible types for union field _thinking_level.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_include_thoughts` .

`_include_thoughts` can be only one of the following:

`includeThoughts`

`boolean`

Optional. If true, the model will include its thoughts in the response. "Thoughts" are the intermediate steps the model takes to arrive at the final response. They can provide insights into the model's reasoning process and help with debugging. If this is true, thoughts are returned only when available.

Union field `_thinking_budget` .

`_thinking_budget` can be only one of the following:

`thinkingBudget`

`integer`

Optional. The token budget for the model's thinking process. The model will make a best effort to stay within this budget. This can be used to control the trade-off between response quality and latency.

Union field `_thinking_level` .

`_thinking_level` can be only one of the following:

`thinkingLevel`

`enum ( ThinkingLevel` )

Optional. The number of thoughts tokens that the model should generate.

### ModelConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureSelectionPreference&quot;: enum (FeatureSelectionPreference)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`featureSelectionPreference`

`enum ( FeatureSelectionPreference` )

Required. Feature selection preference.

### ImageConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _image_output_options can be only one of the following:&quot;imageOutputOptions&quot;: {object (ImageOutputOptions)}// End of list of possible types for union field _image_output_options.// Union field _aspect_ratio can be only one of the following:&quot;aspectRatio&quot;: string// End of list of possible types for union field _aspect_ratio.// Union field _person_generation can be only one of the following:&quot;personGeneration&quot;: enum (PersonGeneration)// End of list of possible types for union field _person_generation.// Union field _image_size can be only one of the following:&quot;imageSize&quot;: string// End of list of possible types for union field _image_size.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_image_output_options` .

`_image_output_options` can be only one of the following:

`imageOutputOptions`

` object ( ImageOutputOptions  ` )

Optional. The image output format for generated images.

Union field `_aspect_ratio` .

`_aspect_ratio` can be only one of the following:

`aspectRatio`

`string`

Optional. The desired aspect ratio for the generated images. The following aspect ratios are supported:

"1:1" "2:3", "3:2" "3:4", "4:3" "4:5", "5:4" "9:16", "16:9" "21:9"

Union field `_person_generation` .

`_person_generation` can be only one of the following:

`personGeneration`

`enum ( PersonGeneration` )

Optional. Controls whether the model can generate people.

Union field `_image_size` .

`_image_size` can be only one of the following:

`imageSize`

`string`

Optional. Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .

### ImageOutputOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _mime_type can be only one of the following:&quot;mimeType&quot;: string// End of list of possible types for union field _mime_type.// Union field _compression_quality can be only one of the following:&quot;compressionQuality&quot;: integer// End of list of possible types for union field _compression_quality.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_mime_type` .

`_mime_type` can be only one of the following:

`mimeType`

`string`

Optional. The image format that the output should be saved as.

Union field `_compression_quality` .

`_compression_quality` can be only one of the following:

`compressionQuality`

`integer`

Optional. The compression quality of the output image.

## Output Schema

Response message for \[PredictionService.GenerateContent\].

### GenerateContentResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;candidates&quot;: [{object (Candidate)}],&quot;modelVersion&quot;: string,&quot;createTime&quot;: string,&quot;responseId&quot;: string,&quot;promptFeedback&quot;: {object (PromptFeedback)},&quot;usageMetadata&quot;: {object (UsageMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`candidates[]`

` object ( Candidate  ` )

Output only. Generated candidates.

`modelVersion`

`string`

Output only. The model version used to generate the response.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when the request is made to the server.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`responseId`

`string`

Output only. response\_id is used to identify each response. It is the encoding of the event\_id.

`promptFeedback`

` object ( PromptFeedback  ` )

Output only. Content filter results for a prompt sent in the request. Note: Sent only in the first stream chunk. Only happens when no candidates were generated due to content violations.

`usageMetadata`

` object ( UsageMetadata  ` )

Usage metadata about the response(s).

### Candidate

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;index&quot;: integer,&quot;content&quot;: {object (Content)},&quot;avgLogprobs&quot;: number,&quot;logprobsResult&quot;: {object (LogprobsResult)},&quot;finishReason&quot;: enum (FinishReason),&quot;safetyRatings&quot;: [{object (SafetyRating)}],&quot;citationMetadata&quot;: {object (CitationMetadata)},&quot;groundingMetadata&quot;: {object (GroundingMetadata)},&quot;urlContextMetadata&quot;: {object (UrlContextMetadata)},// Union field _finish_message can be only one of the following:&quot;finishMessage&quot;: string// End of list of possible types for union field _finish_message.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`index`

`integer`

Output only. The 0-based index of this candidate in the list of generated responses. This is useful for distinguishing between multiple candidates when `candidate_count` \> 1.

`content`

` object ( Content  ` )

Output only. The content of the candidate.

`avgLogprobs`

`number`

Output only. The average log probability of the tokens in this candidate. This is a length-normalized score that can be used to compare the quality of candidates of different lengths. A higher average log probability suggests a more confident and coherent response.

`logprobsResult`

` object ( LogprobsResult  ` )

Output only. The detailed log probability information for the tokens in this candidate. This is useful for debugging, understanding model uncertainty, and identifying potential "hallucinations".

`finishReason`

`enum ( FinishReason` )

Output only. The reason why the model stopped generating tokens. If empty, the model has not stopped generating.

`safetyRatings[]`

` object ( SafetyRating  ` )

Output only. A list of ratings for the safety of a response candidate.

There is at most one rating per category.

`citationMetadata`

` object ( CitationMetadata  ` )

Output only. A collection of citations that apply to the generated content.

`groundingMetadata`

` object ( GroundingMetadata  ` )

Output only. Metadata returned when grounding is enabled. It contains the sources used to ground the generated content.

`urlContextMetadata`

` object ( UrlContextMetadata  ` )

Output only. Metadata returned when the model uses the `url_context` tool to get information from a user-provided URL.

Union field `_finish_message` .

`_finish_message` can be only one of the following:

`finishMessage`

`string`

Output only. Describes the reason the model stopped generating tokens in more detail. This field is returned only when `finish_reason` is set.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;thought&quot;: boolean,&quot;thoughtSignature&quot;: string,&quot;mediaResolution&quot;: {object (MediaResolution)},// Union field data can be only one of the following:&quot;text&quot;: string,&quot;inlineData&quot;: {object (Blob)},&quot;fileData&quot;: {object (FileData)},&quot;functionCall&quot;: {object (FunctionCall)},&quot;functionResponse&quot;: {object (FunctionResponse)},&quot;executableCode&quot;: {object (ExecutableCode)},&quot;codeExecutionResult&quot;: {object (CodeExecutionResult)}// End of list of possible types for union field data.// Union field metadata can be only one of the following:&quot;videoMetadata&quot;: {object (VideoMetadata)}// End of list of possible types for union field metadata.}</code></pre></td>
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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;language&quot;: enum (Language),&quot;code&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`language`

`enum ( Language` )

Required. Programming language of the `code` .

`code`

`string`

Required. The code to be executed.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outcome&quot;: enum (Outcome),&quot;output&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outcome`

`enum ( Outcome` )

Required. Outcome of the code execution.

`output`

`string`

Optional. Contains stdout when code execution is successful, stderr or other description otherwise.

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

`enum ( Level` )

The tokenization quality used for given media.

### LogprobsResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;topCandidates&quot;: [{object (TopCandidates)}],&quot;chosenCandidates&quot;: [{object (Candidate)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`topCandidates[]`

` object ( TopCandidates  ` )

A list of the top candidate tokens at each decoding step. The length of this list is equal to the total number of decoding steps.

`chosenCandidates[]`

` object ( Candidate  ` )

A list of the chosen candidate tokens at each decoding step. The length of this list is equal to the total number of decoding steps. Note that the chosen candidate might not be in `top_candidates` .

### TopCandidates

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;candidates&quot;: [{object (Candidate)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`candidates[]`

` object ( Candidate  ` )

The list of candidate tokens, sorted by log probability in descending order.

### Candidate

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _token can be only one of the following:&quot;token&quot;: string// End of list of possible types for union field _token.// Union field _token_id can be only one of the following:&quot;tokenId&quot;: integer// End of list of possible types for union field _token_id.// Union field _log_probability can be only one of the following:&quot;logProbability&quot;: number// End of list of possible types for union field _log_probability.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_token` .

`_token` can be only one of the following:

`token`

`string`

The token's string representation.

Union field `_token_id` .

`_token_id` can be only one of the following:

`tokenId`

`integer`

The token's numerical ID. While the `token` field provides the string representation of the token, the `token_id` is the numerical representation that the model uses internally. This can be useful for developers who want to build custom logic based on the model's vocabulary.

Union field `_log_probability` .

`_log_probability` can be only one of the following:

`logProbability`

`number`

The log probability of this token. A higher value indicates that the model was more confident in this token. The log probability can be used to assess the relative likelihood of different tokens and to identify when the model is uncertain.

### SafetyRating

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;category&quot;: enum (HarmCategory),&quot;probability&quot;: enum (HarmProbability),&quot;probabilityScore&quot;: number,&quot;severity&quot;: enum (HarmSeverity),&quot;severityScore&quot;: number,&quot;blocked&quot;: boolean,&quot;overwrittenThreshold&quot;: enum (HarmBlockThreshold)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`category`

`enum ( HarmCategory` )

Output only. The harm category of this rating.

`probability`

`enum ( HarmProbability` )

Output only. The probability of harm for this category.

`probabilityScore`

`number`

Output only. The probability score of harm for this category.

`severity`

`enum ( HarmSeverity` )

Output only. The severity of harm for this category.

`severityScore`

`number`

Output only. The severity score of harm for this category.

`blocked`

`boolean`

Output only. Indicates whether the content was blocked because of this rating.

`overwrittenThreshold`

`enum ( HarmBlockThreshold` )

Output only. The overwritten threshold for the safety category of Gemini 2.0 image out. If minors are detected in the output image, the threshold of each safety category will be overwritten if user sets a lower threshold.

### CitationMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;citations&quot;: [{object (Citation)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`citations[]`

` object ( Citation  ` )

Output only. A list of citations for the content.

### Citation

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;startIndex&quot;: integer,&quot;endIndex&quot;: integer,&quot;uri&quot;: string,&quot;title&quot;: string,&quot;license&quot;: string,&quot;publicationDate&quot;: {object (Date)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`startIndex`

`integer`

Output only. The start index of the citation in the content.

`endIndex`

`integer`

Output only. The end index of the citation in the content.

`uri`

`string`

Output only. The URI of the source of the citation.

`title`

`string`

Output only. The title of the source of the citation.

`license`

`string`

Output only. The license of the source of the citation.

`publicationDate`

` object ( Date  ` )

Output only. The publication date of the source of the citation.

### Date

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
  &quot;year&quot;: integer,
  &quot;month&quot;: integer,
  &quot;day&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`year`

`integer`

Year of the date. Must be from 1 to 9999, or 0 to specify a date without a year.

`month`

`integer`

Month of a year. Must be from 1 to 12, or 0 to specify a year without a month and day.

`day`

`integer`

Day of a month. Must be from 1 to 31 and valid for the year and month, or 0 to specify a year by itself or a year and month where the day isn't significant.

### GroundingMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;webSearchQueries&quot;: [string],&quot;imageSearchQueries&quot;: [string],&quot;retrievalQueries&quot;: [string],&quot;groundingChunks&quot;: [{object (GroundingChunk)}],&quot;groundingSupports&quot;: [{object (GroundingSupport)}],&quot;sourceFlaggingUris&quot;: [{object (SourceFlaggingUri)}],// Union field _search_entry_point can be only one of the following:&quot;searchEntryPoint&quot;: {object (SearchEntryPoint)}// End of list of possible types for union field _search_entry_point.// Union field _retrieval_metadata can be only one of the following:&quot;retrievalMetadata&quot;: {object (RetrievalMetadata)}// End of list of possible types for union field _retrieval_metadata.// Union field _google_maps_widget_context_token can be only one of the// following:&quot;googleMapsWidgetContextToken&quot;: string// End of list of possible types for union field// _google_maps_widget_context_token.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`webSearchQueries[]`

`string`

Optional. The web search queries that were used to generate the content. This field is populated only when the grounding source is Google Search.

`imageSearchQueries[]`

`string`

Optional. The image search queries that were used to generate the content. This field is populated only when the grounding source is Google Search with the Image Search search\_type enabled.

`retrievalQueries[]`

`string`

Optional. The queries that were executed by the retrieval tools. This field is populated only when the grounding source is a retrieval tool, such as Agent Platform Search.

`groundingChunks[]`

` object ( GroundingChunk  ` )

A list of supporting references retrieved from the grounding source. This field is populated when the grounding source is Google Search, Agent Platform Search, or Google Maps.

`groundingSupports[]`

` object ( GroundingSupport  ` )

Optional. A list of grounding supports that connect the generated content to the grounding chunks. This field is populated when the grounding source is Google Search or Agent Platform Search.

`sourceFlaggingUris[]`

` object ( SourceFlaggingUri  ` )

Optional. Output only. A list of URIs that can be used to flag a place or review for inappropriate content. This field is populated only when the grounding source is Google Maps.

Union field `_search_entry_point` .

`_search_entry_point` can be only one of the following:

`searchEntryPoint`

` object ( SearchEntryPoint  ` )

Optional. A web search entry point that can be used to display search results. This field is populated only when the grounding source is Google Search.

Union field `_retrieval_metadata` .

`_retrieval_metadata` can be only one of the following:

`retrievalMetadata`

` object ( RetrievalMetadata  ` )

Optional. Output only. Metadata related to the retrieval grounding source.

Union field `_google_maps_widget_context_token` .

`_google_maps_widget_context_token` can be only one of the following:

`googleMapsWidgetContextToken`

`string`

Optional. Output only. A token that can be used to render a Google Maps widget with the contextual data. This field is populated only when the grounding source is Google Maps.

### SearchEntryPoint

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
  &quot;renderedContent&quot;: string,
  &quot;sdkBlob&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`renderedContent`

`string`

Optional. An HTML snippet that can be embedded in a web page or an application's webview. This snippet displays a search result, including the title, URL, and a brief description of the search result.

`sdkBlob`

`string ( bytes format)`

Optional. A base64-encoded JSON object that contains a list of search queries and their corresponding search URLs. This information can be used to build a custom search UI.

A base64-encoded string.

### GroundingChunk

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field chunk_type can be only one of the following:&quot;web&quot;: {object (Web)},&quot;retrievedContext&quot;: {object (RetrievedContext)},&quot;maps&quot;: {object (Maps)}// End of list of possible types for union field chunk_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `chunk_type` . The source of the grounding chunk, which can be from Google Search, Agent Platform Search, or Google Maps. `chunk_type` can be only one of the following:

`web`

` object ( Web  ` )

A grounding chunk from a web page, typically from Google Search. See the `Web` message for details.

`retrievedContext`

` object ( RetrievedContext  ` )

A grounding chunk from a data source retrieved by a retrieval tool, such as Agent Platform Search. See the `RetrievedContext` message for details

`maps`

` object ( Maps  ` )

A grounding chunk from Google Maps. See the `Maps` message for details.

### Web

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _uri can be only one of the following:&quot;uri&quot;: string// End of list of possible types for union field _uri.// Union field _title can be only one of the following:&quot;title&quot;: string// End of list of possible types for union field _title.// Union field _domain can be only one of the following:&quot;domain&quot;: string// End of list of possible types for union field _domain.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_uri` .

`_uri` can be only one of the following:

`uri`

`string`

The URI of the web page that contains the evidence.

Union field `_title` .

`_title` can be only one of the following:

`title`

`string`

The title of the web page that contains the evidence.

Union field `_domain` .

`_domain` can be only one of the following:

`domain`

`string`

The domain of the web page that contains the evidence. This can be used to filter out low-quality sources.

### RetrievedContext

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field context_details can be only one of the following:&quot;ragChunk&quot;: {object (RagChunk)}// End of list of possible types for union field context_details.// Union field _uri can be only one of the following:&quot;uri&quot;: string// End of list of possible types for union field _uri.// Union field _title can be only one of the following:&quot;title&quot;: string// End of list of possible types for union field _title.// Union field _text can be only one of the following:&quot;text&quot;: string// End of list of possible types for union field _text.// Union field _document_name can be only one of the following:&quot;documentName&quot;: string// End of list of possible types for union field _document_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `context_details` . Provides tool-specific details about the retrieved context. This allows for different types of retrieval tools to return their own specific metadata. `context_details` can be only one of the following:

`ragChunk`

` object ( RagChunk  ` )

Additional context for a Retrieval-Augmented Generation (RAG) retrieval result. This is populated only when the RAG retrieval tool is used.

Union field `_uri` .

`_uri` can be only one of the following:

`uri`

`string`

The URI of the retrieved data source.

Union field `_title` .

`_title` can be only one of the following:

`title`

`string`

The title of the retrieved data source.

Union field `_text` .

`_text` can be only one of the following:

`text`

`string`

The content of the retrieved data source.

Union field `_document_name` .

`_document_name` can be only one of the following:

`documentName`

`string`

Output only. The full resource name of the referenced Agent Platform Search document. This is used to identify the specific document that was retrieved. The format is `projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/branches/{branch}/documents/{document}` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;text&quot;: string,&quot;fileId&quot;: string,&quot;chunkId&quot;: string,// Union field _page_span can be only one of the following:&quot;pageSpan&quot;: {object (PageSpan)}// End of list of possible types for union field _page_span.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`text`

`string`

The content of the chunk.

`fileId`

`string`

The ID of the file that the chunk belongs to.

`chunkId`

`string`

The ID of the chunk.

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

### Maps

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;placeAnswerSources&quot;: {object (PlaceAnswerSources)},// Union field _uri can be only one of the following:&quot;uri&quot;: string// End of list of possible types for union field _uri.// Union field _title can be only one of the following:&quot;title&quot;: string// End of list of possible types for union field _title.// Union field _text can be only one of the following:&quot;text&quot;: string// End of list of possible types for union field _text.// Union field _place_id can be only one of the following:&quot;placeId&quot;: string// End of list of possible types for union field _place_id.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`placeAnswerSources`

` object ( PlaceAnswerSources  ` )

The sources that were used to generate the place answer. This includes review snippets and photos that were used to generate the answer, as well as URIs to flag content.

Union field `_uri` .

`_uri` can be only one of the following:

`uri`

`string`

The URI of the place.

Union field `_title` .

`_title` can be only one of the following:

`title`

`string`

The title of the place.

Union field `_text` .

`_text` can be only one of the following:

`text`

`string`

The text of the place answer.

Union field `_place_id` .

`_place_id` can be only one of the following:

`placeId`

`string`

This Place's resource name, in `places/{place_id}` format. This can be used to look up the place in the Google Maps API.

### PlaceAnswerSources

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;reviewSnippets&quot;: [{object (ReviewSnippet)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`reviewSnippets[]`

` object ( ReviewSnippet  ` )

Snippets of reviews that were used to generate the answer.

### ReviewSnippet

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
  &quot;reviewId&quot;: string,
  &quot;googleMapsUri&quot;: string,
  &quot;title&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`reviewId`

`string`

The ID of the review that is being referenced.

`googleMapsUri`

`string`

A link to show the review on Google Maps.

`title`

`string`

The title of the review.

### GroundingSupport

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;groundingChunkIndices&quot;: [integer],&quot;confidenceScores&quot;: [number],&quot;renderedParts&quot;: [integer],// Union field _segment can be only one of the following:&quot;segment&quot;: {object (Segment)}// End of list of possible types for union field _segment.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`groundingChunkIndices[]`

`integer`

A list of indices into the `grounding_chunks` field of the `GroundingMetadata` message. These indices specify which grounding chunks support the claim made in the content segment.

For example, if this field has the values `[1, 3]` , it means that `grounding_chunks[1]` and `grounding_chunks[3]` are the sources for the claim in the content segment.

`confidenceScores[]`

`number`

The confidence scores for the support references. This list is parallel to the `grounding_chunk_indices` list. A score is a value between 0.0 and 1.0, with a higher score indicating a higher confidence that the reference supports the claim.

For Gemini 2.0 and before, this list has the same size as `grounding_chunk_indices` . For Gemini 2.5 and later, this list is empty and should be ignored.

`renderedParts[]`

`integer`

Indices into the `rendered_parts` field of the `GroundingMetadata` message. These indices specify which rendered parts are associated with this support message.

Union field `_segment` .

`_segment` can be only one of the following:

`segment`

` object ( Segment  ` )

The content segment that this support message applies to.

### Segment

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
  &quot;partIndex&quot;: integer,
  &quot;startIndex&quot;: integer,
  &quot;endIndex&quot;: integer,
  &quot;text&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`partIndex`

`integer`

Output only. The index of the `Part` object that this segment belongs to. This is useful for associating the segment with a specific part of the content.

`startIndex`

`integer`

Output only. The start index of the segment in the `Part` , measured in bytes. This marks the beginning of the segment and is inclusive, meaning the byte at this index is the first byte of the segment.

`endIndex`

`integer`

Output only. The end index of the segment in the `Part` , measured in bytes. This marks the end of the segment and is exclusive, meaning the segment includes content up to, but not including, the byte at this index.

`text`

`string`

Output only. The text of the segment.

### RetrievalMetadata

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
  &quot;googleSearchDynamicRetrievalScore&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`googleSearchDynamicRetrievalScore`

`number`

Optional. A score indicating how likely it is that a Google Search query could help answer the prompt. The score is in the range of `[0, 1]` . A score of 1 means the model is confident that a search will be helpful, and 0 means it is not. This score is populated only when Google Search grounding and dynamic retrieval are enabled. The score is used to determine whether to trigger a search.

### SourceFlaggingUri

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
  &quot;sourceId&quot;: string,
  &quot;flagContentUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`sourceId`

`string`

The ID of the place or review.

`flagContentUri`

`string`

The URI that can be used to flag the content.

### UrlContextMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;urlMetadata&quot;: [{object (UrlMetadata)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`urlMetadata[]`

` object ( UrlMetadata  ` )

Output only. A list of URL metadata, with one entry for each URL retrieved by the tool.

### UrlMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;retrievedUrl&quot;: string,&quot;urlRetrievalStatus&quot;: enum (UrlRetrievalStatus)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`retrievedUrl`

`string`

The URL retrieved by the tool.

`urlRetrievalStatus`

`enum ( UrlRetrievalStatus` )

The status of the URL retrieval.

### Timestamp

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

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`nanos`

`integer`

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### PromptFeedback

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;blockReason&quot;: enum (BlockedReason),&quot;safetyRatings&quot;: [{object (SafetyRating)}],&quot;blockReasonMessage&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`blockReason`

`enum ( BlockedReason` )

Output only. The reason why the prompt was blocked.

`safetyRatings[]`

` object ( SafetyRating  ` )

Output only. A list of safety ratings for the prompt. There is one rating per category.

`blockReasonMessage`

`string`

Output only. A readable message that explains the reason why the prompt was blocked.

### UsageMetadata

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;promptTokenCount&quot;: integer,&quot;candidatesTokenCount&quot;: integer,&quot;totalTokenCount&quot;: integer,&quot;toolUsePromptTokenCount&quot;: integer,&quot;thoughtsTokenCount&quot;: integer,&quot;cachedContentTokenCount&quot;: integer,&quot;promptTokensDetails&quot;: [{object (ModalityTokenCount)}],&quot;cacheTokensDetails&quot;: [{object (ModalityTokenCount)}],&quot;candidatesTokensDetails&quot;: [{object (ModalityTokenCount)}],&quot;toolUsePromptTokensDetails&quot;: [{object (ModalityTokenCount)}],&quot;trafficType&quot;: enum (TrafficType)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`promptTokenCount`

`integer`

The total number of tokens in the prompt. This includes any text, images, or other media provided in the request. When `cached_content` is set, this also includes the number of tokens in the cached content.

`candidatesTokenCount`

`integer`

The total number of tokens in the generated candidates.

`totalTokenCount`

`integer`

The total number of tokens for the entire request. This is the sum of `prompt_token_count` , `candidates_token_count` , `tool_use_prompt_token_count` , and `thoughts_token_count` .

`toolUsePromptTokenCount`

`integer`

Output only. The number of tokens in the results from tool executions, which are provided back to the model as input, if applicable.

`thoughtsTokenCount`

`integer`

Output only. The number of tokens that were part of the model's generated "thoughts" output, if applicable.

`cachedContentTokenCount`

`integer`

Output only. The number of tokens in the cached content that was used for this request.

`promptTokensDetails[]`

` object ( ModalityTokenCount  ` )

Output only. A detailed breakdown of the token count for each modality in the prompt.

`cacheTokensDetails[]`

` object ( ModalityTokenCount  ` )

Output only. A detailed breakdown of the token count for each modality in the cached content.

`candidatesTokensDetails[]`

` object ( ModalityTokenCount  ` )

Output only. A detailed breakdown of the token count for each modality in the generated candidates.

`toolUsePromptTokensDetails[]`

` object ( ModalityTokenCount  ` )

Output only. A detailed breakdown by modality of the token counts from the results of tool executions, which are provided back to the model as input.

`trafficType`

`enum ( TrafficType` )

Output only. The traffic type for this request.

### ModalityTokenCount

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modality&quot;: enum (Modality),&quot;tokenCount&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`modality`

`enum ( Modality` )

The modality that this token count applies to.

`tokenCount`

`integer`

The number of tokens counted for this modality.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ✅
