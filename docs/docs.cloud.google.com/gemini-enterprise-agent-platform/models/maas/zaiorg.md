---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/zaiorg
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/zaiorg
title: GLM models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

GLM models on Gemini Enterprise Agent Platform offer fully managed and serverless models as APIs. To use a GLM model on Agent Platform, send a request directly to the Agent Platform API endpoint. Because GLM models use a managed API, there's no need to provision or manage infrastructure.

You can stream your responses to reduce the end-user latency perception. A streamed response uses *server-sent events* (SSE) to incrementally stream the response.

### GLM 4.7

GLM 4.7 is a model from GLM designed for core or vibe coding, tool use, and complex reasoning.

### GLM 5

GLM 5 is a model from GLM targeting complex systems engineering and long-horizon agentic tasks.

## Use GLM models

For managed models, you can use curl commands to send requests to the Gemini Enterprise Agent Platform endpoint using the following model names:

  - For GLM 4.7, use `glm-4.7-maas`
  - For GLM 5, use `glm-5-maas`

To learn how to make streaming and non-streaming calls to GLM models, see [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .

To use a self-deployed Gemini Enterprise Agent Platform model:

1.  Navigate to the [Model Garden console](https://console.cloud.google.com/agent-platform/model-garden) .
2.  Find the relevant Gemini Enterprise Agent Platform model.
3.  Click **Enable** and complete the provided form to get the necessary commercial use licenses.

For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .

## GLM model region availability

GLM models are available in the following regions:

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
<td>GLM 4.7</td>
<td><ul>
<li><code dir="ltr" translate="no">global</code></li>
</ul></td>
</tr>
<tr class="even">
<td>GLM 5</td>
<td><ul>
<li><code dir="ltr" translate="no">global</code></li>
</ul></td>
</tr>
</tbody>
</table>

## What's next

Learn how to [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .
