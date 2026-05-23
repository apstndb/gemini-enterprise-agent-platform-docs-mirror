---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample
title: GeminiExample
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Format for Gemini examples used for Vertex Multimodal datasets.

Fields

`model` `string`

Optional. The fully qualified name of the publisher model or tuned model endpoint to use.

Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`

Tuned model endpoint format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

`contents[]` ` object ( Content  ` )

Required. The content of the current conversation with the model.

For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request.

`cachedContent` `string`

Optional. The name of the cached content used as context to serve the prediction. Note: only used in explicit caching, where users can have control over caching (e.g. what content to cache) and enjoy guaranteed cost savings. Format: `projects/{project}/locations/{location}/cachedContents/{cachedContent}`

`tools[]` ` object ( Tool  ` )

Optional. A list of `Tools` the model may use to generate the next response.

A `Tool` is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model.

`toolConfig` ` object ( ToolConfig  ` )

Optional. Tool config. This config is shared for all tools provided in the request.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only.

label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. label values are optional. label keys must start with a letter.

`safetySettings[]` ` object ( SafetySetting  ` )

Optional. Per request settings for blocking unsafe content. Enforced on GenerateContentResponse.candidates.

`modelArmorConfig` ` object ( ModelArmorConfig  ` )

Optional. Settings for prompt and response sanitization using the Model Armor service. If supplied, safetySettings must not be supplied.

`generationConfig` ` object ( GenerationConfig  ` )

Optional. Generation config.

`systemInstruction` ` object ( Content  ` )

Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;model&quot;: string,&quot;contents&quot;: [{object (Content)}],&quot;cachedContent&quot;: string,&quot;tools&quot;: [{object (Tool)}],&quot;toolConfig&quot;: {object (ToolConfig)},&quot;labels&quot;: {string: string,...},&quot;safetySettings&quot;: [{object (SafetySetting)}],&quot;modelArmorConfig&quot;: {object (ModelArmorConfig)},&quot;generationConfig&quot;: {object (GenerationConfig)},&quot;systemInstruction&quot;: {object (Content)}}</code></pre></td>
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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;functionDeclarations&quot;: [{object (FunctionDeclaration)}],&quot;retrieval&quot;: {object (Retrieval)},&quot;googleSearch&quot;: {object (GoogleSearch)},&quot;googleSearchRetrieval&quot;: {object (GoogleSearchRetrieval)},&quot;googleMaps&quot;: {object (GoogleMaps)},&quot;enterpriseWebSearch&quot;: {object (EnterpriseWebSearch)},&quot;codeExecution&quot;: {object (CodeExecution)},&quot;urlContext&quot;: {object (UrlContext)},&quot;computerUse&quot;: {object (ComputerUse)}}</code></pre></td>
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

` ragCorpora[] (deprecated)  ` `string`

> This item is deprecated\!

Optional. Deprecated. Please use ragResources instead.

`ragResources[]` ` object ( RagResource  ` )

Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.

`ragRetrievalConfig` ` object ( RagRetrievalConfig  ` )

Optional. The retrieval config for the Rag query.

`storeContext` `boolean`

Optional. Currently only supported for Gemini Multimodal Live API.

In Gemini Multimodal Live API, if `storeContext` bool is specified, Gemini will leverage it to automatically memorize the interactions between the client and Gemini, and retrieve context when needed to augment the response generation for users' ongoing and future interactions.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragCorpora&quot;: [string],&quot;ragResources&quot;: [{object (RagResource)}],&quot;ragRetrievalConfig&quot;: {object (RagRetrievalConfig)},&quot;storeContext&quot;: boolean,&quot;similarityTopK&quot;: integer,&quot;vectorDistanceThreshold&quot;: number}</code></pre></td>
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

`hybridSearch` ` object ( HybridSearch  ` )

Optional. Config for Hybrid Search.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;topK&quot;: integer,&quot;hybridSearch&quot;: {object (HybridSearch)},&quot;filter&quot;: {object (Filter)},&quot;ranking&quot;: {object (Ranking)}}</code></pre></td>
</tr>
</tbody>
</table>

## HybridSearch

Config for Hybrid Search.

Fields

`alpha` `number`

Optional. Alpha value controls the weight between dense and sparse vector search results. The range is \[0, 1\], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally.

<table>
<colgroup>
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
  &quot;alpha&quot;: number
}</code></pre></td>
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

## GoogleMaps

Tool to retrieve public maps data for grounding, powered by Google.

Fields

`enableWidget` `boolean`

Optional. If true, include the widget context token in the response.

<table>
<colgroup>
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

## LatLng

An object that represents a latitude/longitude pair. This is expressed as a pair of doubles to represent degrees latitude and degrees longitude. Unless specified otherwise, this object must conform to the [WGS84 standard](https://en.wikipedia.org/wiki/World_Geodetic_System#1984_version) . Values must be within normalized ranges.

Fields

`latitude` `number`

The latitude in degrees. It must be in the range \[-90.0, +90.0\].

`longitude` `number`

The longitude in degrees. It must be in the range \[-180.0, +180.0\].

<table>
<colgroup>
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

## SafetySetting

A safety setting that affects the safety-blocking behavior.

A `SafetySetting` consists of a harm `category` and a `threshold` for that category.

Fields

`category` ` enum ( HarmCategory  ` )

Required. The harm category to be blocked.

`threshold` ` enum ( HarmBlockThreshold  ` )

Required. The threshold for blocking content. If the harm probability exceeds this threshold, the content will be blocked.

`method` ` enum ( HarmBlockMethod  ` )

Optional. The method for blocking content. If not specified, the default behavior is to use the probability score.

<table>
<colgroup>
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

## ModelArmorConfig

Configuration for Model Armor.

Model Armor is a Google Cloud service that provides safety and security filtering for prompts and responses. It helps protect your AI applications from risks such as harmful content, sensitive data leakage, and prompt injection attacks.

Fields

`promptTemplateName` `string`

Optional. The resource name of the Model Armor template to use for prompt screening.

A Model Armor template is a set of customized filters and thresholds that define how Model Armor screens content. If specified, Model Armor will use this template to check the user's prompt for safety and security risks before it is sent to the model.

The name must be in the format `projects/{project}/locations/{location}/templates/{template}` .

`responseTemplateName` `string`

Optional. The resource name of the Model Armor template to use for response screening.

A Model Armor template is a set of customized filters and thresholds that define how Model Armor screens content. If specified, Model Armor will use this template to check the model's response for safety and security risks before it is returned to the user.

The name must be in the format `projects/{project}/locations/{location}/templates/{template}` .

<table>
<colgroup>
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

## GenerationConfig

Configuration for content generation.

This message contains all the parameters that control how the model generates content. It allows you to influence the randomness, length, and structure of the output.

Fields

`stopSequences[]` `string`

Optional. A list of character sequences that will stop the model from generating further tokens. If a stop sequence is generated, the output will end at that point. This is useful for controlling the length and structure of the output. For example, you can use \["\\n", "\#\#\#"\] to stop generation at a new line or a specific marker.

`responseMimeType` `string`

Optional. The IANA standard MIME type of the response. The model will generate output that conforms to this MIME type. Supported values include 'text/plain' (default) and 'application/json'. The model needs to be prompted to output the appropriate response type, otherwise the behavior is undefined.

`responseModalities[]` ` enum ( Modality  ` )

Optional. The modalities of the response. The model will generate a response that includes all the specified modalities. For example, if this is set to `[TEXT, IMAGE]` , the response will include both text and an image.

`thinkingConfig` ` object ( ThinkingConfig  ` )

Optional. Configuration for thinking features. An error will be returned if this field is set for models that don't support thinking.

` modelConfig (deprecated)  ` ` object ( ModelConfig  ` )

> Optional. The `model_config` field is deprecated and is not supported anymore. Use `routing_config` instead.

Optional. Config for model selection.

`temperature` `number`

Optional. Controls the randomness of the output. A higher temperature results in more creative and diverse responses, while a lower temperature makes the output more predictable and focused. The valid range is (0.0, 2.0\].

`topP` `number`

Optional. Specifies the nucleus sampling threshold. The model considers only the smallest set of tokens whose cumulative probability is at least `topP` . This helps generate more diverse and less repetitive responses. For example, a `topP` of 0.9 means the model considers tokens until the cumulative probability of the tokens to select from reaches 0.9. It's recommended to adjust either temperature or `topP` , but not both.

`topK` `number`

Optional. Specifies the top-k sampling threshold. The model considers only the top k most probable tokens for the next token. This can be useful for generating more coherent and less random text. For example, a `topK` of 40 means the model will choose the next word from the 40 most likely words.

`candidateCount` `integer`

Optional. The number of candidate responses to generate.

A higher `candidateCount` can provide more options to choose from, but it also consumes more resources. This can be useful for generating a variety of responses and selecting the best one.

`maxOutputTokens` `integer`

Optional. The maximum number of tokens to generate in the response.

A token is approximately four characters. The default value varies by model. This parameter can be used to control the length of the generated text and prevent overly long responses.

`responseLogprobs` `boolean`

Optional. If set to true, the log probabilities of the output tokens are returned.

log probabilities are the logarithm of the probability of a token appearing in the output. A higher log probability means the token is more likely to be generated. This can be useful for analyzing the model's confidence in its own output and for debugging.

`logprobs` `integer`

Optional. The number of top log probabilities to return for each token.

This can be used to see which other tokens were considered likely candidates for a given position. A higher value will return more options, but it will also increase the size of the response.

`presencePenalty` `number`

Optional. Penalizes tokens that have already appeared in the generated text. A positive value encourages the model to generate more diverse and less repetitive text. Valid values can range from \[-2.0, 2.0\].

`frequencyPenalty` `number`

Optional. Penalizes tokens based on their frequency in the generated text. A positive value helps to reduce the repetition of words and phrases. Valid values can range from \[-2.0, 2.0\].

`seed` `integer`

Optional. A seed for the random number generator.

By setting a seed, you can make the model's output mostly deterministic. For a given prompt and parameters (like temperature, topP, etc.), the model will produce the same response every time. However, it's not a guaranteed absolute deterministic behavior. This is different from parameters like `temperature` , which control the *level* of randomness. `seed` ensures that the "random" choices the model makes are the same on every run, making it essential for testing and ensuring reproducible results.

`responseSchema` ` object ( Schema  ` )

Optional. Lets you to specify a schema for the model's response, ensuring that the output conforms to a particular structure. This is useful for generating structured data such as JSON. The schema is a subset of the [OpenAPI 3.0 schema object](https://spec.openapis.org/oas/v3.0.3#schema) object.

When this field is set, you must also set the `responseMimeType` to `application/json` .

`responseJsonSchema` ` value ( Value  ` format)

Optional. When this field is set, `responseSchema` must be omitted and `responseMimeType` must be set to `application/json` .

`routingConfig` ` object ( RoutingConfig  ` )

Optional. Routing configuration.

`audioTimestamp` `boolean`

Optional. If enabled, audio timestamps will be included in the request to the model. This can be useful for synchronizing audio with other modalities in the response.

`mediaResolution` ` enum ( MediaResolution  ` )

Optional. The token resolution at which input media content is sampled. This is used to control the trade-off between the quality of the response and the number of tokens used to represent the media. A higher resolution allows the model to perceive more detail, which can lead to a more nuanced response, but it will also use more tokens. This does not affect the image dimensions sent to the model.

`speechConfig` ` object ( SpeechConfig  ` )

Optional. The speech generation config.

`enableAffectiveDialog` `boolean`

Optional. If enabled, the model will detect emotions and adapt its responses accordingly. For example, if the model detects that the user is frustrated, it may provide a more empathetic response.

`imageConfig` ` object ( ImageConfig  ` )

Optional. Config for image generation features.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stopSequences&quot;: [string],&quot;responseMimeType&quot;: string,&quot;responseModalities&quot;: [enum (Modality)],&quot;thinkingConfig&quot;: {object (ThinkingConfig)},&quot;modelConfig&quot;: {object (ModelConfig)},&quot;temperature&quot;: number,&quot;topP&quot;: number,&quot;topK&quot;: number,&quot;candidateCount&quot;: integer,&quot;maxOutputTokens&quot;: integer,&quot;responseLogprobs&quot;: boolean,&quot;logprobs&quot;: integer,&quot;presencePenalty&quot;: number,&quot;frequencyPenalty&quot;: number,&quot;seed&quot;: integer,&quot;responseSchema&quot;: {object (Schema)},&quot;responseJsonSchema&quot;: value,&quot;routingConfig&quot;: {object (RoutingConfig)},&quot;audioTimestamp&quot;: boolean,&quot;mediaResolution&quot;: enum (MediaResolution),&quot;speechConfig&quot;: {object (SpeechConfig)},&quot;enableAffectiveDialog&quot;: boolean,&quot;imageConfig&quot;: {object (ImageConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## RoutingConfig

The configuration for routing the request to a specific model. This can be used to control which model is used for the generation, either automatically or by specifying a model name.

Fields

`routing_config` `Union type`

The routing mode for the request. `routing_config` can be only one of the following:

`autoMode` ` object ( AutoRoutingMode  ` )

In this mode, the model is selected automatically based on the content of the request.

`manualMode` ` object ( ManualRoutingMode  ` )

In this mode, the model is specified manually.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// routing_config&quot;autoMode&quot;: {object (AutoRoutingMode)},&quot;manualMode&quot;: {object (ManualRoutingMode)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## AutoRoutingMode

The configuration for automated routing.

When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

Fields

`modelRoutingPreference` ` enum ( ModelRoutingPreference  ` )

The model routing preference.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelRoutingPreference&quot;: enum (ModelRoutingPreference)}</code></pre></td>
</tr>
</tbody>
</table>

## ManualRoutingMode

The configuration for manual routing.

When manual routing is specified, the model will be selected based on the model name provided.

Fields

`modelName` `string`

The name of the model to use. Only public LLM models are accepted.

<table>
<colgroup>
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

## SpeechConfig

Configuration for speech generation.

Fields

`voiceConfig` ` object ( VoiceConfig  ` )

The configuration for the voice to use.

`languageCode` `string`

Optional. The language code (ISO 639-1) for the speech synthesis.

`multiSpeakerVoiceConfig` ` object ( MultiSpeakerVoiceConfig  ` )

The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voiceConfig` .

<table>
<colgroup>
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

## VoiceConfig

Configuration for a voice.

Fields

`voice_config` `Union type`

The configuration for the speaker to use. `voice_config` can be only one of the following:

`prebuiltVoiceConfig` ` object ( PrebuiltVoiceConfig  ` )

The configuration for a prebuilt voice.

`replicatedVoiceConfig` ` object ( ReplicatedVoiceConfig  ` )

Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// voice_config&quot;prebuiltVoiceConfig&quot;: {object (PrebuiltVoiceConfig)},&quot;replicatedVoiceConfig&quot;: {object (ReplicatedVoiceConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## PrebuiltVoiceConfig

Configuration for a prebuilt voice.

Fields

`voiceName` `string`

The name of the prebuilt voice to use.

<table>
<colgroup>
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
  &quot;voiceName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ReplicatedVoiceConfig

The configuration for the replicated voice to use.

Fields

`mimeType` `string`

Optional. The mimetype of the voice sample. The only currently supported value is `audio/wav` . This represents 16-bit signed little-endian wav data, with a 24kHz sampling rate. `mimeType` will default to `audio/wav` if not set.

`voiceSampleAudio` `string ( bytes format)`

Optional. The sample of the custom voice.

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
  &quot;mimeType&quot;: string,
  &quot;voiceSampleAudio&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## MultiSpeakerVoiceConfig

Configuration for a multi-speaker text-to-speech request.

Fields

`speakerVoiceConfigs[]` ` object ( SpeakerVoiceConfig  ` )

Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided.

<table>
<colgroup>
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

## SpeakerVoiceConfig

Configuration for a single speaker in a multi-speaker setup.

Fields

`speaker` `string`

Required. The name of the speaker. This should be the same as the speaker name used in the prompt.

`voiceConfig` ` object ( VoiceConfig  ` )

Required. The configuration for the voice of this speaker.

<table>
<colgroup>
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

## ThinkingConfig

Configuration for the model's thinking features.

"Thinking" is a process where the model breaks down a complex task into smaller, manageable steps. This allows the model to reason about the task, plan its approach, and execute the plan to generate a high-quality response.

Fields

`includeThoughts` `boolean`

Optional. If true, the model will include its thoughts in the response. "Thoughts" are the intermediate steps the model takes to arrive at the final response. They can provide insights into the model's reasoning process and help with debugging. If this is true, thoughts are returned only when available.

`thinkingBudget` `integer`

Optional. The token budget for the model's thinking process. The model will make a best effort to stay within this budget. This can be used to control the trade-off between response quality and latency.

`thinkingLevel` ` enum ( ThinkingLevel  ` )

Optional. The number of thoughts tokens that the model should generate.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;includeThoughts&quot;: boolean,&quot;thinkingBudget&quot;: integer,&quot;thinkingLevel&quot;: enum (ThinkingLevel)}</code></pre></td>
</tr>
</tbody>
</table>

## ModelConfig

Config for model selection.

Fields

`featureSelectionPreference` ` enum ( FeatureSelectionPreference  ` )

Required. feature selection preference.

<table>
<colgroup>
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

## ImageConfig

Configuration for image generation.

This message allows you to control various aspects of image generation, such as the output format, aspect ratio, and whether the model can generate images of people.

Fields

`imageOutputOptions` ` object ( ImageOutputOptions  ` )

Optional. The image output format for generated images.

`aspectRatio` `string`

Optional. The desired aspect ratio for the generated images. The following aspect ratios are supported:

"1:1" "2:3", "3:2" "3:4", "4:3" "4:5", "5:4" "9:16", "16:9" "21:9"

`personGeneration` ` enum ( PersonGeneration  ` )

Optional. Controls whether the model can generate people.

`imageSize` `string`

Optional. Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;imageOutputOptions&quot;: {object (ImageOutputOptions)},&quot;aspectRatio&quot;: string,&quot;personGeneration&quot;: enum (PersonGeneration),&quot;imageSize&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## ImageOutputOptions

The image output format for generated images.

Fields

`mimeType` `string`

Optional. The image format that the output should be saved as.

`compressionQuality` `integer`

Optional. The compression quality of the output image.

<table>
<colgroup>
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
  &quot;compressionQuality&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
