---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-ocr
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-ocr
title: DeepSeek-OCR
description: Understand DeepSeek-OCR, a comprehensive OCR model for complex document analysis and challenging text recognition.
data_source: docs.cloud.google.com
---

> **Caution:** As of July 21, 2026, the `deepseek-ocr-maas` endpoint is deprecated and will be retired on October 21, 2026. For more information, see [Open model deprecations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/open-models) .

DeepSeek-OCR is a comprehensive Optical Character Recognition (OCR) model that analyzes and understands complex documents. It excels at challenging OCR tasks, including recognizing mathematical formulas and processing text that is curved, rotated, or overlapping.

## Managed API (MaaS) specifications

[Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>deepseek-ocr-maas</code></td>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<td>description
Text<br />
Input and output
photo
Image<br />
Input only
mic_off
Audio<br />
Not supported
videocam_off
Video<br />
Not supported</td>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/thinking">Thinking</a><br />
Not supported</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Consumption options</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference">Batch inference</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Pay-as-you-go</a><br />
Standard PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Not supported</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<td><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></td>
<td><ul>
<li>United States: <code>us-central1</code></li>
</ul></td>
</tr>
<tr class="even">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency">ML processing</a></strong></p></th>
<td><ul>
<li>Multi-region: <code>us</code></li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Quotas</th>
<td><ul>
<li><strong><code>us-central1</code></strong> : 8,192 maximum output, 8,192 context length</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Versions</th>
<td><ul>
<li><code>DeepSeek-OCR</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: October 23, 2025</li>
</ul></li>
</ul></td>
<td></td>
</tr>
</tbody>
</table>

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [DeepSeek-OCR model card](https://console.cloud.google.com/agent-platform/publishers/deepseek-ai/model-garden/deepseek-ocr) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
