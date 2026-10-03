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

`text` `object ( `[`TextContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content#TextContent)` )`

`image` `object ( `[`ImageContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content#ImageContent)` )`

`audio` `object ( `[`AudioContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content#AudioContent)` )`

`document` `object ( `[`DocumentContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content#DocumentContent)` )`

`video` `object ( `[`VideoContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content#VideoContent)` )`

`thought `**`(deprecated)`** `object ( ``ThoughtContent`` )`

> This item is deprecated!

`toolCall `**`(deprecated)`** `object ( ``ToolCallContent`` )`

> This item is deprecated!

`toolResult `**`(deprecated)`** `object ( ``ToolResultContent`` )`

> This item is deprecated!

End of mutually exclusive fields.

**JSON representation**

```
{

  // type
  "text": {
    object (TextContent)
  },
  "image": {
    object (ImageContent)
  },
  "audio": {
    object (AudioContent)
  },
  "document": {
    object (DocumentContent)
  },
  "video": {
    object (VideoContent)
  },
  "thought": {
    object (ThoughtContent)
  },
  "toolCall": {
    object (ToolCallContent)
  },
  "toolResult": {
    object (ToolResultContent)
  }
  // Union type
}
```

## TextContent

A text content block.

Fields

`text` `string`

Required. The text content.

`annotations[]` `object ( `[`Annotation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Annotation)` )`

Citation information for model-generated content.

**JSON representation**

```
{
  "text": string,
  "annotations": [
    {
      object (Annotation)
    }
  ]
}
```

## ImageContent

An image content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the image, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`resolution` `enum ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MediaResolution)` )`

The resolution of the media.

`data_or_uri` `Union type`

The image content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The image content.

A base64-encoded string.

`uri` `string`

The URI of the image.

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeTypeString": string,
  "resolution": enum (MediaResolution),

  // data_or_uri
  "data": string,
  "uri": string
  // Union type
}
```

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

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The audio content.

A base64-encoded string.

`uri` `string`

The URI of the audio.

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeTypeString": string,
  "channels": integer,
  "sampleRate": integer,

  // data_or_uri
  "data": string,
  "uri": string
  // Union type
}
```

## DocumentContent

A document content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the document, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`data_or_uri` `Union type`

The document content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The document content.

A base64-encoded string.

`uri` `string`

The URI of the document.

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeTypeString": string,

  // data_or_uri
  "data": string,
  "uri": string
  // Union type
}
```

## VideoContent

A video content block.

Fields

`mimeTypeString` `string`

Flexible MIME type string of the video, superseding mimeType = 1. Note: Bespoke logic in the GAOS parser/serializer maps this to the "mimeType" JSON key.

`resolution` `enum ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MediaResolution)` )`

The resolution of the media.

`name` `string`

A user-defined name for this content block. Can be referenced by the model in the final response.

`data_or_uri` `Union type`

The video content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

The video content.

A base64-encoded string.

`uri` `string`

The URI of the video.

End of mutually exclusive fields.

`processing` `Union type`

How the model processes this video for understanding. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`processingType` `enum ( `[`Processing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Processing)` )`

`processingConfig` `object ( `[`MediaProcessing`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MediaProcessing)` )`

End of mutually exclusive fields.

**JSON representation**

```
{
  "mimeTypeString": string,
  "resolution": enum (MediaResolution),
  "name": string,

  // data_or_uri
  "data": string,
  "uri": string
  // Union type

  // processing
  "processingType": enum (Processing),
  "processingConfig": {
    object (MediaProcessing)
  }
  // Union type
}
```

## FunctionCallContent

> This item is deprecated!

A function tool call content block.

Fields

`name` `string`

Required. The name of the tool to call.

`arguments` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

Required. The arguments to pass to the function.

**JSON representation**

```
{
  "name": string,
  "arguments": {
    object (Struct)
  }
}
```

## CodeExecutionCallContent

> This item is deprecated!

code execution content.

Fields

`arguments` `object ( `[`CodeExecutionCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/CodeExecutionCallArguments)` )`

Required. The arguments to pass to the code execution.

**JSON representation**

```
{
  "arguments": {
    object (CodeExecutionCallArguments)
  }
}
```

## UrlContextCallContent

> This item is deprecated!

URL context content.

Fields

`arguments` `object ( `[`UrlContextCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UrlContextCallArguments)` )`

Required. The arguments to pass to the URL context.

**JSON representation**

```
{
  "arguments": {
    object (UrlContextCallArguments)
  }
}
```

## McpServerToolCallContent

MCPServer tool call content.

Fields

`name` `string`

Required. The name of the tool which was called.

`serverName` `string`

Required. The name of the used MCP server.

`arguments` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

Required. The JSON object of arguments for the function.

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

## GoogleSearchCallContent

> This item is deprecated!

Google Search content.

Fields

`arguments` `object ( `[`GoogleSearchCallArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleSearchCallArguments)` )`

Required. The arguments to pass to Google Search.

`searchType` `enum ( `[`SearchType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SearchType)` )`

The type of search grounding enabled.

**JSON representation**

```
{
  "arguments": {
    object (GoogleSearchCallArguments)
  },
  "searchType": enum (SearchType)
}
```

## FileSearchCallContent

This type has no fields.

> This item is deprecated!

File Search content.

## GoogleMapsCallContent

> This item is deprecated!

Google Maps content.

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

## FunctionResultContent

> This item is deprecated!

A function tool result content block.

Fields

`name` `string`

The name of the tool that was called.

`isError` `boolean`

Whether the tool call resulted in an error.

`result` `Union type`

The result of the tool call. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`structResult` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

`contentList` `object ( `[`FunctionResultSubcontentList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content#FunctionResultSubcontentList)` )`

`stringResult` `string`

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "isError": boolean,

  // result
  "structResult": {
    object (Struct)
  },
  "contentList": {
    object (FunctionResultSubcontentList)
  },
  "stringResult": string
  // Union type
}
```

## FunctionResultSubcontentList

Fields

`contents[]` `object ( `[`FunctionResultSubcontent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content#FunctionResultSubcontent)` )`

**JSON representation**

```
{
  "contents": [
    {
      object (FunctionResultSubcontent)
    }
  ]
}
```

## FunctionResultSubcontent

Fields

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` `object ( `[`TextContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content#TextContent)` )`

`image` `object ( `[`ImageContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content#ImageContent)` )`

End of mutually exclusive fields.

**JSON representation**

```
{

  // type
  "text": {
    object (TextContent)
  },
  "image": {
    object (ImageContent)
  }
  // Union type
}
```

## CodeExecutionResultContent

> This item is deprecated!

code execution result content.

Fields

`result` `string`

Required. The output of the code execution.

`isError` `boolean`

Whether the code execution resulted in an error.

**JSON representation**

```
{
  "result": string,
  "isError": boolean
}
```

## UrlContextResultContent

> This item is deprecated!

URL context result content.

Fields

`result[]` `object ( `[`UrlContextResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UrlContextResult)` )`

Required. The results of the URL context.

`isError` `boolean`

Whether the URL context resulted in an error.

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

## GoogleSearchResultContent

> This item is deprecated!

Google Search result content.

Fields

`result[]` `object ( `[`GoogleSearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleSearchResult)` )`

Required. The results of the Google Search.

`isError` `boolean`

Whether the Google Search resulted in an error.

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

## McpServerToolResultContent

MCPServer tool result content.

Fields

`name` `string`

name of the tool which is called for this specific tool call.

`serverName` `string`

The name of the used MCP server.

`result` `Union type`

The output from the MCP server call. Can be simple text or rich content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`structResult` `object ( `[`Struct`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Struct)` )`

`contentList` `object ( `[`FunctionResultSubcontentList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content#FunctionResultSubcontentList)` )`

`stringResult` `string`

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "serverName": string,

  // result
  "structResult": {
    object (Struct)
  },
  "contentList": {
    object (FunctionResultSubcontentList)
  },
  "stringResult": string
  // Union type
}
```

## FileSearchResultContent

> This item is deprecated!

File Search result content.

Fields

`result[]` `object ( `[`FileSearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FileSearchResult)` )`

The results of the File Search.

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

## GoogleMapsResultContent

> This item is deprecated!

Google Maps result content.

Fields

`result[]` `object ( `[`GoogleMapsResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GoogleMapsResult)` )`

Required. The results of the Google Maps.

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
