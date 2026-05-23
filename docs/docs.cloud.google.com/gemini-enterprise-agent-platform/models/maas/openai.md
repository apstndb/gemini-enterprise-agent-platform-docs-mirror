---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/openai
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/openai
title: OpenAI models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Note:** OpenAI models are not a Google product, and its availability in Gemini Enterprise Agent Platform is subject to the terms for "Separate Offerings" in the AI/ML Services section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) , and separate terms found in the relevant model card.

OpenAI models are available for use as managed APIs and self-deployed models on Gemini Enterprise Agent Platform. You can stream your responses to reduce the end-user latency perception. A streamed response uses *server-sent events* (SSE) to incrementally stream the response.

### gpt-oss 120B

OpenAI gpt-oss 120B is a 120B open-weight language model released under the Apache 2.0 license. It is well-suited for reasoning and function calling use cases. The model is optimized for deployment on consumer hardware.

The 120B model achieves near-parity with OpenAI o4-mini on core reasoning benchmarks, while running on a single 80GB GPU.

### gpt-oss 20B

OpenAI gpt-oss 20B is a 20B open-weight language model released under the Apache 2.0 license. It is well-suited for reasoning and function calling use cases. The model is optimized for deployment on consumer hardware.

The 20B model delivers similar results to OpenAI o3-mini on common benchmarks and can run on edge devices with 16GB of memory, making it ideal for on-device use cases, local inference, or rapid iteration without costly infrastructure.

## Use OpenAI models

For managed models, you can use curl commands to send requests to the Gemini Enterprise Agent Platform endpoint using the following model names:

  - For gpt-oss 120B, use `gpt-oss-120b-maas`
  - For gpt-oss 20B, use `gpt-oss-20b-maas`

To learn how to make streaming and non-streaming calls to OpenAI models, see [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .

To use a self-deployed Gemini Enterprise Agent Platform model:

1.  Navigate to the [Model Garden console](https://console.cloud.google.com/agent-platform/model-garden) .
2.  Find the relevant Gemini Enterprise Agent Platform model.
3.  Click **Enable** and complete the provided form to get the necessary commercial use licenses.

For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .

## OpenAI model region availability

OpenAI models are available in the following regions:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Model</th>
<th>Regions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>gpt-oss 120B</td>
<td><code dir="ltr" translate="no">global</code>
<ul>
<li>Max output: 131,072</li>
<li>Context length: 131,072</li>
</ul>
<code dir="ltr" translate="no">us-central1</code>
<ul>
<li>Max output: 131,072</li>
<li>Context length: 131,072</li>
</ul></td>
</tr>
<tr class="even">
<td>gpt-oss 20B</td>
<td><code dir="ltr" translate="no">us-central1</code>
<ul>
<li>Max output: 32,768</li>
<li>Context length: 131,072</li>
</ul></td>
</tr>
</tbody>
</table>

## What's next

Learn how to [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .
