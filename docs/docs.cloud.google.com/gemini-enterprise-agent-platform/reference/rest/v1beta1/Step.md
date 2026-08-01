---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step
title: Step
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A step in the interaction.

Fields

`type` `Union type`

`type` can be only one of the following:

`thought` ` object ( ThoughtStep  ` )

`toolCall` ` object ( ToolCallStep  ` )

`toolResult` ` object ( ToolResultStep  ` )

`userInput` ` object ( UserInputStep  ` )

DO NOT USE -- These are for 3P JSON only

`modelOutput` ` object ( ModelOutputStep  ` )

` text (deprecated)  ` `object ( LegacyTextContent` )

> This item is deprecated\!

` image (deprecated)  ` `object ( LegacyImageContent` )

> This item is deprecated\!

` audio (deprecated)  ` `object ( LegacyAudioContent` )

> This item is deprecated\!

` document (deprecated)  ` `object ( LegacyDocumentContent` )

> This item is deprecated\!

` video (deprecated)  ` `object ( LegacyVideoContent` )

> This item is deprecated\!

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// type&quot;thought&quot;: {object (ThoughtStep)},&quot;toolCall&quot;: {object (ToolCallStep)},&quot;toolResult&quot;: {object (ToolResultStep)},&quot;userInput&quot;: {object (UserInputStep)},&quot;modelOutput&quot;: {object (ModelOutputStep)},&quot;text&quot;: {object (LegacyTextContent)},&quot;image&quot;: {object (LegacyImageContent)},&quot;audio&quot;: {object (LegacyAudioContent)},&quot;document&quot;: {object (LegacyDocumentContent)},&quot;video&quot;: {object (LegacyVideoContent)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ThoughtStep

A thought step.

Fields

`signature` `string ( bytes format)`

A signature hash for backend validation.

A base64-encoded string.

`summary[]` ` object ( Content  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;signature&quot;: string,&quot;summary&quot;: [{object (Content)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ToolCallStep

Tool call step.

Fields

`id` `string`

Required. A unique id for this specific tool call.

`signature` `string ( bytes format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

`type` can be only one of the following:

`functionCall` ` object ( FunctionCallStep  ` )

`codeExecutionCall` ` object ( CodeExecutionCallStep  ` )

`urlContextCall` ` object ( UrlContextCallStep  ` )

`mcpServerToolCall` ` object ( McpServerToolCallStep  ` )

`googleSearchCall` ` object ( GoogleSearchCallStep  ` )

`fileSearchCall` ` object ( FileSearchCallStep  ` )

`googleMapsCall` ` object ( GoogleMapsCallStep  ` )

`retrievalCall` ` object ( RetrievalCallStep  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;signature&quot;: string,// type&quot;functionCall&quot;: {object (FunctionCallStep)},&quot;codeExecutionCall&quot;: {object (CodeExecutionCallStep)},&quot;urlContextCall&quot;: {object (UrlContextCallStep)},&quot;mcpServerToolCall&quot;: {object (McpServerToolCallStep)},&quot;googleSearchCall&quot;: {object (GoogleSearchCallStep)},&quot;fileSearchCall&quot;: {object (FileSearchCallStep)},&quot;googleMapsCall&quot;: {object (GoogleMapsCallStep)},&quot;retrievalCall&quot;: {object (RetrievalCallStep)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FunctionCallStep

A function tool call step.

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

## CodeExecutionCallStep

code execution call step.

Fields

`arguments` ` object ( CodeExecutionCallStepArguments  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arguments&quot;: {object (CodeExecutionCallStepArguments)}}</code></pre></td>
</tr>
</tbody>
</table>

## CodeExecutionCallStepArguments

The arguments to pass to the code execution.

Fields

`language` ` enum ( Language  ` )

Programming language of the `code` .

`code` `string`

The code to be executed.

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

## Language

Supported programming languages for the generated code.

Enums

`LANGUAGE_UNSPECIFIED`

Unspecified language. This value should not be used.

`PYTHON`

Python \>= 3.10, with numpy and simpy available.

## UrlContextCallStep

URL context call step.

Fields

`arguments` ` object ( UrlContextCallStepArguments  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arguments&quot;: {object (UrlContextCallStepArguments)}}</code></pre></td>
</tr>
</tbody>
</table>

## UrlContextCallStepArguments

The arguments to pass to the URL context.

Fields

`urls[]` `string`

The URLs to fetch.

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
  &quot;urls&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## McpServerToolCallStep

MCPServer tool call step.

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

## GoogleSearchCallStep

Google Search call step.

Fields

`arguments` ` object ( GoogleSearchCallStepArguments  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arguments&quot;: {object (GoogleSearchCallStepArguments)},&quot;searchType&quot;: enum (SearchType)}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleSearchCallStepArguments

The arguments to pass to Google Search.

Fields

`queries[]` `string`

Web search queries for the following-up web search.

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
  &quot;queries&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## FileSearchCallStep

This type has no fields.

File Search call step.

## GoogleMapsCallStep

Google Maps call step.

Fields

