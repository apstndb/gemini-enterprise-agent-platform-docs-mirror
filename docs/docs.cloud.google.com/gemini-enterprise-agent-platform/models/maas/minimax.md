---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/minimax
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/minimax
title: MiniMax models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

MiniMax models are available for use as managed APIs and self-deployed models on Gemini Enterprise Agent Platform. You can stream your responses to reduce the end-user latency perception. A streamed response uses *server-sent events* (SSE) to incrementally stream the response.

## Managed MiniMax models

MiniMax models offer fully managed and serverless models as APIs. To use a MiniMax model on Agent Platform, send a request directly to the Agent Platform API endpoint. When using MiniMax models as a managed API, there's no need to provision or manage infrastructure.

The following models are available from MiniMax to use in Gemini Enterprise Agent Platform. To access a MiniMax model, go to its Model Garden model card.

### MiniMax M2

MiniMax M2 is a model from MiniMax that's designed for agentic and code-related tasks. It is built for end-to-end development workflows and has strong capabilities in planning and executing complex tool-calling tasks. The model is optimized to provide a balance of performance, cost, and inference speed.

## Use MiniMax models

For managed models, you can use curl commands to send requests to the Gemini Enterprise Agent Platform endpoint using the following model names:

  - For MiniMax M2, use `minimax-m2-maas`

To learn how to make streaming and non-streaming calls to MiniMax models, see [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .

To use a self-deployed Gemini Enterprise Agent Platform model:

1.  Navigate to the [Model Garden console](https://console.cloud.google.com/agent-platform/model-garden) .
2.  Find the relevant Gemini Enterprise Agent Platform model.
3.  Click **Enable** and complete the provided form to get the necessary commercial use licenses.

For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .

## MiniMax model region availability

MiniMax models are available in the following regions:

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
<td>MiniMax M2</td>
<td><code dir="ltr" translate="no">global</code>
<ul>
<li>Max output: 196,608</li>
<li>Context length: 196,608</li>
</ul></td>
</tr>
</tbody>
</table>

## What's next

Learn how to [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .
