---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-4
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-4
title: Get started with Gemini 4
description: 'Get started with Gemini 4 in Gemini Enterprise Agent Platform: what''s new, and how to migrate from Gemini 3 models.'
data_source: docs.cloud.google.com
---

The Gemini 4 model family includes the following models:

- **[Gemini 4 Hydrogen](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-hydrogen)** ( `gemini-4-hydrogen` ): Built for speed and efficiency across everyday coding and agentic workflows, multimodal analysis, and tool use.

- **[Gemini 4 Carbon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-carbon)** ( `gemini-4-carbon` ): Google's frontier model that excels at deep work in complex, real-world tasks across domains including coding, finance, legal, cybersecurity, and science.

- **[Gemini 4 Argon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-argon)** ( `gemini-4-argon` ): Google's frontier model that excels at deep work in complex, real-world tasks across domains including coding, finance, legal, cybersecurity, and science.

This guide shows you how to make your first Gemini 4 request, describes what's new in Gemini 4, and explains what changes when you migrate from Gemini 3.8 Flash or Gemini 3.1 Pro. For model-specific details, see the [developer's guide to Gemini 4 Hydrogen](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-hydrogen) , the [developer's guide to Gemini 4 Carbon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-carbon) , and the [developer's guide to Gemini 4 Argon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon) .

## Quickstart

Before you begin, you must authenticate to Gemini Enterprise Agent Platform using an API key or application default credentials (ADC). See [authentication methods](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start?usertype=adc#choose_your_authentication_method) for more information.

### Install the Google Gen AI SDK

Upgrade to the latest `google-genai` SDK ( `>= 2.34.0` for Python, `@google/genai >= 2.32.0` for JavaScript/TypeScript):

```
pip install --upgrade "google-genai>=2.34.0"
```

### Set environment variables

Replace ` GOOGLE_CLOUD_PROJECT ` with your Google Cloud project ID. Gemini 4 Hydrogen and Gemini 4 Carbon are available on the `global` endpoint and in the `us` and `eu` multi-regions (Gemini 4 Argon is also available in `europe-west2` and `asia-southeast1` ):

```
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

### Make your first request

### Python

```
from google import genai

client = genai.Client()

response = client.models.generate_content(
    model="gemini-4-hydrogen",  # Or "gemini-4-carbon"
    contents="How does AI work?",
)
print(response.text)
```

### REST

```
curl -X POST \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
-H "Content-Type: application/json" \
https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-4-carbon:generateContent \
-d '{
  "contents": {
    "role": "USER",
    "parts": { "text": "How does AI work?" }
  }
}'
```

## What's new in Gemini 4

Gemini 4 models introduce the following capabilities and API changes:

### Unified input and output token limit

Gemini 4 models have a unified 1,048,576-token limit that includes both input and output tokens (where output includes thinking, function calls, and the final response). Output can use up to 1,048,576 tokens minus your input tokens. By default, a single synchronous request generates up to 65,536 output tokens (or 32,768 tokens for non-streaming direct HTTP requests on 4 Carbon and 4 Argon).

### Long decodes

When a single turn requires more than 65,536 output tokens (or 32,768 tokens for non-streaming foreground calls on 4 Carbon and 4 Argon), such as formal proofs, complex math or science problems, or multi-file code generation, Gemini 4 models support long decodes up to 1,048,576 tokens (minus your input tokens) on both the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) and `GenerateContent` ( `v1beta1` ). With the latest Google Gen AI SDK ( `google-genai >= 2.34.0` for Python, `@google/genai >= 2.32.0` for JavaScript/TypeScript, Go `>= 1.77.0` , Java `>= 1.80.0` ), setting `max_output_tokens` greater than 65,536 (or greater than 32,768 for non-streaming calls on 4 Carbon and 4 Argon) automatically follows `continuation_token` across segments to return a single response or stream. On the Interactions API, you can also run server-managed asynchronous long decodes with `background=true` or chain `continuation_token` manually in stored ( `store=true` ) or stateless ( `store=false` ) loops.

> **Note:** **Known issue** : Long decoding ( `continuation_token` ) on both the Interactions API and `GenerateContent` ( `generateContent` and `streamGenerateContent` ) is supported only in the `v1beta1` API (not `v1` ) on Agent Platform. The Google Gen AI SDK uses `v1beta1` by default unless you explicitly set `api_version='v1'` ; for direct REST calls, use the `/v1beta1/` endpoint path.

For code samples, SDK version requirements, and implementation rules, see the [developer's guide to Gemini 4 Hydrogen](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-hydrogen#long-decodes) , the [developer's guide to Gemini 4 Carbon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-carbon#long-decodes) , or the [developer's guide to Gemini 4 Argon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon#long-decodes) .

### Thinking levels

Use `thinking_level` to control how much the model reasons before it responds. Gemini 4 models support `LOW` , `MEDIUM` (default on `gemini-4-carbon` and `gemini-4-argon` ), and `HIGH` (default on `gemini-4-hydrogen` , `gemini-4-carbon-cyber-permissive` , and `gemini-4-argon-cyber-permissive` ). `gemini-4-hydrogen` also supports `XHIGH` for extended reasoning depth:

```
from google import genai
from google.genai import types

client = genai.Client()

response = client.models.generate_content(
    model="gemini-4-carbon",
    contents="Design a lock-free ring buffer in Rust for multi-producer, single-consumer telemetry ingestion.",
    config=types.GenerateContentConfig(
        thinking_config=types.ThinkingConfig(
            thinking_level=types.ThinkingLevel.HIGH,
        ),
    ),
)
print(response.text)
```

### Implicit context caching

Gemini 4 models support [implicit caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview) for shared prompt prefixes of 4,096 tokens or more, with durable caching enabled by default. To benefit from it, put static content, such as a code repository or long documents, at the start of your prompt.

### Agentic video understanding

[Agentic video understanding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing) is generally available. It's off by default: uploaded videos use `media_processing="static"` . To turn it on, set `media_processing` to `"agentic"` .

### Sampling parameters

Gemini 4 models ignore custom values for `temperature` , `top_p` , and `top_k` , as Gemini 3 models do. To control output, use `thinking_level` and structured output ( `response_schema` ).

## Migrate from Gemini 3 models

When migrating from Gemini 3.8 Flash to Gemini 4 Hydrogen, or from Gemini 3.1 Pro to Gemini 4 Carbon or Gemini 4 Argon, account for the following behavioral differences in Gemini 4 models:

| Area                                                 | Gemini 3 models                                       | Gemini 4 models                                                                                                                                                                                                                                                                                                                                                                                                                           | What to do                                                                                                                                                                                                                                                                                         |
|------------------------------------------------------|-------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Input and output token limits                        | Separate input (1,048,576) and output (65,536) limits | Unified 1,048,576-token limit across input and output (where output includes thinking, function calls, and the final response); 65,536-token default single-request output limit (32,768 tokens for non-streaming direct HTTP requests on 4 Carbon and 4 Argon), extensible up to 1,048,576 tokens using long decodes                                                                                                                     | Budget input and output together. Upgrade to the latest Google Gen AI SDK and set `max_output_tokens` greater than 65,536 (or use `background=true` or `continuation_token` in custom loops) on the Interactions API or `GenerateContent` for outputs over the single-request limit.               |
| `thinking_budget`                                    | Mapped to a thinking level                            | Returns an HTTP `400` error                                                                                                                                                                                                                                                                                                                                                                                                               | Use `thinking_level` .                                                                                                                                                                                                                                                                             |
| `thinking_level="MINIMAL"`                           | Supported                                             | Returns an HTTP `400` error                                                                                                                                                                                                                                                                                                                                                                                                               | Use `LOW` .                                                                                                                                                                                                                                                                                        |
| Explicit context caching                             | Supported                                             | Not supported                                                                                                                                                                                                                                                                                                                                                                                                                             | Remove `cached_content` references and put static content (4,096 tokens or more) at the start of your prompts.                                                                                                                                                                                     |
| Multi-turn and parallel `thought_signature` handling | Lenient duplicate signature handling                  | Only the first `functionCall` part in a parallel turn carries `thought_signature` (omitting it in the active turn or duplicating it onto sibling `functionCall` parts returns HTTP `400` ); stripping `thought_signature` values from earlier turns degrades reasoning quality and can cause `MALFORMED_FUNCTION_CALL` finish reasons; same-model prompt-prefix edits return HTTP `400` by default ( `prefix_mismatch_behavior="ERROR"` ) | Preserve `thought_signature` across all previous turns (both `functionCall` and final `text` parts), keep it only on the first `functionCall` part in a parallel turn, and set `prefix_mismatch_behavior="DROP"` in `ThinkingConfig` if your harness edits or compacts earlier conversation turns. |
| Token billing                                        | A subset of tokens is billed                          | Every token the model processes is billed, including thinking tokens and internal tool system instructions and function declarations when using grounding. Grounding with Google Search is still billed per query.                                                                                                                                                                                                                        | Review your cost estimates.                                                                                                                                                                                                                                                                        |

To migrate from `gemini-3.8-flash` or `gemini-3.1-pro-preview` , do the following:

1.  Change the model ID to `gemini-4-hydrogen` (from `gemini-3.8-flash` ) or `gemini-4-carbon` or `gemini-4-argon` (from `gemini-3.1-pro-preview` ) and upgrade to the latest Google Gen AI SDK ( `google-genai >= 2.34.0` for Python, `@google/genai >= 2.32.0` for JavaScript/TypeScript).

2.  Account for the unified 1,048,576-token input and output limit and the 65,536-token single-request output cap (32,768 tokens for non-streaming foreground calls on 4 Carbon and 4 Argon), or configure [long decodes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-hydrogen#long-decodes) for larger outputs on the Interactions API or `GenerateContent` .

3.  Replace `thinking_budget` and `thinking_level="MINIMAL"` with `thinking_level` set to `LOW` , `MEDIUM` , `HIGH` , or `XHIGH` ( `XHIGH` is supported on `gemini-4-hydrogen` ).

4.  Remove explicit `cached_content` references.

5.  Preserve `thought_signature` across all previous turns (both `functionCall` and final `text` parts), keep it only on the first `functionCall` part of parallel tool-calling turns, and set `prefix_mismatch_behavior="DROP"` if your application compacts or edits prior turns.

6.  Remove `temperature` , `top_p` , and `top_k` , which have no effect.

## Gemini 4 Carbon for cyber and Gemini 4 Argon Cyber Permissive

Gemini 4 Carbon for cyber and Gemini 4 Argon Cyber Permissive are versions of Gemini 4 Carbon and Gemini 4 Argon for defensive cybersecurity use cases, available behind an allowlist. For differences and access, see [Gemini 4 Carbon for cyber](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-carbon#cyber) and [Gemini 4 Argon Cyber Permissive](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-argon#cyber) .

## What's next

- Read the [developer's guide to Gemini 4 Hydrogen](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-hydrogen) , the [developer's guide to Gemini 4 Carbon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-carbon) , and the [developer's guide to Gemini 4 Argon](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon) .

- See the [Gemini 4 Hydrogen model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-hydrogen) , the [Gemini 4 Carbon model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-carbon) , and the [Gemini 4 Argon model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-argon) for specifications, supported features, and locations.

- Try the [Intro to Gemini 4 Carbon](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_4_carbon.ipynb) and [Intro to Gemini 4 Argon](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_4_argon.ipynb) notebook tutorials.

- Learn more about [thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking) .
