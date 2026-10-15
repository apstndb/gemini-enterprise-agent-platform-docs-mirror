---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon
title: Developer&#39;s guide to Gemini 4 Argon
description: Developer guide for Gemini 4 Argon, covering what's new, API conventions, migration steps, and a quickstart.
data_source: docs.cloud.google.com
---

**Gemini 4 Argon** is Google's frontier model that excels at deep work in complex, real-world tasks across domains including coding, finance, legal, cybersecurity, and science. It's the first model in the Gemini 4 family.

This document covers what's new with 4 Argon, the API conventions it enforces, how to migrate to it, and a quickstart. For an overview of the Gemini 4 family, see [Get started with Gemini 4](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-4) .

## What's new in Gemini 4 Argon?

- **Unified input and output token limit** : 4 Argon has a unified 1,048,576-token limit that includes both input and output tokens (where output includes thinking, function calls, and the final response).
- **Long decodes up to 1,048,576 tokens** : Extends generation beyond the single-request output limit (65,536 tokens, or 32,768 tokens for non-streaming direct HTTP requests) up to 1,048,576 tokens (minus your input tokens) on `GenerateContent` . The Google Gen AI SDK handles `continuation_token` automatically across requests, or you can manage `continuation_token` in your own continuation loop.
- **Thinking levels** : `LOW` , `MEDIUM` (default on `gemini-4-argon` ), and `HIGH` (default on `gemini-4-argon-cyber-permissive` ).
- **Implicit caching with durable caching** : Implicit caching applies automatically to shared prompt prefixes of 6,144 tokens or more, with durable caching enabled by default. Explicit context caching isn't supported.
- **Agentic video understanding** : Generally available, and off by default.

## Quickstart

Before you begin, you must authenticate to Agent Platform using Application Default Credentials (ADC) or an API key. See [Get started with Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start) for more information.

In the following code blocks, replace ` PROJECT_ID ` with your project ID.

### Try it in Agent Studio

