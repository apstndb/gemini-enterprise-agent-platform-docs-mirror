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

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`thought` `object ( `[`ThoughtStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#ThoughtStep)` )`

`toolCall` `object ( `[`ToolCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#ToolCallStep)` )`

`toolResult` `object ( `[`ToolResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#ToolResultStep)` )`

`userInput` `object ( `[`UserInputStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#UserInputStep)` )`

DO NOT USE -- These are for 3P JSON only

`modelOutput` `object ( `[`ModelOutputStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#ModelOutputStep)` )`

`text `**`(deprecated)`** `object ( ``LegacyTextContent`` )`

> This item is deprecated!

`image `**`(deprecated)`** `object ( ``LegacyImageContent`` )`

> This item is deprecated!

`audio `**`(deprecated)`** `object ( ``LegacyAudioContent`` )`

> This item is deprecated!

`document `**`(deprecated)`** `object ( ``LegacyDocumentContent`` )`

> This item is deprecated!

`video `**`(deprecated)`** `object ( ``LegacyVideoContent`` )`

> This item is deprecated!

End of mutually exclusive fields.

**JSON representation**

```
{

  // type
  "thought": {
    object (ThoughtStep)
  },
  "toolCall": {
    object (ToolCallStep)
  },
  "toolResult": {
    object (ToolResultStep)
  },
  "userInput": {
    object (UserInputStep)
  },
  "modelOutput": {
    object (ModelOutputStep)
  },
  "text": {
    object (LegacyTextContent)
  },
  "image": {
    object (LegacyImageContent)
  },
  "audio": {
    object (LegacyAudioContent)
  },
  "document": {
    object (LegacyDocumentContent)
  },
  "video": {
    object (LegacyVideoContent)
  }
  // Union type
}
```

## ThoughtStep

A thought step.

Fields

`signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A signature hash for backend validation.

A base64-encoded string.

`summary[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content)` )`

A summary of the thought.

**JSON representation**

```
{
  "signature": string,
  "summary": [
    {
      object (Content)
    }
  ]
}
```

## ToolCallStep

Tool call step.

Fields

`id` `string`

Required. A unique id for this specific tool call.

`signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`functionCall` `object ( `[`FunctionCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#FunctionCallStep)` )`

`codeExecutionCall` `object ( `[`CodeExecutionCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#CodeExecutionCallStep)` )`

`urlContextCall` `object ( `[`UrlContextCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#UrlContextCallStep)` )`

`mcpServerToolCall` `object ( `[`McpServerToolCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#McpServerToolCallStep)` )`

`googleSearchCall` `object ( `[`GoogleSearchCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#GoogleSearchCallStep)` )`

`fileSearchCall` `object ( `[`FileSearchCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#FileSearchCallStep)` )`

`googleMapsCall` `object ( `[`GoogleMapsCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#GoogleMapsCallStep)` )`

`retrievalCall` `object ( `[`RetrievalCallStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#RetrievalCallStep)` )`

End of mutually exclusive fields.

**JSON representation**

```
{
  "id": string,
  "signature": string,

  // type
  "functionCall": {
    object (FunctionCallStep)
  },
  "codeExecutionCall": {
    object (CodeExecutionCallStep)
  },
  "urlContextCall": {
    object (UrlContextCallStep)
  },
  "mcpServerToolCall": {
    object (McpServerToolCallStep)
  },
  "googleSearchCall": {
    object (GoogleSearchCallStep)
  },
  "fileSearchCall": {
    object (FileSearchCallStep)
  },
  "googleMapsCall": {
    object (GoogleMapsCallStep)
  },
  "retrievalCall": {
    object (RetrievalCallStep)
  }
  // Union type
}
```

## FunctionCallStep

A function tool call step.

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

## CodeExecutionCallStep

code execution call step.

Fields

`arguments` `object ( `[`CodeExecutionCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#CodeExecutionCallStepArguments)` )`

Required. The arguments to pass to the code execution.

**JSON representation**

```
{
  "arguments": {
    object (CodeExecutionCallStepArguments)
  }
}
```

## CodeExecutionCallStepArguments

The arguments to pass to the code execution.

Fields

`language` `enum ( `[`Language`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#Language)` )`

Programming language of the `code` .

`code` `string`

The code to be executed.

**JSON representation**

```
{
  "language": enum (Language),
  "code": string
}
```

## Language

Supported programming languages for the generated code.

| Enums                  |                                                      |
|------------------------|------------------------------------------------------|
| `LANGUAGE_UNSPECIFIED` | Unspecified language. This value should not be used. |
| `PYTHON`               | Python \>= 3.10, with numpy and simpy available.     |

## UrlContextCallStep

URL context call step.

Fields

`arguments` `object ( `[`UrlContextCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#UrlContextCallStepArguments)` )`

Required. The arguments to pass to the URL context.

**JSON representation**

```
{
  "arguments": {
    object (UrlContextCallStepArguments)
  }
}
```

## UrlContextCallStepArguments

The arguments to pass to the URL context.

Fields

`urls[]` `string`

The URLs to fetch.

**JSON representation**

```
{
  "urls": [
    string
  ]
}
```

## McpServerToolCallStep

MCPServer tool call step.

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

## GoogleSearchCallStep

Google Search call step.

Fields

`arguments` `object ( `[`GoogleSearchCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#GoogleSearchCallStepArguments)` )`

Required. The arguments to pass to Google Search.

`searchType` `enum ( `[`SearchType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SearchType)` )`

The type of search grounding enabled.

**JSON representation**

```
{
  "arguments": {
    object (GoogleSearchCallStepArguments)
  },
  "searchType": enum (SearchType)
}
```

## GoogleSearchCallStepArguments

The arguments to pass to Google Search.

Fields

`queries[]` `string`

Web search queries for the following-up web search.

**JSON representation**

```
{
  "queries": [
    string
  ]
}
```

## FileSearchCallStep

This type has no fields.

File Search call step.

## GoogleMapsCallStep

Google Maps call step.

Fields

`arguments` `object ( `[`GoogleMapsCallStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#GoogleMapsCallStepArguments)` )`

The arguments to pass to the Google Maps tool.

**JSON representation**

```
{
  "arguments": {
    object (GoogleMapsCallStepArguments)
  }
}
```

## GoogleMapsCallStepArguments

The arguments to pass to the Google Maps tool.

Fields

`queries[]` `string`

The queries to be executed.

**JSON representation**

```
{
  "queries": [
    string
  ]
}
```

## RetrievalCallStep

Retrieval call step. Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc. RetrievalType decides which tool is used.

Fields

`arguments` `object ( `[`RetrievalStepArguments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrievalStepArguments)` )`

Required. The arguments to pass to the retrieval tool.

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

## ToolResultStep

Tool result step.

Fields

`callId` `string`

Required. id to match the id from the function call block.

`signature` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

A signature hash for backend validation.

A base64-encoded string.

`type` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`functionResult` `object ( `[`FunctionResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#FunctionResultStep)` )`

`codeExecutionResult` `object ( `[`CodeExecutionResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#CodeExecutionResultStep)` )`

`urlContextResult` `object ( `[`UrlContextResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#UrlContextResultStep)` )`

`googleSearchResult` `object ( `[`GoogleSearchResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#GoogleSearchResultStep)` )`

`mcpServerToolResult` `object ( `[`McpServerToolResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#McpServerToolResultStep)` )`

`fileSearchResult` `object ( `[`FileSearchResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#FileSearchResultStep)` )`

`googleMapsResult` `object ( `[`GoogleMapsResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#GoogleMapsResultStep)` )`

`retrievalResult` `object ( `[`RetrievalResultStep`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#RetrievalResultStep)` )`

End of mutually exclusive fields.

**JSON representation**

```
{
  "callId": string,
  "signature": string,

  // type
  "functionResult": {
    object (FunctionResultStep)
  },
  "codeExecutionResult": {
    object (CodeExecutionResultStep)
  },
  "urlContextResult": {
    object (UrlContextResultStep)
  },
  "googleSearchResult": {
    object (GoogleSearchResultStep)
  },
  "mcpServerToolResult": {
    object (McpServerToolResultStep)
  },
  "fileSearchResult": {
    object (FileSearchResultStep)
  },
  "googleMapsResult": {
    object (GoogleMapsResultStep)
  },
  "retrievalResult": {
    object (RetrievalResultStep)
  }
  // Union type
}
```

## FunctionResultStep

result of a function tool call.

Fields

`name` `string`

The name of the tool that was called.

`isError` `boolean`

Whether the tool call resulted in an error.

`result` `object ( `[`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value)` )`

Required. The result of the tool call.

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

## CodeExecutionResultStep

code execution result step.

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

## UrlContextResultStep

URL context result step.

Fields

`result[]` `object ( `[`UrlContextResultItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#UrlContextResultItem)` )`

Required. The results of the URL context.

`isError` `boolean`

Whether the URL context resulted in an error.

**JSON representation**

```
{
  "result": [
    {
      object (UrlContextResultItem)
    }
  ],
  "isError": boolean
}
```

## UrlContextResultItem

The result of the URL context.

Fields

`url` `string`

The URL that was fetched.

`status` `enum ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#Status)` )`

The status of the URL retrieval.

**JSON representation**

```
{
  "url": string,
  "status": enum (Status)
}
```

## Status

The status of the URL retrieval.

| Enums                |     |
|----------------------|-----|
| `STATUS_UNSPECIFIED` |     |
| `SUCCESS`            |     |
| `ERROR`              |     |
| `PAYWALL`            |     |
| `UNSAFE`             |     |

## GoogleSearchResultStep

Google Search result step.

Fields

`result[]` `object ( `[`GoogleSearchResultItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#GoogleSearchResultItem)` )`

Required. The results of the Google Search.

`isError` `boolean`

Whether the Google Search resulted in an error.

**JSON representation**

```
{
  "result": [
    {
      object (GoogleSearchResultItem)
    }
  ],
  "isError": boolean
}
```

## GoogleSearchResultItem

The result of the Google Search.

Fields

`searchSuggestions` `string`

Web content snippet that can be embedded in a web page or an app webview.

**JSON representation**

```
{
  "searchSuggestions": string
}
```

## McpServerToolResultStep

MCPServer tool result step.

Fields

`name` `string`

name of the tool which is called for this specific tool call.

`serverName` `string`

The name of the used MCP server.

`result` `object ( `[`Value`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Value)` )`

Required. The output from the MCP server call. Can be simple text or rich content.

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

## FileSearchResultStep

This type has no fields.

File Search result step.

## GoogleMapsResultStep

Google Maps result step.

Fields

`result[]` `object ( `[`GoogleMapsResultItem`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#GoogleMapsResultItem)` )`

**JSON representation**

```
{
  "result": [
    {
      object (GoogleMapsResultItem)
    }
  ]
}
```

## GoogleMapsResultItem

The result of the Google Maps.

Fields

`places[]` `object ( `[`GoogleMapsResultPlaces`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Step#GoogleMapsResultPlaces)` )`

`widgetContextToken` `string`

**JSON representation**

```
{
  "places": [
    {
      object (GoogleMapsResultPlaces)
    }
  ],
  "widgetContextToken": string
}
```

## GoogleMapsResultPlaces

Fields

`placeId` `string`

`name` `string`

`url` `string`

`reviewSnippets[]` `object ( `[`ReviewSnippet`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ReviewSnippet)` )`

**JSON representation**

```
{
  "placeId": string,
  "name": string,
  "url": string,
  "reviewSnippets": [
    {
      object (ReviewSnippet)
    }
  ]
}
```

## RetrievalResultStep

Vertex Retrieval result step. Used by Vertex Retrieval tools such as Parallel AI, Exa AI, Agent Platform Search, etc.

Fields

`isError` `boolean`

Whether the retrieval resulted in an error.

**JSON representation**

```
{
  "isError": boolean
}
```

## UserInputStep

Input provided by the user.

Fields

`content` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`contentList` `object ( `[`ContentList`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ContentList)` )`

The content of the step. An array of Content objects.

`contentString` `string`

The content of the step. A single string.

End of mutually exclusive fields.

**JSON representation**

```
{

  // content
  "contentList": {
    object (ContentList)
  },
  "contentString": string
  // Union type
}
```

## ModelOutputStep

Output generated by the model.

Fields

`content[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Content)` )`

`error `**`(deprecated)`** `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

> This item is deprecated!

The error result of the operation in case of failure or cancellation.

**JSON representation**

```
{
  "content": [
    {
      object (Content)
    }
  ],
  "error": {
    object (Status)
  }
}
```
