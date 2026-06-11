---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.cachedContents
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.cachedContents
title: 'REST Resource: projects.locations.cachedContents'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: CachedContent

A resource used in LLM queries for users to explicitly specify what to cache and how to cache.

Fields

`name` `string`

Immutable. Identifier. The server-generated resource name of the cached content Format: projects/{project}/locations/{location}/cachedContents/{cachedContent}

`displayName` `string`

Optional. Immutable. The user-generated meaningful display name of the cached content.

`model` `string`

Immutable. The name of the `Model` to use for cached content. Currently, only the published Gemini base models are supported, in form of projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL}

`systemInstruction` ` object ( Content  ` )

Optional. Input only. Immutable. Developer set system instruction. Currently, text only

`contents[]` ` object ( Content  ` )

Optional. Input only. Immutable. The content to cache

`tools[]` ` object ( Tool  ` )

Optional. Input only. Immutable. A list of `Tools` the model may use to generate the next response

`toolConfig` ` object ( ToolConfig  ` )

Optional. Input only. Immutable. Tool config. This config is shared for all tools

`createTime` ` string ( Timestamp  ` format)

Output only. Creation time of the cache entry.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. When the cache entry was last updated in UTC time.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`usageMetadata` ` object ( UsageMetadata  ` )

Output only. metadata on the usage of the cached content.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Input only. Immutable. Customer-managed encryption key spec for a `CachedContent` . If set, this `CachedContent` and all its sub-resources will be secured by this key.

`expiration` `Union type`

Expiration time of the cached content. `expiration` can be only one of the following:

`expireTime` ` string ( Timestamp  ` format)

timestamp of when this resource is considered expired. This is *always* provided on output, regardless of what was sent on input.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`ttl` ` string ( Duration  ` format)

Input only. The TTL for this resource. The expiration time is computed: now + TTL.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;model&quot;: string,&quot;systemInstruction&quot;: {object (Content)},&quot;contents&quot;: [{object (Content)}],&quot;tools&quot;: [{object (Tool)}],&quot;toolConfig&quot;: {object (ToolConfig)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;usageMetadata&quot;: {object (UsageMetadata)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},// expiration&quot;expireTime&quot;: string,&quot;ttl&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Tool

Tool details that the model may use to generate response.

A `Tool` is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model. A Tool object should contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval or GoogleSearchRetrieval).

Fields

`functionDeclarations[]` ` object ( FunctionDeclaration  ` )

Optional. Function tool type. One or more function declarations to be passed to the model along with the current user query. Model may decide to call a subset of these functions by populating `  FunctionCall  ` in the response. user should provide a `  FunctionResponse  ` for each function call in the next turn. Based on the function responses, Model will generate the final response back to the user. Maximum 512 function declarations can be provided.

`retrieval` ` object ( Retrieval  ` )

Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation.

`googleSearch` ` object ( GoogleSearch  ` )

Optional. GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

` googleSearchRetrieval (deprecated)  ` ` object ( GoogleSearchRetrieval  ` )

> Optional. The `google_search_retrieval` field is deprecated. Use `google_search` instead. This field is for use with Gemini 1.5 models; `google_search` is used for Gemini 2.0 and newer models.

Optional. Specialized retrieval tool that is powered by Google Search.

`googleMaps` ` object ( GoogleMaps  ` )

Optional. GoogleMaps tool type. Tool to support Google Maps in Model.

`enterpriseWebSearch` ` object ( EnterpriseWebSearch  ` )

Optional. Tool to support searching public web data, powered by Agent Platform Search and Sec4 compliance.

`parallelAiSearch` ` object ( ParallelAiSearch  ` )

Optional. If specified, Agent Platform will use Parallel.ai to search for information to answer user queries. The search results will be grounded on Parallel.ai and presented to the model for response generation

`codeExecution` ` object ( CodeExecution  ` )

Optional. CodeExecution tool type. Enables the model to execute code as part of generation.

`urlContext` ` object ( UrlContext  ` )

Optional. Tool to support URL context retrieval.

`computerUse` ` object ( ComputerUse  ` )

Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations.

<table>
<colgroup>
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

## FunctionDeclaration

