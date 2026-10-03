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

`contents[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content)` )`

Required. The content of the current conversation with the model.

For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request.

`cachedContent` `string`

Optional. The name of the cached content used as context to serve the prediction. Note: only used in explicit caching, where users can have control over caching (e.g. what content to cache) and enjoy guaranteed cost savings. Format: `projects/{project}/locations/{location}/cachedContents/{cachedContent}`

`tools[]` `object ( `[`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#Tool)` )`

Optional. A list of `Tools` the model may use to generate the next response.

A `Tool` is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model.

`toolConfig` `object ( `[`ToolConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ToolConfig)` )`

Optional. Tool config. This config is shared for all tools provided in the request.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only.

label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. label values are optional. label keys must start with a letter.

`safetySettings[]` `object ( `[`SafetySetting`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#SafetySetting)` )`

Optional. Per request settings for blocking unsafe content. Enforced on GenerateContentResponse.candidates.

`modelArmorConfig` `object ( `[`ModelArmorConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ModelArmorConfig)` )`

Optional. Settings for prompt and response sanitization using the Model Armor service. If supplied, safetySettings must not be supplied.

`generationConfig` `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#GenerationConfig)` )`

Optional. Generation config.

`systemInstruction` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content)` )`

Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph.

**JSON representation**

```
{
  "model": string,
  "contents": [
    {
      object (Content)
    }
  ],
  "cachedContent": string,
  "tools": [
    {
      object (Tool)
    }
  ],
  "toolConfig": {
    object (ToolConfig)
  },
  "labels": {
    string: string,
    ...
  },
  "safetySettings": [
    {
      object (SafetySetting)
    }
  ],
  "modelArmorConfig": {
    object (ModelArmorConfig)
  },
  "generationConfig": {
    object (GenerationConfig)
  },
  "systemInstruction": {
    object (Content)
  }
}
```

## Tool

Tool details that the model may use to generate response.

A `Tool` is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model. A Tool object should contain exactly one type of Tool (e.g FunctionDeclaration, Retrieval or GoogleSearchRetrieval).

Fields

`functionDeclarations[]` `object ( `[`FunctionDeclaration`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/FunctionDeclaration)` )`

Optional. Function tool type. One or more function declarations to be passed to the model along with the current user query. Model may decide to call a subset of these functions by populating [`FunctionCall`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content#Part.FIELDS.function_call) in the response. user should provide a [`FunctionResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content#Part.FIELDS.function_response) for each function call in the next turn. Based on the function responses, Model will generate the final response back to the user. Maximum 512 function declarations can be provided.

`retrieval` `object ( `[`Retrieval`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#Retrieval)` )`

Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation.

`googleSearch` `object ( `[`GoogleSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#GoogleSearch)` )`

Optional. GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

`googleSearchRetrieval `**`(deprecated)`** `object ( `[`GoogleSearchRetrieval`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#GoogleSearchRetrieval)` )`

> Optional. The `google_search_retrieval` field is deprecated. Use `google_search` instead. This field is for use with Gemini 1.5 models; `google_search` is used for Gemini 2.0 and newer models.

Optional. Specialized retrieval tool that is powered by Google Search.

`googleMaps` `object ( `[`GoogleMaps`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#GoogleMaps)` )`

Optional. GoogleMaps tool type. Tool to support Google Maps in Model.

`enterpriseWebSearch` `object ( `[`EnterpriseWebSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/EnterpriseWebSearch)` )`

Optional. Tool to support searching public web data, powered by Agent Platform Search and Sec4 compliance.

`parallelAiSearch` `object ( `[`ParallelAiSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ParallelAiSearch)` )`

Optional. If specified, Agent Platform will use Parallel.ai to search for information to answer user queries. The search results will be grounded on Parallel.ai and presented to the model for response generation

`exaAiSearch` `object ( `[`ExaAiSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ExaAiSearch)` )`

Optional. uses Exa.ai to search for information to answer user queries. The search results will be grounded on Exa.ai and presented to the model for response generation

`codeExecution` `object ( `[`CodeExecution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#CodeExecution)` )`

Optional. CodeExecution tool type. Enables the model to execute code as part of generation.

`urlContext` `object ( `[`UrlContext`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#UrlContext)` )`

Optional. Tool to support URL context retrieval.

`computerUse` `object ( `[`ComputerUse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ComputerUse)` )`

Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations.

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
  "exaAiSearch": {
    object (ExaAiSearch)
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

## Retrieval

Defines a retrieval tool that model can call to access external knowledge.

Fields

`disableAttribution `**`(deprecated)`** `boolean`

> This item is deprecated!

Optional. Deprecated. This option is no longer supported.

`source` `Union type`

The source of the retrieval. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`vertexAiSearch` `object ( `[`VertexAISearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#VertexAISearch)` )`

Set to use data source powered by Agent Platform Search.

`vertexRagStore` `object ( `[`VertexRagStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#VertexRagStore)` )`

Set to use data source powered by Vertex RAG store. user data is uploaded via the VertexRagDataService.

End of mutually exclusive fields.

**JSON representation**

```
{
  "disableAttribution": boolean,

  // source
  "vertexAiSearch": {
    object (VertexAISearch)
  },
  "vertexRagStore": {
    object (VertexRagStore)
  }
  // Union type
}
```

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

`dataStoreSpecs[]` `object ( `[`DataStoreSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#DataStoreSpec)` )`

Specifications that define the specific DataStores to be searched, along with configurations for those data stores. This is only considered for Engines with multiple data stores. It should only be set if engine is used.

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

## DataStoreSpec

Define data stores within engine to filter on in a search call and configurations for those data stores. For more information, see <https://cloud.google.com/generative-ai-app-builder/docs/reference/rpc/google.cloud.discoveryengine.v1#datastorespec>

Fields

`dataStore` `string`

Full resource name of DataStore, such as Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`

`filter` `string`

Optional. Filter specification to filter documents in the data store specified by dataStore field. For more information on filtering, see [Filtering](https://cloud.google.com/generative-ai-app-builder/docs/filter-search-metadata)

**JSON representation**

```
{
  "dataStore": string,
  "filter": string
}
```

## VertexRagStore

Retrieve from Vertex RAG Store for grounding.

Fields

`ragCorpora[] `**`(deprecated)`** `string`

> This item is deprecated!

Optional. Deprecated. Please use ragResources instead.

`ragResources[]` `object ( `[`RagResource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#RagResource)` )`

Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.

`ragRetrievalConfig` `object ( `[`RagRetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#RagRetrievalConfig)` )`

Optional. The retrieval config for the Rag query.

`storeContext` `boolean`

Optional. Currently only supported for Gemini Multimodal Live API.

In Gemini Multimodal Live API, if `storeContext` bool is specified, Gemini will leverage it to automatically memorize the interactions between the client and Gemini, and retrieve context when needed to augment the response generation for users' ongoing and future interactions.

`similarityTopK `**`(deprecated)`** `integer`

> This item is deprecated!

Optional. Number of top k results to return from the selected corpora.

`vectorDistanceThreshold `**`(deprecated)`** `number`

> This item is deprecated!

Optional. Only return results with vector distance smaller than the threshold.

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
  "similarityTopK": integer,
  "vectorDistanceThreshold": number
}
```

## RagResource

The definition of the Rag resource.

Fields

`ragCorpus` `string`

Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{ragCorpus}`

`ragFileIds[]` `string`

Optional. ragFileId. The files should be in the same ragCorpus set in ragCorpus field.

**JSON representation**

```
{
  "ragCorpus": string,
  "ragFileIds": [
    string
  ]
}
```

## RagRetrievalConfig

Specifies the context retrieval config.

Fields

`topK` `integer`

Optional. The number of contexts to retrieve.

`hybridSearch` `object ( `[`HybridSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#HybridSearch)` )`

Optional. Config for Hybrid Search.

`filter` `object ( `[`Filter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#Filter)` )`

Optional. Config for filters.

`ranking` `object ( `[`Ranking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#Ranking)` )`

Optional. Config for ranking and reranking.

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

## HybridSearch

Config for Hybrid Search.

Fields

`alpha` `number`

Optional. Alpha value controls the weight between dense and sparse vector search results. The range is \[0, 1\], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally.

**JSON representation**

```
{
  "alpha": number
}
```

## Filter

Config for filters.

Fields

`metadataFilter` `string`

Optional. String for metadata filtering.

`vector_db_threshold` `Union type`

Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`vectorDistanceThreshold` `number`

Optional. Only returns contexts with vector distance smaller than the threshold.

`vectorSimilarityThreshold` `number`

Optional. Only returns contexts with vector similarity larger than the threshold.

End of mutually exclusive fields.

**JSON representation**

```
{
  "metadataFilter": string,

  // vector_db_threshold
  "vectorDistanceThreshold": number,
  "vectorSimilarityThreshold": number
  // Union type
}
```

## Ranking

Config for ranking and reranking.

Fields

`ranking_config` `Union type`

Config options for ranking. Currently only Rank Service is supported. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`rankService` `object ( `[`RankService`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#RankService)` )`

Optional. Config for Rank service.

`llmRanker` `object ( `[`LlmRanker`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#LlmRanker)` )`

Optional. Config for LlmRanker.

End of mutually exclusive fields.

**JSON representation**

```
{

  // ranking_config
  "rankService": {
    object (RankService)
  },
  "llmRanker": {
    object (LlmRanker)
  }
  // Union type
}
```

## RankService

Config for Rank service.

Fields

`modelName` `string`

Optional. The model name of the rank service. Format: `semantic-ranker-512@latest`

**JSON representation**

```
{
  "modelName": string
}
```

## LlmRanker

Config for LlmRanker.

Fields

`modelName` `string`

Optional. The model name used for ranking. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models) .

**JSON representation**

```
{
  "modelName": string
}
```

## GoogleSearch

GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

Fields

`excludeDomains[]` `string`

Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: \["amazon.com", "facebook.com"\].

`blockingConfidence` `enum ( `[`PhishBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PhishBlockThreshold)` )`

Optional. Sites with confidence level chosen & above this value will be blocked from the search results.

**JSON representation**

```
{
  "excludeDomains": [
    string
  ],
  "blockingConfidence": enum (PhishBlockThreshold)
}
```

## GoogleSearchRetrieval

Tool to retrieve public web data for grounding, powered by Google.

Fields

`dynamicRetrievalConfig` `object ( `[`DynamicRetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/DynamicRetrievalConfig)` )`

Specifies the dynamic retrieval configuration for the given source.

**JSON representation**

```
{
  "dynamicRetrievalConfig": {
    object (DynamicRetrievalConfig)
  }
}
```

## GoogleMaps

Tool to retrieve public maps data for grounding, powered by Google.

Fields

`enableWidget `**`(deprecated)`** `boolean`

> This item is deprecated!

Optional. Deprecated: The Google Maps contextual widget behavior in Grounding with Google Maps is being deprecated; this field is planned for removal and no longer has any effect once removed.

If true, include the widget context token in the response.

**JSON representation**

```
{
  "enableWidget": boolean
}
```

## ParallelAiSearch

ParallelAiSearch tool type. A tool that uses the Parallel.ai search engine for grounding.

Fields

`apiKey` `string`

Optional. The API key for ParallelAiSearch. If an API key is not provided, the system will attempt to verify access by checking for an active Parallel.ai subscription through the Google Cloud Marketplace. See <https://docs.parallel.ai/search/search-quickstart> for more details.

`customConfigs` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. Custom configs for ParallelAiSearch. This field can be used to pass any parameter from the Parallel.ai Search API. See the Parallel.ai documentation for the full list of available parameters and their usage: <https://docs.parallel.ai/api-reference/search-beta/search> Currently only `source_policy` , `excerpts` , `maxResults` , `mode` , `fetch_policy` can be set via this field. For example: { "source_policy": { "include_domains": \["google.com", "wikipedia.org"\], "excludeDomains": \["example.com"\] }, "fetch_policy": { "max_age_seconds": 3600 } }

**JSON representation**

```
{
  "apiKey": string,
  "customConfigs": {
    object
  }
}
```

## ExaAiSearch

ExaAiSearch tool type. A tool that uses the Exa.ai search engine for grounding.

Fields

`apiKey` `string`

Required. The API key for ExaAiSearch.

`customConfigs` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. This field can be used to pass any parameter from the Exa.ai Search API.

**JSON representation**

```
{
  "apiKey": string,
  "customConfigs": {
    object
  }
}
```

## CodeExecution

This type has no fields.

Tool that executes code generated by the model, and automatically returns the result to the model.

See also [`ExecutableCode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content#ExecutableCode) and [`CodeExecutionResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CodeExecutionResult) , which are input and output to this tool.

## UrlContext

This type has no fields.

Tool to support URL context.

## ComputerUse

A tool that enables the model to interact directly with a computer environment.

Fields

`environment` `enum ( `[`Environment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Environment)` )`

Required. The target environment where the computer use tool operates.

`excludedPredefinedFunctions[]` `string`

Optional. A list of predefined functions to explicitly exclude from the model call. By default, [predefined functions](https://cloud.google.com/vertex-ai/generative-ai/docs/computer-use#supported-actions) are included. Excluding functions allows for a more restricted action space or custom definitions for predefined functions.

`enablePromptInjectionDetection` `boolean`

Optional. Whether to enable the prompt injection detection check on the computer use request.

**JSON representation**

```
{
  "environment": enum (Environment),
  "excludedPredefinedFunctions": [
    string
  ],
  "enablePromptInjectionDetection": boolean
}
```

## ToolConfig

Tool config. This config is shared for all tools provided in the request.

Fields

`functionCallingConfig` `object ( `[`FunctionCallingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/FunctionCallingConfig)` )`

Optional. Function calling config.

`retrievalConfig` `object ( `[`RetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#RetrievalConfig)` )`

Optional. Retrieval config.

**JSON representation**

```
{
  "functionCallingConfig": {
    object (FunctionCallingConfig)
  },
  "retrievalConfig": {
    object (RetrievalConfig)
  }
}
```

## RetrievalConfig

Retrieval config.

Fields

`latLng` `object ( `[`LatLng`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#LatLng)` )`

The location of the user.

`languageCode` `string`

The language code of the user.

**JSON representation**

```
{
  "latLng": {
    object (LatLng)
  },
  "languageCode": string
}
```

## LatLng

An object that represents a latitude/longitude pair. This is expressed as a pair of doubles to represent degrees latitude and degrees longitude. Unless specified otherwise, this object must conform to the [WGS84 standard](https://en.wikipedia.org/wiki/World_Geodetic_System#1984_version) . Values must be within normalized ranges.

Fields

`latitude` `number`

The latitude in degrees. It must be in the range \[-90.0, +90.0\].

`longitude` `number`

The longitude in degrees. It must be in the range \[-180.0, +180.0\].

**JSON representation**

```
{
  "latitude": number,
  "longitude": number
}
```

## SafetySetting

A safety setting that affects the safety-blocking behavior.

A `SafetySetting` consists of a harm `category` and a `threshold` for that category.

Fields

`category` `enum ( `[`HarmCategory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HarmCategory)` )`

Required. The harm category to be blocked.

`threshold` `enum ( `[`HarmBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HarmBlockThreshold)` )`

Required. The threshold for blocking content. If the harm probability exceeds this threshold, the content will be blocked.

`method` `enum ( `[`HarmBlockMethod`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HarmBlockMethod)` )`

Optional. The method for blocking content. If not specified, the default behavior is to use the probability score.

**JSON representation**

```
{
  "category": enum (HarmCategory),
  "threshold": enum (HarmBlockThreshold),
  "method": enum (HarmBlockMethod)
}
```

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

**JSON representation**

```
{
  "promptTemplateName": string,
  "responseTemplateName": string
}
```

## GenerationConfig

Configuration for content generation.

This message contains all the parameters that control how the model generates content. It allows you to influence the randomness, length, and structure of the output.

Fields

`stopSequences[]` `string`

Optional. A list of character sequences that will stop the model from generating further tokens. If a stop sequence is generated, the output will end at that point. This is useful for controlling the length and structure of the output. For example, you can use \["\n", "###"\] to stop generation at a new line or a specific marker.

`responseMimeType `**`(deprecated)`** `string`

> This item is deprecated!

Optional. The IANA standard MIME type of the response. The model will generate output that conforms to this MIME type. Supported values include 'text/plain' (default) and 'application/json'. The model needs to be prompted to output the appropriate response type, otherwise the behavior is undefined. Deprecated: Use `responseFormat` instead.

`responseModalities[]` `enum ( `[`Modality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Modality)` )`

Optional. The modalities of the response. The model will generate a response that includes all the specified modalities. For example, if this is set to `[TEXT, IMAGE]` , the response will include both text and an image.

`thinkingConfig` `object ( `[`ThinkingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ThinkingConfig)` )`

Optional. Configuration for thinking features. An error will be returned if this field is set for models that don't support thinking.

`modelConfig `**`(deprecated)`** `object ( `[`ModelConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ModelConfig)` )`

> Optional. The `model_config` field is deprecated and is not supported anymore. Use `routing_config` instead.

Optional. Config for model selection.

`responseFormat[]` `object ( `[`ResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ResponseFormat)` )`

Optional. New response format field for the model to configure output formatting and delivery.

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

`responseSchema `**`(deprecated)`** `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Schema)` )`

> This item is deprecated!

Optional. Lets you to specify a schema for the model's response, ensuring that the output conforms to a particular structure. This is useful for generating structured data such as JSON. The schema is a subset of the [OpenAPI 3.0 schema object](https://spec.openapis.org/oas/v3.0.3#schema) object.

When this field is set, you must also set the `responseMimeType` to `application/json` . Deprecated: Use `responseFormat` instead.

`responseJsonSchema `**`(deprecated)`** `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

> This item is deprecated!

Optional. When this field is set, `responseSchema` must be omitted and `responseMimeType` must be set to `application/json` . Deprecated: Use `responseFormat` instead.

`routingConfig` `object ( `[`RoutingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#RoutingConfig)` )`

Optional. Routing configuration.

`audioTimestamp` `boolean`

Optional. If enabled, audio timestamps will be included in the request to the model. This can be useful for synchronizing audio with other modalities in the response.

`mediaResolution` `enum ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MediaResolution)` )`

Optional. The token resolution at which input media content is sampled. This is used to control the trade-off between the quality of the response and the number of tokens used to represent the media. A higher resolution allows the model to perceive more detail, which can lead to a more nuanced response, but it will also use more tokens. This does not affect the image dimensions sent to the model.

`speechConfig` `object ( `[`SpeechConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#SpeechConfig)` )`

Optional. The speech generation config.

`enableAffectiveDialog` `boolean`

Optional. If enabled, the model will detect emotions and adapt its responses accordingly. For example, if the model detects that the user is frustrated, it may provide a more empathetic response.

`imageConfig `**`(deprecated)`** `object ( `[`ImageConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ImageConfig)` )`

> This item is deprecated!

Optional. Config for image generation features. Deprecated: Use `responseFormat.image` instead.

**JSON representation**

```
{
  "stopSequences": [
    string
  ],
  "responseMimeType": string,
  "responseModalities": [
    enum (Modality)
  ],
  "thinkingConfig": {
    object (ThinkingConfig)
  },
  "modelConfig": {
    object (ModelConfig)
  },
  "responseFormat": [
    {
      object (ResponseFormat)
    }
  ],
  "temperature": number,
  "topP": number,
  "topK": number,
  "candidateCount": integer,
  "maxOutputTokens": integer,
  "responseLogprobs": boolean,
  "logprobs": integer,
  "presencePenalty": number,
  "frequencyPenalty": number,
  "seed": integer,
  "responseSchema": {
    object (Schema)
  },
  "responseJsonSchema": value,
  "routingConfig": {
    object (RoutingConfig)
  },
  "audioTimestamp": boolean,
  "mediaResolution": enum (MediaResolution),
  "speechConfig": {
    object (SpeechConfig)
  },
  "enableAffectiveDialog": boolean,
  "imageConfig": {
    object (ImageConfig)
  }
}
```

## RoutingConfig

The configuration for routing the request to a specific model. This can be used to control which model is used for the generation, either automatically or by specifying a model name.

Fields

`routing_config` `Union type`

The routing mode for the request. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`autoMode` `object ( `[`AutoRoutingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#AutoRoutingMode)` )`

In this mode, the model is selected automatically based on the content of the request.

`manualMode` `object ( `[`ManualRoutingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ManualRoutingMode)` )`

In this mode, the model is specified manually.

End of mutually exclusive fields.

**JSON representation**

```
{

  // routing_config
  "autoMode": {
    object (AutoRoutingMode)
  },
  "manualMode": {
    object (ManualRoutingMode)
  }
  // Union type
}
```

## AutoRoutingMode

The configuration for automated routing.

When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

Fields

`modelRoutingPreference` `enum ( `[`ModelRoutingPreference`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ModelRoutingPreference)` )`

The model routing preference.

**JSON representation**

```
{
  "modelRoutingPreference": enum (ModelRoutingPreference)
}
```

## ManualRoutingMode

The configuration for manual routing.

When manual routing is specified, the model will be selected based on the model name provided.

Fields

`modelName` `string`

The name of the model to use. Only public LLM models are accepted.

**JSON representation**

```
{
  "modelName": string
}
```

## SpeechConfig

Configuration for speech generation.

Fields

`voiceConfig` `object ( `[`VoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#VoiceConfig)` )`

The configuration for the voice to use.

`languageCode` `string`

Optional. The language code (ISO 639-1) for the speech synthesis.

`multiSpeakerVoiceConfig` `object ( `[`MultiSpeakerVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#MultiSpeakerVoiceConfig)` )`

The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voiceConfig` .

**JSON representation**

```
{
  "voiceConfig": {
    object (VoiceConfig)
  },
  "languageCode": string,
  "multiSpeakerVoiceConfig": {
    object (MultiSpeakerVoiceConfig)
  }
}
```

## VoiceConfig

Configuration for a voice.

Fields

`voice_config` `Union type`

The configuration for the speaker to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`prebuiltVoiceConfig` `object ( `[`PrebuiltVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#PrebuiltVoiceConfig)` )`

The configuration for a prebuilt voice.

`replicatedVoiceConfig` `object ( `[`ReplicatedVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ReplicatedVoiceConfig)` )`

Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample.

End of mutually exclusive fields.

**JSON representation**

```
{

  // voice_config
  "prebuiltVoiceConfig": {
    object (PrebuiltVoiceConfig)
  },
  "replicatedVoiceConfig": {
    object (ReplicatedVoiceConfig)
  }
  // Union type
}
```

## PrebuiltVoiceConfig

Configuration for a prebuilt voice.

Fields

`voiceName` `string`

The name of the prebuilt voice to use.

**JSON representation**

```
{
  "voiceName": string
}
```

## ReplicatedVoiceConfig

The configuration for the replicated voice to use.

Fields

`mimeType` `string`

Optional. The mimetype of the voice sample. The only currently supported value is `audio/wav` . This represents 16-bit signed little-endian wav data, with a 24kHz sampling rate. `mimeType` will default to `audio/wav` if not set.

`voiceSampleAudio` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. The sample of the custom voice.

A base64-encoded string.

**JSON representation**

```
{
  "mimeType": string,
  "voiceSampleAudio": string
}
```

## MultiSpeakerVoiceConfig

Configuration for a multi-speaker text-to-speech request.

Fields

`speakerVoiceConfigs[]` `object ( `[`SpeakerVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#SpeakerVoiceConfig)` )`

Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided.

**JSON representation**

```
{
  "speakerVoiceConfigs": [
    {
      object (SpeakerVoiceConfig)
    }
  ]
}
```

## SpeakerVoiceConfig

Configuration for a single speaker in a multi-speaker setup.

Fields

`speaker` `string`

Required. The name of the speaker. This should be the same as the speaker name used in the prompt.

`voiceConfig` `object ( `[`VoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#VoiceConfig)` )`

Required. The configuration for the voice of this speaker.

**JSON representation**

```
{
  "speaker": string,
  "voiceConfig": {
    object (VoiceConfig)
  }
}
```

## ThinkingConfig

Configuration for the model's thinking features.

"Thinking" is a process where the model breaks down a complex task into smaller, manageable steps. This allows the model to reason about the task, plan its approach, and execute the plan to generate a high-quality response.

Fields

`includeThoughts` `boolean`

Optional. If true, the model will include its thoughts in the response. "Thoughts" are the intermediate steps the model takes to arrive at the final response. They can provide insights into the model's reasoning process and help with debugging. If this is true, thoughts are returned only when available.

`thinkingBudget` `integer`

Optional. The token budget for the model's thinking process. The model will make a best effort to stay within this budget. This can be used to control the trade-off between response quality and latency.

`thinkingLevel` `enum ( `[`ThinkingLevel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ThinkingLevel)` )`

Optional. The number of thoughts tokens that the model should generate.

**JSON representation**

```
{
  "includeThoughts": boolean,
  "thinkingBudget": integer,
  "thinkingLevel": enum (ThinkingLevel)
}
```

## ModelConfig

Config for model selection.

Fields

`featureSelectionPreference` `enum ( `[`FeatureSelectionPreference`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/FeatureSelectionPreference)` )`

Required. feature selection preference.

**JSON representation**

```
{
  "featureSelectionPreference": enum (FeatureSelectionPreference)
}
```

## ImageConfig

Configuration for image generation.

This message allows you to control various aspects of image generation, such as the output format, aspect ratio, and whether the model can generate images of people.

Fields

`prominentPeople` `enum ( `[`ProminentPeople`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ProminentPeople)` )`

Optional. Controls whether prominent people (celebrities) generation is allowed. If used with personGeneration, personGeneration enum would take precedence. For instance, if ALLOW_NONE is set, all person generation would be blocked. If this field is unspecified, the default behavior is to allow prominent people.

`imageOutputOptions` `object ( `[`ImageOutputOptions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ImageOutputOptions)` )`

Optional. The image output format for generated images.

`aspectRatio` `string`

Optional. The desired aspect ratio for the generated images. The following aspect ratios are supported:

"1:1" "2:3", "3:2" "3:4", "4:3" "4:5", "5:4" "9:16", "16:9" "21:9"

`personGeneration` `enum ( `[`PersonGeneration`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PersonGeneration)` )`

Optional. Controls whether the model can generate people.

`imageSize` `string`

Optional. Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .

**JSON representation**

```
{
  "prominentPeople": enum (ProminentPeople),
  "imageOutputOptions": {
    object (ImageOutputOptions)
  },
  "aspectRatio": string,
  "personGeneration": enum (PersonGeneration),
  "imageSize": string
}
```

## ImageOutputOptions

The image output format for generated images.

Fields

`mimeType` `string`

Optional. The image format that the output should be saved as.

`compressionQuality` `integer`

Optional. The compression quality of the output image.

**JSON representation**

```
{
  "mimeType": string,
  "compressionQuality": integer
}
```

## ResponseFormat

Configuration for the model to configure output formatting and delivery.

Fields

`format` `Union type`

The format of the output content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` `object ( `[`TextResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#TextResponseFormat)` )`

Text output format.

`audio` `object ( `[`AudioResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AudioResponseFormat)` )`

Audio output format.

`image` `object ( `[`ImageResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#ImageResponseFormat)` )`

Image output format.

`video` `object ( `[`VideoResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#VideoResponseFormat)` )`

Video output format.

End of mutually exclusive fields.

**JSON representation**

```
{

  // format
  "text": {
    object (TextResponseFormat)
  },
  "audio": {
    object (AudioResponseFormat)
  },
  "image": {
    object (ImageResponseFormat)
  },
  "video": {
    object (VideoResponseFormat)
  }
  // Union type
}
```

## TextResponseFormat

Configuration for text-specific output formatting.

Fields

`mimeType` `enum ( ``MimeType`` )`

Optional. The IANA standard MIME type of the response.

`schema` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Optional. The JSON schema that the output should conform to. Only applicable when mimeType is APPLICATION_JSON.

**JSON representation**

```
{
  "mimeType": enum (MimeType),
  "schema": value
}
```

## ImageResponseFormat

Configuration for image-specific output formatting.

Fields

`delivery` `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/DeliveryMode)` )`

Optional. Delivery mode for the generated content.

`mimeType` `enum ( ``MimeType`` )`

Optional. The MIME type of the image output.

`aspectRatio` `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AspectRatio)` )`

Optional. The aspect ratio for the image output.

`imageSize` `enum ( `[`ImageSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSize)` )`

Optional. The size of the image output.

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),
  "mimeType": enum (MimeType),
  "aspectRatio": enum (AspectRatio),
  "imageSize": enum (ImageSize)
}
```

## VideoResponseFormat

Configuration for video-specific output formatting.

Fields

`delivery` `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/DeliveryMode)` )`

Optional. Delivery mode for the generated content.

`gcsUri` `string`

Optional. The Google Cloud Storage URI to store the video output. Required for Vertex if delivery is URI.

`aspectRatio` `enum ( ``AspectRatio`` )`

The aspect ratio for the video output.

`resolution` `string`

Optional. The video output resolution. Supported values: "360p", "720p", "1080p", "4k".

`duration` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. The duration for the video output.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),
  "gcsUri": string,
  "aspectRatio": enum (AspectRatio),
  "resolution": string,
  "duration": string
}
```
