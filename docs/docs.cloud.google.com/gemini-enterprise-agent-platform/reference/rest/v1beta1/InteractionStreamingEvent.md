---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent
title: InteractionStreamingEvent
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`eventId` `string`

The eventId token to be used to resume the interaction stream, from this event.

`metadata` ` object ( StreamMetadata  ` )

Optional metadata accompanying ANY streamed event.

`event_type` `Union type`

The event data. `event_type` can be only one of the following:

` interactionStartEvent (deprecated)  ` ` object ( InteractionStartEvent  ` )

> This item is deprecated\!

The interaction data, used for interaction.start events. Legacy event, used when steps are disabled.

` interactionCompleteEvent (deprecated)  ` ` object ( InteractionCompleteEvent  ` )

> This item is deprecated\!

The interaction data, used for interaction.complete events. Legacy event, used when steps are disabled.

`interactionCreatedEvent` ` object ( InteractionCreatedSseEvent  ` )

The interaction data, used for interaction.created events. Used when steps are enabled.

`interactionCompletedEvent` ` object ( InteractionCompletedSseEvent  ` )

The interaction data, used for interaction.completed events. Used when steps are enabled.

`interactionStatusUpdate` ` object ( InteractionStatusUpdate  ` )

The interaction status data, used for interaction.status\_update events.

`contentStart` ` object ( ContentStart  ` )

The content block start data, used for content.start events. Legacy content-based streaming event, used when steps are disabled.

`contentDelta` ` object ( ContentDelta  ` )

The content block delta data, used for content.delta events. Legacy content-based streaming event, used when steps are disabled.

`contentStop` ` object ( ContentStop  ` )

The content block stop data, used for content.stop events. Legacy content-based streaming event, used when steps are disabled.

`errorEvent` ` object ( ErrorEvent  ` )

The error event data, used for error events.

`stepStart` ` object ( StepStart  ` )

The step start data, used for step.start events. Step-based streaming event, used when steps are enabled.

`stepDelta` ` object ( StepDelta  ` )

The step delta data, used for step.delta events. Step-based streaming event, used when steps are enabled.

`stepStop` ` object ( StepStop  ` )

The step stop data, used for step.stop events. Step-based streaming event, used when steps are enabled.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;eventId&quot;: string,&quot;metadata&quot;: {object (StreamMetadata)},// event_type&quot;interactionStartEvent&quot;: {object (InteractionStartEvent)},&quot;interactionCompleteEvent&quot;: {object (InteractionCompleteEvent)},&quot;interactionCreatedEvent&quot;: {object (InteractionCreatedSseEvent)},&quot;interactionCompletedEvent&quot;: {object (InteractionCompletedSseEvent)},&quot;interactionStatusUpdate&quot;: {object (InteractionStatusUpdate)},&quot;contentStart&quot;: {object (ContentStart)},&quot;contentDelta&quot;: {object (ContentDelta)},&quot;contentStop&quot;: {object (ContentStop)},&quot;errorEvent&quot;: {object (ErrorEvent)},&quot;stepStart&quot;: {object (StepStart)},&quot;stepDelta&quot;: {object (StepDelta)},&quot;stepStop&quot;: {object (StepStop)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## InteractionStartEvent

> This item is deprecated\!

Fields

`interaction` ` object ( Interaction  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;interaction&quot;: {object (Interaction)}}</code></pre></td>
</tr>
</tbody>
</table>

## InteractionCompleteEvent

> This item is deprecated\!

Fields

`interaction` ` object ( Interaction  ` )

Required. The completed interaction with empty outputs to reduce the payload size. Use the preceding ContentDelta events for the actual output.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;interaction&quot;: {object (Interaction)}}</code></pre></td>
</tr>
</tbody>
</table>

## InteractionCreatedSseEvent

Fields

`interaction` ` object ( Interaction  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;interaction&quot;: {object (Interaction)}}</code></pre></td>
</tr>
</tbody>
</table>

## InteractionCompletedSseEvent

Fields

`interaction` ` object ( Interaction  ` )

Required. The completed interaction with empty outputs to reduce the payload size. Use the preceding ContentDelta events for the actual output.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;interaction&quot;: {object (Interaction)}}</code></pre></td>
</tr>
</tbody>
</table>

## InteractionStatusUpdate

Fields

`interactionId` `string`

`status` ` enum ( Status  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;interactionId&quot;: string,&quot;status&quot;: enum (Status)}</code></pre></td>
</tr>
</tbody>
</table>

## ContentStart

Fields

`index` `integer`

`content` ` object ( Content  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;index&quot;: integer,&quot;content&quot;: {object (Content)}}</code></pre></td>
</tr>
</tbody>
</table>

## ContentDelta

Fields

`index` `integer`

