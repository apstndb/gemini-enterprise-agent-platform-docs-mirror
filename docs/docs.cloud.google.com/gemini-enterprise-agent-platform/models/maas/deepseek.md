---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek
title: DeepSeek models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

DeepSeek models are available for use as managed APIs and self-deployed models on Gemini Enterprise Agent Platform. You can stream your responses to reduce the end-user latency perception. A streamed response uses *server-sent events* (SSE) to incrementally stream the response.

## Managed DeepSeek models

> **Note:** DeepSeek models are not Google products, and their availability in Gemini Enterprise Agent Platform is subject to the terms for "Separate Offerings" in the AI/ML Services section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) , and separate terms found in the relevant model card.

DeepSeek models offer fully managed and serverless models as APIs. To use a DeepSeek model on Agent Platform, send a request directly to the Agent Platform API endpoint. When using DeepSeek models as a managed API, there's no need to provision or manage infrastructure.

The following models are available from DeepSeek to use in Gemini Enterprise Agent Platform. To access a DeepSeek model, go to its Model Garden model card.

### DeepSeek-V4.1-Flash

DeepSeek-V4.1-Flash is a multimodal Mixture-of-Experts (MoE) model from DeepSeek built for agentic and coding tasks. It accepts text and image input and has a context window of up to 1M tokens.

## Use DeepSeek models

For managed models, you can use curl commands to send requests to the Gemini Enterprise Agent Platform endpoint using the following model names:

- For DeepSeek-V4.1-Flash, use `deepseek-v4.1-flash-maas`

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
<td>DeepSeek-V4.1-Flash</td>
<td><ul>
<li><code>global</code></li>
</ul></td>
</tr>
</tbody>
</table>

## What's next

Learn how to [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .
