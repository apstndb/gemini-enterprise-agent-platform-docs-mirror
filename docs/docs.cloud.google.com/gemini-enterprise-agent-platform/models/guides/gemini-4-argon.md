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
- **Long decodes up to 1,048,576 tokens** : Extends generation beyond the single-request output limit (65,536 tokens when streaming, or 32,768 tokens for non-streaming foreground requests) up to 1,048,576 tokens (minus your input tokens) on both the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) and `GenerateContent` ( `v1beta1` ). The Google Gen AI SDK handles `continuation_token` automatically across segments, or you can run asynchronous server-managed background decodes ( `background=true` ) or manage `continuation_token` in a custom continuation loop.
- **Thinking levels** : `LOW` , `MEDIUM` (default on `gemini-4-argon` ), and `HIGH` (default on `gemini-4-argon-cyber-permissive` ).
- **Implicit caching with durable caching** : Implicit caching applies automatically to shared prompt prefixes of 4,096 tokens or more, with durable caching enabled by default. Explicit context caching isn't supported.
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

Upgrade to the latest Google Gen AI SDK. Automatic continuation on the Interactions API requires `google-genai >= 2.34.0` for Python, `@google/genai >= 2.32.0` for JavaScript/TypeScript, `>= 1.77.0` for Go, or `>= 1.80.0` for Java (on `GenerateContent` , automatic continuation requires `>= 2.30.1` for Python, `>= 2.29.1` for JavaScript/TypeScript, `>= 1.74.0` for Go, `>= 1.77.0` for Java, `>= 1.26.0` for .NET, or `>= 1.6.0` for Kotlin):

```
pip install --upgrade "google-genai>=2.34.0"
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

### Long decode examples

By default, a single foreground API segment generates up to 65,536 output tokens when streaming or 32,768 output tokens when non-streaming, where output includes thinking, function calls, and the final response. To generate completions up to 1,048,576 tokens (minus your input tokens), use long decodes on either the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) or `GenerateContent` . For continuation options, status transitions, and validation rules, see [Long decodes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon#long-decodes) .

> **Note:** **Known issue** : Long decoding ( `continuation_token` ) on both the Interactions API and `GenerateContent` ( `generateContent` and `streamGenerateContent` ) is supported only in the `v1beta1` API (not `v1` ) on Agent Platform. The Google Gen AI SDK uses `v1beta1` by default unless you override `api_version='v1'` ; for direct REST calls, use the `/v1beta1/` endpoint path as shown in the following examples.

#### Use long decodes with the Interactions API

In `google-genai >= 2.34.0` (Python), `@google/genai >= 2.32.0` (JavaScript/TypeScript), Go `>= 1.77.0` , and Java `>= 1.80.0` , `interactions.create()` automatically follows `continuation_token` across segments whenever a segment returns `status="requires_continuation"` . You can also opt out ( `automatic_continuation=False` ) to run a custom stored ( `store=True` ) or stateless ( `store=False` ) loop:

### Python (SDK automatic)

```
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

# Automatic continuation is enabled by default in google-genai >= 2.34.0.
# Unary calls merge all segments into one Interaction with summed usage.
interaction = client.interactions.create(
    model="gemini-4-argon",
    input="Write a complete formal proof of the prime number theorem.",
    generation_config={
        "max_output_tokens": 256000,
        "thinking_level": "high",
    },
)
print(interaction.output_text)
print(f"Merged segment IDs: {interaction.continuation_ids}")
print(f"Initial input tokens: {interaction.usage.initial_input_tokens}")

# Optional: Delete each stored server segment (last segment first) before its 7-day TTL expires.
for segment_id in reversed(interaction.continuation_ids or [interaction.id]):
    client.interactions.delete(id=segment_id)

# Streaming yields events across all segments in order. Intermediate segments
# emit interaction.completed with status="requires_continuation".
stream = client.interactions.create(
    model="gemini-4-argon",
    input="Write a complete formal proof of the prime number theorem.",
    stream=True,
    generation_config={
        "max_output_tokens": 256000,
        "thinking_level": "high",
    },
)
for event in stream:
    if event.event_type == "step.delta" and getattr(event.delta, "text", None):
        print(event.delta.text, end="", flush=True)
    elif (
        event.event_type == "interaction.completed"
        and event.interaction.status != "requires_continuation"
    ):
        print(f"\nFinal status: {event.interaction.status}")

