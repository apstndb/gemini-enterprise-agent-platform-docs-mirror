---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite
title: Gemini 2.5 Flash-Lite
description: Learn about Gemini 2.5 Flash-Lite, our most cost effective model that supports high throughput tasks.
data_source: docs.cloud.google.com
---

> **Important:** This model is being retired on October 20th, 2026. See [Migrate to latest Gemini models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate) for recommended replacement models.

Gemini 2.5 Flash-Lite is our most balanced Gemini model, optimized for low latency use cases. It comes with the same capabilities that make other Gemini 2.5 models helpful, such as the ability to turn thinking on at different budgets, connecting to tools like Grounding with Google Search and code execution, multimodal input, and a 1 million-token context length.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-2.5-flash-lite) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-2.5-flash-lite) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Note: "Deploy example app" requires a Google Cloud project with billing and Agent Platform API enabled.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<th><code>gemini-2.5-flash-lite</code></th>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<th>description
Text<br />
Input and output
photo
Image<br />
Input only
mic
Audio<br />
Input only
videocam
Video<br />
Input only</th>
<td></td>
</tr>
<tr class="odd">
<th>Token limits</th>
<th>Context window</th>
<td>1,048,576</td>
</tr>
<tr class="even">
<th>Maximum output tokens</th>
<th>65,536</th>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">Thinking</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction">System instructions</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a> preview Preview feature<br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Context caching</a><br />
Implicit context caching, explicit context caching<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Count Tokens</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview">RAG Engine</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview">Chat completions</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models">Tuning</a><br />
Supervised fine-tuning, continuous tuning, preference tuning, tuning checkpoints<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context">URL context</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing">Agentic video understanding</a> preview Preview feature<br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Tools</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview">Grounding</a><br />
Google Search, Parallel Web Search, Exa Web Search<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution">Code execution</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use">Computer use</a> preview Preview feature<br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Consumption options</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference">Batch inference</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Pay-as-you-go</a><br />
Priority PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Input size limit</th>
<th>500 MB</th>
<td></td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<th><strong>Image</strong> photo</th>
<td><ul>
<li>Maximum images per prompt: 3,000</li>
<li>Maximum file size per file for inline data or direct uploads through the console: 7 MB</li>
<li>Maximum file size per file from Google Cloud Storage: 30 MB</li>
<li>Supported MIME types:
<code>image/png</code> , <code>image/jpeg</code> , <code>image/webp</code> , <code>image/heic</code> , <code>image/heif</code></li>
</ul></td>
</tr>
<tr class="even">
<th><strong>Text</strong> description</th>
<th><ul>
<li>Maximum number of files per prompt: 3,000</li>
<li>Maximum number of pages per file: 1,000</li>
<li>Maximum file size per file for the API or Cloud Storage imports: 50 MB(application/pdf) or 7 MB(text/plain)</li>
<li>Maximum file size per file for direct uploads through the console: 7 MB</li>
<li>Supported MIME types:
<code>application/pdf</code> , <code>text/plain</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Video</strong> videocam</th>
<th><ul>
<li>Maximum video length (with audio): Approximately 45 minutes</li>
<li>Maximum video length (without audio): Approximately 1 hour</li>
<li>Maximum number of videos per prompt: 10</li>
<li>Supported MIME types:
<code>video/x-flv</code> , <code>video/quicktime</code> , <code>video/mpeg</code> , <code>video/mpegs</code> , <code>video/mpg</code> , <code>video/mp4</code> , <code>video/webm</code> , <code>video/wmv</code> , <code>video/3gpp</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><strong>Audio</strong> mic</th>
<th><ul>
<li>Maximum audio length per prompt: Approximately 8.4 hours, or up to 1 million tokens</li>
<li>Maximum number of audio files per prompt: 1</li>
<li>Supported MIME types:
<code>audio/x-aac</code> , <code>audio/flac</code> , <code>audio/mp3</code> , <code>audio/m4a</code> , <code>audio/mpeg</code> , <code>audio/mpga</code> , <code>audio/mp4</code> , <code>audio/ogg</code> , <code>audio/pcm</code> , <code>audio/wav</code> , <code>audio/webm</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Parameter defaults</strong> tune</th>
<th><ul>
<li>Temperature: 0.0-2.0 (default 1.0)</li>
<li>topP: 0.0-1.0 (default 0.95)</li>
<li>topK: 64 (fixed)</li>
<li>candidateCount: 1–8 (default 1)</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></th>
<td><ul>
<li>Global: <code>global</code></li>
<li>United States: <code>us-central1</code> , <code>us-east1</code> , <code>us-east4</code> , <code>us-east5</code> , <code>us-south1</code> , <code>us-west1</code> , <code>us-west4</code></li>
<li>Europe: <code>europe-central2</code> , <code>europe-north1</code> , <code>europe-southwest1</code> , <code>europe-west1</code> , <code>europe-west4</code> , <code>europe-west8</code> , <code>europe-west9</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Versions</th>
<th><ul>
<li><code>gemini-2.5-flash-lite</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: July 22, 2025</li>
<li>Retirement date <sup><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite#retirement-date">†</a></sup> : October 20, 2026</li>
</ul></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Security controls</th>
<th><strong>Online prediction</strong></th>
<td><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></td>
</tr>
<tr class="odd">
<th><strong>Batch inference</strong></th>
<th><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><strong>Tuning</strong></th>
<th><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Context caching</strong></th>
<th><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><strong>RAG Engine</strong></th>
<th><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Grounding with Google Search and Grounding with Google Maps</strong></th>
<th><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls">Security controls</a> for more information.</th>
<th></th>
<td></td>
</tr>
</tbody>
</table>

<sup>†</sup> Listed retirement dates refer to retirement of support in Gemini Enterprise Agent Platform. Models may remain accessible through the Gemini API after these dates have passed. The Gemini API is not a Google Cloud offering and is subject to its own terms of service. For details, see the [Gemini API documentation](https://ai.google.dev/) .
