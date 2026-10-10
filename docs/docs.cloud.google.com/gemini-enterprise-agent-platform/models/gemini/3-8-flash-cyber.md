---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-cyber
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-cyber
title: Gemini 3.8 Flash Cyber
description: Learn about Gemini 3.8 Flash Cyber, our model optimized for cyber security.
data_source: docs.cloud.google.com
---

Gemini 3.8 Flash Cyber is a post-training version of the Gemini 3.8 Flash model tailored specifically for cybersecurity use cases. Gemini 3.8 Flash is a Gemini Cyber model subject to Section 31(a) of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) .

Gemini 3.8 Flash Cyber is available in GA behind an allowlist. To request access, contact your Google team or apply for access at [Fairwind Program](https://deepmind.google/fairwind-program/) .

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/chat?model=gemini-3.8-flash-cyber) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/chat?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-3.8-flash-cyber) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

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
<th><code>gemini-3.8-flash-cyber</code></th>
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
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Context caching</a><br />
Implicit context caching, explicit context caching<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview">RAG Engine</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models">Tuning</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context">URL context</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing">Agentic video understanding</a> preview Preview feature<br />
Supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Tools</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview">Grounding</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution">Code execution</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use">Computer use</a> preview Preview feature<br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>APIs</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference">GenerateContent API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a> preview Preview feature<br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Count Tokens API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview">Chat Completions API</a><br />
Supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Consumption options</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference">Batch inference</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Pay-as-you-go</a><br />
Standard PayGo with Usage Tiers, Flex PayGo, Priority PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Not supported</li>
</ul></th>
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
<li>Maximum number of pages per file: 3,000</li>
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
<li>Temperature: 1.0</li>
<li>topP: 0.95</li>
<li>topK: 64</li>
<li>Frequency penalty: 0</li>
<li>Presence penalty: 0</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></th>
<td><ul>
<li>Global: <code>global</code></li>
<li>Multi-region: <code>us</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency">ML processing</a></strong></p></th>
<th><ul>
<li>Multi-region: <code>us</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models">Provisioned Throughput</a></strong></p></th>
<th><ul>
<li>Global: <code>global</code></li>
<li>Multi-region: <code>us</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard PayGo</a></strong></p></th>
<th><ul>
<li>Global: <code>global</code></li>
<li>Multi-region: <code>us</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Versions</th>
<th><ul>
<li><code>gemini-3.8-flash-cyber</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: September 16, 2026</li>
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
<th><strong>Context caching</strong></th>
<th><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls">Security controls</a> for more information.</th>
<th></th>
<td></td>
</tr>
</tbody>
</table>
