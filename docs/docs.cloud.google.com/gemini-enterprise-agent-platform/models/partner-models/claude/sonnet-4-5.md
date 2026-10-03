---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-4-5
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-4-5
title: Claude Sonnet 4.5 on Google Cloud
description: Model details for Claude Sonnet 4.5
data_source: docs.cloud.google.com
---

Claude Sonnet 4.5 on Google Cloud is Anthropic's Sonnet-class model for powering real-world agents, with industry leading capabilities around coding, computer use, cybersecurity, and working with office files like spreadsheets.

**Retirement Date:** Not sooner than Sept 29, 2026.

- **Long-running agents** : Power production-ready assistants for multi-step, real-time applications, from customer support automation to complex operational workflows that require peak accuracy, intelligence, and speed.
- **Coding** : Handle everyday development tasks with enhanced performance - or plan and execute complex software projects spanning hours or days - with the ability to save, maintain, and reference information across multiple sessions.
- **Cybersecurity** : Deploy agents that autonomously patch vulnerabilities before exploitation, shifting from reactive detection to proactive defense.
- **Financial analysis** : Conduct entry-level financial analysis, deliver advanced predictive analysis, or preemptively develop intelligent risk management strategies that leverage best-in-class domain knowledge.
- **Computer use** : A highly accurate model for computer use, enabling developers to direct the model to use computers the way people do.
- **Business tasks** : Generate and edit office files like slides, documents, and spreadsheets with minimal input.
- **Research** : Perform focused analysis across multiple data sources, turning expert analysis into final deliverables. Ideal for complex problem solving, rapid business intelligence, and real-time decision support.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/generative/multimodal/create/text?model=claude-sonnet-4-5) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-4-5)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>claude-sonnet-4-5</code></td>
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
<td>July, 2025</td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>claude-sonnet-4-5</code>
<ul>
<li><strong>Launch stage:</strong> Generally available</li>
<li><strong>Release date:</strong> September 29, 2025</li>
<li><strong>Retirement date not sooner than:</strong> September 29, 2026</li>
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
<li>QPM: 1,500</li>
<li>Input TPM: 1,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 150,000</li>
<li>Context length: 1,000,000 (beta), 200,000 (GA)</li>
</ul>
<p>europe-west1:</p>
<ul>
<li>QPM: 1,800</li>
<li>Input TPM: 1,800,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 180,000</li>
<li>Context length: 1,000,000 (beta), 200,000 (GA)</li>
</ul>
<p>asia-southeast1:</p>
<ul>
<li>QPM: 1,500</li>
<li>Input TPM: 1,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 150,000</li>
<li>Context length: 1,000,000 (beta), 200,000 (GA)</li>
</ul>
<p>global endpoint:</p>
<ul>
<li>QPM: 1,500</li>
<li>Input TPM: 1,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 150,000</li>
<li>Context length: 1,000,000 (beta), 200,000 (GA)</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>
