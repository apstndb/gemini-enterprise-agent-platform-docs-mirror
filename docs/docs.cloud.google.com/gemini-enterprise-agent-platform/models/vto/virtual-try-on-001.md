---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/vto/virtual-try-on-001
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/vto/virtual-try-on-001
title: Virtual Try-On
description: Learn about the Virtual Try-On model (virtual-try-on-001), which lets you generate virtual try-on images.
data_source: docs.cloud.google.com
---

The Virtual Try-On model ( `virtual-try-on-001` ) lets you generate virtual try-on images from an image of a person and product photos that you provide.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/generate;tab=image) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>virtual-try-on-001</code></td>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<td>text_ad_off
Text<br />
Not supported
photo
Image<br />
Input and output
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
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">Thinking</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction">System instructions</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Context caching</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview">RAG Engine</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models">Tuning</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context">URL context</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/generate-virtual-try-on-images">Virtual try-on</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials">Content Credentials (C2PA)</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation">Person generation</a><br />
Supported</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>APIs</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference">GenerateContent API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a> preview Preview feature<br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Count Tokens API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview">Chat Completions API</a><br />
Not supported</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
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
<tr class="even">
<th>Technical specifications</th>
<td><strong>Image</strong> photo</td>
<td><ul>
<li>Maximum images per prompt: 2</li>
<li>Maximum file size per file for inline data or direct uploads through the console: 7 MB</li>
<li>Maximum number of output images per prompt: 4</li>
<li>Supported aspect ratios: Same as input image</li>
<li>Supported resolutions: Same as input image</li>
<li>Supported MIME types:
<code>image/png</code> , <code>image/jpeg</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><strong>Parameter defaults</strong> tune</th>
<td><ul>
<li>candidateCount: 1-4</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<td><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></td>
<td><ul>
<li>United States: <code>us-central1</code> , <code>us-east1</code> , <code>us-east4</code> , <code>us-east5</code> , <code>us-south1</code> , <code>us-west1</code> , <code>us-west4</code></li>
<li>Canada: <code>northamerica-northeast1</code></li>
<li>Europe: <code>europe-west1</code> , <code>europe-west4</code> , <code>europe-west8</code> , <code>europe-west9</code> , <code>europe-southwest1</code> , <code>europe-north1</code></li>
<li>Asia Pacific: <code>asia-northeast1</code> , <code>asia-southeast1</code></li>
<li>Middle East: <code>me-central1</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard PayGo</a></strong></p></th>
<td><ul>
<li>United States: <code>us-central1</code> , <code>us-east1</code> , <code>us-east4</code> , <code>us-east5</code> , <code>us-south1</code> , <code>us-west1</code> , <code>us-west4</code></li>
<li>Canada: <code>northamerica-northeast1</code></li>
<li>Europe: <code>europe-west1</code> , <code>europe-west4</code> , <code>europe-west8</code> , <code>europe-west9</code> , <code>europe-southwest1</code> , <code>europe-north1</code></li>
<li>Asia Pacific: <code>asia-northeast1</code> , <code>asia-southeast1</code></li>
<li>Middle East: <code>me-central1</code></li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models">Provisioned Throughput</a></strong></p></th>
<td><ul>
<li>United States: <code>us-central1</code> , <code>us-east1</code> , <code>us-east4</code> , <code>us-east5</code> , <code>us-south1</code> , <code>us-west1</code> , <code>us-west4</code></li>
<li>Canada: <code>northamerica-northeast1</code></li>
<li>Europe: <code>europe-west1</code> , <code>europe-west4</code> , <code>europe-west8</code> , <code>europe-west9</code> , <code>europe-southwest1</code> , <code>europe-north1</code></li>
<li>Asia Pacific: <code>asia-northeast1</code> , <code>asia-southeast1</code></li>
<li>Middle East: <code>me-central1</code></li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>virtual-try-on-001</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: January 20, 2026</li>
<li>Deprecation date: September 14, 2026</li>
<li>Retirement date <sup><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/vto/virtual-try-on-001#retirement-date">†</a></sup> : March 15, 2027</li>
</ul></li>
</ul></td>
<td></td>
</tr>
</tbody>
</table>

<sup>†</sup> Listed retirement dates refer to retirement of support in Gemini Enterprise Agent Platform. Models may remain accessible through the Gemini API after these dates have passed. The Gemini API is not a Google Cloud offering and is subject to its own terms of service. For details, see the [Gemini API documentation](https://ai.google.dev/) .