# Set automatic_continuation=False to return after a single segment.
single_segment = client.interactions.create(
    model="gemini-4-argon",
    input="Write a complete formal proof of the prime number theorem.",
    generation_config={"max_output_tokens": 256000, "thinking_level": "high"},
    automatic_continuation=False,
)
```

### Python (Custom loop)

```
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

prompt = "Write a complete formal proof of the prime number theorem."

# Stored loop (store=True, default): chain previous_interaction_id + continuation_token
# without resending input.
segment = client.interactions.create(
    model="gemini-4-argon",
    input=prompt,
    store=True,
    generation_config={"max_output_tokens": 131072, "thinking_level": "high"},
    automatic_continuation=False,
)
full_text = segment.output_text or ""

while segment.status == "requires_continuation" and segment.continuation_token:
    segment = client.interactions.create(
        model="gemini-4-argon",
        previous_interaction_id=segment.id,
        continuation_token=segment.continuation_token,
        generation_config={"max_output_tokens": 131072, "thinking_level": "high"},
        automatic_continuation=False,
    )
    full_text += segment.output_text or ""

# If status == "incomplete", max_output_tokens was exhausted; raise max_output_tokens
# to continue (leaving default automatic_continuation=True lets the SDK finish remaining segments).
if segment.status == "incomplete" and segment.continuation_token:
    segment = client.interactions.create(
        model="gemini-4-argon",
        previous_interaction_id=segment.id,
        continuation_token=segment.continuation_token,
        generation_config={"max_output_tokens": 256000, "thinking_level": "high"},
    )
    full_text += segment.output_text or ""

# Stateless loop (store=False): resend original input + continuation_token
# with no previous_interaction_id.
stateless_seg = client.interactions.create(
    model="gemini-4-argon",
    input=prompt,
    store=False,
    generation_config={"max_output_tokens": 131072, "thinking_level": "high"},
    automatic_continuation=False,
)
stateless_text = stateless_seg.output_text or ""
while stateless_seg.status == "requires_continuation" and stateless_seg.continuation_token:
    stateless_seg = client.interactions.create(
        model="gemini-4-argon",
        input=prompt,
        store=False,
        continuation_token=stateless_seg.continuation_token,
        generation_config={"max_output_tokens": 131072, "thinking_level": "high"},
        automatic_continuation=False,
    )
    stateless_text += stateless_seg.output_text or ""
```

### REST (Stored)

```
# Segment 1: Start a stored interaction (store=true by default)
curl -s -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" \
  -d '{
    "model": "gemini-4-argon",
    "store": true,
    "input": "Write a complete formal proof of the prime number theorem.",
    "generation_config": {
      "max_output_tokens": 131072,
      "thinking_level": "high"
    }
  }'

# Segment 2: When status is "requires_continuation", pass previous_interaction_id
# and continuation_token without resending input
curl -s -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" \
  -d '{
    "model": "gemini-4-argon",
    "store": true,
    "previous_interaction_id": "SEGMENT_1_ID",
    "continuation_token": "CONTINUATION_TOKEN",
    "generation_config": {
      "max_output_tokens": 131072,
      "thinking_level": "high"
    }
  }'
```

### REST (Stateless)

```
# Segment 1: Stateless interaction (store=false)
curl -s -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" \
  -d '{
    "model": "gemini-4-argon",
    "store": false,
    "input": "Write a complete formal proof of the prime number theorem.",
    "generation_config": {
      "max_output_tokens": 131072,
      "thinking_level": "high"
    }
  }'

# Segment 2: Resend the original input and continuation_token (no previous_interaction_id)
curl -s -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" \
  -d '{
    "model": "gemini-4-argon",
    "store": false,
    "input": "Write a complete formal proof of the prime number theorem.",
    "continuation_token": "CONTINUATION_TOKEN",
    "generation_config": {
      "max_output_tokens": 131072,
      "thinking_level": "high"
    }
  }'
```

For asynchronous server-managed execution ( `background=True` with `store=True` ) or recovery from streaming checkpoints ( `interaction.status_update` events emitted at 32,768 output tokens and every 5,000 tokens thereafter), use the following patterns:

### Python (Background)

```
import time
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

