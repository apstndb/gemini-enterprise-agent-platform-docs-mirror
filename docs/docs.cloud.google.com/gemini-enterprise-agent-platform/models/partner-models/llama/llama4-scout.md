---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama/llama4-scout
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama/llama4-scout
title: Llama 4 Scout 17B-16E
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Llama 4 Scout 17B-16E delivers state-of-the-art results for its size class that outperforms previous Llama generations and other open and proprietary models on several benchmarks. It features MoE architecture with 17 billion active parameters out of the 109 billion total parameters and 16 experts.

Llama 4 Scout 17B-16E is suited for retrieval tasks within long contexts and tasks that demand reasoning over large amounts of information, such as summarizing multiple large documents, analyzing extensive user interaction logs for personalization, and reasoning across large codebases.

## Managed API (MaaS) specifications

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/generative/multimodal/create/text?model=llama-4-scout-17b-16e-instruct-maas) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/llama-4-maverick-17b-128e-instruct-maas)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>llama-4-scout-17b-16e-instruct-maas</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>GA</td>
</tr>
<tr class="odd">
<th>Supported inputs &amp; outputs</th>
<td><ul>
<li>Inputs:
Text , Code , Images</li>
<li>Outputs:
Text</li>
</ul></td>
</tr>
<tr class="even">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/batch-prediction">Batch predictions</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/function-calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/structured-output">Structured output</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama">Llama Guard</a></li>
</ul></td>
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
<td>August 2024</td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>llama-4-scout-17b-16e-instruct-maas</code>
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
<li><code>us-east5</code></li>
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
<td><p>us-east5:</p>
<ul>
<li>Max output: 8,192</li>
<li>Context length: 1,310,720</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [Llama 4 Scout 17B-16E model card](https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/llama4) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .

## Considerations

- You can include a maximum of three images per request.
- The MaaS endpoint doesn't use Llama Guard, unlike previous versions. To use Llama Guard, deploy Llama Guard from Model Garden and then send the prompts and responses to that endpoint. However, compared to Llama 4, Llama Guard has a more limited context (128,000) and can only process requests with a single image at the beginning of the prompt.
- Batch predictions aren't supported.
