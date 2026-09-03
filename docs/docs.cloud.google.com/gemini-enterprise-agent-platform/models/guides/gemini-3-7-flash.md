---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-7-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-7-flash
title: Developer&#39;s guide to Gemini 3.7 Flash
description: Developer guide for Gemini 3.7 Flash, covering model specifications, comparisons, migration steps, and API integration.
data_source: docs.cloud.google.com
---

**Gemini 3.7 Flash** is our intelligent everyday driver for developers, and delivers a step forward in software engineering, feeling distinctly better to build with. This model brings better intelligence for complex tasks, instruction following, and tool calling into your daily workflows.

This document covers what's new with 3.7 Flash, how it fits within the Gemini model family, how to migrate to 3.7 Flash, and provides a quickstart for using 3.7 Flash.

## How does it fit in the Gemini family?

Gemini 3.7 Flash is the primary agentic workhorse in the Gemini 3 family, bridging the gap between deep-reasoning Pro models and high-throughput Gemini Flash-Lite models while delivering high token efficiency and multi-step multimodal processing.

### Model specifications and comparisons

The following table is a comparison covering some of the specifications between 3.7 Flash, 3.6 Flash, and 3.1 Pro:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-7-flash">Gemini 3.7 Flash</a></th>
<th><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash">Gemini 3.6 Flash</a></th>
<th><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro">Gemini 3.1 Pro</a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Model ID</td>
<td><code dir="ltr" translate="no">gemini-3.7-flash</code></td>
<td><code dir="ltr" translate="no">gemini-3.6-flash</code></td>
<td><code dir="ltr" translate="no">gemini-3.1-pro-preview</code></td>
</tr>
<tr class="even">
<td>Launch stage</td>
<td>GA</td>
<td>GA</td>
<td>Preview</td>
</tr>
<tr class="odd">
<td>Input types</td>
<td>Text, Image, Audio, Video</td>
<td>Text, Image, Audio, Video</td>
<td>Text, Image, Audio, Video</td>
</tr>
<tr class="even">
<td>Output type(s)</td>
<td>Text</td>
<td>Text</td>
<td>Text</td>
</tr>
<tr class="odd">
<td>Context window</td>
<td>1,048,576</td>
<td>1,048,576</td>
<td>1,048,576</td>
</tr>
<tr class="even">
<td>Maximum output token length</td>
<td>65,536</td>
<td>65,536</td>
<td>65,536</td>
</tr>
<tr class="odd">
<td>Supported regions</td>
<td>Global, Multi-region</td>
<td>Global, Multi-region</td>
<td>Global</td>
</tr>
<tr class="even">
<td>Supported thinking levels</td>
<td><code dir="ltr" translate="no">LOW</code> , <code dir="ltr" translate="no">MEDIUM</code> , <code dir="ltr" translate="no">HIGH</code><br />
(Default: <code dir="ltr" translate="no">MEDIUM</code> )</td>
<td><code dir="ltr" translate="no">MINIMAL</code> , <code dir="ltr" translate="no">LOW</code> , <code dir="ltr" translate="no">MEDIUM</code> , <code dir="ltr" translate="no">HIGH</code><br />
(Default: <code dir="ltr" translate="no">MEDIUM</code> )</td>
<td><code dir="ltr" translate="no">LOW</code> , <code dir="ltr" translate="no">MEDIUM</code> , <code dir="ltr" translate="no">HIGH</code><br />
(Default: <code dir="ltr" translate="no">HIGH</code> )</td>
</tr>
<tr class="odd">
<td>Primary focus</td>
<td>Agentic workflows, coding, interactive video understanding</td>
<td>General agentic workflows, multi-step orchestration</td>
<td>Deep reasoning, high-complexity tasks</td>
</tr>
</tbody>
</table>

See the [3.7 Flash model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-7-flash) for the full list of supported capabilities, tools, and consumption options.

## What's new in Gemini 3.7 Flash?

The following table compares standard developer evaluation benchmarks between Gemini 3.7 Flash and 3.6 Flash:

| Evaluation benchmark       | 3.7 Flash | 3.6 Flash |
| -------------------------- | --------- | --------- |
| Terminal-bench 2.1         | 85.1%     | 73.0%     |
| DeepSWE                    | 63.7%     | 49.0%     |
| Humanity's Last Exam (HLE) | 45.7%     | 37.4%     |
| LMArena WebDev             | 1592      | 1532      |