# Start a server-managed background long decode (requires store=True)
interaction = client.interactions.create(
    model="gemini-4-argon",
    input="Write a complete formal proof of the prime number theorem.",
    background=True,
    store=True,
    generation_config={"max_output_tokens": 256000, "thinking_level": "high"},
)

while interaction.status in ("queued", "in_progress"):
    time.sleep(10)
    interaction = client.interactions.get(id=interaction.id)

print(f"Status: {interaction.status}")
print(interaction.output_text)

# Optional: Cancel an in-progress background interaction and resume later
# from its persisted checkpoint continuation_token (if >= 32,768 tokens decoded).
# cancelled = client.interactions.cancel(id=interaction.id)
# if cancelled.continuation_token:
#     resumed = client.interactions.create(
#         model="gemini-4-argon",
#         previous_interaction_id=cancelled.id,
#         continuation_token=cancelled.continuation_token,
#         background=True,
#         generation_config={"max_output_tokens": 256000, "thinking_level": "high"},
#     )
```

### REST (Background)

```
# Start a server-managed background long decode (requires store=true)
curl -s -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" \
  -d '{
    "model": "gemini-4-argon",
    "background": true,
    "store": true,
    "input": "Write a complete formal proof of the prime number theorem.",
    "generation_config": {
      "max_output_tokens": 256000,
      "thinking_level": "high"
    }
  }'

# Poll the interaction until status reaches completed, incomplete, failed, or cancelled
curl -s -X GET \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID"

# Optional: Cancel an in-progress background decode
curl -s -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID/cancel"

# Optional: Resume a cancelled background decode from its checkpoint continuation_token
curl -s -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" \
  -d '{
    "model": "gemini-4-argon",
    "background": true,
    "store": true,
    "previous_interaction_id": "INTERACTION_ID",
    "continuation_token": "CONTINUATION_TOKEN",
    "generation_config": {
      "max_output_tokens": 256000,
      "thinking_level": "high"
    }
  }'
```

### Python (Streaming checkpoints)

```
from google import genai
from google.genai import errors

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

# With default automatic_continuation=True, stream=True automatically
# reconnects from the latest interaction.status_update checkpoint (32,768
# output tokens, then every 5,000 tokens) if no output was yielded after the
# checkpoint. If a disconnect occurs after output was yielded since the last
# checkpoint, the SDK raises ContinuationInterruptedError so you can resume
# from err.continuation_token.
stream = client.interactions.create(
    model="gemini-4-argon",
    input="Write a complete formal proof of the prime number theorem.",
    stream=True,
    store=True,
    generation_config={"max_output_tokens": 256000, "thinking_level": "high"},
)

try:
    for event in stream:
        if event.event_type == "step.delta" and getattr(event.delta, "text", None):
            print(event.delta.text, end="", flush=True)
except errors.ContinuationInterruptedError as err:
    # Resuming from a mid-segment checkpoint regenerates any output yielded
    # after that checkpoint.
    if err.interaction_id and err.continuation_token:
        resumed_stream = client.interactions.create(
            model="gemini-4-argon",
            previous_interaction_id=err.interaction_id,
            continuation_token=err.continuation_token,
            stream=True,
            store=True,
            generation_config={"max_output_tokens": 256000, "thinking_level": "high"},
        )
        for event in resumed_stream:
            if event.event_type == "step.delta" and getattr(event.delta, "text", None):
                print(event.delta.text, end="", flush=True)
```

### REST (Streaming checkpoints)

```
# Start a streaming interaction; save interaction.id from interaction.created
# and the latest continuation_token from interaction.status_update SSE events
curl -N -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" \
  -d '{
    "model": "gemini-4-argon",
    "stream": true,
    "store": true,
    "input": "Write a complete formal proof of the prime number theorem.",
    "generation_config": {
      "max_output_tokens": 256000,
      "thinking_level": "high"
    }
  }'

# Resume a dropped stream from the last saved checkpoint continuation_token
# (for store=false, resend the original input instead of previous_interaction_id)
curl -N -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/interactions" \
  -d '{
    "model": "gemini-4-argon",
    "stream": true,
    "store": true,
    "previous_interaction_id": "SEGMENT_ID",
    "continuation_token": "CHECKPOINT_CONTINUATION_TOKEN",
    "generation_config": {
      "max_output_tokens": 256000,
      "thinking_level": "high"
    }
  }'
