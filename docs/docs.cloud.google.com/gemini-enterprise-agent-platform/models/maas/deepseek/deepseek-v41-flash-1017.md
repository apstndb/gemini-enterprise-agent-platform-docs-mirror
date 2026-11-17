---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-v41-flash-1017
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-v41-flash-1017
title: DeepSeek-V4.1-Flash-1017
description: Explore DeepSeek-V4.1-Flash-1017, an update to DeepSeek-V4.1-Flash with improved reasoning, coding, and agentic performance and a 1M-token context window.
data_source: docs.cloud.google.com
---

DeepSeek-V4.1-Flash-1017 is a minor update to [DeepSeek-V4.1-Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-v41-flash) from DeepSeek. It uses the same multimodal Mixture-of-Experts (MoE) architecture, accepts text and image input, and has a context window of up to 1M tokens. DeepSeek reports improved results on reasoning, coding, agentic, and visual benchmarks compared to DeepSeek-V4.1-Flash, along with shorter outputs and faster task completion.

The `deepseek-v4.1-flash-1017-maas` endpoint is available until at least December 31, 2026. Availability might be extended based on usage and demand. For more information, see [Minimum availability for Preview models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/open-models#minimum-availability) .

## Managed API (MaaS) specifications

[View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/deepseek-ai/model-garden/deepseek-v4.1-flash-1017-maas) [Pricing](https://cloud.google.com/model-garden/partner-models/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>deepseek-v4.1-flash-1017-maas</code></td>
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
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier">Deferred tier</a><br />
Not supported</li>
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
<li><code>deepseek-v4.1-flash-1017-maas</code>
<ul>
<li>Launch stage: Preview</li>
<li>Release date: November 16, 2026</li>
</ul></li>
</ul></td>
<td></td>
</tr>
</tbody>
</table>

## Deploy as a self-deployed model

To self-deploy the model, go to the [DeepSeek-V4.1-Flash-1017 model card](https://console.cloud.google.com/agent-platform/publishers/deepseek-ai/model-garden/deepseek-v4.1;publisherModelVersion=deepseek-v4.1-flash-1017) in the Model Garden console and click **Deploy model** . For more information about deploying open models, see [Deploy open models from Model Garden](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/deploy-model-garden) .

## What's next

- Before you use the model, [grant user access to open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/grant-access-open-models) .
- Learn how to [call MaaS APIs for open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .
- Learn how to use [function calling for open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/function-calling) .
- Learn how to use [structured output for open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/structured-output) .
