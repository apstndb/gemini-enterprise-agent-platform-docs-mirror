---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/qwen/qwen3-next-thinking
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/qwen/qwen3-next-thinking
title: Qwen3-Next-80B Thinking
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Caution:** As of July 21, 2026, the `qwen3-next-80b-a3b-thinking-maas` endpoint is deprecated and will be retired on October 21, 2026. For more information, see [Open model deprecations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/open-models) .

Qwen3-Next-80B Thinking is a language model from the Qwen3-Next family of models. It is specialized for complex problem-solving and deep reasoning. Its "thinking" mode generates a visible, step-by-step reasoning process alongside the final answer, making it ideal for tasks requiring transparent logic, like mathematical proofs, intricate code debugging, or multi-step agent planning.

## Managed API (MaaS) specifications

[Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>qwen3-next-80b-a3b-thinking-maas</code></td>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<td>description
Text<br />
Input and output
hide_image
Image<br />
Not supported
mic_off
Audio<br />
Not supported
videocam_off
Video<br />
Not supported</td>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/thinking">Thinking</a><br />
Supported</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Consumption options</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference">Batch inference</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Pay-as-you-go</a><br />
Standard PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Not supported</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<td><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></td>
<td><ul>
<li>Global: <code>global</code></li>
</ul></td>
</tr>
<tr class="even">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency">ML processing</a></strong></p></th>
<td><ul>
<li>Multi-region: <code>us</code></li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Quotas</th>
<td><ul>
<li><strong><code>global</code></strong> : 262,144 maximum output, 262,144 context length</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Versions</th>
<td><ul>
<li><code>Qwen3-Next Thinking</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: September 15, 2025</li>
</ul></li>
</ul></td>
<td></td>
</tr>
</tbody>
</table>

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [Qwen3-Next-80B Thinking model card](https://console.cloud.google.com/agent-platform/publishers/qwen/model-garden/qwen3-next) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
