---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/ask_contexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/ask_contexts
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `ask_contexts`

Answers a natural-language question directly using contexts retrieved from a RAG Engine Corpus, in a single agentic call. Use this when the user wants a final answer grounded in their corpus and does not need to inspect intermediate retrieved contexts. For raw retrieval use `retrieve_contexts` ; for augmenting a prompt before sending to a separate LLM step use `augment_prompt` .

Note: This tool is backed by a `v1beta1` RPC. Format: 'projects/{project\_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

**Parameters** \* `parent` : The parent resource, of the form `projects/{project}/locations/{location}` . \* `query` : The natural-language query to answer. \* `query.text` : The query text. \* `query.rag_retrieval_config` : Retrieval config (top\_k, filter, ranking) used to gather supporting contexts. \* `tools` : Optional list of tools the agentic retriever may use during answering.

The following sample demonstrate how to use `curl` to invoke the `ask_contexts` MCP tool.

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
    &quot;name&quot;: &quot;ask_contexts&quot;,
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

Agentic Retrieval Ask API for RAG. Request message for `VertexRagService.AskContexts` .

### AskContextsRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;query&quot;: {object (RagQuery)},&quot;tools&quot;: [{object (Tool)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .

`query`

` object ( RagQuery  ` )

Required. Single RAG retrieve query.

`tools[]`

` object ( Tool  ` )

Optional. The tools to use for AskContexts.

### RagQuery

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;similarityTopK&quot;: integer,&quot;ranking&quot;: {object (Ranking)},&quot;ragRetrievalConfig&quot;: {object (RagRetrievalConfig)},// Union field query can be only one of the following:&quot;text&quot;: string// End of list of possible types for union field query.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` similarityTopK (deprecated)  `

`integer`

> This item is deprecated\!

Optional. The number of contexts to retrieve.

` ranking (deprecated)  `

` object ( Ranking  ` )

> This item is deprecated\!

Optional. Configurations for hybrid search results ranking.

`ragRetrievalConfig`

` object ( RagRetrievalConfig  ` )

Optional. The retrieval config for the query.

Union field `query` . The query to retrieve contexts. Currently only text query is supported. `query` can be only one of the following:

`text`

`string`

Optional. The query in text format to get relevant contexts.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;functionDeclarations&quot;: [{object (FunctionDeclaration)}],&quot;retrieval&quot;: {object (Retrieval)},&quot;googleSearch&quot;: {object (GoogleSearch)},&quot;googleSearchRetrieval&quot;: {object (GoogleSearchRetrieval)},&quot;googleMaps&quot;: {object (GoogleMaps)},&quot;enterpriseWebSearch&quot;: {object (EnterpriseWebSearch)},&quot;parallelAiSearch&quot;: {object (ParallelAiSearch)},&quot;codeExecution&quot;: {object (CodeExecution)},&quot;urlContext&quot;: {object (UrlContext)},&quot;computerUse&quot;: {object (ComputerUse)}}</code></pre></td>
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

`parallelAiSearch`

` object ( ParallelAiSearch  ` )

Optional. If specified, Agent Platform will use Parallel.ai to search for information to answer user queries. The search results will be grounded on Parallel.ai and presented to the model for response generation

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

` enum ( Type  ` )

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

` enum ( PhishBlockThreshold  ` )

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

