---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-6-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-6-flash
title: Developer&#39;s guide to Gemini 3.6 Flash
description: Developer guide for Gemini 3.6 Flash, covering model specifications, comparisons, migration steps, and API integration.
data_source: docs.cloud.google.com
---

**Gemini 3.6 Flash** is a high-speed, cost-effective powerhouse model in the Gemini 3 family. Designed to deliver near-Pro agentic capabilities without compromising on performance or value, the model is now generally available (GA) to developers using the [Gemini API](https://ai.google.dev/gemini-api/docs/models/gemini-3.6-flash) and for enterprises using [Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash) .

This document covers what's new with 3.6 Flash, how it fits within the Gemini model family, how to migrate to 3.6 Flash, and provides a quickstart for using 3.6 Flash.

## How does it fit in the Gemini family?

Gemini 3.6 Flash is the primary agentic workhorse in the Gemini 3 family. It bridges the gap between deep-reasoning Pro models and high-throughput Flash-Lite models. Compared to Gemini 3.5 Flash, 3.6 Flash delivers significantly higher quality on multi-step tool orchestration, full-stack code refactoring, and visual reasoning while using fewer tokens and reasoning turns. It offers near-Pro level capabilities at Flash speed and pricing.

### Model specifications and comparisons

The following table is a comparison covering some of the specifications between 3.6 Flash, 3.5 Flash, and 3.1 Pro:

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
<th><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash">Gemini 3.6 Flash</a></th>
<th><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash">Gemini 3.5 Flash</a></th>
<th><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro">Gemini 3.1 Pro</a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Model ID</td>
<td><code dir="ltr" translate="no">gemini-3.6-flash</code></td>
<td><code dir="ltr" translate="no">gemini-3.5-flash</code></td>
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
<td>Global, Multi-region, Americas, Europe, Asia Pacific</td>
<td>Global</td>
</tr>
<tr class="even">
<td>Supported thinking levels</td>
<td><code dir="ltr" translate="no">MINIMAL</code> , <code dir="ltr" translate="no">LOW</code> , <code dir="ltr" translate="no">MEDIUM</code> , <code dir="ltr" translate="no">HIGH</code><br />
(Default: <code dir="ltr" translate="no">MEDIUM</code> )</td>
<td><code dir="ltr" translate="no">MINIMAL</code> , <code dir="ltr" translate="no">LOW</code> , <code dir="ltr" translate="no">MEDIUM</code> , <code dir="ltr" translate="no">HIGH</code><br />
(Default: <code dir="ltr" translate="no">MEDIUM</code> )</td>
<td><code dir="ltr" translate="no">LOW</code> , <code dir="ltr" translate="no">MEDIUM</code> , <code dir="ltr" translate="no">HIGH</code><br />
(Default: <code dir="ltr" translate="no">HIGH</code> )</td>
</tr>
<tr class="odd">
<td>Primary focus</td>
<td>High-efficiency agentic workflows, multi-step orchestration, and full-stack coding</td>
<td>Balanced tasks, tool calling, and intermediate reasoning</td>
<td>Deep reasoning, high-complexity tasks</td>
</tr>
</tbody>
</table>

See the [3.6 Flash model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash) for the full list of supported capabilities, tools, and consumption options.

## What's new in Gemini 3.6 Flash?

3.6 Flash is optimized for multi-step orchestration, full-stack code refactoring, and general reasoning with significantly better token efficiency than its predecessors.

### Capabilities and performance updates

The following is the list of changes in capabilities and performance for 3.6 Flash from preceding models:

  - **Token and turn reduction** : Consumes fewer tokens and completes multi-step workflows in fewer reasoning steps and conversational turns than 3.5 Flash.
  - **Improved code generation** : Produces cleaner code with lower compile-failure and revision rates across application building, prototyping, and IDE agent environments.
  - **Reduced action bias** : Resolves read-only diagnostic tasks without making unsolicited workspace edits or mutating state prematurely.
  - **Multimodal and spatial reasoning** : Delivers improved performance on chart interpretation, visual blueprint conversion, and multi-element web layout generation.
  - **Computer use support** : Supported as a built-in tool for agentic UI automation.
  - **UI styling preference** : Better at creating functional code, though human evaluators noted a preference for previous models for frontend presentation and visual layout. This can be mitigated by providing explicit design guidelines.

### Behavioral and API parameter changes

The following is the list of behavioral and API parameter changes for 3.6 Flash from preceding models:

  - **Step conciseness** : Uses fewer reasoning steps than 3.5 Flash. While this reduces latency and cost on code refactoring and tool workflows, it can cause early exits on extended multi-turn conversational follow-ups where longer iteration chains are needed.
  - **Upfront programmatic inspection** : Prefers running diagnostic code scripts ( `execute_code` ) to inspect problems before mutating state more frequently than 3.5 Flash. While this improves diagnostic accuracy on complex backend refactoring, it can occasionally lead to running extra exploratory inspection steps on simple frontend web and scripting tasks where the previous version would generate code directly.
  - **Default effort** : Carries forward the medium default effort level introduced in 3.5 Flash.
  - **No sampling overrides** : Custom values for `temperature` , `top-k` , or `top-p` parameters are no longer supported. Setting custom values will be ignored in the API surface. Use `thinking_level` or structured JSON schemas to control output determinism instead.
  - **Frequency and presence penalty restrictions** : Custom values for these parameters are no longer supported. Setting them will now throw an active API error.
  - API requests where the last input turn has a role of "Model" are not supported.
  - Empty turns in conversation history are dropped.
  - Invalid thought signatures will now produce errors.
  - Strict function calling: `FunctionResponse` must strictly match the `id` , `name` , and execution count of the preceding `FunctionCall` . Append inline instructions directly inside the function response text, separated by two newlines ( `\n\n` ).

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
      model="gemini-3.6-flash",
      contents="How does AI work?",
    )
    print(response.text)

