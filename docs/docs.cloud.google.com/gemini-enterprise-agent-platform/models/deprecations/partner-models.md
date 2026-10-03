---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/partner-models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/partner-models
title: Partner model deprecations
description: Get deprecation and shutdown details for partner models offered through Model as a Service (MaaS).
data_source: docs.cloud.google.com
---

After a period of time, [MaaS models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/use-partner-models) are deprecated and typically replaced with newer model versions. This page lists deprecated MaaS models and their shutdown dates to help you plan and migrate to newer model versions.

## Anthropic's Claude 3 Haiku on Google Cloud

Anthropic's Claude 3 Haiku on Google Cloud is **deprecated as of February 23, 2026** and will be **shut down on August 23, 2026** . Anthropic's Claude 3 Haiku on Google Cloud is available to existing customers only.

Anthropic's Claude 3 Haiku on Google Cloud is Anthropic's fastest vision and text model for near-instant responses to basic queries, meant for seamless AI experiences mimicking human interactions.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>claude-3-haiku</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>deprecated</td>
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
<th>Token limits</th>
<td><ul>
<li>Maximum input tokens: 200,000</li>
<li>Maximum output tokens: 8,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching">Prompt caching</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens">Count tokens</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch">Batch predictions</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command">Extended thinking</a></li>
</ul></td>
</tr>
<tr class="even">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a></li>
</ul>
Not supported</td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<td></td>
</tr>
<tr class="even">
<th>Images</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/vision">Vision</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="odd">
<th>Documents</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/pdf-support">PDF support</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="even">
<th>Knowledge cutoff date</th>
<td>August 2023</td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>claude-3-haiku</code>
<ul>
<li><strong>Launch stage:</strong> Deprecated</li>
<li><strong>Release date:</strong> March 19, 2024</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="odd">
<th><p>Model availability</p>
<p>(Includes fixed quota &amp; Provisioned Throughput)</p></th>
<td>United States
<ul>
<li><code>us-east5</code></li>
</ul>
Europe
<ul>
<li><code>europe-west1</code></li>
</ul>
Asia Pacific
<ul>
<li><code>asia-southeast1</code></li>
</ul></td>
</tr>
<tr class="even">
<th><p>ML processing</p></th>
<td>United States
<ul>
<li><code>Multi-region</code></li>
</ul>
Europe
<ul>
<li><code>Multi-region</code></li>
</ul>
Asia Pacific
<ul>
<li><code>asia-southeast1</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Quota limits</th>
<td><p>us-east5:</p>
<ul>
<li>QPM: 245</li>
<li>TPM: 600,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul>
<p>europe-west1:</p>
<ul>
<li>QPM: 75</li>
<li>TPM: 181,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul>
<p>asia-southeast1:</p>
<ul>
<li>QPM: 70</li>
<li>TPM: 174,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>

## Claude 3.5 Haiku on Google Cloud

Claude 3.5 Haiku on Google Cloud is **deprecated as of January 5, 2026** and will be **shut down on July 5, 2026** . Claude 3.5 Haiku on Google Cloud is available to existing customers only.

Claude 3.5 Haiku on Google Cloud, the next generation of Anthropic's fastest and most cost-effective model, is optimal for use cases where speed and affordability matter.

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-3-5-haiku)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>claude-3-5-haiku</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>deprecated</td>
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
<th>Token limits</th>
<td><ul>
<li>Maximum input tokens: 200,000</li>
<li>Maximum output tokens: 8,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch">Batch predictions</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching">Prompt caching</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens">Count tokens</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command">Extended thinking</a></li>
</ul></td>
</tr>
<tr class="even">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a></li>
</ul>
Not supported</td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<td></td>
</tr>
<tr class="even">
<th>Images</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/vision">Vision</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="odd">
<th>Documents</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/pdf-support">PDF support</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="even">
<th>Knowledge cutoff date</th>
<td>July 2024</td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>claude-3-5-haiku</code>
<ul>
<li><strong>Launch stage:</strong> Deprecated</li>
<li><strong>Release date:</strong> October 22, 2024</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="odd">
<th><p>Model availability</p>
<p>(Includes fixed quota &amp; Provisioned Throughput)</p></th>
<td>United States
<ul>
<li><code>us-east5</code></li>
</ul>
Europe
<ul>
<li><code>europe-west1</code></li>
</ul></td>
</tr>
<tr class="even">
<th><p>ML processing</p></th>
<td>United States
<ul>
<li><code>Multi-region</code></li>
</ul>
Europe
<ul>
<li><code>Multi-region</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Quota limits</th>
<td><p>us-east5:</p>
<ul>
<li>QPM: 80</li>
<li>TPM: 350,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul>
<p>europe-west1:</p>
<ul>
<li>QPM: 90</li>
<li>TPM: 400,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>

