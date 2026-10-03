---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-4
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-4
title: Claude Sonnet 4 on Google Cloud
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Claude Sonnet 4 on Google Cloud balances impressive performance for coding with the right speed and cost for high-volume use cases:

**Retirement Date:** Not sooner than May 14, 2026.

- **Coding** : Handle everyday development tasks with enhanced performance—power code reviews, bug fixes, API integrations, and feature development with immediate feedback loops.
- **AI Assistants** : Power production-ready assistants for real-time applications—from customer support automation to operational workflows that require both intelligence and speed.
- **Efficient research** : Perform focused analysis across multiple data sources while maintaining fast response times. Ideal for rapid business intelligence, competitive analysis, and real-time decision support.
- **Large-scale content** : Generate and analyze content at scale with improved quality. Create customer communications, analyze user feedback, and produce marketing materials with the right balance of quality and throughput.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/generative/multimodal/create/text?model=claude-sonnet-4) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-4)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>claude-sonnet-4</code></td>
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
<li>Maximum input tokens: 1M (Preview)<br />
200,000 (GA)</li>
<li>Maximum output tokens: 64,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/web-search">Web search</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch">Batch predictions</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching">Prompt caching</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command">Extended thinking</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens">Count tokens</a></li>
</ul>
Not supported</td>
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
<td>March 2025</td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>claude-sonnet-4</code>
<ul>
<li><strong>Launch stage:</strong> Generally available</li>
<li><strong>Release date:</strong> May 22, 2025</li>
<li><strong>Retirement date not sooner than:</strong> May 14, 2026</li>
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
<li>QPM: 35</li>
<li>Input TPM: 280,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 20,000</li>
<li>Context length: 1,000,000</li>
</ul>
<p>europe-west1:</p>
<ul>
<li>QPM: 25</li>
<li>Input TPM: 180,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 20,000</li>
<li>Context length: 1,000,000</li>
</ul>
<p>global endpoint:</p>
<ul>
<li>QPM: 35</li>
<li>Input TPM: 276,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 24,000</li>
<li>Context length: 1,000,000</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>
