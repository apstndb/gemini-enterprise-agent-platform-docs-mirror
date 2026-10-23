---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-v41-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-v41-flash
title: DeepSeek-V4.1-Flash
description: Learn about DeepSeek-V4.1-Flash, a multimodal Mixture-of-Experts model for agentic and coding tasks with a 1M-token context window, available on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

DeepSeek-V4.1-Flash is a multimodal Mixture-of-Experts (MoE) model from DeepSeek built for agentic and coding tasks. It accepts text and image input and has a context window of up to 1M tokens. It activates 8B of its 552B backbone parameters per token during prefill, which keeps input-heavy agentic workloads cost-efficient.

The `deepseek-v4.1-flash-maas` endpoint is available until at least November 28, 2026. Availability might be extended based on usage and demand. For more information, see [Minimum availability for Preview models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/open-models#minimum-availability) .

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
<td><code>deepseek-v4.1-flash-maas</code></td>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<td>description
Text<br />
Input and output
photo
Image<br />
Input only
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
Not supported</li>
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
<li>Global: <code>global</code></li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Quotas</th>
<td><ul>
<li><strong><code>global</code></strong> : 1,048,576 maximum output, 1,048,576 context length</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Versions</th>
<td><ul>
<li><code>deepseek-v4.1-flash-maas</code>
<ul>
<li>Launch stage: Preview</li>
<li>Release date: October 14, 2026</li>
</ul></li>
</ul></td>
<td></td>
</tr>
</tbody>
</table>

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [DeepSeek-V4.1-Flash model card](https://console.cloud.google.com/agent-platform/publishers/deepseek-ai/model-garden/deepseek-v4.1) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
