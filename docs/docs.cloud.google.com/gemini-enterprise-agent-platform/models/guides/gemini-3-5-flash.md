---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash
title: Developer&#39;s guide to Gemini 3.5 Flash
description: Developer guide for Gemini 3.5 Flash, covering model specifications, comparisons, migration steps, and API integration.
data_source: docs.cloud.google.com
---

**Gemini 3.5 Flash** is a high-speed, cost-effective powerhouse model in the Gemini 3 family. Designed to deliver near-Pro agentic capabilities without compromising on performance or value, the model is now generally available (GA) to developers using the [Gemini API](https://ai.google.dev/gemini-api/docs/models/gemini-3.6-flash) and for enterprises using [Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash) .

This document covers what's new with 3.5 Flash, when you should use it, how to migrate to 3.5 Flash, and provides a quickstart for using 3.5 Flash.

## How does it fit in the Gemini family?

The following table is a comparison covering some of the specifications between 3.5 Flash, 3.1 Pro, and 3.1 Flash-Lite:

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
<th><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash">Gemini 3.5 Flash</a></th>
<th><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro">Gemini 3.1 Pro</a></th>
<th><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite">Gemini 3.1 Flash-Lite</a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Model ID</td>
<td><code dir="ltr" translate="no">gemini-3.5-flash</code></td>
<td><code dir="ltr" translate="no">gemini-3.1-pro-preview</code></td>
<td><code dir="ltr" translate="no">gemini-3.1-flash-lite</code></td>
</tr>
<tr class="even">
<td>Launch stage</td>
<td>GA</td>
<td>Preview</td>
<td>GA</td>
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
<td>Global, Multi-region, Americas, Europe, Asia Pacific</td>
<td>Global</td>
<td>Global, Multi-region</td>
</tr>
<tr class="even">
<td>Supported thinking levels</td>
<td><code dir="ltr" translate="no">MINIMAL</code> , <code dir="ltr" translate="no">LOW</code> , <code dir="ltr" translate="no">MEDIUM</code> , <code dir="ltr" translate="no">HIGH</code><br />
(Default: <code dir="ltr" translate="no">MEDIUM</code> )</td>
<td><code dir="ltr" translate="no">LOW</code> , <code dir="ltr" translate="no">MEDIUM</code> , <code dir="ltr" translate="no">HIGH</code><br />
(Default: <code dir="ltr" translate="no">HIGH</code> )</td>
<td><code dir="ltr" translate="no">MINIMAL</code> , <code dir="ltr" translate="no">LOW</code> , <code dir="ltr" translate="no">MEDIUM</code> , <code dir="ltr" translate="no">HIGH</code><br />
(Default: <code dir="ltr" translate="no">MINIMAL</code> )</td>
</tr>
<tr class="odd">
<td>Primary focus</td>
<td>Balanced tasks, tool calling, and intermediate reasoning</td>
<td>Deep reasoning, high-complexity tasks</td>
<td>High-volume, cost-sensitive, and latency-sensitive tasks</td>
</tr>
</tbody>
</table>

See the [3.5 Flash model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash) for the full list of supported capabilities, tools, and consumption options.

### Use case breakdown

The recommended strategy for agentic workflows uses a tiered approach to optimize quality, speed, and cost:

  - **Gemini Pro** : Reserve for high-complexity cognitive tasks requiring deep reasoning, such as initial root planning, complex problem-solving, difficult coding, and critical decision-making.
  - **Gemini Flash** : Use as the primary "workhorse" for execution tasks, tool calling, and intermediate reasoning steps, offering the best balance of performance and efficiency.
  - **Gemini Flash-Lite** : Deploy for high-volume, low-latency preprocessing and structural tasks where speed and cost are paramount, such as intent routing, data extraction, tagging, and classification.

## What's new in Gemini 3.5 Flash?

Gemini 3.5 Flash brings the following changes and improvements to the Gemini model lineup:

  - **Sustained frontier performance** : Our most intelligent Flash model, optimized for agentic and coding tasks at scale.
  - **Agentic execution** : Sub-agent deployment, problem solving, and rapid agentic loops at scale.
  - **Improved coding** : Iterative coding cycles, rapid exploration, and prototyping to test alternate paths and dynamically explore solutions.
  - **Long horizon** : Multi-step workflows and tool use at scale.
  - **Thought preservation** : The model maintains intermediate reasoning across multi-turn conversations automatically. No API changes needed.
  - **New default thinking level** : Default thinking level changed from `HIGH` to `MEDIUM` .
  - **Improved `LOW` thinking** : Thinking level low is now significantly improved for code and agentic tasks that require fewer steps, offering strong quality at lower latency and cost.

You can find further details in the [Key changes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash#key-changes) section.

> **Note:** You might notice an increase in reported token counts. The upgraded infrastructure accurately counts all request components, including complex metadata like response schemas and function calling, which were undercounted in previous versions.

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
      model="gemini-3.5-flash",
      contents="How does AI work?",
    )
    print(response.text)

### REST

    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.5-flash:generateContent \
    -d '{
      "contents": {
        "role": "USER",
        "parts": { "text": "Why is the sky blue?" },
      },
    }'

