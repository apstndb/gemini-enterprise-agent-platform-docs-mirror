---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-5-5
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-5-5
title: Claude Sonnet 5.5 on Google Cloud
description: Claude Sonnet 5.5 is built for coding, agents, and professional work at scale.
data_source: docs.cloud.google.com
---

Claude Sonnet 5.5 on Google Cloud is built for coding, agents, and professional work at scale. For full information, see [Anthropic's documentation](https://platform.claude.com/docs/en/models/sonnet-5-5/overview) .

**Retirement Date:** Not sooner than September 28, 2027.

In addition to the features of Claude Sonnet 5 on Google Cloud, Claude Sonnet 5.5 on Google Cloud adds:

- **New thinking type value** : Claude Sonnet 5.5 on Google Cloud adds a new `thinking.type` value, `between_tools` , which is the lowest thinking setting available on this model. Claude Sonnet 5.5 on Google Cloud doesn't support `thinking: {"type": "disabled"}` . If you want to turn thinking off, or as close to off as possible, use `between_tools` . With `between_tools` , the model does no extended thinking, and the short progress updates it writes between tool calls come back as thinking blocks containing the update text. The response format is unchanged.
- **Adaptive thinking** can be turned on or off.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-5-5) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-5-5)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>claude-sonnet-5-5</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>GA</td>
</tr>
<tr class="odd">
<th>Supported inputs &amp; outputs</th>
<td><ul>
<li>Inputs:
Text , Image , PDF</li>
<li>Outputs:
Text</li>
</ul></td>
</tr>
<tr class="even">
<th>Token limits</th>
<td><ul>
<li>Maximum input tokens: 1,000,000</li>
<li>Maximum output tokens: 128,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.anthropic.com/en/docs/build-with-claude/computer-use">Computer use</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/web-search">Web search</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch">Batch predictions</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching">Prompt caching</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling">Function calling</a></li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens">Count tokens</a></li>
<li><a href="https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/memory-tool">Memory tool</a></li>
</ul>
Not supported</td>
</tr>
<tr class="even">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/quotas">Shared Model Lineage Quota</a></li>
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
<th>Versions</th>
<td><ul>
<li><code>claude-sonnet-5-5</code>
<ul>
<li><strong>Launch stage:</strong> Generally available</li>
<li><strong>Release date:</strong> September 28, 2026</li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="even">
<th><p>Model availability</p>
<p>(Includes fixed quota &amp; Provisioned Throughput)</p></th>
<td>United States
<ul>
<li><code>Multi-region</code></li>
</ul>
Europe
<ul>
<li><code>Multi-region</code></li>
</ul>
Global
<ul>
<li><code>global endpoint</code></li>
</ul></td>
</tr>
<tr class="odd">
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
<tr class="even">
<th>Quota limits</th>
<td><p>Multi-region:</p>
<ul>
<li>QPM: 1,250</li>
<li>Input TPM: 12,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,250,000</li>
<li>Context length: 1,000,000</li>
</ul>
<p>Multi-region:</p>
<ul>
<li>QPM: 1,250</li>
<li>Input TPM: 12,500,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 1,250,000</li>
<li>Context length: 1,000,000</li>
</ul>
<p>global endpoint:</p>
<ul>
<li>QPM: 2,500</li>
<li>Input TPM: 25,000,000 <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input">uncached and cache write</a></li>
<li>Output TPM: 2,500,000</li>
<li>Context length: 1,000,000</li>
</ul></td>
</tr>
<tr class="odd">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>
