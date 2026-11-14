---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta/muse-spark-1-3
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta/muse-spark-1-3
title: Muse Spark 1.3
description: Explore the Muse Spark 1.3 model in Model Garden.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Muse Spark 1.3 from Meta is a reasoning model trained for agentic workflows and competitive coding. It supports built-in tool calling with Model Context Protocol (MCP) support, accepts text and image inputs, and offers a 1M-token context window for multi-step tasks.

Requests on the global `/locations/global/publishers/meta/v1/responses` endpoint pass the bare model ID `muse-spark-1.3` in the `model` field. For an example request, see [Use Meta models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models) .

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/muse-spark-1.3)

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>meta/muse-spark-1.3</code></td>
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
<li><code>meta/muse-spark-1.3</code>
<ul>
<li><strong>Launch stage:</strong> Preview</li>
<li><strong>Release date:</strong> September 24, 2026</li>
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
- **Reasoning output:** Reasoning content is returned in encrypted form for multi-turn replay. Optional reasoning summaries ( `reasoning.summary` ) aren't returned on every response.
- **Tool calling:** Supports built-in tool calling with Model Context Protocol (MCP) support. `tool_choice` supports `auto` only ( `none` , `required` , and named-function choices aren't supported).
- **Recommended sampling:** `temperature` `1.0` , `top_p` `1.0` ( `top_k` disabled).
- **Known limitations:** Audio, video, and PDF inputs, chat completions, and stateful response storage ( `store: true` ) aren't supported. The model isn't trained for tabular input, so results on tabular data can vary. For the full capability list, see the table earlier on this page.

## What's next

- Send requests using [Use Meta models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta#use-meta-models) .
- View [Muse Spark 1.3 on Google Cloud Marketplace](https://console.cloud.google.com/marketplace/product/meta/muse-spark-1-3) .
- Explore the [Meta Model API documentation](https://dev.meta.ai/docs) .
- Review the [Meta Model API Terms of Service](https://dev.meta.ai/legal/terms-of-service) and [Acceptable Use Policy](https://dev.meta.ai/legal/acceptable-use-policy) , which apply alongside the Google Cloud Marketplace Terms of Service.
