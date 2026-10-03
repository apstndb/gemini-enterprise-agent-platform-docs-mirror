---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/ask_contexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/ask_contexts
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `ask_contexts`

Answers a natural-language question directly using contexts retrieved from a RAG Engine Corpus, in a single agentic call. Use this when the user wants a final answer grounded in their corpus and does not need to inspect intermediate retrieved contexts. For raw retrieval use `retrieve_contexts` ; for augmenting a prompt before sending to a separate LLM step use `augment_prompt` .

Note: This tool is backed by a `v1beta1` RPC. Format: 'projects/{project_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

**Parameters** \* `parent` : The parent resource, of the form `projects/{project}/locations/{location}` . \* `query` : The natural-language query to answer. \* `query.text` : The query text. \* `query.rag_retrieval_config` : Retrieval config (top_k, filter, ranking) used to gather supporting contexts. \* `tools` : Optional list of tools the agentic retriever may use during answering.

The following sample demonstrate how to use `curl` to invoke the `ask_contexts` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "ask_contexts",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Agentic Retrieval Ask API for RAG. Request message for `VertexRagService.AskContexts` .

### AskContextsRequest

**JSON representation**

```
{
  "parent": string,
  "query": {
    object (RagQuery)
  },
  "tools": [
    {
      object (Tool)
    }
  ]
}
```

| Fields    |                                                                                                                                                                                                            |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`  | `string` Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` . |
| `query`   | `object ( `[`RagQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/ask_contexts#Input.Schema.RagQuery)` )` Required. Single RAG retrieve query.               |
| `tools[]` | `object ( `[`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Tool)` )` Optional. The tools to use for AskContexts.          |

### RagQuery

**JSON representation**

```
{
  "similarityTopK": integer,
  "ranking": {
    object (Ranking)
  },
  "ragRetrievalConfig": {
    object (RagRetrievalConfig)
  },

  // Union field query can be only one of the following:
  "text": string
  // End of list of possible types for union field query.
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
<td><code>similarityTopK </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>integer</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. The number of contexts to retrieve.</p></td>
</tr>
<tr class="even">
<td><code>ranking </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/ask_contexts#Input.Schema.Ranking"><code>Ranking</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Configurations for hybrid search results ranking.</p></td>
</tr>
<tr class="odd">
<td><code>ragRetrievalConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RagRetrievalConfig"><code>RagRetrievalConfig</code></a><code> )</code></p>
<p>Optional. The retrieval config for the query.</p></td>
</tr>
<tr class="even">
<td>Union field <code>query</code> . The query to retrieve contexts. Currently only text query is supported. <code>query</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>text</code></td>
<td><p><code>string</code></p>
<p>Optional. The query in text format to get relevant contexts.</p></td>
</tr>
</tbody>
</table>

### Ranking

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

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

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

## Output Schema

Response message for `VertexRagService.AskContexts` .

### AskContextsResponse

**JSON representation**

```
{
  "response": string,
  "contexts": {
    object (RagContexts)
  }
}
```

| Fields     |                                                                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `response` | `string` The Retrieval Response.                                                                                                                                                          |
| `contexts` | `object ( `[`RagContexts`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/ask_contexts#Output.Schema.RagContexts)` )` The contexts of the query. |

### RagContexts

**JSON representation**

```
{
  "contexts": [
    {
      object (Context)
    }
  ]
}
```

| Fields       |                                                                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `contexts[]` | `object ( `[`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/ask_contexts#Output.Schema.Context)` )` All its contexts. |

### Context

**JSON representation**

```
{
  "sourceUri": string,
  "sourceDisplayName": string,
  "text": string,
  "distance": number,
  "sparseDistance": number,
  "chunk": {
    object (RagChunk)
  },

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
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
<td><code>sourceUri</code></td>
<td><p><code>string</code></p>
<p>If the file is imported from Cloud Storage or Google Drive, source_uri will be original file URI in Cloud Storage or Google Drive; if file is uploaded, source_uri will be file display name.</p></td>
</tr>
<tr class="even">
<td><code>sourceDisplayName</code></td>
<td><p><code>string</code></p>
<p>The file display name.</p></td>
</tr>
<tr class="odd">
<td><code>text</code></td>
<td><p><code>string</code></p>
<p>The text chunk.</p></td>
</tr>
<tr class="even">
<td><code>distance </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>number</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>The distance between the query dense embedding vector and the context text vector.</p></td>
</tr>
<tr class="odd">
<td><code>sparseDistance </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>number</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>The distance between the query sparse embedding vector and the context text vector.</p></td>
</tr>
<tr class="even">
<td><code>chunk</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/generate_content#Output.Schema.RagChunk"><code>RagChunk</code></a><code> )</code></p>
<p>Context of the retrieved chunk.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_score</code> .</p>
<p><code>_score</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>score</code></td>
<td><p><code>number</code></p>
<p>According to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the context and its range depends on the metric type.</p>
<p>For example, if the metric type is COSINE_DISTANCE, it represents the distance between the query and the context. The larger the distance, the less relevant the context is to the query. The range is [0, 2], while 0 means the most relevant and 2 means the least relevant.</p></td>
</tr>
</tbody>
</table>

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

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