```

#### Use long decodes with GenerateContent

On `GenerateContent` ( `v1beta1` ), set `max_output_tokens` greater than 65,536 for streaming requests or greater than 32,768 for non-streaming requests (up to 1,048,576). The Google Gen AI SDK automatically follows `continuation_token` across segments when `finish_reason` is `CONTINUATION` (set `automatic_continuation=False` in `GenerateContentConfig` to opt out), or you can pass `continuation_token` in a custom loop:

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
    "continuationToken": "CONTINUATION_TOKEN",
    "generationConfig": {
      "maxOutputTokens": 131072,
      "thinkingConfig": {"thinkingLevel": "HIGH"}
    }
  }'
```

## Mandatory API rules and behavioral conventions

> **Important:** Setting `thinking_budget` or `thinking_level="MINIMAL"` returns an HTTP `400` error. Valid values for `thinking_level` are `LOW` , `MEDIUM` (default on `gemini-4-argon` ), and `HIGH` (default on `gemini-4-argon-cyber-permissive` ).

4 Argon enforces the conventions in the following sections for thinking levels, token limits, caching, generation parameters, and multi-turn tool execution.

### Thinking levels

4 Argon supports three `thinking_level` values ( `thinking_budget` and `MINIMAL` return an HTTP `400` validation error). The following table lists each thinking level and its recommended workloads:

| Thinking level                                         | Recommended workloads                                                                             |
|--------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| `HIGH` (default on `gemini-4-argon-cyber-permissive` ) | Multi-file software engineering, formal proofs, architecture design, and vulnerability discovery. |
| `MEDIUM` (default on `gemini-4-argon` )                | General coding, tool use, document Q&A, and video understanding.                                  |
| `LOW`                                                  | Classification, summarization, and metadata extraction.                                           |

### Token limits, caching, and billing

4 Argon applies the following token, caching, media, and billing rules:

- **Unified input and output token limit and single-request output limits** : Token budgets and per-request limits work as follows:
  - The overall token limit of the model is `1,048,576` tokens and includes both input and output tokens (where output includes thinking, function calls, and the final response). `max_output_tokens` controls the output token cap for the generation (up to `1,048,576` minus your input tokens); setting `max_output_tokens` greater than `1,048,576` returns an HTTP `400` error.
  - To avoid unintended long completions, the default single-request output limit (thinking + model response) is 65,536 tokens (or 32,768 tokens for non-streaming direct HTTP requests).
