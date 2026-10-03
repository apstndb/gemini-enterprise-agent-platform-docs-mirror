---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral/codestral-2
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral/codestral-2
title: Codestral 2
description: Codestral 2 with Agent Platform Model Garden
data_source: docs.cloud.google.com
---

Codestral 2 is Mistral's code generation specialized model built specifically for high-precision fill-in-the-middle (FIM) completion. It helps developers write and interact with code through a shared instruction and completion API endpoint. As it masters code and can also converse in a variety of languages, it can be used to design advanced AI applications for software developers.

The latest release of Codestral 2 delivers measurable upgrades over prior version Codestral (25.01):

- 30% increase in accepted completions.
- 10% more retained code after suggestion.
- 50% fewer runaway generations, improving confidence in longer edits.

Improved performance on academic benchmarks for short and long-context FIM completion.

- Code generation: code completion, suggestions, translation.
- Code understanding and documentation: code summarization and explanation.
- Code quality: code review, refactoring, bug fixing and test case generation.
- Code fill-in-the-middle: users can define the starting point of the code using a prompt, and the ending point of the code using an optional suffix and an optional stop. The Codestral model will then generate the code that fits in between, making it ideal for tasks that require a specific piece of code to be generated.

Codestral 2 is well-suited for tasks such as:

- Code generation
- Fill-in-the-middle completion
- Software development applications

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/mistralai/model-garden/codestral-2)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>codestral-2</code></td>
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
<th>Versions</th>
<td><ul>
<li><code>codestral-2</code>
<ul>
<li><strong>Launch stage:</strong> GA</li>
<li><strong>Release date:</strong> October 16, 2025</li>
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
</ul>
Europe
<ul>
<li><code>europe-west4</code></li>
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
<td><p>us-central1:</p>
<ul>
<li>QPM: 1,100</li>
<li>Context length: 128,000 tokens</li>
</ul>
<p>europe-west4:</p>
<ul>
<li>QPM: 1,100</li>
<li>Context length: 128,000 tokens</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>
