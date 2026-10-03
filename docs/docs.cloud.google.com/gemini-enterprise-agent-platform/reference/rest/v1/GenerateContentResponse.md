---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse
title: GenerateContentResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for \[PredictionService.GenerateContent\].

Fields

`candidates[]` `object ( `[`Candidate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#Candidate)` )`

Output only. Generated candidates.

`modelVersion` `string`

Output only. The model version used to generate the response.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when the request is made to the server.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`responseId` `string`

Output only. responseId is used to identify each response. It is the encoding of the eventId.

`promptFeedback` `object ( `[`PromptFeedback`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#PromptFeedback)` )`

Output only. Content filter results for a prompt sent in the request. Note: Sent only in the first stream chunk. Only happens when no candidates were generated due to content violations.

`usageMetadata` `object ( `[`UsageMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#UsageMetadata)` )`

Usage metadata about the response(s).

**JSON representation**

```
{
  "candidates": [
    {
      object (Candidate)
    }
  ],
  "modelVersion": string,
  "createTime": string,
  "responseId": string,
  "promptFeedback": {
    object (PromptFeedback)
  },
  "usageMetadata": {
    object (UsageMetadata)
  }
}
```

## Candidate

A response candidate generated from the model.

Fields

`index` `integer`

Output only. The 0-based index of this candidate in the list of generated responses. This is useful for distinguishing between multiple candidates when `candidateCount` \> 1.

`content` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content)` )`

Output only. The content of the candidate.

`avgLogprobs` `number`

Output only. The average log probability of the tokens in this candidate. This is a length-normalized score that can be used to compare the quality of candidates of different lengths. A higher average log probability suggests a more confident and coherent response.