- **Long decodes** : Single-segment foreground responses generate up to 65,536 output tokens when streaming or 32,768 output tokens when non-streaming. To extend single-turn output up to 1,048,576 tokens (minus input tokens) on the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) or `GenerateContent` ( `v1beta1` ), see [Long decodes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon#long-decodes) .
- **Context caching** : Explicit context caching isn't supported. Implicit caching (with durable caching enabled by default) applies automatically to shared prompt prefixes of 4,096 tokens or more, so put static content at the start of your prompt.
- **Agentic video** : Uploaded videos default to `media_processing="static"` . Set `media_processing="agentic"` to enable [agentic video processing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing) .
- **Token counting and billing** : Every token the model processes is counted and billed, including thinking tokens and internal tool system instructions and function declarations when using grounding. Grounding with Google Search also remains billed per query.

### Parameters, function calling, and chat validation

4 Argon enforces the following rules for generation parameters, tool calls, and chat history:

- **Ignored sampling parameters ( `temperature` , `top_k` , `top_p` )** : The backend ignores custom values. Control reasoning depth with `thinking_level` , and output format with `response_schema` .

- **Unsupported parameters ( `frequency_penalty` , `presence_penalty` , `candidate_count` )** : These return an HTTP `400` error. Remove them from your requests.

- **Function calling** : Tool declarations and execution turns follow these rules:

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

- **Chat sequence validation** : Multi-turn chat payloads enforce the following constraints:

  - History payloads can't end with a `model` role turn.
  - Prefilled model turns aren't supported.

## Long decodes

Long decode splits a generation up to 1,048,576 tokens (minus your input tokens) across multiple segments on either the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) or `GenerateContent` ( `v1beta1` ). On the Interactions API, each foreground segment generates up to 65,536 output tokens when streaming ( `stream=true` ) or 32,768 output tokens when non-streaming ( `stream=false` ) and returns `status="requires_continuation"` with an encrypted `continuation_token` , or you can set `background=true` ( `store=true` ) so the server runs the continuation loop asynchronously and stores the merged output in one `Interaction` . On `GenerateContent` , streaming segments generate up to 65,536 output tokens and non-streaming segments generate up to 32,768 output tokens before emitting `finish_reason=CONTINUATION` with `continuation_token` , continuing until `finish_reason=STOP` . In Agent Studio, setting the output token limit greater than 65,536 up to 1,048,576 handles continuation tokens automatically. For runnable code samples, see the [Long decode quickstart examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon#long-decodes-quickstart) .

### When to use long decode

Most requests finish within the per-request limit (65,536 tokens, or 32,768 tokens for non-streaming REST calls). Use long decode only when one response needs more output than that. Long decode gives the model more room to reason; it does not make answers longer (use `thinking_level` to control reasoning depth).

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

### Choose a continuation option

Select a continuation pattern based on your API surface, storage posture, and runtime environment. All options in the following table reach the same 1,048,576-token limit (minus input tokens) on `gemini-4-argon` and `gemini-4-argon-cyber-permissive` .

| Continuation option                                        | API surface                     | Who starts each segment                                                                                                                                                      | Tokens per segment                                                                                                    | Time limit per request                        | Server storage                                                                                                                                                                                                   | Best for                                                                               |
|------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|-----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| **Google Gen AI SDK automatic continuation (recommended)** | Interactions API ( `v1beta1` )  | Google Gen AI SDKs: Python ( `google-genai >= 2.34.0` ), JavaScript/TypeScript ( `@google/genai >= 2.32.0` ), Go ( `>= 1.77.0` ), and Java ( `>= 1.80.0` )                   | Up to 65,536 ( `stream=true` ) or 32,768 ( `stream=false` )                                                           | 20 minutes per segment                        | [7-day server storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide#session-lifecycle) by default ( `store=true` ), or none ( `store=false` ) | Most stateful or stateless Interactions API applications                               |
| **Background server-managed loop ( `background=true` )**   | Interactions API ( `v1beta1` )  | Agent Platform server loop; your code polls `get`                                                                                                                            | Managed server-side up to `max_output_tokens`                                                                         | Asynchronous (no open client stream required) | 7-day server storage ( `store=true` required)                                                                                                                                                                    | Asynchronous jobs, callers in other languages over REST, and single-record persistence |
| **Custom foreground stored loop ( `store=true` )**         | Interactions API ( `v1beta1` )  | Your code ( `previous_interaction_id` + `continuation_token` , no `input` )                                                                                                  | Up to 65,536 ( `stream=true` , checkpoints every 5,000 tokens after 32,768) or 32,768 ( `stream=false` )              | 20 minutes per segment                        | 7-day server storage ( `store=true` )                                                                                                                                                                            | REST callers and custom checkpoint recovery                                            |
| **Custom foreground stateless loop ( `store=false` )**     | Interactions API ( `v1beta1` )  | Your code (original `input` + `continuation_token` , no `previous_interaction_id` )                                                                                          | Up to 65,536 ( `stream=true` , checkpoints every 5,000 tokens after 32,768) or 32,768 ( `stream=false` )              | 20 minutes per segment                        | No server storage ( [Zero Data Retention](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention#customer-data-retention) workflows)                                       | Custom REST harnesses requiring stateless execution                                    |
| **Google Gen AI SDK automatic continuation (recommended)** | `GenerateContent` ( `v1beta1` ) | Google Gen AI SDKs: Python ( `>= 2.30.1` ), JavaScript/TypeScript ( `>= 2.29.1` ), Go ( `>= 1.74.0` ), Java ( `>= 1.77.0` ), .NET ( `>= 1.26.0` ), and Kotlin ( `>= 1.6.0` ) | Up to 65,536 ( `generate_content_stream` ) or 32,768 ( `generate_content` )                                           | 20 minutes per segment                        | No server storage ( [Zero Data Retention](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention#customer-data-retention) workflows)                                       | Existing `GenerateContent` applications                                                |
| **Custom continuation loop**                               | `GenerateContent` ( `v1beta1` ) | Your code (original `contents` + `continuation_token` )                                                                                                                      | Up to 65,536 ( `streamGenerateContent` , checkpoints every 5,000 tokens after 32,768) or 32,768 ( `generateContent` ) | 20 minutes per segment                        | No server storage ( [Zero Data Retention](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention#customer-data-retention) workflows)                                       | Direct REST `GenerateContent` callers and evaluation harnesses                         |

### API version and SDK requirements

Long decodes require the following API version and minimum SDK versions:

- **`v1beta1` API requirement (known issue)** : Long decoding ( `continuation_token` ) on both the Interactions API and `GenerateContent` ( `generateContent` and `streamGenerateContent` ) is supported only in the `v1beta1` API (not `v1` ) on Agent Platform. The Google Gen AI SDK uses `v1beta1` by default unless `api_version='v1'` is specified in `http_options` (or `api_version="v1"` on `interactions.create` ); for direct REST calls, use the `/v1beta1/` endpoint path.
- **SDK versions and OpenAI compatibility** : For automatic continuation on the Interactions API, upgrade to Python `google-genai >= 2.34.0` , JavaScript/TypeScript `@google/genai >= 2.32.0` , Go `>= 1.77.0` , or Java `>= 1.80.0` (for other languages on the Interactions API, call the REST API directly with `background=true` or a custom continuation loop). For automatic continuation on `GenerateContent` , upgrade to Python `>= 2.30.1` , JavaScript/TypeScript `>= 2.29.1` , Go `>= 1.74.0` , Java `>= 1.77.0` , .NET `>= 1.26.0` , or Kotlin `>= 1.6.0` . Earlier SDK versions and the OpenAI compatibility layer cannot retrieve long completions using continuation tokens.

### Interactions API continuation rules

The following status transitions, chaining rules, and storage behaviors apply to long decodes on the Interactions API.

#### Status values and output token budget

When `generation_config.max_output_tokens` is omitted on an Interactions API request, the total output budget defaults to 65,536 tokens (so a non-streaming call stops at 32,768 tokens with `status="requires_continuation"` , and a second segment can generate the remaining 32,768 tokens). Set `generation_config.max_output_tokens` up to `1,048,576` (minus input tokens) for longer decodes in both foreground and `background=true` modes. The server returns the following status values:

- `requires_continuation` : The per-segment output limit (32,768 non-streaming or 65,536 streaming) was reached before `max_output_tokens` ; pass the returned `continuation_token` on the next request to continue decoding.
- `incomplete` : The total `max_output_tokens` budget was exhausted; continuing with `continuation_token` without raising `max_output_tokens` returns an HTTP `400` error ( `max_output_tokens has already been exhausted` ). Increase `max_output_tokens` on the next request to resume decoding.
- `completed` : Generation finished naturally and `continuation_token` is cleared.

#### Chaining, mode switching, and segment storage

Continuation requests on the Interactions API enforce the following rules:

- **Stored continuation ( `store=true` , default)** : Pass `previous_interaction_id` set to the segment `id` that issued the `continuation_token` along with `continuation_token` , and omit `input` (the stored segment already holds the turn input). Always pair each `continuation_token` with the `previous_interaction_id` of the segment that issued it; passing a `continuation_token` on an already `completed` interaction returns an HTTP `400` error.
- **Stateless continuation ( `store=false` )** : Omit `previous_interaction_id` and resend the original `input` alongside `continuation_token` on every segment.
- **Switching `store` modes across segments** : You can switch from stored ( `store=true` ) to stateless ( `store=false` ) mid-decode by omitting `previous_interaction_id` and resending the original `input` with `continuation_token` . Switching from stateless ( `store=false` ) to stored ( `store=true` ) isn't supported because no stored parent interaction exists for `previous_interaction_id` .
- **Foreground and `background=true` mode switching and branching** : Stored continuations ( `store=true` ) can switch between foreground ( `background=false` ) and background ( `background=true` ) execution across segments, including resuming a cancelled `background=true` interaction from its checkpoint `continuation_token` (persisted after 32,768 output tokens) in either background or foreground mode. Reusing the same `previous_interaction_id` and `continuation_token` creates independent branched continuations.
- **Turn-boundary enforcement** : Starting a new user turn ( `previous_interaction_id` with new `input` and no `continuation_token` ) from a segment whose status is `requires_continuation` or `incomplete` returns an HTTP `400` error. Finish continuing the decode to `completed` , or branch your next turn from the most recent `completed` interaction. Once the final segment reaches `completed` , passing that final segment's `id` as `previous_interaction_id` reconstructs the full conversation history across all prior segments.
- **Parameter consistency across segments** : Changing `model` , `system_instruction` , or function declarations ( `tools` ) on a continuation segment returns an HTTP `400` error. Keep `thinking_level` and built-in tools unchanged across segments as well (see [Known issues](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon#known-issues) ).
- **Single-segment `get` , `list` , and `delete` behavior** : In foreground mode ( `background=false` ), each segment is stored as a separate `Interaction` resource ( `interactions.get(id)` returns only that segment, `interactions.list()` lists each segment separately, and `interactions.delete(id)` deletes only that segment; when deleting a chain of segments, delete in reverse order from the last segment backward). In the Google Gen AI SDK with `automatic_continuation=True` ( `stream=False` ), `interactions.create()` merges all segments on return and populates `interaction.continuation_ids` with the ordered segment IDs (ending with `interaction.id` ). If a later segment fails, exceeds a numeric per-call `timeout` , or drops mid-stream after progress was made past a resumable checkpoint, the SDK raises `ContinuationInterruptedError` carrying `partial_interaction` , `continuation_token` , `interaction_id` , and `continuation_ids` so you can resume from `continuation_token` .

### GenerateContent custom loop rules

In a custom `GenerateContent` continuation loop, follow these rules:

- Set `max_output_tokens` greater than 65,536 (streaming) or 32,768 (non-streaming) up to 1,048,576, and resend the original `contents` , `system_instruction` , and `tools` on every continuation request along with the latest `continuation_token` (a top-level field on `GenerateContentRequest` in REST, or in `GenerateContentConfig` in the Google Gen AI SDK).
- Don't append partial model output into `contents` or send a follow-up prompt asking the model to continue.
- Continue looping as long as `finish_reason` is `CONTINUATION` and `continuation_token` is present, even if a segment spent all 32,768 or 65,536 tokens on thinking ( `parts: [{"text": ""}]` ). If `finish_reason` is `MAX_TOKENS` when `continuation_token` is present, raise `max_output_tokens` in the next request.
- Combine accumulated parts into a single `model` turn for multi-turn history only after `STOP` .

### Token counting, compaction, and implicit caching

Token accounting and caching across continuation segments work as follows:

- On the Interactions API, non-streaming `interactions.create()` calls with `automatic_continuation=True` and server-managed `background=true` interactions sum token counts across all segments in `usage` ( `total_input_tokens` , `total_cached_tokens` , `total_output_tokens` , `total_thought_tokens` , `total_tokens` ), preserving the first segment's prompt count in `usage.initial_input_tokens` . In custom foreground loops and streamed `interaction.completed` events, each segment's `usage` reports only that segment's delta, so sum `usage` fields across segments for total billed tokens.
- On `GenerateContent` , the Python Google Gen AI SDK ( `generate_content` and `generate_content_stream` ) accumulates total billed tokens across segments in the final `usage_metadata` and preserves `initial_prompt_token_count` . In custom REST loops, sum the final `prompt_token_count` , `cached_content_token_count` , `candidates_token_count` , and `thoughts_token_count` across segments.
- Because each foreground continuation segment re-prefills the conversation and previously generated tokens as input, `usage.total_input_tokens` (on the Interactions API) and `prompt_token_count` (on `GenerateContent` ) increase across segments. Don't use cumulative input counts to trigger context compaction in agent harnesses; instead, check `usage.initial_input_tokens` (or `initial_prompt_token_count` on `GenerateContent` ) and compact only after the turn finishes ( `status="completed"` or no `continuation_token` ).
- Each continuation segment re-prefills the prompt plus previously decoded tokens and automatically receives the 95% implicit context caching discount (4,096-token minimum) when segments run back-to-back within the 15 to 20 minute cache TTL. Completed segments are billed at the end of each segment even if a later segment fails or is cancelled.

## Migrate to 4 Argon from 3.1 Pro

The following behavior is different from `gemini-3.1-pro-preview` :

- 4 Argon has a unified 1,048,576-token limit across input and output (where output includes thinking, function calls, and the final response), instead of separate input and output limits. Single-request output is capped at 65,536 tokens when streaming (or 32,768 tokens for non-streaming foreground requests), and can be extended up to 1,048,576 tokens using [long decodes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon#long-decodes) on the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) or `GenerateContent` (handled automatically in the Google Gen AI SDK, with `background=true` on the Interactions API, or using `continuation_token` in custom loops).
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
2.  **Upgrade to the latest Google Gen AI SDK and account for the unified input and output token limit** : Upgrade to `google-genai >= 2.34.0` (Python), `@google/genai >= 2.32.0` (JavaScript/TypeScript), Go `>= 1.77.0` , or Java `>= 1.80.0` for Interactions API automatic continuation (or `>= 2.30.1` Python / `>= 2.29.1` JavaScript on `GenerateContent` ). Input and output tokens (including thinking and function calls) share the unified 1,048,576-token limit. For outputs exceeding 65,536 tokens (up to 1,048,576 tokens) on the Interactions API or `GenerateContent` , set `max_output_tokens` greater than 65,536 so the Google Gen AI SDK continues automatically across segments (or use `background=true` or a custom `continuation_token` loop).
3.  **Replace the reasoning budget parameter** : Replace `thinking_budget` and `MINIMAL` with `thinking_level` set to `LOW` , `MEDIUM` (default on `gemini-4-argon` ), or `HIGH` (default on `gemini-4-argon-cyber-permissive` ) (use lowercase `"low"` , `"medium"` , or `"high"` on the Interactions API).
4.  **Remove explicit caching** and front-load static prompt content (4,096 tokens or more) for automatic implicit caching.
5.  **Remove parameters that have no effect or aren't supported** : Remove ignored and rejected generation fields as follows:
    - Remove `temperature` , `top_p` , and `top_k` , which are ignored.
    - Remove `candidate_count` , `frequency_penalty` , and `presence_penalty` .
    - Remove any prefilled model turns from conversation histories.

## Summary checklist for developers

Target model ID: `gemini-4-argon` (or `gemini-4-argon-cyber-permissive` for Fairwind-approved projects), and upgrade to the latest Google Gen AI SDK (Python `google-genai >= 2.34.0` , JS/TS `@google/genai >= 2.32.0` , Go `>= 1.77.0` , Java `>= 1.80.0` for Interactions API automatic continuation; .NET `>= 1.26.0` and Kotlin `>= 1.6.0` for `GenerateContent` )

Location: `global` , `us` , or `eu`

Budget for a unified 1,048,576-token input and output limit and a 65,536-token single-request output cap (32,768 tokens for non-streaming foreground calls), or set `max_output_tokens` up to 1,048,576 on the Interactions API or `GenerateContent` for long decodes.

Use `thinking_level` ( `MEDIUM` by default on `gemini-4-argon` , `HIGH` by default on `gemini-4-argon-cyber-permissive` ; valid values: `LOW` , `MEDIUM` , `HIGH` on `GenerateContent` , or `low` , `medium` , `high` on the Interactions API). Remove `thinking_budget` and `MINIMAL` .

Remove the following parameters: `frequency_penalty` , `presence_penalty` , `candidate_count` , `temperature` , `top_p` , and `top_k` .

Remove any prefilled model turns from multi-turn chat request histories.

Remove explicit caching calls, and put static prompt content (4,096 tokens or more) first for implicit caching.

## Known issues

The following known issues apply to 4 Argon long decodes:

- **Long decodes require `v1beta1`** : Long decoding ( `continuation_token` ) on both the Interactions API and the `GenerateContent` API ( `generateContent` and `streamGenerateContent` ) is supported only in the `v1beta1` API (not `v1` ) on Agent Platform. The Google Gen AI SDK uses `v1beta1` by default unless `api_version='v1'` is set in `http_options` (or `api_version="v1"` on `interactions.create` ); for direct REST calls, use the `/v1beta1/` endpoint path.
- **Parameter changes across Interactions API continuation segments** : Changing `model` , `system_instruction` , or function declarations across continuation segments returns an HTTP `400` error, whereas mid-decode changes to `generation_config.thinking_level` or built-in tools ( `google_search` , `code_execution` , `url_context` ) aren't rejected by server validation. Keep `thinking_level` and built-in tools unchanged across all segments of a continuation loop.

## Additional resources

- [Gemini 4 Argon model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-argon)
- [Get started with Gemini 4](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-4)
- [Introductory notebook](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_4_argon.ipynb)
- [Gemini 4 Argon Cyber Permissive](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-argon#cyber)
