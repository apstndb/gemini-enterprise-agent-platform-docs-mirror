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

Muse Wonder from Meta is a high-capability reasoning model built for complex software engineering and long-horizon agentic work. In multi-step coding, autonomous agent, and computer-use workflows, it plans tasks, delegates to sub-agents, calls tools in parallel, and recovers from errors. It accepts text and image inputs with a 1M-token context window.

Requests on the global `/locations/global/publishers/meta/v1/responses` endpoint pass the bare model ID `muse-wonder-1.0` in the `model` field. For an example request, see [Use Meta models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models) .

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/muse-wonder-1.0)

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
Text , Image</li>
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
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models">Responses API</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models">Function calling</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models">Structured output</a> preview Preview feature</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models">Reasoning</a> preview Preview feature</li>
</ul>
Not supported
<ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models">Chat Completions API</a> preview Preview feature</li>
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

## Inference parameters and limitations

Keep the following inference parameters and limitations in mind when sending requests:

- **Reasoning effort:** Set `reasoning.effort` to `minimal` , `low` , `medium` , `high` , or `xhigh` . `max` isn't available on Google Cloud, and `none` isn't supported. Pricing is the same at every effort level.
- **Reasoning output:** Reasoning summaries aren't returned. Reasoning content is returned only in encrypted form for multi-turn replay.
- **Tool calling:** Supports built-in tool calling with parallel tool calls. `tool_choice` supports `auto` only ( `none` , `required` , and named-function choices aren't supported).
- **Recommended sampling:** `temperature` `1.0` , `top_p` `1.0` ( `top_k` disabled).
- **Known limitations:** Audio, video, and PDF inputs, chat completions, and stateful response storage ( `store: true` ) aren't supported. The model has limited visual and spatial reasoning, especially for 3D tasks. For the full capability list, see the table earlier on this page.
- **Usage restriction:** Muse Wonder isn't intended for use by individuals under the age of 18.

## What's next

- Send requests using [Use Meta models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models) .
- View [Muse Wonder on Google Cloud Marketplace](https://console.cloud.google.com/marketplace/product/meta/muse-wonder-1-0) .
- Read the [Muse Wonder model card](https://research.meta.ai/static/muse-wonder-model-card) and explore the [Meta Model API documentation](https://dev.meta.ai/docs) .
- Review the [Meta Model API Terms of Service](https://dev.meta.ai/legal/terms-of-service) and [Acceptable Use Policy](https://dev.meta.ai/legal/acceptable-use-policy) , which apply alongside the Google Cloud Marketplace Terms of Service.
