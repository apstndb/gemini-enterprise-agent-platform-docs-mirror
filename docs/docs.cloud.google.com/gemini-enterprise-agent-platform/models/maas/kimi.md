---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/kimi
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/kimi
title: Kimi models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Kimi models are available for use as managed APIs and self-deployed models on Gemini Enterprise Agent Platform. You can stream your responses to reduce the end-user latency perception. A streamed response uses *server-sent events* (SSE) to incrementally stream the response.

## Managed Kimi models

Kimi models offer fully managed and serverless models as APIs. To use a Kimi model on Agent Platform, send a request directly to the Agent Platform API endpoint. When using Kimi models as a managed API, there's no need to provision or manage infrastructure.

The following models are available from Kimi to use in Gemini Enterprise Agent Platform. To access a Kimi model, go to its Model Garden model card.

### Kimi K2 Thinking

Kimi K2 Thinking is a thinking model from Kimi that excels at complex problem-solving and deep reasoning.

## Use Kimi models

For managed models, you can use curl commands to send requests to the Gemini Enterprise Agent Platform endpoint using the following model names:

  - For Kimi K2 Thinking, use `kimi-k2-thinking-maas`

To learn how to make streaming and non-streaming calls to Kimi models, see [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .

To use a self-deployed Gemini Enterprise Agent Platform model:

1.  Navigate to the [Model Garden console](https://console.cloud.google.com/agent-platform/model-garden) .
2.  Find the relevant Gemini Enterprise Agent Platform model.
3.  Click **Enable** and complete the provided form to get the necessary commercial use licenses.

For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .

## Kimi model region availability

Kimi models are available in the following regions:

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
<td>Kimi K2 Thinking</td>
<td><code dir="ltr" translate="no">global</code>
<ul>
<li>Max output: 262,144</li>
<li>Context length: 262,144</li>
</ul></td>
</tr>
</tbody>
</table>

## What's next

Learn how to [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .
