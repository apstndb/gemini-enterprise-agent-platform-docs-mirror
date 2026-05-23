---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.publishers.models/embedContent
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.publishers.models/embedContent
title: 'Method: models.embedContent'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.publishers.models.embedContent

Embed content with multimodal inputs.

### Endpoint

post `https: / /{service-endpoint} /v1 /{model}:embedContent`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`model` `string`

Required. The name of the publisher model requested to serve the prediction. Format: `projects/{project}/locations/{location}/publishers/*/models/*`

### Request body

The request body contains data with the following structure:

Fields

`content` ` object ( Content  ` )

Required. The content to be embedded.

` title (deprecated)  ` `string`

Optional. Deprecated: Please use EmbedContentConfig.title instead. The title for the text.

` taskType (deprecated)  ` ` enum ( EmbeddingTaskType  ` )

Optional. Deprecated: Please use EmbedContentConfig.task\_type instead. The task type of the embedding.

` outputDimensionality (deprecated)  ` `integer`

Optional. Deprecated: Please use EmbedContentConfig.output\_dimensionality instead. Reduced dimension for the output embedding. If set, excessive values in the output embedding are truncated from the end.

` autoTruncate (deprecated)  ` `boolean`

Optional. Deprecated: Please use EmbedContentConfig.auto\_truncate instead. Whether to silently truncate the input content if it's longer than the maximum sequence length.

`embedContentConfig` ` object ( EmbedContentConfig  ` )

Optional. Configuration for the models.embedContent request.

### Response body

Response message for `  PredictionService.EmbedContent  ` .

If successful, the response body contains data with the following structure:

Fields

`embedding` ` object ( Embedding  ` )

The embedding generated from the input content.

`usageMetadata` ` object ( UsageMetadata  ` )

Usage metadata about the response(s).

`truncated` `boolean`

Whether the input content was truncated before generating the embedding.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;embedding&quot;: {object (Embedding)},&quot;usageMetadata&quot;: {object (UsageMetadata)},&quot;truncated&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## EmbeddingTaskType

Represents a downstream task the embeddings will be used for.

Enums

`UNSPECIFIED`

Unset value, which will default to one of the other enum values.

`RETRIEVAL_QUERY`

Specifies the given text is a query in a search/retrieval setting.

`RETRIEVAL_DOCUMENT`

Specifies the given text is a document from the corpus being searched.

`SEMANTIC_SIMILARITY`

Specifies the given text will be used for STS.

`CLASSIFICATION`

Specifies that the given text will be classified.

`CLUSTERING`

Specifies that the embeddings will be used for clustering.

`QUESTION_ANSWERING`

Specifies that the embeddings will be used for question answering.

`FACT_VERIFICATION`

Specifies that the embeddings will be used for fact verification.

`CODE_RETRIEVAL_QUERY`

Specifies that the embeddings will be used for code retrieval.

## EmbedContentConfig

Configurations for the models.embedContent API.

Fields

`title` `string`

Optional. The title for the text.

Only applicable to text-only embedding models.

`taskType` ` enum ( EmbeddingTaskType  ` )

Optional. The task type of the embedding.

Only applicable to text-only embedding models.

`autoTruncate` `boolean`

Optional. Whether to silently truncate the input content if it's longer than the maximum sequence length.

Only applicable to text-only embedding models.

`outputDimensionality` `integer`

Optional. Reduced dimension for the output embedding. If set, excessive values in the output embedding are truncated from the end.

`documentOcr` `boolean`

Optional. Whether to enable OCR for document content.

`audioTrackExtraction` `boolean`

Optional. Whether to extract audio from video content.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;title&quot;: string,&quot;taskType&quot;: enum (EmbeddingTaskType),&quot;autoTruncate&quot;: boolean,&quot;outputDimensionality&quot;: integer,&quot;documentOcr&quot;: boolean,&quot;audioTrackExtraction&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## Embedding

A list of floats representing an embedding.

Fields

`values[]` `number`

Embedding vector values.

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
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

## UsageMetadata

Usage metadata about the content generation request and response. This message provides a detailed breakdown of token usage and other relevant metrics.

Fields

`promptTokenCount` `integer`

The total number of tokens in the prompt. This includes any text, images, or other media provided in the request. When `cachedContent` is set, this also includes the number of tokens in the cached content.

`candidatesTokenCount` `integer`

The total number of tokens in the generated candidates.

`totalTokenCount` `integer`

The total number of tokens for the entire request. This is the sum of `promptTokenCount` , `candidatesTokenCount` , `toolUsePromptTokenCount` , and `thoughtsTokenCount` .

`toolUsePromptTokenCount` `integer`

Output only. The number of tokens in the results from tool executions, which are provided back to the model as input, if applicable.

`thoughtsTokenCount` `integer`

Output only. The number of tokens that were part of the model's generated "thoughts" output, if applicable.

`cachedContentTokenCount` `integer`

Output only. The number of tokens in the cached content that was used for this request.

`promptTokensDetails[]` ` object ( ModalityTokenCount  ` )

Output only. A detailed breakdown of the token count for each modality in the prompt.

`cacheTokensDetails[]` ` object ( ModalityTokenCount  ` )

Output only. A detailed breakdown of the token count for each modality in the cached content.

`candidatesTokensDetails[]` ` object ( ModalityTokenCount  ` )

Output only. A detailed breakdown of the token count for each modality in the generated candidates.

`toolUsePromptTokensDetails[]` ` object ( ModalityTokenCount  ` )

Output only. A detailed breakdown by modality of the token counts from the results of tool executions, which are provided back to the model as input.

`trafficType` ` enum ( TrafficType  ` )

Output only. The traffic type for this request.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;promptTokenCount&quot;: integer,&quot;candidatesTokenCount&quot;: integer,&quot;totalTokenCount&quot;: integer,&quot;toolUsePromptTokenCount&quot;: integer,&quot;thoughtsTokenCount&quot;: integer,&quot;cachedContentTokenCount&quot;: integer,&quot;promptTokensDetails&quot;: [{object (ModalityTokenCount)}],&quot;cacheTokensDetails&quot;: [{object (ModalityTokenCount)}],&quot;candidatesTokensDetails&quot;: [{object (ModalityTokenCount)}],&quot;toolUsePromptTokensDetails&quot;: [{object (ModalityTokenCount)}],&quot;trafficType&quot;: enum (TrafficType)}</code></pre></td>
</tr>
</tbody>
</table>

## TrafficType

The type of traffic that this request was processed with, indicating which quota gets consumed.

Enums

`TRAFFIC_TYPE_UNSPECIFIED`

Unspecified request traffic type.

`ON_DEMAND`

type for Pay-As-You-Go traffic.

`PROVISIONED_THROUGHPUT`

type for Provisioned Throughput traffic.