### REST

    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.6-flash:generateContent \
    -d '{
      "contents": {
        "role": "USER",
        "parts": { "text": "Why is the sky blue?" },
      },
    }'

## Migrate to 3.6 Flash from 3.5 Flash or 3.1 Pro

To migrate to 3.6 Flash from 3.5 Flash or 3.1 Pro, do the following steps:

1.  **Update the model ID** : Change model string in your API calls to `gemini-3.6-flash` .
2.  **Adapt your code to the new Gemini 3 family API rules** : Gemini 3.6 Flash strictly enforces the parameter rules and API conventions established across the Gemini 3 family:
      - **Remove temperature, top-K, and top-P** : Remove these custom parameters from your payload. While they won't throw an error, the model will ignore them entirely. Instead, use the `thinking_level` parameter or `json_schema` structured outputs to control output determinism.
      - **Remove frequency and presence penalties** : Remove any custom configurations for frequency or presence penalties to prevent your API calls from throwing runtime errors.
      - **Ensure your chat integration does not attempt model prefilling** : Review your message history arrays to ensure that your API payload does not end with an empty user turn or model turn.. If the last object in your history array is a " `model` " role (GenerateContent API) or " `model_output` " type (Interactions API), restructure the sequence to avoid triggering a strict validation error.
      - **Use `thinking_level`** : Remove instances of the deprecated `thinking_budget` parameter and use `thinking_level` instead.
      - **Enforce strict function calling conventions** : The `FunctionResponse` must strictly match the `id` , `name` , and execution count of the preceding `FunctionCall` . If you need to append inline instructions, place them directly inside the function response text separated by two newlines ( `\n\n` ).
3.  **Account for workflow shifts** :
      - If your application relies on multi-turn conversational loops, test your workflows to ensure the model's new step conciseness does not trigger premature exits.
      - If building frontend or basic scripting agents, monitor for unnecessary exploratory `execute_code` calls due to the model's new bias toward upfront programmatic inspection.

## Workarounds for pre-tool text requirements

If your prompt requires the model to output structured text (XLM, YAML, Json, etc) (for example, `<UPDATE>...</UPDATE>` ) immediately before making a tool call, the tool call may occasionally fail with a `Malformed_Function_Call` error. You can use one of the following workarounds to resolve this issue:

  - (Recommended) Instruct the model to put its pre-tool notes inside a dedicated `update()` function call instead of raw text. See the [next section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-6-flash#wrap-working-notes) for detailed implementation instructions.
  - Instruct the model to write notes as Markdown headers (for example, `# UPDATE` , `## PLAN` ) instead of structured text.
  - Don't require the model to output text before tool calls.

### Recommended solution: Wrap working notes in a dedicated function call

Instead of the original instruction:

    Before calling a tool, in every response you MUST first output a single
    `<UPDATE>` part as specified, don't skip this part or any of required sub-tags
    within `<UPDATE>`.

Use this updated instruction:

    Before calling any other tool, in every response you MUST first call `update`
    with all required parameters (previous_step, plan, next_step, external).

Update all references to the old `<UPDATE>` XML format in the customer request. Then add the corresponding function declaration for the update function:

    {
      "name": "update",
      "description": "Update working notes (previous step analysis, plan, next step, external note).",
      "parameters": {
        "type": "OBJECT",
        "properties": {
          "previous_step": {
            "type": "STRING",
            "description": "Key findings and outcomes since the previous step."
          },
          "plan": {
            "type": "STRING",
            "description": "The current status of the plan."
          },
          "next_step": {
            "type": "STRING",
            "description": "Brief explanation of the immediate next action according to the plan."
          },
          "external": {
            "type": "STRING",
            "description": "A short, plain-language note shown to the User about what you are ABOUT TO DO next."
          }
        },
        "required": [
          "previous_step",
          "plan",
          "next_step",
          "external"
        ]
      }
    }

The model will make two calls in the same step: the `update()` call that replaces the structured XML, and the actual function call it wants to make.

## Additional resources

  - [Gemini 3.6 Flash model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash)
  - [Introductory notebook](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_3_6_flash.ipynb)
