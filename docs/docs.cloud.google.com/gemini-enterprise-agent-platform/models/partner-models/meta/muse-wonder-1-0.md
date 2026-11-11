---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta/muse-wonder-1-0
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta/muse-wonder-1-0
title: Muse Wonder
description: Explore the Muse Wonder model in Model Garden.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Muse Wonder from Meta is a high-capability reasoning model built for complex software engineering and long-horizon agentic work. In multi-step coding, autonomous agent, and computer-use workflows, it plans tasks, delegates to sub-agents, calls tools in parallel, and recovers from errors. It accepts text, image, and PDF inputs with a 1M-token context window.

Requests on the global `/locations/global/publishers/meta/v1/responses` endpoint pass the bare model ID `muse-wonder-1.0` in the `model` field. For an example request, see [Use Meta models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>meta/muse-wonder-1.0</code></td>
</tr>
<tr class="even">
<th>Launch stage</th>
<td>Preview</td>
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
<li>Maximum input tokens: 1,048,576</li>
</ul></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models">Function calling</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models">Structured output</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models">Reasoning</a> preview Preview feature</li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/batch-prediction">Batch predictions</a> preview Preview feature</li>
</ul></td>
</tr>
<tr class="even">
<th>Usage types</th>
<td>Supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard pay-as-you-go</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a> preview Preview feature</li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a> preview Preview feature</li>
</ul></td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>meta/muse-wonder-1.0</code>
<ul>
<li><strong>Launch stage:</strong> Preview</li>
<li><strong>Release date:</strong> November 9, 2026</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<td></td>
</tr>
<tr class="odd">
<th><p>Model availability</p></th>
<td>Global
<ul>
<li><code>global endpoint</code></li>
</ul></td>
</tr>
<tr class="even">
<th>Quota limits</th>
<td><p>global endpoint:</p>
<ul>
<li>Context length: 1,048,576</li>
</ul></td>
</tr>
<tr class="odd">
<th>Pricing</th>
<td>See <a href="https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing">Pricing</a> .</td>
</tr>
</tbody>
</table>
