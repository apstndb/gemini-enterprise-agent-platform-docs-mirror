---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-live
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-live
title: Gemini 3.8 Live
description: Learn about Gemini 3.8 Live, offering improved voice quality, reliability, and real-time agent orchestration.
data_source: docs.cloud.google.com
---

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal-live?model=gemini-3.8-live) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<th><code>gemini-3.8-live</code></th>
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
Input and output
videocam
Video<br />
Input and output</th>
<td></td>
</tr>
<tr class="odd">
<th>Token limits</th>
<th>Maximum input tokens</th>
<td>128K</td>
</tr>
<tr class="even">
<th>Maximum output tokens</th>
<th>64K</th>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">Thinking</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction">System instructions</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a> preview Preview feature<br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Context caching</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Count Tokens</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview">RAG Engine</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview">Chat completions</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models">Tuning</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context">URL context</a><br />
Not supported</li>
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
Not supported</li>
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
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Pay-as-you-go</a><br />
Standard PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Technical specifications</th>
<th><strong>Text</strong> description</th>
<td><ul>
<li>Supported MIME types:
<code>text/plain</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><strong>Image</strong> photo</th>
<th><ul>
<li>Supported resolutions: Minimum: 704x1280 or 1280x704</li>
<li>Supported aspect ratios: Portrait, Landscape</li>
<li>Supported MIME types:
<code>image/png</code> , <code>image/jpeg</code> , <code>image/webp</code> , <code>image/heic</code> , <code>image/heif</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><strong>Audio</strong> mic</th>
<th><ul>
<li>Maximum number of audio files per prompt: 1-stream</li>
<li>Required audio input format: Raw 16-bit PCM audio at 16kHz, little-endian</li>
<li>Required audio output format: Raw 16-bit PCM audio at 24kHz, little-endian</li>
<li>Supported MIME types:
<code>audio/x-aac</code> , <code>audio/flac</code> , <code>audio/mp3</code> , <code>audio/m4a</code> , <code>audio/mpeg</code> , <code>audio/mpga</code> , <code>audio/mp4</code> , <code>audio/ogg</code> , <code>audio/pcm</code> , <code>audio/wav</code> , <code>audio/webm</code> , <code>audio/mpa</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Video</strong> videocam</th>
<th><ul>
<li>Supported resolutions: Minimum: 704x1280 or 1280x704</li>
<li>Supported aspect ratios: Portrait, Landscape</li>
<li>Supported MIME types:
<code>video/x-flv</code> , <code>video/quicktime</code> , <code>video/mpeg</code> , <code>video/mpegs</code> , <code>video/mpg</code> , <code>video/mp4</code> , <code>video/webm</code> , <code>video/wmv</code> , <code>video/3gpp</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></th>
<td><ul>
<li>Multi-region: <code>us</code> , <code>eu</code></li>
<li>United States: <code>us-central1</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models">Provisioned Throughput</a></strong></p></th>
<th><ul>
<li>Multi-region: <code>us</code> , <code>eu</code></li>
<li>United States: <code>us-central1</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard PayGo</a></strong></p></th>
<th><ul>
<li>Multi-region: <code>us</code> , <code>eu</code></li>
<li>United States: <code>us-central1</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Knowledge cutoff date</th>
<th>January 2025</th>
<td></td>
</tr>
<tr class="even">
<th>Versions</th>
<th><ul>
<li><code>gemini-3.8-live</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: September 24, 2026</li>
</ul></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Security controls</th>
<th><strong>Online prediction</strong></th>
<td><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></td>
</tr>
<tr class="even">
<th>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls">Security controls</a> for more information.</th>
<th></th>
<td></td>
</tr>
</tbody>
</table>