## Claude 3.7 Sonnet on Google Cloud

Claude 3.7 Sonnet on Google Cloud is **deprecated as of November 11, 2025** and will be **shut down on May 11, 2026** . Claude 3.7 Sonnet on Google Cloud is available to existing customers only.

Claude 3.7 Sonnet on Google Cloud is a state-of-the-art model for real-world software engineering tasks and agentic capabilities.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>claude-3-7-sonnet</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>deprecated</td>
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
<th>Token limits</th>
<td><ul>
<li>Maximum input tokens: 200,000</li>
<li>Maximum output tokens: 128,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch">Batch predictions</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching">Prompt caching</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens">Count tokens</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command">Extended thinking</a></li>
</ul></td>
</tr>
<tr class="even">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a></li>
</ul>
Not supported</td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<td></td>
</tr>
<tr class="even">
<th>Images</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/vision">Vision</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="odd">
<th>Documents</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/pdf-support">PDF support</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="even">
<th>Knowledge cutoff date</th>
<td>November 2024</td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>claude-3-7-sonnet</code>
<ul>
<li><strong>Launch stage:</strong> Deprecated</li>
<li><strong>Release date:</strong> March 20, 2025</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="odd">
<th><p>Model availability</p>
<p>(Includes fixed quota &amp; Provisioned Throughput)</p></th>
<td>United States
<ul>
<li><code>us-east5</code></li>
</ul>
Europe
<ul>
<li><code>europe-west1</code></li>
</ul>
Global
<ul>
<li><code>global endpoint</code></li>
</ul></td>
</tr>
<tr class="even">
<th><p>ML processing</p></th>
<td>United States
<ul>
<li><code>Multi-region</code></li>
</ul>
Europe
<ul>
<li><code>Multi-region</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Quota limits</th>
<td><p>us-east5:</p>
<ul>
<li>QPM: 55</li>
<li>TPM: 500,000 ( <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached</a> input and output)</li>
<li>Context length: 200,000</li>
</ul>
<p>europe-west1:</p>
<ul>
<li>QPM: 40</li>
<li>TPM: 300,000 ( <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached</a> input and output)</li>
<li>Context length: 200,000</li>
</ul>
<p>global endpoint:</p>
<ul>
<li>QPM: 35</li>
<li>TPM: 300,000 ( <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached</a> input and output)</li>
<li>Context length: 200,000</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>

## Claude 3.5 Sonnet v2 on Google Cloud

Claude 3.5 Sonnet v2 on Google Cloud is **deprecated as of August 20, 2025** and will be **shut down on February 19, 2026** . Claude 3.5 Sonnet v2 on Google Cloud is available to existing customers only.

Claude 3.5 Sonnet v2 on Google Cloud is a state-of-the-art model for real-world software engineering tasks and agentic capabilities.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/generative/multimodal/create/text?model=claude-3-5-sonnet-v2)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>claude-3-5-sonnet-v2</code></td>
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
<th>Token limits</th>
<td><ul>
<li>Maximum input tokens: 200,000</li>
<li>Maximum output tokens: 8,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch">Batch predictions</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching">Prompt caching</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens">Count tokens</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command">Extended thinking</a></li>
</ul></td>
</tr>
<tr class="even">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a></li>
</ul>
Not supported</td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<td></td>
</tr>
<tr class="even">
<th>Images</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/vision">Vision</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="odd">
<th>Documents</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/pdf-support">PDF support</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="even">
<th>Knowledge cutoff date</th>
<td>August 2024</td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>claude-3-5-sonnet-v2</code>
<ul>
<li><strong>Launch stage:</strong> Generally available</li>
<li><strong>Release date:</strong> October 22, 2024</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="odd">
<th><p>Model availability</p>
<p>(Includes fixed quota &amp; Provisioned Throughput)</p></th>
<td>United States
<ul>
<li><code>us-east5</code></li>
</ul>
Europe
<ul>
<li><code>europe-west1</code></li>
</ul>
Global
<ul>
<li><code>global endpoint</code></li>
</ul></td>
</tr>
<tr class="even">
<th><p>ML processing</p></th>
<td>United States
<ul>
<li><code>Multi-region</code></li>
</ul>
Europe
<ul>
<li><code>Multi-region</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Quota limits</th>
<td><p>us-east5:</p>
<ul>
<li>QPM: 90</li>
<li>TPM: 540,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul>
<p>europe-west1:</p>
<ul>
<li>QPM: 55</li>
<li>TPM: 330,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul>
<p>global endpoint:</p>
<ul>
<li>QPM: 25</li>
<li>TPM: 140,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>