`arguments` ` object ( GoogleMapsCallStepArguments  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arguments&quot;: {object (GoogleMapsCallStepArguments)}}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleMapsCallStepArguments

The arguments to pass to the Google Maps tool.

Fields

`queries[]` `string`

The queries to be executed.

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
  &quot;queries&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## RetrievalCallStep

Retrieval call step. Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc. RetrievalType decides which tool is used.

Fields

`arguments` ` object ( RetrievalStepArguments  ` )

Required. The arguments to pass to the retrieval tool.

`retrievalType` ` enum ( RetrievalType  ` )

The type of retrieval tools.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arguments&quot;: {object (RetrievalStepArguments)},&quot;retrievalType&quot;: enum (RetrievalType)}</code></pre></td>
</tr>
</tbody>
</table>

## ToolResultStep

Tool result step.

Fields

`callId` `string`

Required. id to match the id from the function call block.

`signature` `string ( bytes format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

`type` can be only one of the following:

`functionResult` ` object ( FunctionResultStep  ` )

`codeExecutionResult` ` object ( CodeExecutionResultStep  ` )

`urlContextResult` ` object ( UrlContextResultStep  ` )

`googleSearchResult` ` object ( GoogleSearchResultStep  ` )

`mcpServerToolResult` ` object ( McpServerToolResultStep  ` )

`fileSearchResult` ` object ( FileSearchResultStep  ` )

`googleMapsResult` ` object ( GoogleMapsResultStep  ` )

`retrievalResult` ` object ( RetrievalResultStep  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;callId&quot;: string,&quot;signature&quot;: string,// type&quot;functionResult&quot;: {object (FunctionResultStep)},&quot;codeExecutionResult&quot;: {object (CodeExecutionResultStep)},&quot;urlContextResult&quot;: {object (UrlContextResultStep)},&quot;googleSearchResult&quot;: {object (GoogleSearchResultStep)},&quot;mcpServerToolResult&quot;: {object (McpServerToolResultStep)},&quot;fileSearchResult&quot;: {object (FileSearchResultStep)},&quot;googleMapsResult&quot;: {object (GoogleMapsResultStep)},&quot;retrievalResult&quot;: {object (RetrievalResultStep)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FunctionResultStep

result of a function tool call.

Fields

`name` `string`

The name of the tool that was called.

`isError` `boolean`

Whether the tool call resulted in an error.

`result` ` object ( Value  ` )

Required. The result of the tool call.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;isError&quot;: boolean,&quot;result&quot;: {object (Value)}}</code></pre></td>
</tr>
</tbody>
</table>

## CodeExecutionResultStep

code execution result step.

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

## UrlContextResultStep

URL context result step.

Fields

`result[]` ` object ( UrlContextResultItem  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;result&quot;: [{object (UrlContextResultItem)}],&quot;isError&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## UrlContextResultItem

The result of the URL context.

Fields

`url` `string`

The URL that was fetched.

`status` ` enum ( Status  ` )

The status of the URL retrieval.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;url&quot;: string,&quot;status&quot;: enum (Status)}</code></pre></td>
</tr>
</tbody>
</table>

## Status

The status of the URL retrieval.

Enums

`STATUS_UNSPECIFIED`

`SUCCESS`

`ERROR`

`PAYWALL`

`UNSAFE`

## GoogleSearchResultStep

Google Search result step.

Fields

`result[]` ` object ( GoogleSearchResultItem  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;result&quot;: [{object (GoogleSearchResultItem)}],&quot;isError&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleSearchResultItem

The result of the Google Search.

Fields

`searchSuggestions` `string`

Web content snippet that can be embedded in a web page or an app webview.

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
  &quot;searchSuggestions&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## McpServerToolResultStep

MCPServer tool result step.

Fields

`name` `string`

name of the tool which is called for this specific tool call.

`serverName` `string`

The name of the used MCP server.

`result` ` object ( Value  ` )

Required. The output from the MCP server call. Can be simple text or rich content.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;serverName&quot;: string,&quot;result&quot;: {object (Value)}}</code></pre></td>
</tr>
</tbody>
</table>

## FileSearchResultStep

This type has no fields.

File Search result step.

## GoogleMapsResultStep

Google Maps result step.

Fields

`result[]` ` object ( GoogleMapsResultItem  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;result&quot;: [{object (GoogleMapsResultItem)}]}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleMapsResultItem

The result of the Google Maps.

Fields

`places[]` ` object ( GoogleMapsResultPlaces  ` )

`widgetContextToken` `string`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;places&quot;: [{object (GoogleMapsResultPlaces)}],&quot;widgetContextToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleMapsResultPlaces

Fields

`placeId` `string`

`name` `string`

`url` `string`

`reviewSnippets[]` ` object ( ReviewSnippet  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;placeId&quot;: string,&quot;name&quot;: string,&quot;url&quot;: string,&quot;reviewSnippets&quot;: [{object (ReviewSnippet)}]}</code></pre></td>
</tr>
</tbody>
</table>

## RetrievalResultStep

Vertex Retrieval result step. Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc.

Fields

`isError` `boolean`

Whether the retrieval resulted in an error.

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
  &quot;isError&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## UserInputStep

Input provided by the user.

Fields

`content` `Union type`

`content` can be only one of the following:

`contentList` ` object ( ContentList  ` )

The content of the step. An array of Content objects.

`contentString` `string`

The content of the step. A single string.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// content&quot;contentList&quot;: {object (ContentList)},&quot;contentString&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ModelOutputStep

Output generated by the model.

Fields

`content[]` ` object ( Content  ` )

`error` ` object ( Status  ` )

The error result of the operation in case of failure or cancellation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;content&quot;: [{object (Content)}],&quot;error&quot;: {object (Status)}}</code></pre></td>
</tr>
</tbody>
</table>
