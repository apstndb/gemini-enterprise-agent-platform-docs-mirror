---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/grok-4-1-fast
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/grok-4-1-fast
title: Grok 4.1 Fast
description: Explore Grok 4.1 Fast models.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Deprecated:** The Grok 4.1 model family (including `xai/grok-4.1-fast-reasoning` and `xai/grok-4.1-fast-non-reasoning` ) is deprecated on the Gemini Enterprise Agent Platform and will be shut down on August 20, 2026. After this date, Google Agent Platform Model as a Service (MaaS) will no longer serve these models. To maintain service, migrate your applications to newer xAI models (such as Grok 4.2 or Grok 4.3) or choose an alternative model from the Google Cloud Model Garden.

Grok 4.1 Fast is a cost-effective model from xAI. It excels at tool calling for lightweight tasks, powers latency-sensitive applications, and performs well in search-related tasks.

## Reasoning

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/xai/model-garden/grok-4.1-fast-reasoning)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>grok-4.1-fast-reasoning</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>deprecated</td>
</tr>
<tr class="odd">
<th>Supported inputs &amp; outputs</th>
<td><ul>
<li>Inputs:
Text , Image</li>
<li>Outputs:
Text</li>
</ul></td>
</tr>
<tr class="even">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/capabilities/function-calling">Function calling</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/capabilities/structured-output">Structured output</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/capabilities/reasoning">Reasoning</a> preview Preview feature</li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/batch-prediction">Batch predictions</a> preview Preview feature</li>
</ul></td>
</tr>
<tr class="odd">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok#quota">Fixed quota</a> preview Preview feature</li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/resources/throughput-quota">Standard pay-as-you-go</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a> preview Preview feature</li>
</ul></td>
</tr>
<tr class="even">
<th>Versions</th>
<td><ul>
<li><code>grok-4.1-fast-reasoning</code>
<ul>
<li><strong>Launch stage:</strong> Deprecated</li>
<li><strong>Release date:</strong> April 7, 2026</li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="even">
<th><p>Model availability</p></th>
<td>Global
<ul>
<li><code>global endpoint</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Quota limits</th>
<td><p>global endpoint:</p>
<ul>
<li>QPM: 160</li>
<li>Input TPM: 880,000</li>
<li>Output TPM: 40,000</li>
<li>Context length: 128,000</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>

## Non-Reasoning

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/xai/model-garden/grok-4.1-fast-non-reasoning)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>grok-4.1-fast-non-reasoning</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>deprecated</td>
</tr>
<tr class="odd">
<th>Supported inputs &amp; outputs</th>
<td><ul>
<li>Inputs:
Text , Image</li>
<li>Outputs:
Text</li>
</ul></td>
</tr>
<tr class="even">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/capabilities/function-calling">Function calling</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/capabilities/structured-output">Structured output</a> preview Preview feature</li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/batch-prediction">Batch predictions</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/capabilities/reasoning">Reasoning</a> preview Preview feature</li>
</ul></td>
</tr>
<tr class="odd">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok#quota">Fixed quota</a> preview Preview feature</li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/resources/throughput-quota">Standard pay-as-you-go</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a> preview Preview feature</li>
</ul></td>
</tr>
<tr class="even">
<th>Versions</th>
<td><ul>
<li><code>grok-4.1-fast-non-reasoning</code>
<ul>
<li><strong>Launch stage:</strong> Deprecated</li>
<li><strong>Release date:</strong> April 7, 2026</li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="even">
<th><p>Model availability</p></th>
<td>Global
<ul>
<li><code>global endpoint</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Quota limits</th>
<td><p>global endpoint:</p>
<ul>
<li>QPM: 160</li>
<li>Input TPM: 880,000</li>
<li>Output TPM: 40,000</li>
<li>Context length: 128,000</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>