## Claude 3.5 Sonnet on Google Cloud

Claude 3.5 Sonnet on Google Cloud is **deprecated as of August 20, 2025** and will be **shut down on February 19, 2026** . Claude 3.5 Sonnet on Google Cloud is available to existing customers only.

Claude 3.5 Sonnet on Google Cloud outperforms Anthropic's Claude 3 Opus on Google Cloud on a wide range of Anthropic's evaluations with the speed and cost of Anthropic's mid-tier model, Claude 3 Sonnet on Google Cloud.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>claude-3-5-sonnet</code></td>
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
<th>Token limits</th>
<td><ul>
<li>Maximum input tokens: 200,000</li>
<li>Maximum output tokens: 8,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching">Prompt caching</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens">Count tokens</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch">Batch predictions</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command">Extended thinking</a></li>
</ul></td>
</tr>
<tr class="even">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a></li>
</ul>
Not supported</td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<td></td>
</tr>
<tr class="even">
<th>Images</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/vision">Vision</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="odd">
<th>Documents</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/pdf-support">PDF support</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="even">
<th>Knowledge cutoff date</th>
<td>April 2024</td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>claude-3-5-sonnet</code>
<ul>
<li><strong>Launch stage:</strong> Generally available</li>
<li><strong>Release date:</strong> June 20, 2024</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="odd">
<th><p>Model availability</p>
<p>(Includes fixed quota &amp; Provisioned Throughput)</p></th>
<td>United States
<ul>
<li><code>us-east5</code></li>
</ul>
Europe
<ul>
<li><code>europe-west1</code></li>
</ul>
Asia Pacific
<ul>
<li><code>asia-southeast1</code></li>
</ul></td>
</tr>
<tr class="even">
<th><p>ML processing</p></th>
<td>United States
<ul>
<li><code>Multi-region</code></li>
</ul>
Europe
<ul>
<li><code>Multi-region</code></li>
</ul>
Asia Pacific
<ul>
<li><code>asia-southeast1</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Quota limits</th>
<td><p>us-east5:</p>
<ul>
<li>QPM: 80</li>
<li>TPM: 350,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul>
<p>europe-west1:</p>
<ul>
<li>QPM: 130</li>
<li>TPM: 600,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul>
<p>asia-southeast1:</p>
<ul>
<li>QPM: 35</li>
<li>TPM: 150,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>

## Jamba 1.5 Large

Jamba 1.5 Large is **deprecated as of August 27, 2025** and will be **shut down on February 27, 2026** . Jamba 1.5 Large is available to existing customers only.

AI21 Labs's Jamba 1.5 Large is well balanced across quality, throughput, and low cost.

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/model-garden)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>jamba-1.5-large</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>Preview</td>
</tr>
<tr class="odd">
<th>Supported inputs &amp; outputs</th>
<td><ul>
<li>Inputs:
Text , Documents</li>
<li>Outputs:
Text</li>
</ul></td>
</tr>
<tr class="even">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a></li>
</ul></td>
</tr>
<tr class="odd">
<th>Knowledge cutoff date</th>
<td>March 2024</td>
</tr>
<tr class="even">
<th>Versions</th>
<td><ul>
<li><code>jamba-1.5-large</code>
<ul>
<li><strong>Launch stage:</strong> Preview</li>
<li><strong>Release date:</strong> August 22, 2024</li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="even">
<th><p>Model availability</p></th>
<td>United States
<ul>
<li><code>us-central1</code></li>
</ul>
Europe
<ul>
<li><code>europe-west4</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><p>ML processing</p></th>
<td>United States
<ul>
<li><code>Multi-region</code></li>
</ul></td>
</tr>
<tr class="even">
<th>Quota limits</th>
<td><p>us-central1:</p>
<ul>
<li>QPM: 20</li>
<li>TPM: 20,000</li>
<li>Context length: 256,000</li>
</ul>
<p>europe-west4:</p>
<ul>
<li>QPM: 20</li>
<li>TPM: 20,000</li>
<li>Context length: 256,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>

