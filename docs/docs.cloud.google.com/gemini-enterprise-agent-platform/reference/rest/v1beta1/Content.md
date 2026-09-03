---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content
title: Content
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The content of the response.

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` ` object ( TextContent  ` )

`image` ` object ( ImageContent  ` )

`audio` ` object ( AudioContent  ` )

`document` ` object ( DocumentContent  ` )

`video` ` object ( VideoContent  ` )

` thought (deprecated)  ` ` object ( ThoughtContent  ` )

> This item is deprecated\!

` toolCall (deprecated)  ` ` object ( ToolCallContent  ` )

> This item is deprecated\!

` toolResult (deprecated)  ` ` object ( ToolResultContent  ` )

> This item is deprecated\!

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// type&quot;text&quot;: {object (TextContent)},&quot;image&quot;: {object (ImageContent)},&quot;audio&quot;: {object (AudioContent)},&quot;document&quot;: {object (DocumentContent)},&quot;video&quot;: {object (VideoContent)},&quot;thought&quot;: {object (ThoughtContent)},&quot;toolCall&quot;: {object (ToolCallContent)},&quot;toolResult&quot;: {object (ToolResultContent)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TextContent

A text content block.

Fields

`text` `string`

Required. The text content.

`annotations[]` ` object ( Annotation  ` )

Citation information for model-generated content.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;text&quot;: string,&quot;annotations&quot;: [{object (Annotation)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ImageContent

An image content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the image, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`resolution` ` enum ( MediaResolution  ` )

The resolution of the media.

`data_or_uri` `Union type`

The image content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( bytes format)`

The image content.

A base64-encoded string.

`uri` `string`

The URI of the image.

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeTypeString&quot;: string,&quot;resolution&quot;: enum (MediaResolution),// data_or_uri&quot;data&quot;: string,&quot;uri&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## AudioContent

An audio content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the audio, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`channels` `integer`

The number of audio channels.

`sampleRate` `integer`

The sample rate of the audio.

`data_or_uri` `Union type`

The audio content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( bytes format)`

The audio content.

A base64-encoded string.

`uri` `string`

The URI of the audio.

End of mutually exclusive fields.

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
  &quot;mimeTypeString&quot;: string,
  &quot;channels&quot;: integer,
  &quot;sampleRate&quot;: integer,

  // data_or_uri
  &quot;data&quot;: string,
  &quot;uri&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## DocumentContent

A document content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the document, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`data_or_uri` `Union type`

The document content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( bytes format)`

The document content.

A base64-encoded string.

`uri` `string`

The URI of the document.

End of mutually exclusive fields.

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
  &quot;mimeTypeString&quot;: string,

  // data_or_uri
  &quot;data&quot;: string,
  &quot;uri&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## VideoContent

A video content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the video, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`resolution` ` enum ( MediaResolution  ` )

The resolution of the media.

`name` `string`

A user-defined name for this content block. Can be referenced by the model in the final response.

`data_or_uri` `Union type`

The video content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( bytes format)`

The video content.

A base64-encoded string.

`uri` `string`

The URI of the video.

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeTypeString&quot;: string,&quot;resolution&quot;: enum (MediaResolution),&quot;name&quot;: string,// data_or_uri&quot;data&quot;: string,&quot;uri&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ThoughtContent

> This item is deprecated\!

A thought content block.

Fields

`signature` `string ( bytes format)`

signature to match the backend source to be part of the generation.

A base64-encoded string.

`summary[]` ` object ( ThoughtSummaryContent  ` )

A summary of the thought.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;signature&quot;: string,&quot;summary&quot;: [{object (ThoughtSummaryContent)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ThoughtSummaryContent

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` ` object ( TextContent  ` )

`image` ` object ( ImageContent  ` )

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// type&quot;text&quot;: {object (TextContent)},&quot;image&quot;: {object (ImageContent)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ToolCallContent

> This item is deprecated\!

Tool call content.

Fields

`id` `string`

Required. A unique id for this specific tool call.

`signature` `string ( bytes format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`functionCall` ` object ( FunctionCallContent  ` )

`codeExecutionCall` ` object ( CodeExecutionCallContent  ` )

`urlContextCall` ` object ( UrlContextCallContent  ` )

`mcpServerToolCall` ` object ( McpServerToolCallContent  ` )

`googleSearchCall` ` object ( GoogleSearchCallContent  ` )

`fileSearchCall` ` object ( FileSearchCallContent  ` )

`googleMapsCall` ` object ( GoogleMapsCallContent  ` )

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;signature&quot;: string,// type&quot;functionCall&quot;: {object (FunctionCallContent)},&quot;codeExecutionCall&quot;: {object (CodeExecutionCallContent)},&quot;urlContextCall&quot;: {object (UrlContextCallContent)},&quot;mcpServerToolCall&quot;: {object (McpServerToolCallContent)},&quot;googleSearchCall&quot;: {object (GoogleSearchCallContent)},&quot;fileSearchCall&quot;: {object (FileSearchCallContent)},&quot;googleMapsCall&quot;: {object (GoogleMapsCallContent)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FunctionCallContent

> This item is deprecated\!

A function tool call content block.

Fields

`name` `string`

Required. The name of the tool to call.

`arguments` ` object ( Struct  ` )

Required. The arguments to pass to the function.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;arguments&quot;: {object (Struct)}}</code></pre></td>
</tr>
</tbody>
</table>

## CodeExecutionCallContent

> This item is deprecated\!

code execution content.

Fields

`arguments` ` object ( CodeExecutionCallArguments  ` )

Required. The arguments to pass to the code execution.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arguments&quot;: {object (CodeExecutionCallArguments)}}</code></pre></td>
</tr>
</tbody>
</table>

## UrlContextCallContent

> This item is deprecated\!

URL context content.

Fields

`arguments` ` object ( UrlContextCallArguments  ` )

Required. The arguments to pass to the URL context.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arguments&quot;: {object (UrlContextCallArguments)}}</code></pre></td>
</tr>
</tbody>
</table>

## McpServerToolCallContent

MCPServer tool call content.

Fields

`name` `string`

Required. The name of the tool which was called.

`serverName` `string`

Required. The name of the used MCP server.

`arguments` ` object ( Struct  ` )

Required. The JSON object of arguments for the function.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;serverName&quot;: string,&quot;arguments&quot;: {object (Struct)}}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleSearchCallContent

> This item is deprecated\!

Google Search content.

Fields

`arguments` ` object ( GoogleSearchCallArguments  ` )

Required. The arguments to pass to Google Search.

`searchType` ` enum ( SearchType  ` )

The type of search grounding enabled.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arguments&quot;: {object (GoogleSearchCallArguments)},&quot;searchType&quot;: enum (SearchType)}</code></pre></td>
</tr>
</tbody>
</table>

## FileSearchCallContent

This type has no fields.

> This item is deprecated\!

File Search content.

## GoogleMapsCallContent

> This item is deprecated\!

Google Maps content.

Fields

`arguments` ` object ( GoogleMapsCallArguments  ` )

The arguments to pass to the Google Maps tool.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arguments&quot;: {object (GoogleMapsCallArguments)}}</code></pre></td>
</tr>
</tbody>
</table>

## ToolResultContent

> This item is deprecated\!

Tool result content.

Fields

`callId` `string`

Required. id to match the id from the function call block.

`signature` `string ( bytes format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`functionResult` ` object ( FunctionResultContent  ` )

`codeExecutionResult` ` object ( CodeExecutionResultContent  ` )

`urlContextResult` ` object ( UrlContextResultContent  ` )

`googleSearchResult` ` object ( GoogleSearchResultContent  ` )

`mcpServerToolResult` ` object ( McpServerToolResultContent  ` )

`fileSearchResult` ` object ( FileSearchResultContent  ` )

`googleMapsResult` ` object ( GoogleMapsResultContent  ` )

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;callId&quot;: string,&quot;signature&quot;: string,// type&quot;functionResult&quot;: {object (FunctionResultContent)},&quot;codeExecutionResult&quot;: {object (CodeExecutionResultContent)},&quot;urlContextResult&quot;: {object (UrlContextResultContent)},&quot;googleSearchResult&quot;: {object (GoogleSearchResultContent)},&quot;mcpServerToolResult&quot;: {object (McpServerToolResultContent)},&quot;fileSearchResult&quot;: {object (FileSearchResultContent)},&quot;googleMapsResult&quot;: {object (GoogleMapsResultContent)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FunctionResultContent

> This item is deprecated\!

A function tool result content block.

Fields

`name` `string`

The name of the tool that was called.

`isError` `boolean`

Whether the tool call resulted in an error.

`result` `Union type`

The result of the tool call. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`structResult` ` object ( Struct  ` )

`contentList` ` object ( FunctionResultSubcontentList  ` )

`stringResult` `string`

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;isError&quot;: boolean,// result&quot;structResult&quot;: {object (Struct)},&quot;contentList&quot;: {object (FunctionResultSubcontentList)},&quot;stringResult&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FunctionResultSubcontentList

Fields

`contents[]` ` object ( FunctionResultSubcontent  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contents&quot;: [{object (FunctionResultSubcontent)}]}</code></pre></td>
</tr>
</tbody>
</table>

## FunctionResultSubcontent

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` ` object ( TextContent  ` )

`image` ` object ( ImageContent  ` )

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// type&quot;text&quot;: {object (TextContent)},&quot;image&quot;: {object (ImageContent)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## CodeExecutionResultContent

> This item is deprecated\!

code execution result content.

Fields

`result` `string`

Required. The output of the code execution.

`isError` `boolean`

Whether the code execution resulted in an error.

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
  &quot;result&quot;: string,
  &quot;isError&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## UrlContextResultContent

> This item is deprecated\!

URL context result content.

Fields

`result[]` ` object ( UrlContextResult  ` )

Required. The results of the URL context.

`isError` `boolean`

Whether the URL context resulted in an error.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;result&quot;: [{object (UrlContextResult)}],&quot;isError&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleSearchResultContent

> This item is deprecated\!

Google Search result content.

Fields

`result[]` ` object ( GoogleSearchResult  ` )

Required. The results of the Google Search.

`isError` `boolean`

Whether the Google Search resulted in an error.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;result&quot;: [{object (GoogleSearchResult)}],&quot;isError&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## McpServerToolResultContent

MCPServer tool result content.

Fields

`name` `string`

name of the tool which is called for this specific tool call.

`serverName` `string`

The name of the used MCP server.

`result` `Union type`

The output from the MCP server call. Can be simple text or rich content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`structResult` ` object ( Struct  ` )

`contentList` ` object ( FunctionResultSubcontentList  ` )

`stringResult` `string`

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;serverName&quot;: string,// result&quot;structResult&quot;: {object (Struct)},&quot;contentList&quot;: {object (FunctionResultSubcontentList)},&quot;stringResult&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FileSearchResultContent

> This item is deprecated\!

File Search result content.

Fields

`result[]` ` object ( FileSearchResult  ` )

The results of the File Search.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;result&quot;: [{object (FileSearchResult)}]}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleMapsResultContent

> This item is deprecated\!

Google Maps result content.

Fields

`result[]` ` object ( GoogleMapsResult  ` )

Required. The results of the Google Maps.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;result&quot;: [{object (GoogleMapsResult)}]}</code></pre></td>
</tr>
</tbody>
</table>
