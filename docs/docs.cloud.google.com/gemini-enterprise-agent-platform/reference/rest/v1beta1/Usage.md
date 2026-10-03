---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage
title: Usage
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Statistics on the interaction request's token usage.

Fields

`totalInputTokens` `integer`

Number of tokens in the prompt (context).

`inputTokensByModality[]` `object ( `[`ModalityTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage#ModalityTokens)` )`

A breakdown of input token usage by modality.

`totalCachedTokens` `integer`

Number of tokens in the cached part of the prompt (the cached content).

`cachedTokensByModality[]` `object ( `[`ModalityTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage#ModalityTokens)` )`

A breakdown of cached token usage by modality.

`totalOutputTokens` `integer`

Total number of tokens across all the generated responses.

`outputTokensByModality[]` `object ( `[`ModalityTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage#ModalityTokens)` )`

A breakdown of output token usage by modality.

`totalToolUseTokens` `integer`

Number of tokens present in tool-use prompt(s).

`toolUseTokensByModality[]` `object ( `[`ModalityTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage#ModalityTokens)` )`

A breakdown of tool-use token usage by modality.

`totalThoughtTokens` `integer`

Number of tokens of thoughts for thinking models.

`totalTokens` `integer`

Total token count for the interaction request (prompt + responses + other internal tokens).

`groundingToolCount[]` `object ( `[`GroundingToolCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage#GroundingToolCount)` )`

Grounding tool count.

**JSON representation**

```
{
  "totalInputTokens": integer,
  "inputTokensByModality": [
    {
      object (ModalityTokens)
    }
  ],
  "totalCachedTokens": integer,
  "cachedTokensByModality": [
    {
      object (ModalityTokens)
    }
  ],
  "totalOutputTokens": integer,
  "outputTokensByModality": [
    {
      object (ModalityTokens)
    }
  ],
  "totalToolUseTokens": integer,
  "toolUseTokensByModality": [
    {
      object (ModalityTokens)
    }
  ],
  "totalThoughtTokens": integer,
  "totalTokens": integer,
  "groundingToolCount": [
    {
      object (GroundingToolCount)
    }
  ]
}
```

## ModalityTokens

The token count for a single response modality.

Fields

`modality` `enum ( `[`ResponseModality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ResponseModality)` )`

The modality associated with the token count.

`tokens` `integer`

Number of tokens for the modality.

**JSON representation**

```
{
  "modality": enum (ResponseModality),
  "tokens": integer
}
```

## GroundingToolCount

The number of grounding tool counts.

Fields

`type` `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Usage#Type)` )`

The grounding tool type associated with the count.

`count` `integer`

The number of grounding tool counts.

**JSON representation**

```
{
  "type": enum (Type),
  "count": integer
}
```

## Type

The type of grounding tool.

| Enums              |                                                                                    |
|--------------------|------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED` | Default value. This value is unused.                                               |
| `GOOGLE_SEARCH`    | Grounding with Google Web Search and Image Search, & Web Grounding for Enterprise. |
| `GOOGLE_MAPS`      | Grounding with Google Maps.                                                        |
| `RETRIEVAL`        | Grounding with customer's data, for example, VertexAISearch.                       |
