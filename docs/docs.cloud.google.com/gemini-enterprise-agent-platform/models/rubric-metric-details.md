---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details
title: Details for managed rubric-based metrics
description: Understand Agent Platform's managed rubric-based metrics for test-driven evaluation, including adaptive and static rubrics.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page provides a full list of managed rubric-based metrics offered by the Gen AI evaluation service, which you can use in the GenAI Client in Vertex AI SDK.

For more information about test-driven evaluation, see [Define your evaluation metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/determine-eval) .

## Overview

The Gen AI evaluation service offers a list of managed rubric-based metrics for the test-driven evaluation framework:

  - For metrics with adaptive rubrics, most of them include both the workflow for rubric generation for each prompt and rubric validation. You can run them separately if needed. See [Run an evaluation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/run-evaluation) for details.

  - For metrics with static rubrics, no per-prompt rubrics are generated. For details regarding the intended outputs, see [Metric details](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#managed-metrics-details) .

Each managed rubric-based metric has a versioning number. The metric uses the latest version by default, but you can pin to a specific version if needed:

    from vertexai import types
    
    text_quality_metric = types.RubricMetric.TEXT_QUALITY
    general_quality_v1 = types.RubricMetric.GENERAL_QUALITY(version='v1')

## Backward compatibility

For metrics offered as a [Metric prompt templates](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/metrics-templates) , you can still access the pointwise metrics through the GenAI Client in Vertex AI SDK through the same approach. Pairwise metrics are not supported by the GenAI Client in Vertex AI SDK, but see [Run an evaluation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/run-evaluation) to compare two models in the same evaluation.

    from vertexai import types
    
    # Access metrics represented by metric prompt template examples
    coherence = types.RubricMetric.COHERENCE
    fluency = types.RubricMetric.FLUENCY

## Managed metrics details

This section lists managed metrics with details such as their type, required inputs, and expected output:

  - [General quality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#general-quality)
  - [Text quality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#text-quality)
  - [Instruction following](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#instruction-following)
  - [Grounding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#grounding)
  - [Safety](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#safety)
  - [Multi-turn general quality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#multi-turn-general-quality)
  - [Multi-turn text quality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#multi-turn-text-quality)
  - [Agent final response match](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#agent-final-response-match)
  - [Agent final response reference free](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#agent-final-response-reference-free)
  - [Agent final response quality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#agent-final-response-quality)
  - [Agent hallucination](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#agent-hallucination)
  - [Agent tool use quality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#agent-tool-use-quality)
  - [Agent multi-turn task success](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#agent-multi-turn-task-success)
  - [Agent multi-turn tool use quality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#agent-multi-turn-tool-use-quality)
  - [Agent multi-turn trajectory quality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#agent-multi-turn-trajectory-quality)
  - [Gecko text-to-image quality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#gecko-t2i)
  - [Gecko text-to-video quality](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/rubric-metric-details#gecko-t2v)

### General quality

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">general_quality_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>A comprehensive adaptive rubrics metric that evaluates the overall quality of a model's response. It automatically generates and assesses a broad range of criteria based on the prompt's content. This is the recommended starting point for most evaluations.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.GENERAL_QUALITY</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">response</code></li>
<li>(Optional) <code dir="ltr" translate="no">rubric_groups</code></li>
</ul>
If you have rubrics already generated, you can provide them directly for evaluation.</td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>6 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Text quality

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">text_quality_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>A targeted adaptive rubrics metric that specifically evaluates the linguistic quality of the response. It assesses aspects like fluency, coherence, and grammar.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.TEXT_QUALITY</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">response</code></li>
<li>(Optional) <code dir="ltr" translate="no">rubric_groups</code></li>
</ul>
If you have rubrics already generated, you can provide them directly for evaluation.</td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>6 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Instruction following

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">instruction_following_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>A targeted adaptive rubrics metric that measures how well the response adheres to the specific constraints and instructions given in the prompt.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.INSTRUCTION_FOLLOWING</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">response</code></li>
<li>(Optional) <code dir="ltr" translate="no">rubric_groups</code></li>
</ul>
If you have rubrics already generated, You can provide them directly for evaluation.</td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code> (passing rate)</li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>6 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Grounding

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">grounding_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Static rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>A score-based metric that checks for factuality and consistency. It verifies that the model's response is grounded based on the context.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.GROUNDING</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">response</code></li>
<li><code dir="ltr" translate="no">context</code></li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">explanation</code></li>
</ul>
The score has a range of <code dir="ltr" translate="no">0-1</code> , and represents the rate of claims labeled as <code dir="ltr" translate="no">supported</code> or <code dir="ltr" translate="no">no_rad</code> (not requiring factual attributions, such as greetings, questions, or disclaimers) to the input prompt.<br />
The explanation contains groupings of sentence, label, reasoning and excerpt from context.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>1 call to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Safety

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">safety_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Static rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>A score-based metric that assesses whether the model's response violated one or more of the following policies:
<ul>
<li>PII &amp; Demographic Data</li>
<li>Hate Speech</li>
<li>Dangerous Content</li>
<li>Harassment</li>
<li>Sexually Explicit</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.SAFETY</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">response</code></li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">explanation</code></li>
</ul>
For the score, <code dir="ltr" translate="no">0</code> is unsafe and <code dir="ltr" translate="no">1</code> is safe.<br />
The explanation field includes violated policies.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>10 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Multi-turn general quality

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">multi_turn_general_quality_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>An adaptive rubrics metric that evaluates the overall quality of a model's response within the context of a multi-turn dialogue.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.MULTI_TURN_GENERAL_QUALITY</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code> with multi-turn conversations</li>
<li><code dir="ltr" translate="no">response</code></li>
<li>(Optional) <code dir="ltr" translate="no">rubric_groups</code></li>
</ul>
If you have rubrics already generated, you can provide them directly for evaluation.</td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li>rubrics and corresponding verdicts</li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>6 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Multi-turn text quality

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">multi_turn_text_quality_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>An adaptive rubrics metric that evaluates the text quality of a model's response within the context of a multi-turn dialogue.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.TEXT_QUALITY</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code> with multi-turn conversations</li>
<li><code dir="ltr" translate="no">response</code></li>
<li>(Optional) <code dir="ltr" translate="no">rubric_groups</code></li>
</ul>
If you have rubrics already generated, you can provide them directly for evaluation.</td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>6 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Agent final response match

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">final_response_match_v2</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Static rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>A metric that evaluates the quality of an AI agent's final answer by comparing it to a provided reference answer (ground truth).</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.FINAL_RESPONSE_MATCH</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">response</code></li>
<li><code dir="ltr" translate="no">reference</code></li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><strong>Score</strong>
<ul>
<li>1: Valid response that matches the reference.</li>
<li>0: Invalid response that does not match the reference.</li>
</ul>
<strong>Explanation</strong></td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>5 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Agent final response reference free

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">final_response_reference_free_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>An adaptive rubrics metric that evaluates the quality of an AI agent's final answer without needing a reference answer.<br />
You need to provide rubrics for this metric, as it doesn't support auto-generated rubrics.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.FINAL_RESPONSE_REFERENCE_FREE</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">response</code></li>
<li><code dir="ltr" translate="no">rubric_groups</code></li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>5 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Agent final response quality

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">final_response_quality_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>A comprehensive adaptive rubrics metric that evaluates the overall quality of an agent's response. It automatically generates a broad range of criteria based on the agent configuration (developer instruction and declarations for tools available to the agent) and the user's prompt, then assesses the generated criteria based on tool usage in intermediate events and final answer by the agent.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.FINAL_RESPONSE_QUALITY</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">response</code></li>
<li><code dir="ltr" translate="no">developer_instruction</code></li>
<li><code dir="ltr" translate="no">tool_declarations</code> (can be an empty list)</li>
<li><code dir="ltr" translate="no">intermediate_events</code> (containing function calls &amp; responses, can be an empty list)</li>
<li>(Optional) <code dir="ltr" translate="no">rubric_groups</code> (If you have rubrics already generated, you can provide them directly for evaluation)</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
<br />
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>5 calls to Gemini 2.5 Flash and 1 call to Gemini 2.5 Pro</td>
</tr>
</tbody>
</table>

### Agent hallucination

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">hallucination_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Static Rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>A score-based metric that checks for factuality and consistency of text responses by segmenting the response into atomic claims. It verifies if each claim is grounded or not based on tool usage in the intermediate events. It can also be leveraged to evaluate any intermediate text responses by setting the flag <code dir="ltr" translate="no">evaluate_intermediate_nl_responses</code> to true.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.HALLUCINATION</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">response</code></li>
<li><code dir="ltr" translate="no">developer_instruction</code></li>
<li><code dir="ltr" translate="no">tool_declarations</code> (can be an empty list)</li>
<li><code dir="ltr" translate="no">intermediate_events</code> (containing function calls &amp; responses, can be an empty list)</li>
<li><code dir="ltr" translate="no">evaluate_intermediate_nl_responses</code> (default is False)</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">explanation</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score has a range of <code dir="ltr" translate="no">0-1</code> , and represents the ratio of sentences labeled as <code dir="ltr" translate="no">supported</code> or <code dir="ltr" translate="no">no_rad</code> to the total number of sentences.<br />
<br />
The <code dir="ltr" translate="no">explanation</code> field is a JSON string containing a list of per-event objects with the following schema:
<pre dir="ltr" data-is-upgraded="" data-syntax="JSON" translate="no"><code>[
  {
    &quot;response&quot;: &quot;string&quot;,
    &quot;score&quot;: &quot;double&quot;,
    &quot;explanation&quot;: [
      {
        &quot;sentence&quot;: &quot;string&quot;,
        &quot;label&quot;: &quot;supported | unsupported | contradictory | disputed | no_rad&quot;,
        &quot;rationale&quot;: &quot;string&quot;,
        &quot;supporting_excerpt&quot;: &quot;string or null&quot;,
        &quot;contradicting_excerpt&quot;: &quot;string or null&quot;
      }
    ]
  }
]</code></pre>
Each <code dir="ltr" translate="no">explanation</code> entry contains one object per segmented sentence with the following fields:
<ul>
<li><code dir="ltr" translate="no">sentence</code> : The exact sentence extracted during the sentence segmentation step.</li>
<li><code dir="ltr" translate="no">label</code> : The classification of the sentence, one of:
<ul>
<li><code dir="ltr" translate="no">supported</code> : The sentence is entailed by the context.</li>
<li><code dir="ltr" translate="no">unsupported</code> : The sentence is not entailed by the context.</li>
<li><code dir="ltr" translate="no">contradictory</code> : The sentence is falsified by the context.</li>
<li><code dir="ltr" translate="no">disputed</code> : The context contains both supporting and contradicting information.</li>
<li><code dir="ltr" translate="no">no_rad</code> : The sentence does not require factual attribution (for example, opinions, greetings, questions, or disclaimers).</li>
</ul></li>
<li><code dir="ltr" translate="no">rationale</code> : A brief explanation for the label assignment.</li>
<li><code dir="ltr" translate="no">supporting_excerpt</code> (present for <code dir="ltr" translate="no">supported</code> and <code dir="ltr" translate="no">disputed</code> labels): A relevant excerpt from the context that supports the sentence.</li>
<li><code dir="ltr" translate="no">contradicting_excerpt</code> (present for <code dir="ltr" translate="no">contradictory</code> and <code dir="ltr" translate="no">disputed</code> labels): A relevant excerpt from the context that contradicts the sentence.</li>
</ul></td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>2 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Agent tools usage quality

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">tool_use_quality_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>A targeted adaptive rubrics metric that evaluates the selection of appropriate tools, correct parameter usage, and adherence to the specified sequence of operations.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.TOOL_USE_QUALITY</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">developer_instruction</code></li>
<li><code dir="ltr" translate="no">tool_declarations</code> (can be an empty list)</li>
<li><code dir="ltr" translate="no">intermediate_events</code> (containing function calls &amp; responses, can be an empty list)</li>
<li>(Optional) <code dir="ltr" translate="no">rubric_groups</code> (If you have rubrics already generated, you can provide them directly for evaluation)</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>5 calls to Gemini 2.5 Flash and 1 call to Gemini 2.5 Pro</td>
</tr>
</tbody>
</table>

### Agent multi-turn task success

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">multi_turn_task_success_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>An adaptive rubrics metric that evaluates whether the agent successfully fulfilled user goals across an entire multi-turn conversation. It focuses on observable outcomes and confirmations in the agent's responses rather than intermediate processes such as specific tool calls or reasoning steps.<br />
<br />
The metric operates in three steps:
<ol>
<li><strong>Intent extraction</strong> : Identifies user goals and intents from the conversation.</li>
<li><strong>Rubric generation</strong> : Creates criteria based on the extracted intents, agent instructions, and tool definitions.</li>
<li><strong>Rubric validation</strong> : Validates the agent's overall responses against the generated rubrics.</li>
</ol></td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.MULTI_TURN_TASK_SUCCESS</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">agent_eval_data</code> (multi-turn conversation trace including model inputs, responses, and tool calls)</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>2 calls to Gemini 3.1 Pro and 5 calls to Gemini 3 Flash</td>
</tr>
</tbody>
</table>

### Agent multi-turn tool use quality

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">multi_turn_tool_use_quality_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>An adaptive rubrics metric that evaluates the technical and semantic correctness of the agent's tool calls across an entire multi-turn conversation. It verifies that the agent selected the correct tools, populated arguments correctly, and adhered to the tool schemas for each user goal.<br />
<br />
The metric operates in three steps:
<ol>
<li><strong>Intent extraction</strong> : Identifies user goals and intents from the conversation.</li>
<li><strong>Rubric generation</strong> : Maps each intent to expected tool selection, argument correctness, and schema compliance criteria.</li>
<li><strong>Rubric validation</strong> : Validates the agent's actual tool calls against the generated rubrics.</li>
</ol></td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.MULTI_TURN_TOOL_USE_QUALITY</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">agent_eval_data</code> (multi-turn conversation trace including model inputs, responses, and tool calls)</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>2 calls to Gemini 3.1 Pro and 5 calls to Gemini 3 Flash</td>
</tr>
</tbody>
</table>

### Agent multi-turn trajectory quality

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">multi_turn_trajectory_quality_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>An adaptive rubrics metric that evaluates the quality of the agent's step-by-step execution trajectory across an entire multi-turn conversation. It focuses on the logical structure and technical validity of the agent's path rather than just the final response.<br />
<br />
The metric operates in three steps:
<ol>
<li><strong>Intent extraction</strong> : Identifies user goals and intents from the conversation.</li>
<li><strong>Rubric generation</strong> : Produces criteria across three dimensions: <strong>causal validity</strong> (correct sequence of tool routing, state tracking, and data passing), <strong>efficiency</strong> (minimizing unnecessary steps), and <strong>adaptive robustness</strong> (handling edge cases and errors).</li>
<li><strong>Rubric validation</strong> : Validates the agent's actual execution path against the generated rubrics.</li>
</ol></td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.MULTI_TURN_TRAJECTORY_QUALITY</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">agent_eval_data</code> (multi-turn conversation trace including model inputs, responses, and tool calls)</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>2 calls to Gemini 3.1 Pro and 5 calls to Gemini 3 Flash</td>
</tr>
</tbody>
</table>

### Gecko text-to-image quality

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">gecko_text2image_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>The <a href="https://arxiv.org/abs/2404.16820">Gecko</a> text-to-image metric is an adaptive, rubric-based method for evaluating the quality of a generated image against its corresponding text prompt. It works by first generating a set of questions from the prompt, which serve as a detailed, prompt-specific rubric. A model then answers these questions based on the generated image.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.GECKO_TEXT2IMAGE</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">response</code> - should be file data with image MIME type</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>2 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

### Gecko text-to-video quality

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Latest version</strong></td>
<td><code dir="ltr" translate="no">gecko_text2video_v1</code></td>
</tr>
<tr class="even">
<td><strong>Type</strong></td>
<td>Adaptive rubrics</td>
</tr>
<tr class="odd">
<td><strong>Description</strong></td>
<td>The <a href="https://arxiv.org/abs/2404.16820">Gecko</a> text-to-video metric is an adaptive, rubric-based method for evaluating the quality of a generated video against its corresponding text prompt. It works by first generating a set of questions from the prompt, which serve as a detailed, prompt-specific rubric. A model then answers these questions based on the generated video.</td>
</tr>
<tr class="even">
<td><strong>How to access in SDK</strong></td>
<td><code dir="ltr" translate="no">types.RubricMetric.GECKO_TEXT2VIDEO</code></td>
</tr>
<tr class="odd">
<td><strong>Input</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">prompt</code></li>
<li><code dir="ltr" translate="no">response</code> - should be file data with video MIME type</li>
</ul></td>
</tr>
<tr class="even">
<td><strong>Output</strong></td>
<td><ul>
<li><code dir="ltr" translate="no">score</code></li>
<li><code dir="ltr" translate="no">rubrics</code> and corresponding <code dir="ltr" translate="no">verdicts</code></li>
</ul>
The score represents the passing rate of the response based on the rubrics.</td>
</tr>
<tr class="odd">
<td><strong>Number of LLM calls</strong></td>
<td>2 calls to Gemini 2.5 Flash</td>
</tr>
</tbody>
</table>

## What's next

  - [Prepare your evaluation dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/evaluation-dataset) .