## Jamba 1.5 Mini

Jamba 1.5 Mini is **deprecated as of August 27, 2025** and will be **shut down on February 27, 2026** . Jamba 1.5 Mini is available to existing customers only.

AI21 Labs's Jamba 1.5 Mini is well balanced across quality, throughput, and low cost.

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/model-garden)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>jamba-1.5-mini</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>Preview</td>
</tr>
<tr class="odd">
<th>Supported inputs &amp; outputs</th>
<td><ul>
<li>Inputs:
Text , Documents</li>
<li>Outputs:
Text</li>
</ul></td>
</tr>
<tr class="even">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a></li>
</ul></td>
</tr>
<tr class="odd">
<th>Knowledge cutoff date</th>
<td>March 2024</td>
</tr>
<tr class="even">
<th>Versions</th>
<td><ul>
<li><code>jamba-1.5-mini</code>
<ul>
<li><strong>Launch stage:</strong> Preview</li>
<li><strong>Release date:</strong> August 22, 2024</li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="even">
<th><p>Model availability</p></th>
<td>United States
<ul>
<li><code>us-central1</code></li>
</ul>
Europe
<ul>
<li><code>europe-west4</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><p>ML processing</p></th>
<td>United States
<ul>
<li><code>Multi-region</code></li>
</ul></td>
</tr>
<tr class="even">
<th>Quota limits</th>
<td><p>us-central1:</p>
<ul>
<li>QPM: 50</li>
<li>TPM: 60,000</li>
<li>Context length: 256,000</li>
</ul>
<p>europe-west4:</p>
<ul>
<li>QPM: 50</li>
<li>TPM: 60,000</li>
<li>Context length: 256,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>

## Claude 3 Opus on Google Cloud

Anthropic's Claude 3 Opus on Google Cloud is **deprecated as of June 30, 2025** and will be **shut down on August 1, 2025** . Claude 3 Opus on Google Cloud is available to existing customers only.

Anthropic's Claude 3 Opus on Google Cloud is a powerful AI model with top-level performance on highly complex tasks. It can navigate open-ended prompts and sight-unseen scenarios with remarkable fluency and human-like understanding. Claude 3 Opus on Google Cloud is optimized for the following use cases:

- Task automation, such as interactive coding and planning, or running complex actions across APIs and databases.

- Research and development tasks, such as research review, brainstorming and hypothesis generation, and product testing.

- Strategy tasks, such as advanced analysis of charts and graphs, financials and market trends, and forecasting.

- Vision tasks, such as processing images to return text output. Also, analysis of charts, graphs, technical diagrams, reports, and other visual content.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>claude-3-opus</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>deprecated</td>
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
<th>Token limits</th>
<td><ul>
<li>Maximum input tokens: 200,000</li>
<li>Maximum output tokens: 8,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching">Prompt caching</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens">Count tokens</a></li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch">Batch predictions</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command">Extended thinking</a></li>
</ul></td>
</tr>
<tr class="even">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a></li>
</ul>
Not supported</td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<td></td>
</tr>
<tr class="even">
<th>Images</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/vision">Vision</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="odd">
<th>Documents</th>
<td><ul>
<li><strong>Limitation and specifications:</strong> See <a href="https://docs.anthropic.com/en/docs/build-with-claude/pdf-support">PDF support</a> in Anthropic's documentation</li>
</ul></td>
</tr>
<tr class="even">
<th>Knowledge cutoff date</th>
<td>August 2023</td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>claude-3-opus</code>
<ul>
<li><strong>Launch stage:</strong> Deprecated</li>
<li><strong>Release date:</strong> May 31, 2024</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="odd">
<th><p>Model availability</p>
<p>(Includes fixed quota &amp; Provisioned Throughput)</p></th>
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
<li>QPM: 20</li>
<li>TPM: 105,000 (input and output)</li>
<li>Context length: 200,000</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>