`delta` ` object ( ContentDeltaData  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;index&quot;: integer,&quot;delta&quot;: {object (ContentDeltaData)}}</code></pre></td>
</tr>
</tbody>
</table>

## ContentDeltaData

The delta content data for a content block.

Fields

`type` `Union type`

The type of the delta content. `type` can be only one of the following:

`text` ` object ( TextDelta  ` )

`image` ` object ( ImageDelta  ` )

`audio` ` object ( AudioDelta  ` )

`document` ` object ( DocumentDelta  ` )

`video` ` object ( VideoDelta  ` )

`thoughtSummary` ` object ( ThoughtSummaryDelta  ` )

`thoughtSignature` ` object ( ThoughtSignatureDelta  ` )

`toolCall` ` object ( ToolCallDelta  ` )

`toolResult` ` object ( ToolResultDelta  ` )

`textAnnotation` ` object ( TextAnnotationDelta  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// type&quot;text&quot;: {object (TextDelta)},&quot;image&quot;: {object (ImageDelta)},&quot;audio&quot;: {object (AudioDelta)},&quot;document&quot;: {object (DocumentDelta)},&quot;video&quot;: {object (VideoDelta)},&quot;thoughtSummary&quot;: {object (ThoughtSummaryDelta)},&quot;thoughtSignature&quot;: {object (ThoughtSignatureDelta)},&quot;toolCall&quot;: {object (ToolCallDelta)},&quot;toolResult&quot;: {object (ToolResultDelta)},&quot;textAnnotation&quot;: {object (TextAnnotationDelta)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TextDelta

Fields

`text` `string`

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
  &quot;text&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ImageDelta

Fields

`mimeType` `enum ( MimeType` )

`resolution` ` enum ( MediaResolution  ` )

The resolution of the media.

`data_or_uri` `Union type`

`data_or_uri` can be only one of the following:

`data` `string ( bytes format)`

A base64-encoded string.

`uri` `string`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeType&quot;: enum (MimeType),&quot;resolution&quot;: enum (MediaResolution),// data_or_uri&quot;data&quot;: string,&quot;uri&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## AudioDelta

Fields

`mimeType` ` enum ( MimeType  ` )

` rate (deprecated)  ` `integer`

> This item is deprecated\!

Deprecated. Use sampleRate instead. The value is ignored.

`sampleRate` `integer`

The sample rate of the audio.

`channels` `integer`

The number of audio channels.

`data_or_uri` `Union type`

`data_or_uri` can be only one of the following:

`data` `string ( bytes format)`

A base64-encoded string.

`uri` `string`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeType&quot;: enum (MimeType),&quot;rate&quot;: integer,&quot;sampleRate&quot;: integer,&quot;channels&quot;: integer,// data_or_uri&quot;data&quot;: string,&quot;uri&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## DocumentDelta

Fields

`mimeType` `enum ( MimeType` )

`data_or_uri` `Union type`

`data_or_uri` can be only one of the following:

`data` `string ( bytes format)`

A base64-encoded string.

`uri` `string`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeType&quot;: enum (MimeType),// data_or_uri&quot;data&quot;: string,&quot;uri&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## VideoDelta

Fields

`mimeType` `enum ( MimeType` )

`resolution` ` enum ( MediaResolution  ` )

The resolution of the media.

`data_or_uri` `Union type`

`data_or_uri` can be only one of the following:

`data` `string ( bytes format)`

A base64-encoded string.

`uri` `string`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeType&quot;: enum (MimeType),&quot;resolution&quot;: enum (MediaResolution),// data_or_uri&quot;data&quot;: string,&quot;uri&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ThoughtSummaryDelta

Fields

`content` ` object ( Content  ` )

A new summary item to be added to the thought.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;content&quot;: {object (Content)}}</code></pre></td>
</tr>
</tbody>
</table>

## ThoughtSignatureDelta

Fields

`signature` `string ( bytes format)`

signature to match the backend source to be part of the generation.

A base64-encoded string.

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
  &quot;signature&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ToolCallDelta

Fields

`id` `string`

Required. A unique id for this specific tool call.

`signature` `string ( bytes format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

`type` can be only one of the following:

`functionCall` ` object ( FunctionCallDelta  ` )

`codeExecutionCall` ` object ( CodeExecutionCallDelta  ` )

`urlContextCall` ` object ( UrlContextCallDelta  ` )

`googleSearchCall` ` object ( GoogleSearchCallDelta  ` )

`mcpServerToolCall` ` object ( McpServerToolCallDelta  ` )

`fileSearchCall` ` object ( FileSearchCallDelta  ` )

`googleMapsCall` ` object ( GoogleMapsCallDelta  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;signature&quot;: string,// type&quot;functionCall&quot;: {object (FunctionCallDelta)},&quot;codeExecutionCall&quot;: {object (CodeExecutionCallDelta)},&quot;urlContextCall&quot;: {object (UrlContextCallDelta)},&quot;googleSearchCall&quot;: {object (GoogleSearchCallDelta)},&quot;mcpServerToolCall&quot;: {object (McpServerToolCallDelta)},&quot;fileSearchCall&quot;: {object (FileSearchCallDelta)},&quot;googleMapsCall&quot;: {object (GoogleMapsCallDelta)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FunctionCallDelta

Fields

`name` `string`

`arguments` ` object ( Struct  ` )

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

## CodeExecutionCallDelta

Fields

`arguments` ` object ( CodeExecutionCallArguments  ` )

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

## UrlContextCallDelta

Fields

`arguments` ` object ( UrlContextCallArguments  ` )

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

## GoogleSearchCallDelta

Fields

`arguments` ` object ( GoogleSearchCallArguments  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arguments&quot;: {object (GoogleSearchCallArguments)}}</code></pre></td>
</tr>
</tbody>
</table>

## McpServerToolCallDelta

Fields

`name` `string`

`serverName` `string`

`arguments` ` object ( Struct  ` )

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

## FileSearchCallDelta

This type has no fields.

## GoogleMapsCallDelta

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

## ToolResultDelta

Fields

`callId` `string`

Required. id to match the id from the function call block.

`signature` `string ( bytes format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

`type` can be only one of the following:

`functionResult` ` object ( FunctionResultDelta  ` )

`codeExecutionResult` ` object ( CodeExecutionResultDelta  ` )

`urlContextResult` ` object ( UrlContextResultDelta  ` )

`googleSearchResult` ` object ( GoogleSearchResultDelta  ` )

`mcpServerToolResult` ` object ( McpServerToolResultDelta  ` )

`fileSearchResult` ` object ( FileSearchResultDelta  ` )

`googleMapsResult` ` object ( GoogleMapsResultDelta  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;callId&quot;: string,&quot;signature&quot;: string,// type&quot;functionResult&quot;: {object (FunctionResultDelta)},&quot;codeExecutionResult&quot;: {object (CodeExecutionResultDelta)},&quot;urlContextResult&quot;: {object (UrlContextResultDelta)},&quot;googleSearchResult&quot;: {object (GoogleSearchResultDelta)},&quot;mcpServerToolResult&quot;: {object (McpServerToolResultDelta)},&quot;fileSearchResult&quot;: {object (FileSearchResultDelta)},&quot;googleMapsResult&quot;: {object (GoogleMapsResultDelta)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FunctionResultDelta

Fields

`name` `string`

`isError` `boolean`

`result` ` object ( Value  ` )

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

## CodeExecutionResultDelta

Fields

`result` `string`

`isError` `boolean`

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

## UrlContextResultDelta

Fields

`result[]` ` object ( UrlContextResult  ` )

`isError` `boolean`

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

## GoogleSearchResultDelta

Fields

`result[]` ` object ( GoogleSearchResult  ` )

`isError` `boolean`

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

## McpServerToolResultDelta

Fields

`name` `string`

`serverName` `string`

`result` ` object ( Value  ` )

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

## FileSearchResultDelta

Fields

`result[]` ` object ( FileSearchResult  ` )

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

## GoogleMapsResultDelta

Fields

`result[]` ` object ( GoogleMapsResult  ` )

The results of the Google Maps.

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

## TextAnnotationDelta

Fields

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;annotations&quot;: [{object (Annotation)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ContentStop

Fields

`index` `integer`

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
  &quot;index&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## ErrorEvent

Fields

`error` ` object ( Error  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;error&quot;: {object (Error)}}</code></pre></td>
</tr>
</tbody>
</table>

## Error

Error message from an interaction.

Fields

`code` `string`

A URI that identifies the error type.

`message` `string`

A human-readable error message.

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
  &quot;code&quot;: string,
  &quot;message&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## StepStart

Fields

`index` `integer`

`step` ` object ( Step  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;index&quot;: integer,&quot;step&quot;: {object (Step)}}</code></pre></td>
</tr>
</tbody>
</table>

## StepDelta

Fields

`index` `integer`

`delta` ` object ( StepDeltaData  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;index&quot;: integer,&quot;delta&quot;: {object (StepDeltaData)}}</code></pre></td>
</tr>
</tbody>
</table>

## StepDeltaData

Fields

`type` `Union type`

`type` can be only one of the following:

`text` ` object ( TextDelta  ` )

`image` ` object ( ImageDelta  ` )

`audio` ` object ( AudioDelta  ` )

`document` ` object ( DocumentDelta  ` )

`video` ` object ( VideoDelta  ` )

`thoughtSummary` ` object ( ThoughtSummaryDelta  ` )

`thoughtSignature` ` object ( ThoughtSignatureDelta  ` )

`textAnnotationDelta` ` object ( TextAnnotationDelta  ` )