Structured representation of a function declaration as defined by the [OpenAPI 3.0 specification](https://spec.openapis.org/oas/v3.0.3) . Included in this declaration are the function name, description, parameters and response type. This FunctionDeclaration is a representation of a block of code that can be used as a `Tool` by the model and executed by the client.

Fields

`name` `string`

Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots, colons and dashes, with a maximum length of 128.

`description` `string`

Optional. description and purpose of the function. Model uses it to decide how and whether to call the function.

`parameters` ` object ( Schema  ` )

Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1

`parametersJsonSchema` ` value ( Value  ` format)

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

`response` ` object ( Schema  ` )

Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function.

`responseJsonSchema` ` value ( Value  ` format)

Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function.

This field is mutually exclusive with `response` .

<table>
<colgroup>
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

## Retrieval

Defines a retrieval tool that model can call to access external knowledge.

Fields

` disableAttribution (deprecated)  ` `boolean`

> This item is deprecated\!

Optional. Deprecated. This option is no longer supported.

`source` `Union type`

The source of the retrieval. `source` can be only one of the following:

`vertexAiSearch` ` object ( VertexAISearch  ` )

Set to use data source powered by Agent Platform Search.

`vertexRagStore` ` object ( VertexRagStore  ` )

Set to use data source powered by Vertex RAG store. user data is uploaded via the VertexRagDataService.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;disableAttribution&quot;: boolean,// source&quot;vertexAiSearch&quot;: {object (VertexAISearch)},&quot;vertexRagStore&quot;: {object (VertexRagStore)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## VertexAISearch

Retrieve from Agent Platform Search datastore or engine for grounding. datastore and engine are mutually exclusive. See <https://cloud.google.com/products/agent-builder>

Fields

`datastore` `string`

Optional. Fully-qualified Agent Platform Search data store resource id. Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`

`engine` `string`

Optional. Fully-qualified Agent Platform Search engine resource id. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}`

`maxResults` `integer`

Optional. Number of search results to return per query. The default value is 10. The maximumm allowed value is 10.

`filter` `string`

Optional. Filter strings to be passed to the search API.

`dataStoreSpecs[]` ` object ( DataStoreSpec  ` )

Specifications that define the specific DataStores to be searched, along with configurations for those data stores. This is only considered for Engines with multiple data stores. It should only be set if engine is used.

<table>
<colgroup>
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

## DataStoreSpec

Define data stores within engine to filter on in a search call and configurations for those data stores. For more information, see <https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec>

Fields

`dataStore` `string`