To test prompts and configure `gemini-4-argon` in the [Agent Studio](https://console.cloud.google.com/agent-platform/studio/chat?model=gemini-4-argon) UI:

1.  Open [Agent Studio](https://console.cloud.google.com/agent-platform/studio/chat?model=gemini-4-argon) in your Google Cloud project and select `gemini-4-argon` under the Gemini group.
2.  In **Model settings** , configure:
    - **Thinking level** : Choose `Low` , `Medium` (default), or `High` .
    - **Region** : Select `Global` , `us` , or `eu` .
    - **Output token limit** : Set between `32,768` and `1,048,576` ( `1,048,576` default). Agent Studio handles continuation tokens automatically for responses over the single-request limit.

### Installation

Upgrade to the latest Google Gen AI SDK ( `google-genai >= 2.30.1` for Python, `@google/genai >= 2.29.1` for JavaScript, `>= 1.74.0` for Go, `>= 1.77.0` for Java, `>= 1.26.0` for .NET, or `>= 1.6.0` for Kotlin):

```
pip install --upgrade "google-genai>=2.30.1"
```

### Basic request

### Python (GenerateContent)

```
from google import genai
from google.genai import types

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

response = client.models.generate_content(
    model="gemini-4-argon",
    contents="Design a lock-free ring buffer in Rust for multi-producer, single-consumer telemetry ingestion.",
    config=types.GenerateContentConfig(
        thinking_config=types.ThinkingConfig(
            thinking_level="MEDIUM",  # Default: "MEDIUM" (Valid: "LOW", "MEDIUM", "HIGH")
        ),
    ),
)
print(response.text)
```

### Python (Interactions API)

```
from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

# Turn 1: Initial request (stored server-side by default)
turn1 = client.interactions.create(
    model="gemini-4-argon",
    input="Design a lock-free ring buffer in Rust for multi-producer, single-consumer telemetry ingestion.",
    store=True,
)
print(turn1.output_text)

# Turn 2: Continue the conversation using previous_interaction_id
turn2 = client.interactions.create(
    model="gemini-4-argon",
    input="Add a bounded backpressure policy and unit tests for concurrent writers.",
    previous_interaction_id=turn1.id,
)
print(turn2.output_text)
```

### REST

```
curl -X POST \
-H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
-H "Content-Type: application/json" \
"https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-4-argon:generateContent" \
-d '{
  "contents": [
    {
      "role": "user",
      "parts": [
        {
          "text": "Provide an architectural review of this Go interface."
        }
      ]
    }
  ],
  "generationConfig": {
    "thinkingConfig": {
      "thinkingLevel": "MEDIUM"
    }
  }
}'
```

### Structured output

```
from pydantic import BaseModel, Field
from google import genai
from google.genai import types

class ArchitectureReview(BaseModel):
    component: str = Field(description="Service or module name")
    bottlenecks: list[str] = Field(description="Throughput or latency bottlenecks")
    recommended_changes: list[str] = Field(description="Concrete refactoring steps")

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

response = client.models.generate_content(
    model="gemini-4-argon",
    contents="Review a synchronous order-processing pipeline backed by a single primary database at 15,000 writes/sec.",
    config=types.GenerateContentConfig(
        response_mime_type="application/json",
        response_schema=ArchitectureReview,
        thinking_config=types.ThinkingConfig(thinking_level="HIGH"),
    ),
)
print(response.text)
```

### Long decodes

By default, a single API request generates up to 65,536 output tokens (or 32,768 tokens for non-streaming direct HTTP requests), where output includes thinking, function calls, and the final response. To generate completions up to 1,048,576 tokens on `GenerateContent` ( `v1beta1` ), set `max_output_tokens` greater than 65,536 for streaming requests or greater than 32,768 for non-streaming requests (up to 1,048,576). The Google Gen AI SDK automatically follows `continuation_token` across requests when `finish_reason` is `CONTINUATION` (set `automatic_continuation=False` in `GenerateContentConfig` to disable automatic continuation), or you can pass `continuation_token` in a custom loop.

> **Note:** **Known issue** : Long decoding on `GenerateContent` ( `generateContent` and `streamGenerateContent` ) is supported only in the `v1beta1` API (not `v1` ). The Google Gen AI SDK uses `v1beta1` by default unless you override `http_options={'api_version': 'v1'}` ; for direct REST calls, use the `v1beta1` endpoint path as shown in the following example.

### Python (SDK - Recommended)

```
from google import genai
from google.genai import types

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

# Automatic continuation is enabled by default in google-genai >= 2.30.1.
# Chunks across all continuation requests are yielded as a single stream.
for chunk in client.models.generate_content_stream(
    model="gemini-4-argon",
    contents="Write a complete formal proof of the prime number theorem.",
    config=types.GenerateContentConfig(
        max_output_tokens=256000,
        thinking_config=types.ThinkingConfig(thinking_level="HIGH"),
    ),
):
    print(chunk.text, end="")

# Set automatic_continuation=False to disable automatic continuation.
for chunk in client.models.generate_content_stream(
    model="gemini-4-argon",
    contents="Write a complete formal proof of the prime number theorem.",
    config=types.GenerateContentConfig(
        thinking_config=types.ThinkingConfig(thinking_level="HIGH"),
        automatic_continuation=False,
    ),
):
    print(chunk.text, end="")
```

### REST (Custom continuation loop)

```
# Request 1: Initial request with maxOutputTokens > 32,768
curl -s -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-4-argon:generateContent" \
  -d '{
    "contents": [{
      "role": "user",
      "parts": [{"text": "Write a complete formal proof of the prime number theorem."}]
    }],
    "generationConfig": {
      "maxOutputTokens": 131072,
      "thinkingConfig": {"thinkingLevel": "HIGH"}
    }
  }'

# Request 2: Resend the original request with top-level continuationToken
# from Request 1 (candidates[0].continuationToken)
curl -s -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-4-argon:generateContent" \
  -d '{
    "contents": [{
      "role": "user",
      "parts": [{"text": "Write a complete formal proof of the prime number theorem."}]
    }],
    "continuationToken": "CONTINUATION_TOKEN_FROM_REQUEST_1",
    "generationConfig": {
      "maxOutputTokens": 131072,
      "thinkingConfig": {"thinkingLevel": "HIGH"}
    }
  }'
```

## Mandatory API rules and behavioral conventions

> **Important:** Setting `thinking_budget` or `thinking_level="MINIMAL"` returns an HTTP `400` error. Valid values for `thinking_level` are `LOW` , `MEDIUM` (default on `gemini-4-argon` ), and `HIGH` (default on `gemini-4-argon-cyber-permissive` ).

Gemini 4 Argon enforces the following conventions:

- **Thinking levels** : 4 Argon supports three `thinking_level` values ( `thinking_budget` and `MINIMAL` return an HTTP `400` validation error):

  | Thinking level                                         | Recommended workloads                                                                             |
  |--------------------------------------------------------|---------------------------------------------------------------------------------------------------|
  | `HIGH` (default on `gemini-4-argon-cyber-permissive` ) | Multi-file software engineering, formal proofs, architecture design, and vulnerability discovery. |
  | `MEDIUM` (default on `gemini-4-argon` )                | General coding, tool use, document Q&A, and video understanding.                                  |
  | `LOW`                                                  | Classification, summarization, and metadata extraction.                                           |

- **Unified input and output token limit and single-request output limits** :

  - `1,048,576` is the overall token limit of the model and includes both input and output tokens (where output includes thinking, function calls, and the final response). `max_output_tokens` controls the output token cap for the generation (up to `1,048,576` minus your input tokens); setting `max_output_tokens` greater than `1,048,576` returns an HTTP `400` error.
  - To avoid unintended long completions, the default single-request output limit (thinking + model response) is 65,536 tokens (or 32,768 tokens for non-streaming direct HTTP requests).

- **Long decodes** :

  - **How long decode works** : Long decode splits a generation up to 1,048,576 tokens across multiple `GenerateContent` inferences. For example, if a task requires 256,000 output tokens (including thoughts, function calls, and the final response), the first streaming request generates up to 65,536 output tokens and emits `finish_reason=CONTINUATION` with an encrypted `continuation_token` containing a hash of the original prompt and the generation state up to that point. Including `continuation_token` in subsequent requests with the original prompt continues generation from where it left off until `continuation_token` is no longer emitted and `finish_reason=STOP` . (In Agent Studio, setting the output token limit greater than 65,536 up to 1,048,576 handles continuation tokens automatically.)
  - **When to use long decode** : Most requests finish within the per-request limit (65,536 tokens, or 32,768 tokens for non-streaming REST calls). Use long decode only when one response needs more output than that. Long decode gives the model more room to reason; it does not make answers longer (use `thinking_level` to control reasoning depth).

  | Workload                                                         | Use long decode? | Why                                                                                                                                     |
  |------------------------------------------------------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
  | Hard math, science, research, and formal proofs                  | Yes              | The model can spend more than 65,536 tokens to explore and check its reasoning.                                                         |
  | The hardest coding and agentic tasks                             | Yes              | Some tasks need more than 65,536 tokens of thinking and code in one response. Most coding and agentic tasks finish under 65,536 tokens. |
  | Evaluation harnesses that stop at the output limit               | Yes              | Long decode prevents cut-off answers when the model spends an entire 65,536- or 32,768-token request on thinking.                       |
  | Chat, Q&A, summarization, classification, and extraction         | No               | These tasks finish well under 32,768 tokens.                                                                                            |
  | Requests for a fixed length, such as "write a 700,000-word book" | No               | The model does not follow length targets.                                                                                               |
  | Agents that call tools in many short turns                       | No               | Each turn is short. Large outputs on each turn fill the unified 1,048,576-token input and output limit quickly.                         |
  | Prompts near the 1,048,576-token input limit                     | No               | Output can use only 1,048,576 tokens minus your input.                                                                                  |
  | Latency-sensitive requests                                       | No               | Long decode can run for several minutes.                                                                                                |

  - **Choosing a continuation option** : Choose one of two options. Most developers use Option 1. All options reach the same 1,048,576-token limit on `gemini-4-argon` and `gemini-4-argon-cyber-permissive` .

  | Dimension               | Option 1: Google Gen AI SDK (recommended)                                                                                                                                         | Option 2: Your own streaming loop ( `streamGenerateContent` )        | Option 2: Your own non-streaming loop ( `generateContent` ) |
  |-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------|-------------------------------------------------------------|
  | Who starts each segment | Google Gen AI SDKs: Python ( `google-genai` ) 2.30.1, JavaScript ( `@google/genai` ) 2.29.1, Go 1.74.0, Java 1.77.0, .NET 1.26.0, and Kotlin 1.6.0. You set `max_output_tokens` . | Your code, at each checkpoint or after a dropped stream              | Your code, every 32,768 tokens                              |
  | Tokens per request      | Up to 65,536 per segment                                                                                                                                                          | 65,536 per stream, with a checkpoint every 5,000 tokens after 32,768 | 32,768 per request                                          |
  | Time limit per request  | 20 minutes                                                                                                                                                                        | 20 minutes                                                           | 20 minutes                                                  |
  | Storage                 | No server storage (ZDR-compliant)                                                                                                                                                 | No server storage (ZDR-compliant)                                    | No server storage (ZDR-compliant)                           |
  | Best for                | Most applications                                                                                                                                                                 | REST callers and custom harnesses that stream                        | Simple evaluation harnesses                                 |

  - **Implementation rules and limitations** :
    - **`v1beta1` API requirement (known issue)** : Long decoding ( `continuation_token` ) on `GenerateContent` ( `generateContent` and `streamGenerateContent` ) is supported only in the `v1beta1` API (not `v1` ). The Google Gen AI SDK uses `v1beta1` by default unless `api_version='v1'` is specified in `http_options` ; for direct REST calls, use the `v1beta1` endpoint path. Long decode isn't supported on the Interactions API.
    - **SDK versions and OpenAI compatibility** : Upgrade to the latest Google Gen AI SDK ( `google-genai >= 2.30.1` for Python, `@google/genai >= 2.29.1` for JavaScript, `>= 1.74.0` for Go, `>= 1.77.0` for Java, `>= 1.26.0` for .NET, or `>= 1.6.0` for Kotlin). Older SDK versions and the OpenAI compatibility layer cannot retrieve long completions using continuation tokens. For custom client implementations, refer to the Google Gen AI SDK reference implementations in [Python](https://github.com/googleapis/python-genai/blob/v2.30.1/google/genai/models.py#L6111) and [JavaScript/TypeScript](https://github.com/googleapis/js-genai/blob/v2.29.1/src/models.ts#L88) .
    - **Resend the original request with `continuation_token`** : In a custom loop, set `max_output_tokens` greater than 65,536 (streaming) or 32,768 (unary) up to 1,048,576, and resend the original `contents` , `system_instruction` , and `tools` on every continuation request along with the latest `continuation_token` (a top-level field on `GenerateContentRequest` in REST, or in `GenerateContentConfig` in the Google Gen AI SDK). Don't append partial model output into `contents` or send a follow-up prompt asking the model to continue.
    - **Continue through thinking-only requests** : Loop while `finish_reason` is `CONTINUATION` and `continuation_token` is present, even if a request spent all 32,768 or 65,536 tokens thinking ( `parts: [{"text": ""}]` ). If `finish_reason` is `MAX_TOKENS` when `continuation_token` is present, generation reached the requested `max_output_tokens` cap—raise `max_output_tokens` in the request. Combine accumulated parts into a single `model` turn for multi-turn history only after `STOP` .
    - **Token counting, compaction, and 95% implicit cache discount** :
      - In the Python Google Gen AI SDK ( `generate_content` and `generate_content_stream` ), the final response or chunk's `usage_metadata` accumulates total billed tokens across continuation requests. Because each continuation request re-prefills prior partial completions as input tokens, `prompt_token_count` increases cumulatively across continuation requests—don't use `prompt_token_count` to trigger context compaction in agent harnesses. Instead, read `initial_prompt_token_count` (on `GenerateContentResponse` or `usage_metadata` ), and wait until `GenerateContent` completes (no `continuation_token` present) before compacting.
      - In custom REST loops, `usage_metadata` is cumulative within each request; sum the final `prompt_token_count` , `cached_content_token_count` , `candidates_token_count` , and `thoughts_token_count` across requests.
      - Each continuation request re-prefills the prompt plus prior decoded tokens and automatically receives the 95% implicit context caching discount (6,144-token minimum) when requests run back-to-back within the 15–20 minute cache TTL.
      - `streamGenerateContent` and `generateContent` return `usage_metadata` at the end of each request (65,536 streaming / 32,768 unary), and billing occurs at the end of the request.

- **Ignored sampling parameters ( `temperature` , `top_k` , `top_p` )** : The backend ignores custom values. Control reasoning depth with `thinking_level` , and output format with `response_schema` .

- **Unsupported parameters ( `frequency_penalty` , `presence_penalty` , `candidate_count` )** : These return an HTTP `400` error. Remove them from your requests.

- **Context caching** : Explicit context caching isn't supported. Implicit caching (with durable caching enabled by default) applies automatically to shared prompt prefixes of 6,144 tokens or more, so put static content at the start of your prompt.

- **Agentic video** : Uploaded videos default to `media_processing="static"` . Set `media_processing="agentic"` to enable [agentic video processing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing) .

- **Token counting and billing** : Every token the model processes is counted and billed, including thinking tokens and internal tool system instructions and function declarations when using grounding. Grounding with Google Search also remains billed per query.

- **Function calling** :

  - **Turn symmetry** : Each `FunctionResponse` must match the `id` , `name` , and order of the preceding `FunctionCall` .

  - **Sequential execution** : Prefer sequential tool execution turns in multi-step tool loops.

  - **Pre-tool formatting** : Separate inline instructions with `\n\n` and avoid unstructured text before tool calls. To log intermediate state before a tool call, use a dedicated function declaration:

    ```
    {
      "name": "update",
      "description": "Update working notes before tool execution",
      "parameters": {
        "type": "OBJECT",
        "properties": {
          "previous_step": {"type": "STRING"},
          "plan": {"type": "STRING"},
          "next_step": {"type": "STRING"}
        },
        "required": ["previous_step", "plan", "next_step"]
      }
    }
    ```

- **Chat sequence validation** :

  - History payloads can't end with a `model` role turn.
  - Prefilled model turns aren't supported.

## Migrate to 4 Argon from 3.1 Pro

The following behavior is different from `gemini-3.1-pro-preview` :

- 4 Argon has a unified 1,048,576-token limit across input and output (where output includes thinking, function calls, and the final response), instead of separate input and output limits. Single-request output is capped at 65,536 tokens (or 32,768 tokens for non-streaming direct HTTP requests), and can be extended up to 1,048,576 tokens using [long decodes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon#long-decodes) on `GenerateContent` (handled automatically in the Google Gen AI SDK, or using `continuation_token` in custom loops).
- `thinking_budget` returns an HTTP `400` error instead of being mapped to a thinking level. `MINIMAL` also returns an error.
- Explicit context caching isn't supported.
- Every token the model processes is billed, including internal tool system instructions and function declarations when using grounding.

For a side-by-side comparison, see [Migrate from Gemini 3.1 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-4#migrate) .

```
 client = genai.Client(
     enterprise=True,
     project="PROJECT_ID",
     location="global", # Supports "global", "us", and "eu"
 )

 response = client.models.generate_content(
-    model="gemini-3.1-pro-preview",
+    model="gemini-4-argon",
     contents=prompt,
     config=types.GenerateContentConfig(
-        temperature=0.0,
-        cached_content="projects/.../cachedContents/...", # Explicit caching unsupported
         thinking_config=types.ThinkingConfig(
-            thinking_budget=16384, # Returns HTTP 400 instead of mapping silently
-            thinking_level="MINIMAL", # MINIMAL unsupported on Gemini 4 Argon
+            thinking_level="MEDIUM", # Valid: "LOW", "MEDIUM" (default), "HIGH"
         ),
     ),
 )
```

To migrate from `gemini-3.1-pro-preview` , do the following:

1.  **Update the model ID** to `gemini-4-argon` (or `gemini-4-argon-cyber-permissive` for Fairwind-approved cybersecurity workloads).
2.  **Upgrade to the latest Google Gen AI SDK and account for the unified input and output token limit** : Upgrade to `google-genai >= 2.30.1` (Python), `@google/genai >= 2.29.1` (JavaScript), or the equivalent latest Google Gen AI SDK. Input and output tokens (including thinking and function calls) share the unified 1,048,576-token limit. For outputs exceeding 65,536 tokens (up to 1,048,576 tokens) on `GenerateContent` , set `max_output_tokens` greater than 65,536 so the Google Gen AI SDK continues automatically across requests (or handle `continuation_token` in your own REST loop).
3.  **Replace the reasoning budget parameter** : Replace `thinking_budget` and `MINIMAL` with `thinking_level` set to `LOW` , `MEDIUM` (default on `gemini-4-argon` ), or `HIGH` (default on `gemini-4-argon-cyber-permissive` ).
4.  **Remove explicit caching** and front-load static prompt content (6,144 tokens or more) for automatic implicit caching.
5.  **Remove parameters that have no effect or aren't supported** :
    - Remove `temperature` , `top_p` , and `top_k` , which are ignored.
    - Remove `candidate_count` , `frequency_penalty` , and `presence_penalty` .
    - Remove any prefilled model turns from conversation histories.

## Summary checklist for developers

Target model ID: `gemini-4-argon` (or `gemini-4-argon-cyber-permissive` for Fairwind-approved projects), and upgrade to the latest Google Gen AI SDK (Python `google-genai >= 2.30.1` , JS `@google/genai >= 2.29.1` , Go `>= 1.74.0` , Java `>= 1.77.0` , .NET `>= 1.26.0` , Kotlin `>= 1.6.0` )

Location: `global` , `us` , or `eu`

Budget for a unified 1,048,576-token input and output limit and a 65,536-token single-request output cap (32,768 tokens for non-streaming direct HTTP calls), or set `max_output_tokens` up to 1,048,576 on `GenerateContent` for long decodes.

Use `thinking_level` ( `MEDIUM` by default on `gemini-4-argon` , `HIGH` by default on `gemini-4-argon-cyber-permissive` ; valid values: `LOW` , `MEDIUM` , `HIGH` ). Remove `thinking_budget` and `MINIMAL` .

Remove the following parameters: `frequency_penalty` , `presence_penalty` , `candidate_count` , `temperature` , `top_p` , and `top_k` .

Remove any prefilled model turns from multi-turn chat request histories.

Remove explicit caching calls, and put static prompt content (6,144 tokens or more) first for implicit caching.

## Known issues

- **Long decodes on `GenerateContent` require `v1beta1`** : Long decoding ( `continuation_token` ) on the `GenerateContent` API ( `generateContent` and `streamGenerateContent` ) is supported only in the `v1beta1` API (not `v1` ). The Google Gen AI SDK uses `v1beta1` by default unless `api_version='v1'` is set in `http_options` ; for direct REST calls, use the `v1beta1` endpoint path.

## Additional resources

- [Gemini 4 Argon model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-argon)
- [Get started with Gemini 4](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-4)
- [Introductory notebook](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_4_argon.ipynb)
- [Gemini 4 Argon Cyber Permissive](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-argon#cyber)
