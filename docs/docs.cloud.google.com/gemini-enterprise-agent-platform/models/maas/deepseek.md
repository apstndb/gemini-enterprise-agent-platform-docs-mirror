---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek
title: DeepSeek models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

DeepSeek models are available for use as managed APIs and self-deployed models on Gemini Enterprise Agent Platform. You can stream your responses to reduce the end-user latency perception. A streamed response uses *server-sent events* (SSE) to incrementally stream the response.

## Managed DeepSeek models

> **Note:** The DeepSeek R1 model is not a Google product, and its availability in Gemini Enterprise Agent Platform is subject to the terms for "Separate Offerings" in the AI/ML Services section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) , and separate terms found in the relevant model card.

DeepSeek models offer fully managed and serverless models as APIs. To use a DeepSeek model on Agent Platform, send a request directly to the Agent Platform API endpoint. When using DeepSeek models as a managed API, there's no need to provision or manage infrastructure.

The following models are available from DeepSeek to use in Gemini Enterprise Agent Platform. To access a DeepSeek model, go to its Model Garden model card.

### DeepSeek-OCR

DeepSeek-OCR is a comprehensive Optical Character Recognition (OCR) model that analyzes and understands complex documents. It excels at challenging OCR tasks, including recognizing mathematical formulas and processing text that is curved, rotated, or overlapping.

### DeepSeek-V3.2

DeepSeek-V3.2 is a model that harmonizes high computational efficiency with superior reasoning and agent performance. DeepSeek's approach is built upon three key technical breakthroughs: DeepSeek Sparse Attention (DSA), scalable reinforcement learning framework, and large scale agentic task synthesis pipeline.

### DeepSeek-V3.1

DeepSeek-V3.1 is a hybrid model that supports both thinking mode and non-thinking mode. Compared to the previous version, this upgrade brings improvements in hybrid thinking modes, tool calling, and thinking efficiency.

### DeepSeek R1 (0528)

DeepSeek R1 (0528) is the latest version of the DeepSeek R1 model. Compared to DeepSeek-R1, it has significantly improved depth of reasoning and inference capabilities. DeepSeek R1 (0528) excels in wide range tasks, such as creative writing, general question answering, editing, and summarization.

#### Considerations

For production-ready safety, integrate DeepSeek R1 (0528) with [Model Armor](https://cloud.google.com/security-command-center/docs/model-armor-overview) , which screens LLM prompts and responses for various security and safety risks.

## Use DeepSeek models

For managed models, you can use curl commands to send requests to the Gemini Enterprise Agent Platform endpoint using the following model names:

  - For DeepSeek-OCR, use `deepseek-ocr-maas`
  - For DeepSeek-V3.2, use `deepseek-v3.2-maas`
  - For DeepSeek-V3.1, use `deepseek-v3.1-maas`
  - For DeepSeek R1 (0528), use `deepseek-r1-0528-maas`

To learn how to make streaming and non-streaming calls to DeepSeek models, see [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .

To use a self-deployed Gemini Enterprise Agent Platform model:

1.  Navigate to the [Model Garden console](https://console.cloud.google.com/agent-platform/model-garden) .
2.  Find the relevant Gemini Enterprise Agent Platform model.
3.  Click **Enable** and complete the provided form to get the necessary commercial use licenses.

For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .

## DeepSeek model region availability

DeepSeek models are available in the following regions:

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
<td>DeepSeek-OCR</td>
<td><ul>
<li><code dir="ltr" translate="no">us-central1</code></li>
</ul></td>
</tr>
<tr class="even">
<td>DeepSeek-V3.2</td>
<td><ul>
<li><code dir="ltr" translate="no">global</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>DeepSeek-V3.1</td>
<td><ul>
<li><code dir="ltr" translate="no">us-central1</code></li>
</ul></td>
</tr>
<tr class="even">
<td>DeepSeek R1 (0528)</td>
<td><ul>
<li><code dir="ltr" translate="no">us-central1</code></li>
</ul></td>
</tr>
</tbody>
</table>

## What's next

Learn how to [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .
