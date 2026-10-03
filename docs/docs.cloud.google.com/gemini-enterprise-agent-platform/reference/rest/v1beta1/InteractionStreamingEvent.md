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

`event_type` `Union type`

The event data. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`interactionStartEvent `**`(deprecated)`** `object ( ``InteractionStartEvent`` )`

> This item is deprecated!

The interaction data, used for interaction.start events. Legacy event, used when steps are disabled.

`interactionCompleteEvent `**`(deprecated)`** `object ( ``InteractionCompleteEvent`` )`

> This item is deprecated!

The interaction data, used for interaction.complete events. Legacy event, used when steps are disabled.

`interactionCreatedEvent` `object ( `[`InteractionCreatedSseEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#InteractionCreatedSseEvent)` )`

The interaction data, used for interaction.created events. Used when steps are enabled.

`interactionCompletedEvent` `object ( `[`InteractionCompletedSseEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#InteractionCompletedSseEvent)` )`

The interaction data, used for interaction.completed events. Used when steps are enabled.

`interactionStatusUpdate` `object ( `[`InteractionStatusUpdate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#InteractionStatusUpdate)` )`

The interaction status data, used for interaction.status_update events.

`contentStart `**`(deprecated)`** `object ( ``ContentStart`` )`

> This item is deprecated!

The content block start data, used for content.start events. Legacy content-based streaming event, used when steps are disabled.

`contentDelta `**`(deprecated)`** `object ( ``ContentDelta`` )`

> This item is deprecated!

The content block delta data, used for content.delta events. Legacy content-based streaming event, used when steps are disabled.

`contentStop `**`(deprecated)`** `object ( ``ContentStop`` )`

> This item is deprecated!

The content block stop data, used for content.stop events. Legacy content-based streaming event, used when steps are disabled.

`errorEvent` `object ( `[`ErrorEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ErrorEvent)` )`

The error event data, used for error events.

`stepStart` `object ( `[`StepStart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#StepStart)` )`

The step start data, used for step.start events. Step-based streaming event, used when steps are enabled.

`stepDelta` `object ( `[`StepDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#StepDelta)` )`

The step delta data, used for step.delta events. Step-based streaming event, used when steps are enabled.

`stepStop` `object ( `[`StepStop`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#StepStop)` )`

The step stop data, used for step.stop events. Step-based streaming event, used when steps are enabled.

End of mutually exclusive fields.

**JSON representation**

```
{
  "eventId": string,

  // event_type
  "interactionStartEvent": {
    object (InteractionStartEvent)
  },
  "interactionCompleteEvent": {
    object (InteractionCompleteEvent)
  },
  "interactionCreatedEvent": {
    object (InteractionCreatedSseEvent)
  },
  "interactionCompletedEvent": {
    object (InteractionCompletedSseEvent)
  },
  "interactionStatusUpdate": {
    object (InteractionStatusUpdate)
  },
  "contentStart": {
    object (ContentStart)
  },
  "contentDelta": {
    object (ContentDelta)
  },
  "contentStop": {
    object (ContentStop)
  },
  "errorEvent": {
    object (ErrorEvent)
  },
  "stepStart": {
    object (StepStart)
  },
  "stepDelta": {
    object (StepDelta)
  },
  "stepStop": {
    object (StepStop)
  }
  // Union type
}
```

## InteractionCreatedSseEvent

Server response confirming that a new interaction was created.

Fields

`interaction` `object ( `[`Interaction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction)` )`

Required. Partial interaction resource emitted when the stream is created.

**JSON representation**

```
{
  "interaction": {
    object (Interaction)
  }
}
```

## InteractionCompletedSseEvent

Signals that the Interaction completed. Sent when the Interaction receives Complete/Cancel or naturally terminates. No more input can be sent to the Interaction after this.

Fields

`interaction` `object ( `[`Interaction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Interaction)` )`

Required. Partial completed interaction resource emitted at the end of the stream.

**JSON representation**

```
{
  "interaction": {
    object (Interaction)
  }
}
```

## InteractionStatusUpdate

Fields

`interactionId` `string`

`status` `enum ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Status)` )`

**JSON representation**

```
{
  "interactionId": string,
  "status": enum (Status)
}
```

## ContentDeltaData

The delta content data for a content block.

Fields

`type` `Union type`

The type of the delta content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` `object ( `[`TextDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#TextDelta)` )`

`image` `object ( `[`ImageDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ImageDelta)` )`

`audio` `object ( `[`AudioDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#AudioDelta)` )`

`document` `object ( `[`DocumentDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#DocumentDelta)` )`

`video` `object ( `[`VideoDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#VideoDelta)` )`

`thoughtSummary` `object ( `[`ThoughtSummaryDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ThoughtSummaryDelta)` )`

`thoughtSignature` `object ( `[`ThoughtSignatureDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ThoughtSignatureDelta)` )`

`toolCall` `object ( `[`ToolCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ToolCallDelta)` )`

`toolResult` `object ( `[`ToolResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ToolResultDelta)` )`

`textAnnotation` `object ( `[`TextAnnotationDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#TextAnnotationDelta)` )`

End of mutually exclusive fields.

**JSON representation**

```
{

  // type
  "text": {
    object (TextDelta)
  },
  "image": {
    object (ImageDelta)
  },
  "audio": {
    object (AudioDelta)
  },
  "document": {
    object (DocumentDelta)
  },
  "video": {
    object (VideoDelta)
  },
  "thoughtSummary": {
    object (ThoughtSummaryDelta)
  },
  "thoughtSignature": {
    object (ThoughtSignatureDelta)
  },
  "toolCall": {
    object (ToolCallDelta)
  },
  "toolResult": {
    object (ToolResultDelta)
  },
  "textAnnotation": {
    object (TextAnnotationDelta)
  }
  // Union type
}
```

## TextDelta

Fields

`text` `string`

**JSON representation**

```
{
  "text": string
}
```

## ImageDelta

Fields

`mimeType` `enum ( ``MimeType`` )`

`resolution` `enum ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MediaResolution)` )`

The resolution of the media.

`data_or_uri` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A base64-encoded string.

`uri` `string`

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeType": enum (MimeType),
  "resolution": enum (MediaResolution),

  // data_or_uri
  "data": string,
  "uri": string
  // Union type
}
```

## AudioDelta

Fields

`mimeType` `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MimeType)` )`

`rate `**`(deprecated)`** `integer`

> This item is deprecated!

Deprecated. Use sampleRate instead. The value is ignored.

`sampleRate` `integer`

The sample rate of the audio.

`channels` `integer`

The number of audio channels.

`data_or_uri` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A base64-encoded string.

`uri` `string`

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeType": enum (MimeType),
  "rate": integer,
  "sampleRate": integer,
  "channels": integer,

  // data_or_uri
  "data": string,
  "uri": string
  // Union type
}
```

## DocumentDelta

Fields

`mimeType` `enum ( ``MimeType`` )`

`data_or_uri` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A base64-encoded string.

`uri` `string`

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeType": enum (MimeType),

  // data_or_uri
  "data": string,
  "uri": string
  // Union type
}
```

## VideoDelta

Fields

`mimeType` `enum ( ``MimeType`` )`

`resolution` `enum ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MediaResolution)` )`

