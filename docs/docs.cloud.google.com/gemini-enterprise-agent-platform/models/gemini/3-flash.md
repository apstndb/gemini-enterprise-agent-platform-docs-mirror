---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-flash
title: Gemini 3 Flash
description: Learn about Gemini 3 Flash, Google's latest Gemini Flash model.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

Gemini 3 Flash combines Gemini 3 Pro's reasoning capabilities with the Flash line's levels on latency, efficiency, and cost. It not only enables everyday tasks with improved reasoning, but is designed to tackle the most complex agentic workflows.

See [Get started with Gemini 3](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-3) for information on what's new with the Gemini 3 family of models.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-3-flash-preview) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemini-3-flash-preview) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-3-flash-preview) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

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
<th><code>gemini-3-flash-preview</code></th>
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
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models">Tuning</a><br />
Not supported</li>
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
Google Search<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution">Code execution</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use">Computer use</a> preview Preview feature<br />
Supported</li>
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
Standard PayGo, Flex PayGo, Priority PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Technical specifications</th>
<th><strong>Image</strong> photo</th>
<td><ul>
<li>Maximum images per prompt: 3000</li>
<li>Maximum file size per file for inline data or direct uploads through the console: 7 MB</li>
<li>Maximum file size per file from Google Cloud Storage: 30 MB</li>
<li>Default resolution tokens: 1120</li>
<li>Supported MIME types:
<code>image/png</code> , <code>image/jpeg</code> , <code>image/webp</code> , <code>image/heic</code> , <code>image/heif</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><strong>Text</strong> description</th>
<th><ul>
<li>Maximum number of files per prompt: 3000</li>
<li>Maximum number of pages per file: 3000</li>
<li>Maximum file size per file for the API or Cloud Storage imports: 50 MB(application/pdf) or 7 MB(text/plain)</li>
<li>Maximum file size per file for direct uploads through the console: 7 MB</li>
<li>Default resolution tokens: 560</li>
<li>OCR for scanned PDFs: Not used by default</li>
<li>Supported MIME types:
<code>application/pdf</code> , <code>text/plain</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><strong>Video</strong> videocam</th>
<th><ul>
<li>Maximum video length (with audio): Approximately 45 minutes</li>
<li>Maximum video length (without audio): Approximately 1 hour</li>
<li>Maximum number of videos per prompt: 10</li>
<li>Default resolution tokens per frame: 70</li>
<li>Supported MIME types:
<code>video/x-flv</code> , <code>video/quicktime</code> , <code>video/mpeg</code> , <code>video/mpegs</code> , <code>video/mpg</code> , <code>video/mp4</code> , <code>video/webm</code> , <code>video/wmv</code> , <code>video/3gpp</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Audio</strong> mic</th>
<th><ul>
<li>Maximum audio length per prompt: Approximately 8.4 hours, or up to 1 million tokens</li>
<li>Maximum number of audio files per prompt: 1</li>
<li>Speech understanding for: Audio summarization, transcription, and translation</li>
<li>Supported MIME types:
<code>audio/x-aac</code> , <code>audio/flac</code> , <code>audio/mp3</code> , <code>audio/m4a</code> , <code>audio/mpeg</code> , <code>audio/mpga</code> , <code>audio/mp4</code> , <code>audio/ogg</code> , <code>audio/pcm</code> , <code>audio/wav</code> , <code>audio/webm</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><strong>Parameter defaults</strong> tune</th>
<th><ul>
<li>Temperature: 0.0-2.0 (default 1.0)</li>
<li>topP: 0.0-1.0 (default 0.95)</li>
<li>topK: 64 (fixed)</li>
<li>candidateCount: 1–8 (default 1)</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></th>
<td><ul>
<li>Global: <code>global</code></li>
</ul></td>
</tr>
<tr class="even">
<th>Versions</th>
<th><ul>
<li><code>gemini-3-flash-preview</code>
<ul>
<li>Launch stage: Public preview</li>
<li>Release date: December 17, 2025</li>
</ul></li>
</ul></th>
<td></td>
</tr>
</tbody>
</table>
