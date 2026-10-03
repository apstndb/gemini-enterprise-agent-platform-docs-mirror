---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral/mistral-ocr
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral/mistral-ocr
title: Mistral OCR (25.05)
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Mistral OCR (25.05) is an Optical Character Recognition API for document understanding. Mistral OCR (25.05) excels in understanding complex document elements, including interleaved imagery, mathematical expressions, tables, and advanced layouts such as LaTeX formatting. The model enables deeper understanding of rich documents such as scientific papers with charts, graphs, equations and figures.

Mistral OCR (25.05) is an ideal model to use in combination with a RAG system that takes multimodal documents (such as slides or complex PDFs) as input.

You can couple Mistral OCR (25.05) with other Mistral models to reformat the results. This combination ensures that the extracted content is not only accurate but also presented in a structured and coherent manner, making it suitable for various downstream applications and analyses.

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/mistralai/model-garden/mistral-ocr-2505)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>mistral-ocr-2505</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>GA</td>
</tr>
<tr class="odd">
<th>Supported inputs &amp; outputs</th>
<td><ul>
<li>Inputs:
Documents</li>
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
<li><code>Mistral OCR (25.05)</code>
<ul>
<li><strong>Launch stage:</strong> GA</li>
<li><strong>Release date:</strong> May 14, 2025</li>
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
<li>QPM: 30</li>
<li>Pages per request: 30 (1 page = 1 million input tokens and 1 million output tokens)</li>
<li>Context length: 30 pages</li>
<li>Max request size: 30MB for streaming, 10MB for unary</li>
</ul>
<p>europe-west4:</p>
<ul>
<li>QPM: 30</li>
<li>Pages per request: 30 (1 page = 1 million input tokens and 1 million output tokens)</li>
<li>Context length: 30 pages</li>
<li>Max request size: 30MB for streaming, 10MB for unary</li>
</ul></td>
</tr>
<tr class="even">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>