Full resource name of DataStore, such as Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`

`filter` `string`

Optional. Filter specification to filter documents in the data store specified by dataStore field. For more information on filtering, see [Filtering](https://cloud.google.com/generative-ai-app-builder/docs/filter-search-metadata)

<table>
<colgroup>
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

## VertexRagStore

Retrieve from Vertex RAG Store for grounding.

Fields

`ragResources[]` ` object ( RagResource  ` )

Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.

`ragRetrievalConfig` ` object ( RagRetrievalConfig  ` )

Optional. The retrieval config for the Rag query.

` similarityTopK (deprecated)  ` `integer`

> This item is deprecated\!

Optional. Number of top k results to return from the selected corpora.

` vectorDistanceThreshold (deprecated)  ` `number`

> This item is deprecated\!

Optional. Only return results with vector distance smaller than the threshold.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragResources&quot;: [{object (RagResource)}],&quot;ragRetrievalConfig&quot;: {object (RagRetrievalConfig)},&quot;similarityTopK&quot;: integer,&quot;vectorDistanceThreshold&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## RagResource

The definition of the Rag resource.

Fields

`ragCorpus` `string`

Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

`ragFileIds[]` `string`

Optional. ragFileId. The files should be in the same ragCorpus set in ragCorpus field.

<table>
<colgroup>
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

## RagRetrievalConfig

Specifies the context retrieval config.

Fields

`topK` `integer`

Optional. The number of contexts to retrieve.

`filter` ` object ( Filter  ` )

Optional. Config for filters.

`ranking` ` object ( Ranking  ` )

Optional. Config for ranking and reranking.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;topK&quot;: integer,&quot;filter&quot;: {object (Filter)},&quot;ranking&quot;: {object (Ranking)}}</code></pre></td>
</tr>
</tbody>
</table>

## Filter

Config for filters.

Fields

`metadataFilter` `string`

Optional. String for metadata filtering.

`vector_db_threshold` `Union type`

Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. `vector_db_threshold` can be only one of the following:

`vectorDistanceThreshold` `number`

Optional. Only returns contexts with vector distance smaller than the threshold.

`vectorSimilarityThreshold` `number`

Optional. Only returns contexts with vector similarity larger than the threshold.

<table>
<colgroup>
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
  &quot;metadataFilter&quot;: string,

  // vector_db_threshold
  &quot;vectorDistanceThreshold&quot;: number,
  &quot;vectorSimilarityThreshold&quot;: number
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## Ranking

Config for ranking and reranking.

Fields

`ranking_config` `Union type`

Config options for ranking. Currently only Rank Service is supported. `ranking_config` can be only one of the following:

`rankService` ` object ( RankService  ` )

Optional. Config for Rank service.

`llmRanker` ` object ( LlmRanker  ` )

Optional. Config for LlmRanker.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// ranking_config&quot;rankService&quot;: {object (RankService)},&quot;llmRanker&quot;: {object (LlmRanker)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## RankService

Config for Rank service.

Fields

`modelName` `string`

Optional. The model name of the rank service. Format: `semantic-ranker-512@latest`

<table>
<colgroup>
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
  &quot;modelName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## LlmRanker

Config for LlmRanker.

Fields

`modelName` `string`

Optional. The model name used for ranking. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models) .

<table>
<colgroup>
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
  &quot;modelName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## GoogleSearch

GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

Fields

`excludeDomains[]` `string`

Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: \["amazon.com", "facebook.com"\].

`blockingConfidence` ` enum ( PhishBlockThreshold  ` )

Optional. Sites with confidence level chosen & above this value will be blocked from the search results.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;excludeDomains&quot;: [string],&quot;blockingConfidence&quot;: enum (PhishBlockThreshold)}</code></pre></td>
</tr>
</tbody>
</table>

## PhishBlockThreshold

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

## GoogleSearchRetrieval

Tool to retrieve public web data for grounding, powered by Google.

Fields

`dynamicRetrievalConfig` ` object ( DynamicRetrievalConfig  ` )

Specifies the dynamic retrieval configuration for the given source.

<table>
<colgroup>
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

## DynamicRetrievalConfig

Describes the options to customize dynamic retrieval.

Fields

`mode` ` enum ( Mode  ` )

The mode of the predictor to be used in dynamic retrieval.

`dynamicThreshold` `number`

Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mode&quot;: enum (Mode),&quot;dynamicThreshold&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## Mode

The mode of the predictor to be used in dynamic retrieval.

Enums

`MODE_UNSPECIFIED`

Always trigger retrieval.

`MODE_DYNAMIC`

Run retrieval only when system decides it is necessary.

## GoogleMaps

Tool to retrieve public maps data for grounding, powered by Google.

Fields

` enableWidget (deprecated)  ` `boolean`

> This item is deprecated\!

Optional. Deprecated: The Google Maps contextual widget behavior in Grounding with Google Maps is being deprecated; this field is planned for removal and no longer has any effect once removed.

If true, include the widget context token in the response.

<table>
<colgroup>
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

## EnterpriseWebSearch

Tool to search public web data, powered by Agent Platform Search and Sec4 compliance.

Fields

`excludeDomains[]` `string`

Optional. List of domains to be excluded from the search results. The default limit is 2000 domains.

`blockingConfidence` ` enum ( PhishBlockThreshold  ` )

Optional. Sites with confidence level chosen & above this value will be blocked from the search results.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;excludeDomains&quot;: [string],&quot;blockingConfidence&quot;: enum (PhishBlockThreshold)}</code></pre></td>
</tr>
</tbody>
</table>

## ParallelAiSearch

ParallelAiSearch tool type. A tool that uses the Parallel.ai search engine for grounding.

Fields

`apiKey` `string`

Optional. The API key for ParallelAiSearch. If an API key is not provided, the system will attempt to verify access by checking for an active Parallel.ai subscription through the Google Cloud Marketplace. See <https://docs.parallel.ai/search/search-quickstart> for more details.

`customConfigs` ` object ( Struct  ` format)

Optional. Custom configs for ParallelAiSearch. This field can be used to pass any parameter from the Parallel.ai Search API. See the Parallel.ai documentation for the full list of available parameters and their usage: <https://docs.parallel.ai/api-reference/search-beta/search> Currently only `source_policy` , `excerpts` , `maxResults` , `mode` , `fetch_policy` can be set via this field. For example: { "source\_policy": { "include\_domains": \["google.com", "wikipedia.org"\], "excludeDomains": \["example.com"\] }, "fetch\_policy": { "max\_age\_seconds": 3600 } }

<table>
<colgroup>
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

## CodeExecution

This type has no fields.

Tool that executes code generated by the model, and automatically returns the result to the model.

See also `  ExecutableCode  ` and `  CodeExecutionResult  ` , which are input and output to this tool.

## UrlContext

This type has no fields.

Tool to support URL context.

## ComputerUse

Tool to support computer use.

Fields

`environment` ` enum ( Environment  ` )

Required. The environment being operated.

`excludedPredefinedFunctions[]` `string`

Optional. By default, [predefined functions](https://cloud.google.com/vertex-ai/generative-ai/docs/computer-use#supported-actions) are included in the final model call. Some of them can be explicitly excluded from being automatically included. This can serve two purposes: 1. Using a more restricted / different action space. 2. Improving the definitions / instructions of predefined functions.

<table>
<colgroup>
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

## Environment

Represents the environment being operated, such as a web browser.

Enums

`ENVIRONMENT_UNSPECIFIED`

Defaults to browser.

`ENVIRONMENT_BROWSER`

Operates in a web browser.

## ToolConfig

Tool config. This config is shared for all tools provided in the request.

Fields

`functionCallingConfig` ` object ( FunctionCallingConfig  ` )

Optional. Function calling config.

`retrievalConfig` ` object ( RetrievalConfig  ` )

Optional. Retrieval config.

<table>
<colgroup>
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

## FunctionCallingConfig

Function calling config.

Fields

`mode` ` enum ( Mode  ` )

Optional. Function calling mode.

`allowedFunctionNames[]` `string`

Optional. Function names to call. Only set when the Mode is ANY. Function names should match `  FunctionDeclaration.name  ` . With mode set to ANY, model will predict a function call from the set of function names provided.

`streamFunctionCallArguments` `boolean`

Optional. When set to true, arguments of a single function call will be streamed out in multiple parts/contents/responses. Partial parameter results will be returned in the `FunctionCall.partial_args` field.

<table>
<colgroup>
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

## Mode

Function calling mode.

Enums

`MODE_UNSPECIFIED`

Unspecified function calling mode. This value should not be used.

`AUTO`

Default model behavior, model decides to predict either function calls or natural language response.

`ANY`

Model is constrained to always predicting function calls only. If "allowedFunctionNames" are set, the predicted function calls will be limited to any one of "allowedFunctionNames", else the predicted function calls will be any one of the provided "functionDeclarations".

`NONE`

Model will not predict any function calls. Model behavior is same as when not passing any function declarations.

`VALIDATED`

Model is constrained to predict either function calls or natural language response. If "allowedFunctionNames" are set, the predicted function calls will be limited to any one of "allowedFunctionNames", else the predicted function calls will be any one of the provided "functionDeclarations".

## RetrievalConfig

Retrieval config.

Fields

`latLng` ` object ( LatLng  ` )

The location of the user.

`languageCode` `string`

The language code of the user.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;latLng&quot;: {object (LatLng)},&quot;languageCode&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## UsageMetadata

metadata on the usage of the cached content.

Fields

`totalTokenCount` `integer`

Total number of tokens that the cached content consumes.

`textCount` `integer`

Number of text characters.

`imageCount` `integer`

Number of images.

`videoDurationSeconds` `integer`

Duration of video in seconds.

`audioDurationSeconds` `integer`

Duration of audio in seconds.

<table>
<colgroup>
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
  &quot;totalTokenCount&quot;: integer,
  &quot;textCount&quot;: integer,
  &quot;imageCount&quot;: integer,
  &quot;videoDurationSeconds&quot;: integer,
  &quot;audioDurationSeconds&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates cached content, this call will initialize the cached content in the data storage, and users need to pay for the cache data storage.

### `            delete           `

Deletes cached content

### `            get           `

Gets cached content configurations

### `            list           `

Lists cached contents in a project

### `            patch           `

Updates cached content configurations