The resolution of the media.

`data_or_uri` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A base64-encoded string.

`uri` `string`

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeType": enum (MimeType),
  "resolution": enum (MediaResolution),

  // data_or_uri
  "data": string,
  "uri": string
  // Union type
}
```

## ThoughtSummaryDelta

Fields

`content` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content)` )`

A new summary item to be added to the thought.

**JSON representation**

```
{
  "content": {
    object (Content)
  }
}
```

## ThoughtSignatureDelta

Fields

`signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

signature to match the backend source to be part of the generation.

A base64-encoded string.

**JSON representation**

```
{
  "signature": string
}
```

## ToolCallDelta

Fields

`id` `string`

Required. A unique id for this specific tool call.

`signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`functionCall` `object ( `[`FunctionCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#FunctionCallDelta)` )`

`codeExecutionCall` `object ( `[`CodeExecutionCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#CodeExecutionCallDelta)` )`

`urlContextCall` `object ( `[`UrlContextCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#UrlContextCallDelta)` )`

`googleSearchCall` `object ( `[`GoogleSearchCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#GoogleSearchCallDelta)` )`

`mcpServerToolCall` `object ( `[`McpServerToolCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#McpServerToolCallDelta)` )`

`fileSearchCall` `object ( `[`FileSearchCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#FileSearchCallDelta)` )`

`googleMapsCall` `object ( `[`GoogleMapsCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#GoogleMapsCallDelta)` )`

End of mutually exclusive fields.

**JSON representation**

```
{
  "id": string,
  "signature": string,

  // type
  "functionCall": {
    object (FunctionCallDelta)
  },
  "codeExecutionCall": {
    object (CodeExecutionCallDelta)
  },
  "urlContextCall": {
    object (UrlContextCallDelta)
  },
  "googleSearchCall": {
    object (GoogleSearchCallDelta)
  },
  "mcpServerToolCall": {
    object (McpServerToolCallDelta)
  },
  "fileSearchCall": {
    object (FileSearchCallDelta)
  },
  "googleMapsCall": {
    object (GoogleMapsCallDelta)
  }
  // Union type
}
```

## FunctionCallDelta

Fields

`name` `string`

`arguments` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

**JSON representation**

```
{
  "name": string,
  "arguments": {
    object (Struct)
  }
}
```

## CodeExecutionCallDelta

Fields

`arguments` `object ( `[`CodeExecutionCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/CodeExecutionCallArguments)` )`

**JSON representation**

```
{
  "arguments": {
    object (CodeExecutionCallArguments)
  }
}
```

## UrlContextCallDelta

Fields

`arguments` `object ( `[`UrlContextCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UrlContextCallArguments)` )`

**JSON representation**

```
{
  "arguments": {
    object (UrlContextCallArguments)
  }
}
```

## GoogleSearchCallDelta

Fields

`arguments` `object ( `[`GoogleSearchCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleSearchCallArguments)` )`

**JSON representation**

```
{
  "arguments": {
    object (GoogleSearchCallArguments)
  }
}
```

## McpServerToolCallDelta

Fields

`name` `string`

`serverName` `string`

`arguments` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

**JSON representation**

```
{
  "name": string,
  "serverName": string,
  "arguments": {
    object (Struct)
  }
}
```

## FileSearchCallDelta

This type has no fields.

## GoogleMapsCallDelta

Fields

`arguments` `object ( `[`GoogleMapsCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleMapsCallArguments)` )`

The arguments to pass to the Google Maps tool.

**JSON representation**

```
{
  "arguments": {
    object (GoogleMapsCallArguments)
  }
}
```

## ToolResultDelta

Fields

`callId` `string`

Required. id to match the id from the function call block.

`signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`functionResult` `object ( `[`FunctionResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#FunctionResultDelta)` )`

`codeExecutionResult` `object ( `[`CodeExecutionResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#CodeExecutionResultDelta)` )`

`urlContextResult` `object ( `[`UrlContextResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#UrlContextResultDelta)` )`

`googleSearchResult` `object ( `[`GoogleSearchResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#GoogleSearchResultDelta)` )`

`mcpServerToolResult` `object ( `[`McpServerToolResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#McpServerToolResultDelta)` )`

`fileSearchResult` `object ( `[`FileSearchResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#FileSearchResultDelta)` )`

`googleMapsResult` `object ( `[`GoogleMapsResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#GoogleMapsResultDelta)` )`

End of mutually exclusive fields.

**JSON representation**

```
{
  "callId": string,
  "signature": string,

  // type
  "functionResult": {
    object (FunctionResultDelta)
  },
  "codeExecutionResult": {
    object (CodeExecutionResultDelta)
  },
  "urlContextResult": {
    object (UrlContextResultDelta)
  },
  "googleSearchResult": {
    object (GoogleSearchResultDelta)
  },
  "mcpServerToolResult": {
    object (McpServerToolResultDelta)
  },
  "fileSearchResult": {
    object (FileSearchResultDelta)
  },
  "googleMapsResult": {
    object (GoogleMapsResultDelta)
  }
  // Union type
}
```

## FunctionResultDelta

Fields

`name` `string`

`isError` `boolean`

`result` `object ( `[`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value)` )`

**JSON representation**

```
{
  "name": string,
  "isError": boolean,
  "result": {
    object (Value)
  }
}
```

## CodeExecutionResultDelta

Fields

`result` `string`

`isError` `boolean`

**JSON representation**

```
{
  "result": string,
  "isError": boolean
}
```

## UrlContextResultDelta

Fields

`result[]` `object ( `[`UrlContextResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UrlContextResult)` )`

`isError` `boolean`

**JSON representation**

```
{
  "result": [
    {
      object (UrlContextResult)
    }
  ],
  "isError": boolean
}
```

## GoogleSearchResultDelta

Fields

`result[]` `object ( `[`GoogleSearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleSearchResult)` )`

`isError` `boolean`

**JSON representation**

```
{
  "result": [
    {
      object (GoogleSearchResult)
    }
  ],
  "isError": boolean
}
```

## McpServerToolResultDelta

Fields

`name` `string`

`serverName` `string`

`result` `object ( `[`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value)` )`

**JSON representation**

```
{
  "name": string,
  "serverName": string,
  "result": {
    object (Value)
  }
}
```

## FileSearchResultDelta

Fields

`result[]` `object ( `[`FileSearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FileSearchResult)` )`

**JSON representation**

```
{
  "result": [
    {
      object (FileSearchResult)
    }
  ]
}
```

## GoogleMapsResultDelta

Fields

`result[]` `object ( `[`GoogleMapsResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleMapsResult)` )`

The results of the Google Maps.

**JSON representation**

```
{
  "result": [
    {
      object (GoogleMapsResult)
    }
  ]
}
```

## TextAnnotationDelta

Fields

`annotations[]` `object ( `[`Annotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Annotation)` )`

Citation information for model-generated content.

**JSON representation**

```
{
  "annotations": [
    {
      object (Annotation)
    }
  ]
}
```

## ErrorEvent

Fields

`error` `object ( `[`Error`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Error)` )`

**JSON representation**

```
{
  "error": {
    object (Error)
  }
}
```

## StepStart

Fields

`index` `integer`

`step` `object ( `[`Step`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step)` )`

**JSON representation**

```
{
  "index": integer,
  "step": {
    object (Step)
  }
}
```

## StepDelta

Fields

`index` `integer`

`delta` `object ( `[`StepDeltaData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#StepDeltaData)` )`

**JSON representation**

```
{
  "index": integer,
  "delta": {
    object (StepDeltaData)
  }
}
```

## StepDeltaData

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` `object ( `[`TextDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#TextDelta)` )`

`image` `object ( `[`ImageDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ImageDelta)` )`

`audio` `object ( `[`AudioDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#AudioDelta)` )`

`document` `object ( `[`DocumentDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#DocumentDelta)` )`

`video` `object ( `[`VideoDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#VideoDelta)` )`

`thoughtSummary` `object ( `[`ThoughtSummaryDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ThoughtSummaryDelta)` )`

`thoughtSignature` `object ( `[`ThoughtSignatureDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ThoughtSignatureDelta)` )`

`textAnnotationDelta` `object ( `[`TextAnnotationDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#TextAnnotationDelta)` )`

`argumentsDelta` `object ( `[`ArgumentsDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ArgumentsDelta)` )`

`serverToolCall` `object ( `[`ServerToolCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ServerToolCallDelta)` )`

`serverToolResult` `object ( `[`ServerToolResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#ServerToolResultDelta)` )`

`functionResult` `object ( `[`FunctionResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#FunctionResultDelta)` )`

End of mutually exclusive fields.

**JSON representation**

```
{

  // type
  "text": {
    object (TextDelta)
  },
  "image": {
    object (ImageDelta)
  },
  "audio": {
    object (AudioDelta)
  },
  "document": {
    object (DocumentDelta)
  },
  "video": {
    object (VideoDelta)
  },
  "thoughtSummary": {
    object (ThoughtSummaryDelta)
  },
  "thoughtSignature": {
    object (ThoughtSignatureDelta)
  },
  "textAnnotationDelta": {
    object (TextAnnotationDelta)
  },
  "argumentsDelta": {
    object (ArgumentsDelta)
  },
  "serverToolCall": {
    object (ServerToolCallDelta)
  },
  "serverToolResult": {
    object (ServerToolResultDelta)
  },
  "functionResult": {
    object (FunctionResultDelta)
  }
  // Union type
}
```

## ArgumentsDelta

Fields

`arguments` `string`

**JSON representation**

```
{
  "arguments": string
}
```

## ServerToolCallDelta

Fields

`signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`codeExecutionCall` `object ( `[`CodeExecutionCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#CodeExecutionCallDelta)` )`

`urlContextCall` `object ( `[`UrlContextCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#UrlContextCallDelta)` )`

`googleSearchCall` `object ( `[`GoogleSearchCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#GoogleSearchCallDelta)` )`

`mcpServerToolCall` `object ( `[`McpServerToolCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#McpServerToolCallDelta)` )`

`fileSearchCall` `object ( `[`FileSearchCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#FileSearchCallDelta)` )`

`googleMapsCall` `object ( `[`GoogleMapsCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#GoogleMapsCallDelta)` )`

`retrievalCall` `object ( `[`RetrievalCallDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#RetrievalCallDelta)` )`

End of mutually exclusive fields.

**JSON representation**

```
{
  "signature": string,

  // type
  "codeExecutionCall": {
    object (CodeExecutionCallDelta)
  },
  "urlContextCall": {
    object (UrlContextCallDelta)
  },
  "googleSearchCall": {
    object (GoogleSearchCallDelta)
  },
  "mcpServerToolCall": {
    object (McpServerToolCallDelta)
  },
  "fileSearchCall": {
    object (FileSearchCallDelta)
  },
  "googleMapsCall": {
    object (GoogleMapsCallDelta)
  },
  "retrievalCall": {
    object (RetrievalCallDelta)
  }
  // Union type
}
```

## RetrievalCallDelta

Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc. RetrievalType decides which tool is used.

Fields

`arguments` `object ( `[`RetrievalStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrievalStepArguments)` )`

Required. The arguments to pass to the Retrieval tool.

`retrievalType` `enum ( `[`RetrievalType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrievalType)` )`

The type of retrieval tools.

**JSON representation**

```
{
  "arguments": {
    object (RetrievalStepArguments)
  },
  "retrievalType": enum (RetrievalType)
}
```

## ServerToolResultDelta

Fields

`signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`codeExecutionResult` `object ( `[`CodeExecutionResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#CodeExecutionResultDelta)` )`

`urlContextResult` `object ( `[`UrlContextResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#UrlContextResultDelta)` )`

`googleSearchResult` `object ( `[`GoogleSearchResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#GoogleSearchResultDelta)` )`

`mcpServerToolResult` `object ( `[`McpServerToolResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#McpServerToolResultDelta)` )`

`fileSearchResult` `object ( `[`FileSearchResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#FileSearchResultDelta)` )`

`googleMapsResult` `object ( `[`GoogleMapsResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#GoogleMapsResultDelta)` )`

`retrievalResult` `object ( `[`RetrievalResultDelta`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/InteractionStreamingEvent#RetrievalResultDelta)` )`

End of mutually exclusive fields.

**JSON representation**

```
{
  "signature": string,

  // type
  "codeExecutionResult": {
    object (CodeExecutionResultDelta)
  },
  "urlContextResult": {
    object (UrlContextResultDelta)
  },
  "googleSearchResult": {
    object (GoogleSearchResultDelta)
  },
  "mcpServerToolResult": {
    object (McpServerToolResultDelta)
  },
  "fileSearchResult": {
    object (FileSearchResultDelta)
  },
  "googleMapsResult": {
    object (GoogleMapsResultDelta)
  },
  "retrievalResult": {
    object (RetrievalResultDelta)
  }
  // Union type
}
```

## RetrievalResultDelta

Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc. ToolResultDelta.type

Fields

`isError` `boolean`

Whether the retrieval resulted in an error.

**JSON representation**

```
{
  "isError": boolean
}
```

## StepStop

Fields

`index` `integer`

`usage` `object ( `[`Usage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage)` )`

Cumulative model usage stats from the start of the session.

`stepUsage` `object ( `[`Usage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage)` )`

Model usage stats for this specific step.

**JSON representation**

```
{
  "index": integer,
  "usage": {
    object (Usage)
  },
  "stepUsage": {
    object (Usage)
  }
}
```