## Quickstart

Before you begin, you must authenticate to Agent Platform using Application Default Credentials (ADC) or an API key. See [Get started with Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start) for more information.

In the following code blocks, replace PROJECT\_ID with your project ID.

### Installation

Ensure you are using the latest `google-genai` SDK:

    pip install --upgrade google-genai

### Basic request

### Python

    from google import genai
    
    client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")
    
    response = client.models.generate_content(
      model="gemini-3.7-flash",
      contents="How does AI work?",
    )
    print(response.text)

### REST

    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.7-flash:generateContent \
    -d '{
      "contents": {
        "role": "USER",
        "parts": { "text": "Why is the sky blue?" },
      },
    }'

## Mandatory API rules and behavioral conventions

> **Important:** `thinking_level="MINIMAL"` is not available for 3.7 Flash. Explicitly setting `thinking_level` to `MINIMAL` will return an API validation error. Valid configurations are `LOW` , `MEDIUM` (default), and `HIGH` .

Gemini 3.7 Flash strictly enforces the following standard Gemini 3 family API conventions:

  - **Deprecated sampling parameters ( `temperature` , `top_k` , `top_p` )** : These parameters are ignored by the backend. Instead, you can control determinism using `thinking_level` ( `LOW` , `MEDIUM` , `HIGH` ) and `response_schema` or `json_schema` .

  - **Unsupported parameters ( `frequency_penalty` , `presence_penalty` , `candidate_count` )** : Passing `frequency_penalty` , `presence_penalty` or `candidate_count` will throw an active API error. Remove them from legacy client code.

  - **Strict function calling rules** : A `FunctionResponse` turn must strictly match the `id` , `name` , and execution count of the preceding `FunctionCall` .
    
      - **Multimodal assets** : Always place multimodal assets inside the response payload.
    
      - **Formatting and pre-tool text** : Format inline instructions using `\n\n` . If you encounter `Malformed_Function_Call` errors tied to pre-tool text, clean up leading commentary prior to tool calls.
    
      - To pass intermediate working notes or status updates prior to a tool call, wrap them in a dedicated `update()` function call rather than emitting raw XML or text:
        
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

  - **Chat sequence validation** :
    
      - History payloads cannot end with a " `model` " role turn.
      - Prefilled model turns are unsupported and must be removed when upgrading.
      - Empty turns in conversation history are automatically dropped or will produce validation errors.

## Migrate to 3.7 Flash from 3.5 Flash or 3.6 Flash

To migrate to 3.7 Flash from 3.5 Flash or 3.6 Flash, do the following steps:

1.  **Update the model ID** : Change model string in your API calls to `gemini-3.7-flash` .
2.  **Replace the reasoning budget parameter** : Replace integer `thinking_budget` configurations with the string enum `thinking_level` set to one of the following values:
      - `HIGH` : Recommended for dense visual QA, split-second movement detection (sports, editing), or multi-step reasoning across 60+ minute videos.
      - `MEDIUM` : The default thinking level. This level provides optimal balance for general video Q\&A, lecture summarization, and clip retrieval.
      - `LOW` : Recommended for tasks like fast transcript-focused searches or basic metadata extraction.
3.  **Strip deprecated and unsupported parameters** :
      - Remove `temperature` , `top_p` , and `top_k` .
      - Remove `candidate_count` , `frequency_penalty` , and `presence_penalty` .
      - Remove any prefilled model turns from conversation histories.

## Summary checklist for developers

Target model ID: `gemini-3.7-flash`

Use `thinking_level` ( `MEDIUM` by default; valid values: `LOW` , `MEDIUM` , `HIGH` ) instead of the deprecated `thinking_budget` or `temperature` fields. `MINIMAL` is unsupported for this model.

Remove the following unsupported parameters: `frequency_penalty` , `presence_penalty` , `candidate_count` , `temperature` , `top_p` , and `top_k` .

Remove any prefilled model turns from multi-turn chat request histories.

Ensure strict `FunctionResponse` matching ( `id` or `call_id` and `name` ) and format pre-tool instructions with `\n\n` .

## Additional resources

  - [Gemini 3.7 Flash model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-7-flash)
  - [Introductory notebook](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_3_7_flash.ipynb)