`argumentsDelta` ` object ( ArgumentsDelta  ` )

`serverToolCall` ` object ( ServerToolCallDelta  ` )

`serverToolResult` ` object ( ServerToolResultDelta  ` )

`functionResult` ` object ( FunctionResultDelta  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// type&quot;text&quot;: {object (TextDelta)},&quot;image&quot;: {object (ImageDelta)},&quot;audio&quot;: {object (AudioDelta)},&quot;document&quot;: {object (DocumentDelta)},&quot;video&quot;: {object (VideoDelta)},&quot;thoughtSummary&quot;: {object (ThoughtSummaryDelta)},&quot;thoughtSignature&quot;: {object (ThoughtSignatureDelta)},&quot;textAnnotationDelta&quot;: {object (TextAnnotationDelta)},&quot;argumentsDelta&quot;: {object (ArgumentsDelta)},&quot;serverToolCall&quot;: {object (ServerToolCallDelta)},&quot;serverToolResult&quot;: {object (ServerToolResultDelta)},&quot;functionResult&quot;: {object (FunctionResultDelta)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ArgumentsDelta

Fields

`arguments` `string`

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
  &quot;arguments&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ServerToolCallDelta

Fields

`signature` `string ( bytes format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

`type` can be only one of the following:

`codeExecutionCall` ` object ( CodeExecutionCallDelta  ` )

`urlContextCall` ` object ( UrlContextCallDelta  ` )

`googleSearchCall` ` object ( GoogleSearchCallDelta  ` )

`mcpServerToolCall` ` object ( McpServerToolCallDelta  ` )

`fileSearchCall` ` object ( FileSearchCallDelta  ` )

`googleMapsCall` ` object ( GoogleMapsCallDelta  ` )

`retrievalCall` ` object ( RetrievalCallDelta  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;signature&quot;: string,// type&quot;codeExecutionCall&quot;: {object (CodeExecutionCallDelta)},&quot;urlContextCall&quot;: {object (UrlContextCallDelta)},&quot;googleSearchCall&quot;: {object (GoogleSearchCallDelta)},&quot;mcpServerToolCall&quot;: {object (McpServerToolCallDelta)},&quot;fileSearchCall&quot;: {object (FileSearchCallDelta)},&quot;googleMapsCall&quot;: {object (GoogleMapsCallDelta)},&quot;retrievalCall&quot;: {object (RetrievalCallDelta)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## RetrievalCallDelta

Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc. RetrievalType decides which tool is used.

Fields

`arguments` ` object ( RetrievalStepArguments  ` )

Required. The arguments to pass to the Retrieval tool.

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

## ServerToolResultDelta

Fields

`signature` `string ( bytes format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

`type` can be only one of the following:

`codeExecutionResult` ` object ( CodeExecutionResultDelta  ` )

`urlContextResult` ` object ( UrlContextResultDelta  ` )

`googleSearchResult` ` object ( GoogleSearchResultDelta  ` )

`mcpServerToolResult` ` object ( McpServerToolResultDelta  ` )

`fileSearchResult` ` object ( FileSearchResultDelta  ` )

`googleMapsResult` ` object ( GoogleMapsResultDelta  ` )

`retrievalResult` ` object ( RetrievalResultDelta  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;signature&quot;: string,// type&quot;codeExecutionResult&quot;: {object (CodeExecutionResultDelta)},&quot;urlContextResult&quot;: {object (UrlContextResultDelta)},&quot;googleSearchResult&quot;: {object (GoogleSearchResultDelta)},&quot;mcpServerToolResult&quot;: {object (McpServerToolResultDelta)},&quot;fileSearchResult&quot;: {object (FileSearchResultDelta)},&quot;googleMapsResult&quot;: {object (GoogleMapsResultDelta)},&quot;retrievalResult&quot;: {object (RetrievalResultDelta)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## RetrievalResultDelta

Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc. ToolResultDelta.type

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

## StepStop

Fields

`index` `integer`

`usage` ` object ( Usage  ` )

Cumulative model usage stats from the start of the session.

`stepUsage` ` object ( Usage  ` )

Model usage stats for this specific step.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;index&quot;: integer,&quot;usage&quot;: {object (Usage)},&quot;stepUsage&quot;: {object (Usage)}}</code></pre></td>
</tr>
</tbody>
</table>

## StreamMetadata

Fields

`totalUsage` ` object ( Usage  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;totalUsage&quot;: {object (Usage)}}</code></pre></td>
</tr>
</tbody>
</table>