`logprobsResult` `object ( `[`LogprobsResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#LogprobsResult)` )`

Output only. The detailed log probability information for the tokens in this candidate. This is useful for debugging, understanding model uncertainty, and identifying potential "hallucinations".

`finishReason` `enum ( `[`FinishReason`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#FinishReason)` )`

Output only. The reason why the model stopped generating tokens. If empty, the model has not stopped generating.

`safetyRatings[]` `object ( `[`SafetyRating`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#SafetyRating)` )`

Output only. A list of ratings for the safety of a response candidate.

There is at most one rating per category.

`citationMetadata` `object ( `[`CitationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#CitationMetadata)` )`

Output only. A collection of citations that apply to the generated content.

`groundingMetadata` `object ( `[`GroundingMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GroundingMetadata)` )`

Output only. metadata returned when grounding is enabled. It contains the sources used to ground the generated content.

`urlContextMetadata` `object ( `[`UrlContextMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#UrlContextMetadata)` )`

Output only. metadata returned when the model uses the `urlContext` tool to get information from a user-provided URL.

`finishMessage` `string`

Output only. Describes the reason the model stopped generating tokens in more detail. This field is returned only when `finishReason` is set.

**JSON representation**

```
{
  "index": integer,
  "content": {
    object (Content)
  },
  "avgLogprobs": number,
  "logprobsResult": {
    object (LogprobsResult)
  },
  "finishReason": enum (FinishReason),
  "safetyRatings": [
    {
      object (SafetyRating)
    }
  ],
  "citationMetadata": {
    object (CitationMetadata)
  },
  "groundingMetadata": {
    object (GroundingMetadata)
  },
  "urlContextMetadata": {
    object (UrlContextMetadata)
  },
  "finishMessage": string
}
```

## LogprobsResult

The log probabilities of the tokens generated by the model.

This is useful for understanding the model's confidence in its predictions and for debugging. For example, you can use log probabilities to identify when the model is making a less confident prediction or to explore alternative responses that the model considered. A low log probability can also indicate that the model is "hallucinating" or generating factually incorrect information.

Fields

`topCandidates[]` `object ( `[`TopCandidates`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#TopCandidates)` )`

A list of the top candidate tokens at each decoding step. The length of this list is equal to the total number of decoding steps.

`chosenCandidates[]` `object ( `[`Candidate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#Candidate_1)` )`

A list of the chosen candidate tokens at each decoding step. The length of this list is equal to the total number of decoding steps. Note that the chosen candidate might not be in `topCandidates` .

**JSON representation**

```
{
  "topCandidates": [
    {
      object (TopCandidates)
    }
  ],
  "chosenCandidates": [
    {
      object (Candidate)
    }
  ]
}
```

## TopCandidates

A list of the top candidate tokens and their log probabilities at each decoding step. This can be used to see what other tokens the model considered.

Fields

`candidates[]` `object ( `[`Candidate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#Candidate_1)` )`

The list of candidate tokens, sorted by log probability in descending order.

**JSON representation**

```
{
  "candidates": [
    {
      object (Candidate)
    }
  ]
}
```

## Candidate

A single token and its associated log probability.

Fields

`token` `string`

The token's string representation.

`tokenId` `integer`

The token's numerical id. While the `token` field provides the string representation of the token, the `tokenId` is the numerical representation that the model uses internally. This can be useful for developers who want to build custom logic based on the model's vocabulary.

`logProbability` `number`

The log probability of this token. A higher value indicates that the model was more confident in this token. The log probability can be used to assess the relative likelihood of different tokens and to identify when the model is uncertain.

**JSON representation**

```
{
  "token": string,
  "tokenId": integer,
  "logProbability": number
}
```

## FinishReason

The reason why the model stopped generating tokens. If this field is empty, the model has not stopped generating.

| Enums                       |                                                                                                                                                                                                  |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `FINISH_REASON_UNSPECIFIED` | The finish reason is unspecified.                                                                                                                                                                |
| `STOP`                      | The model reached a natural stopping point or a configured stop sequence.                                                                                                                        |
| `MAX_TOKENS`                | The model generated the maximum number of tokens allowed by the `maxOutputTokens` parameter.                                                                                                     |
| `SAFETY`                    | The model stopped generating because the content potentially violates safety policies. NOTE: When streaming, the `content` field is empty if content filters block the output.                   |
| `RECITATION`                | The model stopped generating because the content may be a recitation from a source.                                                                                                              |
| `OTHER`                     | The model stopped generating for a reason not otherwise specified.                                                                                                                               |
| `BLOCKLIST`                 | The model stopped generating because the content contains a term from a configured blocklist.                                                                                                    |
| `PROHIBITED_CONTENT`        | The model stopped generating because the content may be prohibited.                                                                                                                              |
| `SPII`                      | The model stopped generating because the content may contain sensitive personally identifiable information (SPII).                                                                               |
| `MALFORMED_FUNCTION_CALL`   | The model generated a function call that is syntactically invalid and can't be parsed.                                                                                                           |
| `MODEL_ARMOR`               | The model response was blocked by Model Armor.                                                                                                                                                   |
| `IMAGE_SAFETY`              | The generated image potentially violates safety policies.                                                                                                                                        |
| `IMAGE_PROHIBITED_CONTENT`  | The generated image may contain prohibited content.                                                                                                                                              |
| `IMAGE_RECITATION`          | The generated image may be a recitation from a source.                                                                                                                                           |
| `IMAGE_OTHER`               | The image generation stopped for a reason not otherwise specified.                                                                                                                               |
| `UNEXPECTED_TOOL_CALL`      | The model generated a function call that is semantically invalid. This can happen, for example, if function calling is not enabled or the generated function is not in the function declaration. |
| `NO_IMAGE`                  | The model was expected to generate an image, but didn't.                                                                                                                                         |

## SafetyRating

A safety rating for a piece of content.

The safety rating contains the harm category and the harm probability level.

Fields

`category` `enum ( `[`HarmCategory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/HarmCategory)` )`

Output only. The harm category of this rating.

`probability` `enum ( `[`HarmProbability`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#HarmProbability)` )`

Output only. The probability of harm for this category.

`probabilityScore` `number`

Output only. The probability score of harm for this category.

`severity` `enum ( `[`HarmSeverity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#HarmSeverity)` )`

Output only. The severity of harm for this category.

`severityScore` `number`

Output only. The severity score of harm for this category.

`blocked` `boolean`

Output only. Indicates whether the content was blocked because of this rating.

`overwrittenThreshold` `enum ( `[`HarmBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/HarmBlockThreshold)` )`

Output only. The overwritten threshold for the safety category of Gemini 2.0 image out. If minors are detected in the output image, the threshold of each safety category will be overwritten if user sets a lower threshold.

**JSON representation**

```
{
  "category": enum (HarmCategory),
  "probability": enum (HarmProbability),
  "probabilityScore": number,
  "severity": enum (HarmSeverity),
  "severityScore": number,
  "blocked": boolean,
  "overwrittenThreshold": enum (HarmBlockThreshold)
}
```

## HarmProbability

The probability of harm for a given category.

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `HARM_PROBABILITY_UNSPECIFIED` | The harm probability is unspecified. |
| `NEGLIGIBLE`                   | The harm probability is negligible.  |
| `LOW`                          | The harm probability is low.         |
| `MEDIUM`                       | The harm probability is medium.      |
| `HIGH`                         | The harm probability is high.        |

## HarmSeverity

The severity of harm for a given category.

| Enums                       |                                   |
|-----------------------------|-----------------------------------|
| `HARM_SEVERITY_UNSPECIFIED` | The harm severity is unspecified. |
| `HARM_SEVERITY_NEGLIGIBLE`  | The harm severity is negligible.  |
| `HARM_SEVERITY_LOW`         | The harm severity is low.         |
| `HARM_SEVERITY_MEDIUM`      | The harm severity is medium.      |
| `HARM_SEVERITY_HIGH`        | The harm severity is high.        |

## CitationMetadata

A collection of citations that apply to a piece of generated content.

Fields

`citations[]` `object ( `[`Citation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#Citation)` )`

Output only. A list of citations for the content.

**JSON representation**

```
{
  "citations": [
    {
      object (Citation)
    }
  ]
}
```

## Citation

A citation for a piece of generatedcontent.

Fields

`startIndex` `integer`

Output only. The start index of the citation in the content.

`endIndex` `integer`

Output only. The end index of the citation in the content.

`uri` `string`

Output only. The URI of the source of the citation.

`title` `string`

Output only. The title of the source of the citation.

`license` `string`

Output only. The license of the source of the citation.

`publicationDate` `object ( `[`Date`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Date)` )`

Output only. The publication date of the source of the citation.

**JSON representation**

```
{
  "startIndex": integer,
  "endIndex": integer,
  "uri": string,
  "title": string,
  "license": string,
  "publicationDate": {
    object (Date)
  }
}
```

## UrlContextMetadata

metadata returned when the model uses the `urlContext` tool to get information from a user-provided URL.

Fields

`urlMetadata[]` `object ( `[`UrlMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#UrlMetadata)` )`

Output only. A list of URL metadata, with one entry for each URL retrieved by the tool.

**JSON representation**

```
{
  "urlMetadata": [
    {
      object (UrlMetadata)
    }
  ]
}
```

## UrlMetadata

The metadata for a single URL retrieval.

Fields

`retrievedUrl` `string`

The URL retrieved by the tool.

`urlRetrievalStatus` `enum ( `[`UrlRetrievalStatus`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#UrlRetrievalStatus)` )`

The status of the URL retrieval.

**JSON representation**

```
{
  "retrievedUrl": string,
  "urlRetrievalStatus": enum (UrlRetrievalStatus)
}
```

## UrlRetrievalStatus

The status of a URL retrieval.

| Enums                              |                                      |
|------------------------------------|--------------------------------------|
| `URL_RETRIEVAL_STATUS_UNSPECIFIED` | Default value. This value is unused. |
| `URL_RETRIEVAL_STATUS_SUCCESS`     | The URL was retrieved successfully.  |
| `URL_RETRIEVAL_STATUS_ERROR`       | The URL retrieval failed.            |

## PromptFeedback

Content filter results for a prompt sent in the request. Note: This is sent only in the first stream chunk and only if no candidates were generated due to content violations.

Fields

`blockReason` `enum ( `[`BlockedReason`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#BlockedReason)` )`

Output only. The reason why the prompt was blocked.

`safetyRatings[]` `object ( `[`SafetyRating`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#SafetyRating)` )`

Output only. A list of safety ratings for the prompt. There is one rating per category.

`blockReasonMessage` `string`

Output only. A readable message that explains the reason why the prompt was blocked.

**JSON representation**

```
{
  "blockReason": enum (BlockedReason),
  "safetyRatings": [
    {
      object (SafetyRating)
    }
  ],
  "blockReasonMessage": string
}
```

## BlockedReason

The reason why the prompt was blocked.

| Enums                        |                                                                                                                                              |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| `BLOCKED_REASON_UNSPECIFIED` | The blocked reason is unspecified.                                                                                                           |
| `SAFETY`                     | The prompt was blocked for safety reasons.                                                                                                   |
| `OTHER`                      | The prompt was blocked for other reasons. For example, it may be due to the prompt's language, or because it contains other harmful content. |
| `BLOCKLIST`                  | The prompt was blocked because it contains a term from the terminology blocklist.                                                            |
| `PROHIBITED_CONTENT`         | The prompt was blocked because it contains prohibited content.                                                                               |
| `MODEL_ARMOR`                | The prompt was blocked by Model Armor.                                                                                                       |
| `IMAGE_SAFETY`               | The prompt was blocked because it contains content that is unsafe for image generation.                                                      |
| `JAILBREAK`                  | The prompt was blocked as a jailbreak attempt.                                                                                               |

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

`promptTokensDetails[]` `object ( `[`ModalityTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModalityTokenCount)` )`

Output only. A detailed breakdown of the token count for each modality in the prompt.

`cacheTokensDetails[]` `object ( `[`ModalityTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModalityTokenCount)` )`

Output only. A detailed breakdown of the token count for each modality in the cached content.

`candidatesTokensDetails[]` `object ( `[`ModalityTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModalityTokenCount)` )`

Output only. A detailed breakdown of the token count for each modality in the generated candidates.

`toolUsePromptTokensDetails[]` `object ( `[`ModalityTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModalityTokenCount)` )`

Output only. A detailed breakdown by modality of the token counts from the results of tool executions, which are provided back to the model as input.

`trafficType` `enum ( `[`TrafficType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse#TrafficType)` )`

Output only. The traffic type for this request.

**JSON representation**

```
{
  "promptTokenCount": integer,
  "candidatesTokenCount": integer,
  "totalTokenCount": integer,
  "toolUsePromptTokenCount": integer,
  "thoughtsTokenCount": integer,
  "cachedContentTokenCount": integer,
  "promptTokensDetails": [
    {
      object (ModalityTokenCount)
    }
  ],
  "cacheTokensDetails": [
    {
      object (ModalityTokenCount)
    }
  ],
  "candidatesTokensDetails": [
    {
      object (ModalityTokenCount)
    }
  ],
  "toolUsePromptTokensDetails": [
    {
      object (ModalityTokenCount)
    }
  ],
  "trafficType": enum (TrafficType)
}
```

## TrafficType

The type of traffic that this request was processed with, indicating which quota is consumed.

| Enums                      |                                                      |
|----------------------------|------------------------------------------------------|
| `TRAFFIC_TYPE_UNSPECIFIED` | Unspecified request traffic type.                    |
| `ON_DEMAND`                | The request was processed using Pay-As-You-Go quota. |
| `ON_DEMAND_PRIORITY`       | type for priority Pay-As-You-Go traffic.             |
| `ON_DEMAND_FLEX`           | type for Flex traffic.                               |
| `PROVISIONED_THROUGHPUT`   | type for Provisioned Throughput traffic.             |
