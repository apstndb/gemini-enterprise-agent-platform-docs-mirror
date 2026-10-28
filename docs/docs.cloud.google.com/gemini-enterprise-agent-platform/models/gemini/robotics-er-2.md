---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/robotics-er-2
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/robotics-er-2
title: Gemini Robotics ER 2
description: Learn about Gemini Robotics ER 2, a vision-language model for spatial reasoning, video understanding, and robot task orchestration on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/terms/genai-preview-products) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .
>
> For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

Gemini Robotics ER 2 ( `gemini-robotics-er-2-preview` ) is a *vision-language model* (VLM) available on Gemini Enterprise Agent Platform that delivers precise reasoning about a robot's physical environment. Built on Gemini 3.5 Flash, it specializes in embodied reasoning capabilities such as spatial reasoning, pointing, instrument reading, robot video understanding (including moment finding and progress classification), and multi-step robot and tool orchestration.

For setup instructions, code samples, and capability guides, see the [Gemini Robotics ER 2 overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er) .

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal?mode=prompt&model=gemini-robotics-er-2-preview) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemini-robotics-er-2-preview-info) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?mode=prompt&model=gemini-robotics-er-2-preview&deploy=true) [Developer guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/gemini-robotics-er) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#gemini-robotics)

Note: "Deploy example app" requires a Google Cloud project with billing and Agent Platform API enabled.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<th><code>gemini-robotics-er-2-preview</code></th>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<th>description
Text<br />
Input and output
photo
Image<br />
Input only
mic
Audio<br />
Input only
videocam
Video<br />
Input only</th>
<td></td>
</tr>
<tr class="odd">
<th>Token limits</th>
<th>Input token limit</th>
<td>131,072</td>
</tr>
<tr class="even">
<th>Output token limit</th>
<th>65,536</th>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">Thinking</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction">System instructions</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Context caching</a><br />
Implicit context caching, explicit context caching<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview">RAG Engine</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models">Tuning</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing">Agentic video understanding</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Tools</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview">Grounding</a><br />
Google Search, Google Maps<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution">Code execution</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context">URL context</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use">Computer use</a> preview Preview feature<br />
Supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>APIs</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference">GenerateContent API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a> preview Preview feature<br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Count Tokens API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview">Chat Completions API</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Consumption options</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference">Batch inference</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Pay-as-you-go</a><br />
Standard PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></th>
<td><ul>
<li>Global: <code>global</code></li>
</ul></td>
</tr>
<tr class="even">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard PayGo</a></strong></p></th>
<th><ul>
<li>Global: <code>global</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Quota limits</th>
<th>250 requests per minute (RPM) default per project (200 to 300 RPM depending on project quota tier)</th>
<td></td>
</tr>
<tr class="even">
<th>Versions</th>
<th><ul>
<li><code>gemini-robotics-er-2-preview</code>
<ul>
<li>Launch stage: Preview</li>
<li>Release date: October 27, 2026</li>
</ul></li>
</ul></th>
<td></td>
</tr>
</tbody>
</table>