` enum ( Mode  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enableWidget&quot;: boolean,&quot;groundingTypes&quot;: {object (GroundingTypes)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` enableWidget (deprecated)  `

`boolean`

> This item is deprecated\!

Optional. Deprecated: The Google Maps contextual widget behavior in Grounding with Google Maps is being deprecated; this field is planned for removal and no longer has any effect once removed.

If true, include the widget context token in the response.

`groundingTypes`

` object ( GroundingTypes  ` )

Optional. Specifies the types of Google Maps grounding to enable. Defaults to `places` when unset.

### GroundingTypes

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;places&quot;: {object (Places)},&quot;routing&quot;: {object (Routing)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`places`

`object ( Places` )

Optional. Enables grounding with Google Maps Places. This is the default grounding type when no `GroundingTypes` are specified.

`routing`

`object ( Routing` )

Optional. Enables grounding with Google Maps Routing APIs (ComputeRoutes and SearchAlongRoute).

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

` enum ( PhishBlockThreshold  ` )

Optional. Sites with confidence level chosen & above this value will be blocked from the search results.

### ParallelAiSearch

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
  &quot;apiKey&quot;: string,
  &quot;customConfigs&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`apiKey`

`string`

Optional. The API key for ParallelAiSearch. If an API key is not provided, the system will attempt to verify access by checking for an active Parallel.ai subscription through the Google Cloud Marketplace. See <https://docs.parallel.ai/search/search-quickstart> for more details.

`customConfigs`

` object ( Struct  ` format)

Optional. Custom configs for ParallelAiSearch. This field can be used to pass any parameter from the Parallel.ai Search API. See the Parallel.ai documentation for the full list of available parameters and their usage: <https://docs.parallel.ai/api-reference/search-beta/search> Currently only `source_policy` , `excerpts` , `max_results` , `mode` , `fetch_policy` can be set via this field. For example: { "source\_policy": { "include\_domains": \["google.com", "wikipedia.org"\], "exclude\_domains": \["example.com"\] }, "fetch\_policy": { "max\_age\_seconds": 3600 } }

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

` enum ( Environment  ` )

Required. The environment being operated.

`excludedPredefinedFunctions[]`

`string`

Optional. By default, [predefined functions](https://cloud.google.com/vertex-ai/generative-ai/docs/computer-use#supported-actions) are included in the final model call. Some of them can be explicitly excluded from being automatically included. This can serve two purposes: 1. Using a more restricted / different action space. 2. Improving the definitions / instructions of predefined functions.

### Type

Type contains the list of OpenAPI data types as defined by <https://swagger.io/docs/specification/data-models/data-types/>

Enums

`TYPE_UNSPECIFIED`

Not specified, should not be used.

`STRING`

OpenAPI string type

`NUMBER`

OpenAPI number type

`INTEGER`

OpenAPI integer type

`BOOLEAN`

OpenAPI boolean type

`ARRAY`

OpenAPI array type

`OBJECT`

OpenAPI object type

`NULL`

Null type

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

Enums

`NULL_VALUE`

Null value.

### PhishBlockThreshold

These are available confidence level user can set to block malicious urls with chosen confidence and above. For understanding different confidence of webrisk, please refer to <https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel>

Enums

`PHISH_BLOCK_THRESHOLD_UNSPECIFIED`

Defaults to unspecified.

`BLOCK_LOW_AND_ABOVE`

Blocks Low and above confidence URL that is risky.

`BLOCK_MEDIUM_AND_ABOVE`

Blocks Medium and above confidence URL that is risky.

`BLOCK_HIGH_AND_ABOVE`

Blocks High and above confidence URL that is risky.

`BLOCK_HIGHER_AND_ABOVE`

Blocks Higher and above confidence URL that is risky.

`BLOCK_VERY_HIGH_AND_ABOVE`

Blocks Very high and above confidence URL that is risky.

`BLOCK_ONLY_EXTREMELY_HIGH`

Blocks Extremely high confidence URL that is risky.

### Mode

The mode of the predictor to be used in dynamic retrieval.

Enums

`MODE_UNSPECIFIED`

Always trigger retrieval.

`MODE_DYNAMIC`

Run retrieval only when system decides it is necessary.

### Environment

Represents the environment being operated, such as a web browser.

Enums

`ENVIRONMENT_UNSPECIFIED`

Defaults to browser.

`ENVIRONMENT_BROWSER`

Operates in a web browser.

## Output Schema

Response message for `VertexRagService.AskContexts` .

### AskContextsResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;response&quot;: string,&quot;contexts&quot;: {object (RagContexts)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`response`

`string`

The Retrieval Response.

`contexts`

` object ( RagContexts  ` )

The contexts of the query.

### RagContexts

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contexts&quot;: [{object (Context)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`contexts[]`

` object ( Context  ` )

All its contexts.

### Context

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceUri&quot;: string,&quot;sourceDisplayName&quot;: string,&quot;text&quot;: string,&quot;distance&quot;: number,&quot;sparseDistance&quot;: number,&quot;chunk&quot;: {object (RagChunk)},// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`sourceUri`

`string`

If the file is imported from Cloud Storage or Google Drive, source\_uri will be original file URI in Cloud Storage or Google Drive; if file is uploaded, source\_uri will be file display name.

`sourceDisplayName`

`string`

The file display name.

`text`

`string`

The text chunk.

` distance (deprecated)  `

`number`

> This item is deprecated\!

The distance between the query dense embedding vector and the context text vector.

` sparseDistance (deprecated)  `

`number`

> This item is deprecated\!

The distance between the query sparse embedding vector and the context text vector.

`chunk`

` object ( RagChunk  ` )

Context of the retrieved chunk.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

According to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the context and its range depends on the metric type.

For example, if the metric type is COSINE\_DISTANCE, it represents the distance between the query and the context. The larger the distance, the less relevant the context is to the query. The range is \[0, 2\], while 0 means the most relevant and 2 means the least relevant.

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

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