## Key changes

This section describes in further detail the following changes introduced in Gemini 3.5 Flash:

  - [New default thinking level ( `MEDIUM` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash#default-thinking-level)
  - [Thought preservation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash#thought-preservation)
  - [Deprecated: Sampling parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash#deprecated-sampling-parameters)
  - [Deprecated: `thinking_budget`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash#deprecated-thinking-budget)

### New default thinking level

The default thinking level for Gemini 3 models is now `MEDIUM` , changed from `HIGH` in the preview version of Gemini 3 Flash. Thinking level `MEDIUM` yields strong results across a wide range of tasks while being faster and more cost-efficient.

The supported thinking levels are:

  - **`MINIMAL`** : Matches the "no thinking" setting for most queries. The model may think very minimally for complex tasks like coding. Minimizes latency for chat or high throughput applications.
  - **`LOW`** : Light reasoning for most tasks with high speed and lower cost.
  - **`MEDIUM`** : (Default) Balanced setting for most tasks requiring reasoning.
  - **`HIGH`** : Maximizes reasoning to optimize for task performance. The model may take longer than the `MEDIUM` setting to generate the first token, but the output will be more thorough.

For example, use `HIGH` for logic puzzles, math word problems, or tricky scenarios where the model needs to reason through multiple steps:

    from google import genai
    from google.genai import types
    
    client = genai.Client()
    
    response = client.models.generate_content(
       model="gemini-3.5-flash",
       contents="A farmer has chickens and rabbits. There are 35 heads and 94 legs. How many chickens and how many rabbits does he have? Show your step-by-step logic.",
       config=types.GenerateContentConfig(
           thinking_config=types.ThinkingConfig(
               thinking_level=types.ThinkingLevel.HIGH
           )
       ),
    )
    print(response.text)

The `thinking_level` parameter is optional. If omitted, 3.5 Flash will use its default setting ( `MEDIUM` ).

> **Note:** The `thinking_level` parameter and the legacy `thinking_budget` parameter are exclusive to one another. Using both in a request will return a `400` error.

### Thought preservation

The model maintains intermediate reasoning across multi-turn conversations automatically. When present in the conversation history, reasoning context carries forward automatically, improving performance on complex multi-step tasks like iterative debugging and code refactoring. No API changes needed.

Thoughts from previous turns are now preserved by default. The service no longer clears thought history from the conversation context before passing it to the model.

When sending conversation history, be consistent with previous turns: either include full context (thoughts, function calls, responses) or omit it entirely. Partial context can degrade model performance.

> **Note:** Thought preservation may increase token usage and response time. For simple, independent queries, clearing thoughts between turns can help.

### Deprecated: Sampling parameters

The following sampling parameters are no longer recommended for Gemini 3 models:

  - `temperature`
  - `top_p`
  - `top_k`

The model manages its own sampling for optimal results. Remove these parameters from all requests. To ensure determinism, define a system instruction with explicit rules for your specific use case.

### Deprecated: `thinking_budget`

The raw numeric `thinking_budget` parameter is no longer supported across all Gemini 3 models. Use the `thinking_level` string enum instead.

    # ⚠️ Before (not recommended)
    config = types.GenerateContentConfig(
        thinking_config=types.ThinkingConfig(thinking_budget=7500)
    )
    
    # ✅ After
    config = types.GenerateContentConfig(
        thinking_config=types.ThinkingConfig(thinking_level="MEDIUM")
    )

## Best practices

This section describes the following best practices for using 3.5 Flash:

  - [Use strict response matching for function calls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash#strict-response-matching)
  - [Include multimodal content in the function response `parts`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash#multimodal-content)
  - [Use inline instructions in the function response](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash#inline-instructions)
  - [Reduce unnecessary tool calls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash#reduce-unnecessary-tool-calls)

### Use strict response matching for function calls

Mismatched responses cause the model to return empty responses with `finish_reason: STOP` in most cases. Always follow these conventions:

  - **Include `id`** : Every `FunctionResponse` must include the `id` from the corresponding `FunctionCall` .
  - **Match `name`** : The `name` in the response must match the `name` in the call.
  - **Match counts** : Return exactly one `FunctionResponse` for each `FunctionCall` received.

The following code is an example of a correct function call:

    # ✅ Include matching id and name in the function response
    final_response = client.models.generate_content(
        model="gemini-3.5-flash",
        config=config,
        contents=[
            *previous_contents,
            response.candidates[0].content,
            types.Content(role="user", parts=[
                types.Part.from_function_response(
                    name=tool_call.name,
                    response={"result": result},
                    id=tool_call.id,
                )
            ]),
        ],
    )

### Include multimodal content in the function response `parts`

Providing images outside the function response can lead to unexpected model behavior such as thought leakage and result in lower quality. Follow the recommendation included in [Introduction to function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling#mm-fr) and include multimodal content in the function response parts that you send to the model. The model can process this multimodal content in its next turn to produce a more informed response.

For example:

    # ✅ Include multimodal content in the function response
    final_response = client.models.generate_content(
        model="gemini-3.5-flash",
        config=config,
        contents=[
            *previous_contents,
            response.candidates[0].content,
            types.Content(role="user", parts=[
                types.Part.from_function_response(
                    name=tool_call.name,
                    response={
                        "result": "instrument.jpg",
                        "image": base64_image_data,
                    },
                    id=tool_call.id,
                )
            ]),
        ],
    )

## Use inline instructions in the function response

Providing platform instructions along with function responses as subsequent `parts` can lead to unexpected model behavior such as thought leakage and result in lower quality. Instead, append it to the end of the function response text separated by two newlines.

For example:

    # ✅ Append inline instructions to the end of the function response separated by two newlines
    result_text = f"{json.dumps(result)}\n\n<your inline instructions>"
    
    final_response = client.models.generate_content(
        model="gemini-3.5-flash",
        config=config,
        contents=[
            *previous_contents,
            response.candidates[0].content,
            types.Content(role="user", parts=[
                types.Part.from_function_response(
                    name=tool_call.name,
                    response={"result": result_text},
                    id=tool_call.id,
                )
            ]),
        ],
    )

### Reduce unnecessary tool calls

If you experience an overuse of tool calls, two techniques help minimize them:

1.  **Reduce the thinking level** : Higher thinking levels encourage the model to use more tools to explore and verify, so lowering the level can reduce tool calls.

2.  **Add a system instruction** : If overuse persists after adjusting the thinking level, consider a prompt that restricts tool usage. For example:
    
        You have a limited action budget of <n> tool calls. Use them efficiently.

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

  - (Recommended) Instruct the model to put its pre-tool notes inside a dedicated `update()` function call instead of raw text. See the [next section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-5-flash#wrap-working-notes) for detailed implementation instructions.
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

  - [Gemini 3.5 Flash model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
  - [Introductory notebook](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/getting-started/intro_gemini_3_5_flash.ipynb)
