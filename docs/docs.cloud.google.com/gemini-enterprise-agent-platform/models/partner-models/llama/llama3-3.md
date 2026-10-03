---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama/llama3-3
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama/llama3-3
title: Llama 3.3 70B
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Caution:** As of July 21, 2026, the `llama-3.3-70b-instruct-maas` endpoint is deprecated and will be retired on October 21, 2026. For more information, see [Open model deprecations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/open-models) .

Llama 3.3 70B is a text-only 70B instruction-tuned model that provides enhanced performance relative to Llama 3.1 70B and to Llama 3.2 90B when used for text-only applications.

## Managed API (MaaS) specifications

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/llama-3.3-70b-instruct-maas)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>llama-3.3-70b-instruct-maas</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>GA</td>
</tr>
<tr class="odd">
<th>Supported inputs &amp; outputs</th>
<td><ul>
<li>Inputs:
Text , Code</li>
<li>Outputs:
Text</li>
</ul></td>
</tr>
<tr class="even">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/batch-prediction">Batch predictions</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama">Llama Guard</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/function-calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/structured-output">Structured output</a></li>
</ul>
Not supported</td>
</tr>
<tr class="odd">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard pay-as-you-go</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a></li>
</ul></td>
</tr>
<tr class="even">
<th>Knowledge cutoff date</th>
<td>December 2023</td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>llama-3.3-70b-instruct-maas</code>
<ul>
<li><strong>Launch stage:</strong> GA</li>
<li><strong>Release date:</strong> April 29, 2025</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="odd">
<th><p>Model availability</p></th>
<td>United States
<ul>
<li><code>us-central1</code></li>
</ul></td>
</tr>
<tr class="even">
<th><p>ML processing</p></th>
<td>United States
<ul>
<li><code>Multi-region</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Quota limits</th>
<td><p>us-central1:</p>
<ul>
<li>Max output: 8,192</li>
<li>Context length: 128,000</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [Llama 3.3 70B model card](https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/llama3-3) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
